# Security Headers Configuration
<!-- DE: # Sicherheits-Header-Konfiguration -->

Protect against XSS, Clickjacking, MIME sniffing, and other common web attacks.
<!-- DE: Schutz gegen XSS, Clickjacking, MIME-Sniffing und andere häufige Web-Angriffe. -->

## Setup
<!-- DE: ## Einrichtung -->

Add security headers to `next.config.ts`:
<!-- DE: Sicherheits-Header zu `next.config.ts` hinzufügen: -->

```typescript
import type { NextConfig } from 'next'

const nextConfig: NextConfig = {
  async headers() {
    return [
      {
        source: '/:path*',
        headers: [
          {
            key: 'X-Frame-Options',
            value: 'DENY',
          },
          {
            key: 'X-Content-Type-Options',
            value: 'nosniff',
          },
          {
            key: 'Referrer-Policy',
            value: 'origin-when-cross-origin',
          },
          {
            key: 'Strict-Transport-Security',
            value: 'max-age=31536000; includeSubDomains',
          },
        ],
      },
    ]
  },
}

export default nextConfig
```
<!-- DE: Vier Sicherheits-Header für alle Routen in next.config.ts konfigurieren. -->

## What Each Header Does
<!-- DE: ## Was jeder Header bewirkt -->

| Header | Protection |
|--------|-----------|
| X-Frame-Options: DENY | Prevents your site from being embedded in iframes (clickjacking) |
| X-Content-Type-Options: nosniff | Prevents browsers from guessing content types (MIME sniffing) |
| Referrer-Policy | Controls how much URL info is sent to other sites |
| Strict-Transport-Security | Forces HTTPS connections |
<!-- DE:
| Header | Schutz |
|--------|--------|
| X-Frame-Options: DENY | Verhindert, dass die Seite in iFrames eingebettet wird (Clickjacking) |
| X-Content-Type-Options: nosniff | Verhindert, dass Browser Content-Types erraten (MIME-Sniffing) |
| Referrer-Policy | Kontrolliert, wie viele URL-Informationen an andere Seiten gesendet werden |
| Strict-Transport-Security | Erzwingt HTTPS-Verbindungen |
-->

## Verify After Deployment
<!-- DE: ## Nach der Bereitstellung verifizieren -->
1. Open Chrome DevTools
2. Go to Network tab
3. Click on any request to your site
4. Check Response Headers section
5. Verify all 4 headers are present
<!-- DE:
1. Chrome DevTools öffnen
2. Zum Network-Tab wechseln
3. Eine beliebige Anfrage an die Seite anklicken
4. Abschnitt „Response Headers" prüfen
5. Verifizieren, dass alle 4 Header vorhanden sind
-->

## Advanced (Optional)
<!-- DE: ## Erweitert (Optional) -->
**Content-Security-Policy (CSP)** - The most powerful header, but can break your app if misconfigured. Only add after thorough testing:
<!-- DE: **Content-Security-Policy (CSP)** – Der mächtigste Header, kann aber die App bei falscher Konfiguration beschädigen. Nur nach gründlichem Testen hinzufügen: -->
```
Content-Security-Policy: default-src 'self'; script-src 'self' 'unsafe-inline'
```
Start with report-only mode first: `Content-Security-Policy-Report-Only`
<!-- DE: Zunächst den Report-only-Modus verwenden: `Content-Security-Policy-Report-Only` -->
