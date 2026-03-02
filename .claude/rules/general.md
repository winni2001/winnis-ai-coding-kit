# General Project Rules
<!-- DE: # Allgemeine Projektregeln -->

## Feature Tracking
<!-- DE: ## Feature-Verfolgung -->
- All features are tracked in `features/INDEX.md` - read it before starting any work
- Feature specs live in `features/PROJ-X-feature-name.md`
- Feature IDs are sequential: check INDEX.md for the next available number
- One feature per spec file (Single Responsibility)
- Never combine multiple independent functionalities in one spec
<!-- DE:
- Alle Features werden in `features/INDEX.md` verfolgt – vor jeder Arbeit lesen
- Feature-Spezifikationen befinden sich in `features/PROJ-X-feature-name.md`
- Feature-IDs sind fortlaufend: INDEX.md auf die nächste verfügbare Nummer prüfen
- Ein Feature pro Spezifikationsdatei (Einzelverantwortlichkeit)
- Niemals mehrere unabhängige Funktionalitäten in einer Spezifikation kombinieren
-->

## Git Conventions
<!-- DE: ## Git-Konventionen -->
- Commit format: `type(PROJ-X): description`
- Types: feat, fix, refactor, test, docs, deploy, chore
- Check existing features before creating new ones: `ls features/ | grep PROJ-`
- Check existing components before building: `git ls-files src/components/`
- Check existing APIs before building: `git ls-files src/app/api/`
<!-- DE:
- Commit-Format: `type(PROJ-X): Beschreibung`
- Typen: feat, fix, refactor, test, docs, deploy, chore
- Vorhandene Features vor dem Erstellen neuer prüfen: `ls features/ | grep PROJ-`
- Vorhandene Komponenten vor dem Bauen prüfen: `git ls-files src/components/`
- Vorhandene APIs vor dem Bauen prüfen: `git ls-files src/app/api/`
-->

## Human-in-the-Loop
<!-- DE: ## Mensch im Prozess (Human-in-the-Loop) -->
- Always ask for user approval before finalizing deliverables
- Present options using clear choices rather than open-ended questions
- Never proceed to the next workflow phase without user confirmation
<!-- DE:
- Vor dem Abschluss von Lieferergebnissen immer die Genehmigung des Nutzers einholen
- Optionen mit klaren Auswahlmöglichkeiten statt offener Fragen präsentieren
- Niemals ohne Bestätigung des Nutzers zur nächsten Workflow-Phase übergehen
-->

## Status Updates
<!-- DE: ## Statusaktualisierungen -->
- Update `features/INDEX.md` when feature status changes
- Update the feature spec header status field
- Valid statuses: Planned, In Progress, In Review, Deployed
<!-- DE:
- `features/INDEX.md` aktualisieren, wenn sich der Feature-Status ändert
- Das Statusfeld im Feature-Spec-Header aktualisieren
- Gültige Status: Planned (Geplant), In Progress (In Arbeit), In Review (In Prüfung), Deployed (Veröffentlicht)
-->

## File Handling
<!-- DE: ## Dateibehandlung -->
- ALWAYS read a file before modifying it - never assume contents from memory
- After context compaction, re-read files before continuing work
- When unsure about current project state, read `features/INDEX.md` first
- Run `git diff` to verify what has already been changed in this session
- Never guess at import paths, component names, or API routes - verify by reading
<!-- DE:
- Datei IMMER vor dem Bearbeiten lesen – Inhalte niemals aus dem Gedächtnis annehmen
- Nach der Kontextverdichtung Dateien vor dem Weiterarbeiten erneut lesen
- Bei Unsicherheit über den aktuellen Projektstatus zuerst `features/INDEX.md` lesen
- `git diff` ausführen, um zu prüfen, was in dieser Sitzung bereits geändert wurde
- Importpfade, Komponentennamen oder API-Routen niemals erraten – durch Lesen verifizieren
-->

## Handoffs Between Skills
<!-- DE: ## Übergaben zwischen Skills -->
- After completing a skill, suggest the next skill to the user
- Format: "Next step: Run `/skillname` to [action]"
- Handoffs are always user-initiated, never automatic
<!-- DE:
- Nach Abschluss eines Skills den nächsten Skill vorschlagen
- Format: „Nächster Schritt: Führe `/skillname` aus, um [Aktion]"
- Übergaben sind immer nutzerinitiiert, nie automatisch
-->
