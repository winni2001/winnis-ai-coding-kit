# Rate Limiting
<!-- DE: # Rate-Limiting -->

Prevent abuse, DDoS attacks, and excessive API usage.
<!-- DE: Missbrauch, DDoS-Angriffe und übermäßige API-Nutzung verhindern. -->

## When to Add Rate Limiting
<!-- DE: ## Wann Rate-Limiting hinzufügen -->
- **MVP:** Optional (focus on features first)
- **Production with users:** Recommended on auth endpoints and public APIs
- **Public-facing APIs:** Required
<!-- DE:
- **MVP:** Optional (zuerst auf Features konzentrieren)
- **Produktion mit Nutzern:** Empfohlen für Auth-Endpunkte und öffentliche APIs
- **Öffentlich zugängliche APIs:** Erforderlich
-->

## Setup with Upstash Redis
<!-- DE: ## Einrichtung mit Upstash Redis -->

### 1. Install Dependencies
<!-- DE: ### 1. Abhängigkeiten installieren -->
```bash
npm install @upstash/ratelimit @upstash/redis
```

### 2. Create Upstash Account
<!-- DE: ### 2. Upstash-Konto erstellen -->
- Go to [upstash.com](https://upstash.com) (free tier: 10k requests/day)
- Create a Redis database
- Copy REST URL and token
<!-- DE:
- Zu [upstash.com](https://upstash.com) gehen (kostenlose Stufe: 10.000 Anfragen/Tag)
- Eine Redis-Datenbank erstellen
- REST-URL und Token kopieren
-->

### 3. Add Environment Variables
<!-- DE: ### 3. Umgebungsvariablen hinzufügen -->
```bash
# .env.local
UPSTASH_REDIS_REST_URL=https://xxx.upstash.io
UPSTASH_REDIS_REST_TOKEN=xxx
```

### 4. Create Rate Limiter
<!-- DE: ### 4. Rate-Limiter erstellen -->
```typescript
// src/lib/rate-limit.ts
import { Ratelimit } from '@upstash/ratelimit'
import { Redis } from '@upstash/redis'

export const ratelimit = new Ratelimit({
  redis: Redis.fromEnv(),
  limiter: Ratelimit.slidingWindow(10, '10 s'), // 10 requests per 10 seconds
})
```
<!-- DE: Rate-Limiter mit Sliding-Window-Algorithmus erstellen: 10 Anfragen pro 10 Sekunden. -->

### 5. Use in API Routes
<!-- DE: ### 5. In API-Routen verwenden -->
```typescript
// src/app/api/example/route.ts
import { ratelimit } from '@/lib/rate-limit'
import { NextRequest, NextResponse } from 'next/server'

export async function POST(request: NextRequest) {
  const ip = request.headers.get('x-forwarded-for') ?? 'anonymous'
  const { success, limit, remaining } = await ratelimit.limit(ip)

  if (!success) {
    return NextResponse.json(
      { error: 'Too many requests' },
      {
        status: 429,
        headers: {
          'X-RateLimit-Limit': limit.toString(),
          'X-RateLimit-Remaining': remaining.toString(),
        },
      }
    )
  }

  // Process request normally...
}
```
<!-- DE: Rate-Limiter in API-Routen einbinden: IP-Adresse prüfen und bei Überschreitung HTTP 429 zurückgeben. -->

### 6. Use in Middleware (Global)
<!-- DE: ### 6. In Middleware verwenden (global) -->
```typescript
// middleware.ts
import { ratelimit } from '@/lib/rate-limit'
import { NextRequest, NextResponse } from 'next/server'

export async function middleware(request: NextRequest) {
  // Only rate limit API routes
  if (request.nextUrl.pathname.startsWith('/api/')) {
    const ip = request.headers.get('x-forwarded-for') ?? 'anonymous'
    const { success } = await ratelimit.limit(ip)

    if (!success) {
      return NextResponse.json({ error: 'Too Many Requests' }, { status: 429 })
    }
  }
}

export const config = {
  matcher: '/api/:path*',
}
```
<!-- DE: Rate-Limiting global in der Next.js Middleware anwenden – gilt für alle API-Routen. -->

## Recommended Limits
<!-- DE: ## Empfohlene Limits -->

| Endpoint Type | Limit | Window |
|--------------|-------|--------|
| Login/Register | 5 requests | 1 minute |
| Password Reset | 3 requests | 5 minutes |
| General API | 30 requests | 10 seconds |
| File Upload | 5 requests | 1 minute |
<!-- DE:
| Endpunkt-Typ | Limit | Zeitfenster |
|--------------|-------|-------------|
| Login/Registrierung | 5 Anfragen | 1 Minute |
| Passwort-Reset | 3 Anfragen | 5 Minuten |
| Allgemeine API | 30 Anfragen | 10 Sekunden |
| Datei-Upload | 5 Anfragen | 1 Minute |
-->

## Alternative
<!-- DE: ## Alternative -->
**Vercel Edge Config** - Simpler but less flexible. Built into Vercel, no external service needed.
<!-- DE: **Vercel Edge Config** – Einfacher, aber weniger flexibel. In Vercel integriert, kein externer Dienst erforderlich. -->
