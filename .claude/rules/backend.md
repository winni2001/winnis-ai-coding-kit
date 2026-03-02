# Backend Development Rules
<!-- DE: # Backend-Entwicklungsregeln -->

## Database (Supabase)
<!-- DE: ## Datenbank (Supabase) -->
- ALWAYS enable Row Level Security on every table
- Create RLS policies for SELECT, INSERT, UPDATE, DELETE
- Add indexes on columns used in WHERE, ORDER BY, and JOIN clauses
- Use foreign keys with ON DELETE CASCADE where appropriate
- Never skip RLS - security first
<!-- DE:
- Row Level Security auf JEDER Tabelle IMMER aktivieren
- RLS-Richtlinien für SELECT, INSERT, UPDATE, DELETE erstellen
- Indizes auf Spalten anlegen, die in WHERE-, ORDER BY- und JOIN-Klauseln verwendet werden
- Fremdschlüssel mit ON DELETE CASCADE verwenden, wo angemessen
- RLS niemals überspringen – Sicherheit hat Vorrang
-->

## API Routes
<!-- DE: ## API-Routen -->
- Validate all inputs using Zod schemas before processing
- Always check authentication: verify user session exists
- Return meaningful error messages with appropriate HTTP status codes
- Use `.limit()` on all list queries
<!-- DE:
- Alle Eingaben mit Zod-Schemas vor der Verarbeitung validieren
- Authentifizierung immer prüfen: sicherstellen, dass eine Nutzersitzung existiert
- Aussagekräftige Fehlermeldungen mit passenden HTTP-Statuscodes zurückgeben
- `.limit()` bei allen Listenabfragen verwenden
-->

## Query Patterns
<!-- DE: ## Abfragemuster -->
- Use Supabase joins instead of N+1 query loops
- Use `unstable_cache` from Next.js for rarely-changing data
- Always handle errors from Supabase responses
<!-- DE:
- Supabase-Joins statt N+1-Abfrageschleifen verwenden
- `unstable_cache` von Next.js für selten geänderte Daten nutzen
- Fehler aus Supabase-Antworten immer behandeln
-->

## Security
<!-- DE: ## Sicherheit -->
- Never hardcode secrets in source code
- Use environment variables for all credentials
- Validate and sanitize all user input
- Use parameterized queries (Supabase handles this)
<!-- DE:
- Geheimnisse niemals im Quellcode hart kodieren
- Umgebungsvariablen für alle Anmeldeinformationen verwenden
- Alle Nutzereingaben validieren und bereinigen
- Parametrisierte Abfragen verwenden (Supabase übernimmt dies)
-->
