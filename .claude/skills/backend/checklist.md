# Backend Implementation Checklist
<!-- DE: # Backend-Implementierungs-Checkliste -->

## Core Checklist
<!-- DE: ## Kern-Checkliste -->
- [ ] Checked existing tables/APIs via git before creating new ones
- [ ] Database tables created in Supabase
- [ ] Row Level Security enabled on ALL new tables
- [ ] RLS policies created for SELECT, INSERT, UPDATE, DELETE
- [ ] Indexes created on performance-critical columns
- [ ] Foreign keys set with appropriate ON DELETE behavior
- [ ] All planned API endpoints implemented in `/src/app/api/`
- [ ] Authentication verified (no access without valid session)
- [ ] Input validation with Zod on all POST/PUT requests
- [ ] Meaningful error messages with correct HTTP status codes
- [ ] No TypeScript errors in API routes
- [ ] All endpoints tested manually
- [ ] No hardcoded secrets in source code
- [ ] Frontend connected to real API endpoints
- [ ] User has reviewed and approved
<!-- DE:
- [ ] Vorhandene Tabellen/APIs via git geprüft, bevor neue erstellt wurden
- [ ] Datenbanktabellen in Supabase erstellt
- [ ] Row Level Security auf ALLEN neuen Tabellen aktiviert
- [ ] RLS-Richtlinien für SELECT, INSERT, UPDATE, DELETE erstellt
- [ ] Indizes auf leistungskritischen Spalten angelegt
- [ ] Fremdschlüssel mit passendem ON DELETE-Verhalten gesetzt
- [ ] Alle geplanten API-Endpunkte in `/src/app/api/` implementiert
- [ ] Authentifizierung geprüft (kein Zugriff ohne gültige Sitzung)
- [ ] Eingabevalidierung mit Zod auf allen POST/PUT-Anfragen
- [ ] Aussagekräftige Fehlermeldungen mit korrekten HTTP-Statuscodes
- [ ] Keine TypeScript-Fehler in API-Routen
- [ ] Alle Endpunkte manuell getestet
- [ ] Keine hart kodierten Geheimnisse im Quellcode
- [ ] Frontend mit echten API-Endpunkten verbunden
- [ ] Nutzer hat geprüft und genehmigt
-->

## Verification (run before marking complete)
<!-- DE: ## Verifizierung (vor dem Abschluss ausführen) -->
- [ ] `npm run build` passes without errors
- [ ] All acceptance criteria from feature spec addressed in API
- [ ] All API endpoints return correct status codes (test with curl or browser)
- [ ] `features/INDEX.md` status updated to "In Progress"
- [ ] Code committed to git
<!-- DE:
- [ ] `npm run build` läuft ohne Fehler durch
- [ ] Alle Akzeptanzkriterien aus der Feature-Spezifikation in der API abgedeckt
- [ ] Alle API-Endpunkte geben korrekte Statuscodes zurück (mit curl oder Browser testen)
- [ ] `features/INDEX.md` Status auf „In Progress" aktualisiert
- [ ] Code in git eingecheckt
-->

## Performance Checklist
<!-- DE: ## Performance-Checkliste -->
- [ ] All frequently filtered columns have indexes
- [ ] No N+1 queries (use Supabase joins instead of loops)
- [ ] All list queries use `.limit()`
- [ ] Zod validation on all write endpoints
- [ ] Slow queries cached where appropriate (optional for MVP)
- [ ] Rate limiting on public-facing APIs (optional for MVP)
<!-- DE:
- [ ] Alle häufig gefilterten Spalten haben Indizes
- [ ] Keine N+1-Abfragen (Supabase-Joins statt Schleifen verwenden)
- [ ] Alle Listenabfragen verwenden `.limit()`
- [ ] Zod-Validierung auf allen Schreib-Endpunkten
- [ ] Langsame Abfragen wo angemessen gecacht (optional für MVP)
- [ ] Rate Limiting auf öffentlichen APIs (optional für MVP)
-->
