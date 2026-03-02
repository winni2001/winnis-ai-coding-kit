# Error Tracking Setup (Sentry)
<!-- DE: # Fehler-Tracking-Einrichtung (Sentry) -->

Track production errors automatically so you know about issues before your users report them.
<!-- DE: Produktionsfehler automatisch verfolgen, um Probleme zu erkennen, bevor Nutzer sie melden. -->

## Setup (5 minutes)
<!-- DE: ## Einrichtung (5 Minuten) -->

### 1. Create Sentry Account
<!-- DE: ### 1. Sentry-Konto erstellen -->
- Go to [sentry.io](https://sentry.io) (free tier available for small apps)
- Create a new project and select "Next.js"
<!-- DE:
- Zu [sentry.io](https://sentry.io) gehen (kostenlose Stufe für kleine Apps verfügbar)
- Ein neues Projekt erstellen und „Next.js" auswählen
-->

### 2. Install Next.js Integration
<!-- DE: ### 2. Next.js-Integration installieren -->
```bash
npx @sentry/wizard@latest -i nextjs
```
This automatically:
- Installs `@sentry/nextjs`
- Creates `sentry.client.config.ts` and `sentry.server.config.ts`
- Updates `next.config.ts` with Sentry webpack plugin
<!-- DE:
Dies geschieht automatisch:
- `@sentry/nextjs` wird installiert
- `sentry.client.config.ts` und `sentry.server.config.ts` werden erstellt
- `next.config.ts` wird mit dem Sentry-Webpack-Plugin aktualisiert
-->

### 3. Add Environment Variables
<!-- DE: ### 3. Umgebungsvariablen hinzufügen -->
Add to `.env.local` (local) and Vercel Dashboard (production):
<!-- DE: Zu `.env.local` (lokal) und Vercel Dashboard (Produktion) hinzufügen: -->
```bash
SENTRY_DSN=https://xxx@xxx.ingest.sentry.io/xxx
NEXT_PUBLIC_SENTRY_DSN=https://xxx@xxx.ingest.sentry.io/xxx
SENTRY_AUTH_TOKEN=sntrys_xxx  # For source maps upload
```

### 4. Verify Setup
<!-- DE: ### 4. Einrichtung verifizieren -->
Trigger a test error and check Sentry Dashboard:
<!-- DE: Einen Testfehler auslösen und das Sentry-Dashboard prüfen: -->
```typescript
// Temporary test - remove after verification
throw new Error("Sentry test error")
```

## What You Get
<!-- DE: ## Was du erhältst -->
- Automatic error capture (client + server)
- Stack traces with source maps
- Error grouping and deduplication
- Email alerts for new errors
- Performance monitoring (optional)
<!-- DE:
- Automatische Fehlererfassung (Client + Server)
- Stack Traces mit Source Maps
- Fehlergruppierung und Deduplizierung
- E-Mail-Benachrichtigungen bei neuen Fehlern
- Performance-Monitoring (optional)
-->

## Alternative
<!-- DE: ## Alternative -->
**Vercel Error Tracking** - Built-in, simpler, but fewer features. Available in Vercel Dashboard under "Monitoring".
<!-- DE: **Vercel Error Tracking** – Integriert, einfacher, aber weniger Funktionen. Im Vercel Dashboard unter „Monitoring" verfügbar. -->
