# Security Rules
<!-- DE: # Sicherheitsregeln -->

## Secrets Management
<!-- DE: ## Geheimnisverwaltung -->
- NEVER commit secrets, API keys, or credentials to git
- Use `.env.local` for local development (already in .gitignore)
- Use `NEXT_PUBLIC_` prefix ONLY for values safe to expose in browser
- Document all required env vars in `.env.local.example` with dummy values
<!-- DE:
- Geheimnisse, API-Schlüssel oder Anmeldedaten NIEMALS in git einchecken
- `.env.local` für die lokale Entwicklung verwenden (bereits in .gitignore)
- Das Präfix `NEXT_PUBLIC_` NUR für Werte verwenden, die im Browser sicher offengelegt werden können
- Alle erforderlichen Umgebungsvariablen in `.env.local.example` mit Platzhalterwerten dokumentieren
-->

## Input Validation
<!-- DE: ## Eingabevalidierung -->
- Validate ALL user input on the server side with Zod
- Never trust client-side validation alone
- Sanitize data before database insertion
<!-- DE:
- ALLE Nutzereingaben serverseitig mit Zod validieren
- Clientseitige Validierung allein niemals vertrauen
- Daten vor dem Einfügen in die Datenbank bereinigen
-->

## Authentication
<!-- DE: ## Authentifizierung -->
- Always verify authentication before processing API requests
- Use Supabase RLS as a second line of defense
- Implement rate limiting on authentication endpoints
<!-- DE:
- Authentifizierung vor der Verarbeitung von API-Anfragen immer prüfen
- Supabase RLS als zweite Verteidigungslinie verwenden
- Rate Limiting an Authentifizierungs-Endpunkten implementieren
-->

## Security Headers
<!-- DE: ## Sicherheits-Header -->
- X-Frame-Options: DENY
- X-Content-Type-Options: nosniff
- Referrer-Policy: origin-when-cross-origin
- Strict-Transport-Security with includeSubDomains
<!-- DE:
- X-Frame-Options: DENY (verhindert Einbettung der Seite in iframes – Clickjacking-Schutz)
- X-Content-Type-Options: nosniff (verhindert MIME-Typ-Sniffing durch den Browser)
- Referrer-Policy: origin-when-cross-origin (kontrolliert, welche Referrer-Informationen weitergegeben werden)
- Strict-Transport-Security mit includeSubDomains (erzwingt HTTPS-Verbindungen)
-->

## Code Review Triggers
<!-- DE: ## Auslöser für Code-Reviews -->
- Any changes to RLS policies require explicit user approval
- Any changes to authentication flow require explicit user approval
- Any new environment variables must be documented in .env.local.example
<!-- DE:
- Jede Änderung an RLS-Richtlinien erfordert ausdrückliche Nutzergenehmigung
- Jede Änderung am Authentifizierungsablauf erfordert ausdrückliche Nutzergenehmigung
- Jede neue Umgebungsvariable muss in .env.local.example dokumentiert werden
-->
