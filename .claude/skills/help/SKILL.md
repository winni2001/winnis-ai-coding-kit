---
name: help
description: Context-aware guide that tells you where you are in the workflow and what to do next. Use anytime you're unsure.
argument-hint: [optional question]
user-invocable: true
allowed-tools: Read, Glob, Grep, Bash
model: opus
---
<!-- DE: Beschreibung: Kontextsensitiver Leitfaden, der dir zeigt, wo du im Workflow bist und was als nächstes zu tun ist. Jederzeit verwendbar, wenn du unsicher bist. -->

# Project Help Guide
<!-- DE: # Projekt-Hilfsleitfaden -->

You are a helpful project assistant. Your job is to analyze the current project state and tell the user exactly where they are and what to do next.
<!-- DE: Du bist ein hilfreicher Projektassistent. Deine Aufgabe ist es, den aktuellen Projektstatus zu analysieren und dem Nutzer genau zu sagen, wo er sich befindet und was als nächstes zu tun ist. -->

## When Invoked
<!-- DE: ## Wenn aufgerufen -->

### Step 1: Analyze Current State
<!-- DE: ### Schritt 1: Aktuellen Zustand analysieren -->

Read these files to understand where the project stands:
<!-- DE: Diese Dateien lesen, um den Projektstand zu verstehen: -->

1. **Check PRD:** Read `docs/PRD.md`
   - Is it still the empty template? → Project not initialized yet
   - Is it filled out? → Project has been set up

2. **Check Feature Index:** Read `features/INDEX.md`
   - No features listed? → No features created yet
   - Features exist? → Check their statuses

3. **Check Feature Specs:** For each feature in INDEX.md, check if:
   - Tech Design section exists (added by /architecture)
   - QA Test Results section exists (added by /qa)
   - Deployment section exists (added by /deploy)

4. **Check Codebase:** Quick scan of what's been built
   - `ls src/components/*.tsx 2>/dev/null` → Custom components
   - `ls src/app/api/ 2>/dev/null` → API routes
   - `ls src/components/ui/` → Installed shadcn components
<!-- DE:
1. **PRD prüfen:** `docs/PRD.md` lesen
   - Noch die leere Vorlage? → Projekt noch nicht initialisiert
   - Ausgefüllt? → Projekt wurde eingerichtet

2. **Feature-Index prüfen:** `features/INDEX.md` lesen
   - Keine Features aufgelistet? → Noch keine Features erstellt
   - Features vorhanden? → Deren Status prüfen

3. **Feature-Spezifikationen prüfen:** Für jedes Feature in INDEX.md prüfen, ob:
   - Tech-Design-Abschnitt vorhanden (hinzugefügt von /architecture)
   - QA-Testergebnisse-Abschnitt vorhanden (hinzugefügt von /qa)
   - Deployment-Abschnitt vorhanden (hinzugefügt von /deploy)

4. **Codebasis prüfen:** Schneller Überblick über das Gebaute
   - `ls src/components/*.tsx 2>/dev/null` → Eigene Komponenten
   - `ls src/app/api/ 2>/dev/null` → API-Routen
   - `ls src/components/ui/` → Installierte shadcn-Komponenten
-->

### Step 2: Determine Next Action
<!-- DE: ### Schritt 2: Nächste Aktion bestimmen -->

Based on the state analysis, determine what the user should do next:
<!-- DE: Basierend auf der Zustandsanalyse bestimmen, was der Nutzer als nächstes tun soll: -->

**If PRD is empty template:**
> Your project hasn't been initialized yet.
> Run `/requirements` with a description of what you want to build.
> Example: `/requirements I want to build a task management app for small teams`

**If PRD exists but no features:**
> Your PRD is set up but no features have been created yet.
> Run `/requirements` to create your first feature specification.

**If features exist with status "Planned" (no Tech Design):**
> Feature PROJ-X is ready for architecture design.
> Run `/architecture` to create the technical design for `features/PROJ-X-name.md`

**If features have Tech Design but no implementation:**
> Feature PROJ-X has a tech design and is ready for implementation.
> Run `/frontend` to build the UI for `features/PROJ-X-name.md`
> (If backend is needed, run `/backend` after frontend is done)

**If features are implemented but no QA:**
> Feature PROJ-X is implemented and ready for testing.
> Run `/qa` to test `features/PROJ-X-name.md` against its acceptance criteria.

**If features have passed QA but aren't deployed:**
> Feature PROJ-X has passed QA and is ready for deployment.
> Run `/deploy` to deploy to production.

**If all features are deployed:**
> All current features are deployed! You can:
> - Run `/requirements` to add a new feature
> - Check `docs/PRD.md` for planned features not yet specified
<!-- DE:
**Falls PRD noch die leere Vorlage ist:**
> Dein Projekt wurde noch nicht initialisiert.
> Führe `/requirements` mit einer Beschreibung dessen aus, was du bauen möchtest.
> Beispiel: `/requirements Ich möchte ein Aufgabenverwaltungs-Tool für kleine Teams bauen`

**Falls PRD vorhanden, aber keine Features:**
> Dein PRD ist eingerichtet, aber es wurden noch keine Features erstellt.
> Führe `/requirements` aus, um deine erste Feature-Spezifikation zu erstellen.

**Falls Features mit Status „Planned" vorhanden (kein Tech Design):**
> Feature PROJ-X ist bereit für das Architekturdesign.
> Führe `/architecture` aus, um das technische Design für `features/PROJ-X-name.md` zu erstellen.

**Falls Features ein Tech Design haben, aber keine Implementierung:**
> Feature PROJ-X hat ein Tech Design und ist bereit für die Implementierung.
> Führe `/frontend` aus, um die UI für `features/PROJ-X-name.md` zu bauen.
> (Falls Backend benötigt wird, führe `/backend` nach dem Frontend aus)

**Falls Features implementiert, aber kein QA:**
> Feature PROJ-X ist implementiert und bereit zum Testen.
> Führe `/qa` aus, um `features/PROJ-X-name.md` gegen seine Akzeptanzkriterien zu testen.

**Falls Features QA bestanden haben, aber noch nicht deployed:**
> Feature PROJ-X hat QA bestanden und ist bereit für das Deployment.
> Führe `/deploy` aus, um in die Produktion zu deployen.

**Falls alle Features deployed sind:**
> Alle aktuellen Features sind deployed! Du kannst:
> - `/requirements` ausführen, um ein neues Feature hinzuzufügen
> - `docs/PRD.md` auf geplante Features prüfen, die noch nicht spezifiziert sind
-->

### Step 3: Answer User Questions
<!-- DE: ### Schritt 3: Nutzerfragen beantworten -->

If the user asked a specific question (via arguments), answer it in the context of the current project state. Common questions:
<!-- DE: Falls der Nutzer eine spezifische Frage gestellt hat (via Argumente), im Kontext des aktuellen Projektstatus beantworten. Häufige Fragen: -->

- "What skills are available?" → List all 6 skills with brief descriptions
- "How do I add a new feature?" → Explain `/requirements` workflow
- "How do I customize this template?" → Point to CLAUDE.md, rules/, skills/
- "What's the project structure?" → Explain the directory layout
- "How do I deploy?" → Explain `/deploy` workflow and prerequisites
<!-- DE:
- „Welche Skills sind verfügbar?" → Alle 6 Skills mit kurzen Beschreibungen auflisten
- „Wie füge ich ein neues Feature hinzu?" → `/requirements`-Workflow erklären
- „Wie passe ich dieses Template an?" → Auf CLAUDE.md, rules/, skills/ hinweisen
- „Was ist die Projektstruktur?" → Verzeichnislayout erklären
- „Wie deploye ich?" → `/deploy`-Workflow und Voraussetzungen erklären
-->

## Output Format
<!-- DE: ## Ausgabeformat -->

Always respond with this structure:
<!-- DE: Immer mit dieser Struktur antworten: -->

### Current Project Status
_Brief summary of where the project stands_
<!-- DE: ### Aktueller Projektstatus -->
<!-- DE: _Kurze Zusammenfassung des Projektstands_ -->

### Features Overview
_Table of features and their current status (from INDEX.md)_
<!-- DE: ### Features-Übersicht -->
<!-- DE: _Tabelle der Features und ihres aktuellen Status (aus INDEX.md)_ -->

### Recommended Next Step
_The single most important thing to do next, with the exact command_
<!-- DE: ### Empfohlener nächster Schritt -->
<!-- DE: _Das einzeln wichtigste als nächstes zu tun, mit dem genauen Befehl_ -->

### Other Available Actions
_Other things the user could do right now_
<!-- DE: ### Weitere verfügbare Aktionen -->
<!-- DE: _Andere Dinge, die der Nutzer jetzt tun könnte_ -->

If the user asked a specific question, answer that FIRST, then show the status overview.
<!-- DE: Falls der Nutzer eine spezifische Frage gestellt hat, diese ZUERST beantworten, dann die Statusübersicht zeigen. -->

## Important
<!-- DE: ## Wichtig -->
- Be concise and actionable
- Always give the exact command to run
- Reference specific file paths
- Don't explain the framework architecture in detail unless asked
- Focus on: "Here's where you are, here's what to do next"
<!-- DE:
- Prägnant und handlungsorientiert sein
- Immer den genauen auszuführenden Befehl angeben
- Spezifische Dateipfade referenzieren
- Die Framework-Architektur nicht im Detail erklären, außer wenn gefragt
- Fokus auf: „Hier bist du, das ist als nächstes zu tun"
-->
