# AI Coding Starter Kit
<!-- DE: # KI-Coding-Starter-Kit -->

> Build production-ready web apps faster with AI-powered Skills handling Requirements, Architecture, Development, QA, and Deployment.
<!-- DE: > Produktionsreife Web-Apps schneller bauen mit KI-gestützten Skills für Anforderungen, Architektur, Entwicklung, QA und Deployment. -->

This template uses [Claude Code](https://docs.anthropic.com/en/docs/claude-code) with modern Skills, Rules, and Sub-Agents to provide a complete AI-powered development workflow.
<!-- DE: Diese Vorlage verwendet [Claude Code](https://docs.anthropic.com/en/docs/claude-code) mit modernen Skills, Rules und Sub-Agents für einen vollständigen KI-gestützten Entwicklungs-Workflow. -->

## Quick Start
<!-- DE: ## Schnellstart -->

### 1. Clone & Install
<!-- DE: ### 1. Klonen und installieren -->

```bash
git clone https://github.com/YOUR_USERNAME/ai-coding-starter-kit.git my-project
cd my-project
npm install
```

### 2. (Optional) Supabase Setup
<!-- DE: ### 2. (Optional) Supabase-Einrichtung -->

If you need a backend:
<!-- DE: Falls ein Backend benötigt wird: -->

1. Create Supabase Project: [supabase.com](https://supabase.com)
2. Copy `.env.local.example` to `.env.local`
3. Add your Supabase credentials
4. Uncomment the Supabase client in `src/lib/supabase.ts`
<!-- DE:
1. Supabase-Projekt erstellen: [supabase.com](https://supabase.com)
2. `.env.local.example` nach `.env.local` kopieren
3. Supabase-Zugangsdaten hinzufügen
4. Den Supabase-Client in `src/lib/supabase.ts` auskommentieren
-->

Skip this step if you're building frontend-only (landing pages, portfolios, etc.)
<!-- DE: Diesen Schritt überspringen, wenn nur ein Frontend gebaut wird (Landing Pages, Portfolios usw.) -->

### 3. Start Development
<!-- DE: ### 3. Entwicklung starten -->

```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) in your browser.
<!-- DE: [http://localhost:3000](http://localhost:3000) im Browser öffnen. -->

### 4. Initialize Your Project
<!-- DE: ### 4. Projekt initialisieren -->

Open Claude Code and describe your project. The `/requirements` skill automatically detects that this is a fresh project and enters **Init Mode**:
<!-- DE: Claude Code öffnen und das Projekt beschreiben. Der `/requirements`-Skill erkennt automatisch, dass es sich um ein neues Projekt handelt, und wechselt in den **Init-Modus**: -->

```
/requirements I want to build a project management tool for small teams
where users can create projects, assign tasks, and track progress.
```

The skill will:
1. Ask interactive questions to clarify your vision, target users, and MVP scope
2. Create your **Product Requirements Document** (`docs/PRD.md`)
3. Break the project into individual features (Single Responsibility)
4. Create all **feature specs** (`features/PROJ-1.md`, `PROJ-2.md`, etc.)
5. Update **feature tracking** (`features/INDEX.md`)
6. Recommend which feature to build first
<!-- DE:
Der Skill wird:
1. Interaktive Fragen stellen, um Vision, Zielnutzer und MVP-Umfang zu klären
2. Das **Product Requirements Document** (`docs/PRD.md`) erstellen
3. Das Projekt in einzelne Features aufteilen (Single Responsibility)
4. Alle **Feature-Spezifikationen** erstellen (`features/PROJ-1.md`, `PROJ-2.md` usw.)
5. Das **Feature-Tracking** (`features/INDEX.md`) aktualisieren
6. Empfehlen, welches Feature zuerst gebaut werden soll
-->

You don't need to put everything in the first prompt - a brief description is enough. The skill asks follow-up questions interactively.
<!-- DE: Nicht alles in den ersten Prompt schreiben – eine kurze Beschreibung reicht. Der Skill stellt interaktiv Folgefragen. -->

### 5. Build Features
<!-- DE: ### 5. Features bauen -->

After project initialization, build features one at a time using skills:
<!-- DE: Nach der Projektinitialisierung Features nacheinander mit Skills bauen: -->

```
/architecture    Design the tech approach for features/PROJ-1-user-auth.md
/frontend        Build the UI for features/PROJ-1-user-auth.md
/backend         Build the API for features/PROJ-1-user-auth.md
/qa              Test features/PROJ-1-user-auth.md
/deploy          Deploy to Vercel
```

Each skill suggests the next step when it finishes. Handoffs are always user-initiated.
<!-- DE: Jeder Skill schlägt den nächsten Schritt vor, wenn er fertig ist. Übergaben werden immer vom Nutzer initiiert. -->

To add more features later, run `/requirements` again - it detects the existing PRD and adds a single feature.
<!-- DE: Um später weitere Features hinzuzufügen, `/requirements` erneut ausführen – es erkennt das vorhandene PRD und fügt ein einzelnes Feature hinzu. -->

---

## Available Skills
<!-- DE: ## Verfügbare Skills -->

| Skill | Command | What It Does |
|-------|---------|-------------|
| Requirements Engineer | `/requirements` | Creates feature specs with user stories, acceptance criteria, edge cases |
| Solution Architect | `/architecture` | Designs PM-friendly tech architecture (no code, only high-level design) |
| Frontend Developer | `/frontend` | Builds UI with React, Tailwind CSS, and shadcn/ui |
| Backend Developer | `/backend` | Builds APIs, database schemas, RLS policies with Supabase |
| QA Engineer | `/qa` | Tests features against acceptance criteria + security audit |
| DevOps | `/deploy` | Deploys to Vercel with production-ready checks |
| Help | `/help` | Context-aware guide: shows where you are and what to do next |
<!-- DE:
| Skill | Befehl | Was er tut |
|-------|--------|------------|
| Anforderungsingenieur | `/requirements` | Erstellt Feature-Spezifikationen mit User Stories, Akzeptanzkriterien, Randfällen |
| Solution Architect | `/architecture` | Entwirft PM-freundliche Tech-Architektur (kein Code, nur übergeordnetes Design) |
| Frontend-Entwickler | `/frontend` | Baut UI mit React, Tailwind CSS und shadcn/ui |
| Backend-Entwickler | `/backend` | Baut APIs, Datenbankschemata, RLS-Richtlinien mit Supabase |
| QA-Ingenieur | `/qa` | Testet Features gegen Akzeptanzkriterien + Sicherheitsaudit |
| DevOps | `/deploy` | Deployt auf Vercel mit produktionsreifen Prüfungen |
| Hilfe | `/help` | Kontextbewusster Leitfaden: zeigt, wo du bist und was als nächstes zu tun ist |
-->

### How Skills Work
<!-- DE: ### Wie Skills funktionieren -->

- **Skills** are defined in `.claude/skills/` and auto-discovered by Claude Code
- **Rules** in `.claude/rules/` are auto-applied based on file context (no manual loading)
- **Sub-Agents** run heavy tasks (frontend, backend, QA) in isolated contexts for cost efficiency
- **CLAUDE.md** provides project context automatically at every session start
<!-- DE:
- **Skills** werden in `.claude/skills/` definiert und automatisch von Claude Code erkannt
- **Rules** in `.claude/rules/` werden automatisch basierend auf dem Dateikontext angewendet (kein manuelles Laden)
- **Sub-Agents** führen aufwändige Aufgaben (Frontend, Backend, QA) in isolierten Kontexten durch
- **CLAUDE.md** stellt bei jedem Sitzungsstart automatisch Projektkontext bereit
-->

---

## Development Workflow
<!-- DE: ## Entwicklungs-Workflow -->

```
1. Define    /requirements  -->  Feature spec in features/PROJ-X.md
2. Design    /architecture  -->  Tech design added to feature spec
3. Build     /frontend      -->  UI components implemented
             /backend       -->  APIs + database (if needed)
4. Test      /qa            -->  Test results added to feature spec
5. Ship      /deploy        -->  Deployed to Vercel
```
<!-- DE:
1. Definieren  /requirements  -->  Feature-Spezifikation in features/PROJ-X.md
2. Entwerfen   /architecture  -->  Tech-Design zur Feature-Spezifikation hinzugefügt
3. Bauen       /frontend      -->  UI-Komponenten implementiert
               /backend       -->  APIs + Datenbank (falls benötigt)
4. Testen      /qa            -->  Testergebnisse zur Feature-Spezifikation hinzugefügt
5. Liefern     /deploy        -->  Auf Vercel deployed
-->

### Feature Tracking
<!-- DE: ### Feature-Tracking -->

Features are tracked in `features/INDEX.md`:
<!-- DE: Features werden in `features/INDEX.md` verfolgt: -->

| ID | Feature | Status | Spec |
|----|---------|--------|------|
| PROJ-1 | User Login | Deployed | [Spec](features/PROJ-1-user-login.md) |
| PROJ-2 | Dashboard | In Progress | [Spec](features/PROJ-2-dashboard.md) |

Every skill reads this file at start and updates it when done, preventing duplicate work.
<!-- DE: Jeder Skill liest diese Datei beim Start und aktualisiert sie nach Abschluss, um doppelte Arbeit zu vermeiden. -->

---

## Tech Stack
<!-- DE: ## Tech-Stack -->

| Category | Tool | Why? |
|----------|------|------|
| **Framework** | Next.js 16 | React + Server Components + App Router |
| **Language** | TypeScript | Type safety |
| **Styling** | Tailwind CSS | Utility-first CSS |
| **UI Library** | shadcn/ui | Copy-paste, customizable components |
| **Backend** | Supabase (optional) | PostgreSQL + Auth + Storage + Realtime |
| **Deployment** | Vercel | Zero-config Next.js hosting |
| **Validation** | Zod | Runtime type validation |
<!-- DE:
| Kategorie | Tool | Warum? |
|-----------|------|--------|
| **Framework** | Next.js 16 | React + Server Components + App Router |
| **Sprache** | TypeScript | Typsicherheit |
| **Styling** | Tailwind CSS | Utility-first CSS |
| **UI-Bibliothek** | shadcn/ui | Copy-paste, anpassbare Komponenten |
| **Backend** | Supabase (optional) | PostgreSQL + Auth + Storage + Realtime |
| **Deployment** | Vercel | Zero-Config Next.js-Hosting |
| **Validierung** | Zod | Laufzeit-Typvalidierung |
-->

---

## Project Structure
<!-- DE: ## Projektstruktur -->

```
ai-coding-starter-kit/
+-- CLAUDE.md                        <-- Auto-loaded project context
+-- .claude/
|   +-- settings.json                <-- Team permissions (committed)
|   +-- settings.local.json          <-- Personal overrides (gitignored)
|   +-- rules/                       <-- Auto-applied coding rules
|   |   +-- general.md                   Git workflow, feature tracking
|   |   +-- frontend.md                  shadcn/ui, component standards
|   |   +-- backend.md                   RLS, validation, queries
|   |   +-- security.md                  Secrets, headers, auth
|   +-- skills/                      <-- Invocable workflows (/command)
|   |   +-- requirements/SKILL.md        /requirements
|   |   +-- architecture/SKILL.md        /architecture
|   |   +-- frontend/SKILL.md            /frontend (runs as sub-agent)
|   |   +-- backend/SKILL.md             /backend (runs as sub-agent)
|   |   +-- qa/SKILL.md                  /qa (runs as sub-agent)
|   |   +-- deploy/SKILL.md              /deploy
|   |   +-- help/SKILL.md                /help
|   +-- agents/                      <-- Sub-agent configs
|       +-- frontend-dev.md              Model, tools, limits
|       +-- backend-dev.md
|       +-- qa-engineer.md
+-- features/                        <-- Feature specifications
|   +-- INDEX.md                         Status tracking
|   +-- README.md                        Spec format documentation
+-- docs/
|   +-- PRD.md                       <-- Product Requirements Document
|   +-- production/                  <-- Production setup guides
|       +-- error-tracking.md            Sentry setup (5 min)
|       +-- security-headers.md          XSS/Clickjacking protection
|       +-- performance.md               Lighthouse, optimization
|       +-- database-optimization.md     Indexing, N+1, caching
|       +-- rate-limiting.md             Upstash Redis
+-- src/
|   +-- app/                         <-- Pages (Next.js App Router)
|   +-- components/
|   |   +-- ui/                      <-- shadcn/ui components (35+ installed)
|   +-- hooks/                       <-- Custom React hooks
|   +-- lib/                         <-- Utilities
+-- public/                          <-- Static files
```
<!-- DE:
Erklärung der Projektstruktur:
- CLAUDE.md: Automatisch geladener Projektkontext bei jedem Sitzungsstart
- .claude/rules/: Automatisch angewendete Coding-Regeln je nach Dateikontext
- .claude/skills/: Aufrufbare Workflows über /Befehle
- .claude/agents/: Konfigurationen für Sub-Agents (Modell, Tools, Limits)
- features/: Feature-Spezifikationen und Status-Tracking
- docs/PRD.md: Product Requirements Document
- docs/production/: Produktions-Einrichtungsanleitungen
- src/: Quellcode (Next.js App Router, shadcn/ui-Komponenten, Hooks, Utilities)
-->

---

## Getting Started
<!-- DE: ## Erste Schritte -->

### 1. Fill Out Your PRD
<!-- DE: ### 1. PRD ausfüllen -->

Define your product vision in `docs/PRD.md`:
- What are you building and why?
- Who are the target users?
- What features are on the roadmap?
<!-- DE:
Produktvision in `docs/PRD.md` definieren:
- Was wird gebaut und warum?
- Wer sind die Zielnutzer?
- Welche Features sind auf der Roadmap?
-->

### 2. Build Your First Feature
<!-- DE: ### 2. Erstes Feature bauen -->

Run `/requirements` with your feature idea. The skill will:
- Ask interactive questions to clarify requirements
- Create a feature spec in `features/PROJ-1-name.md`
- Update `features/INDEX.md` with the new feature
- Suggest running `/architecture` as the next step
<!-- DE:
`/requirements` mit der Feature-Idee ausführen. Der Skill wird:
- Interaktive Fragen stellen, um Anforderungen zu klären
- Eine Feature-Spezifikation in `features/PROJ-1-name.md` erstellen
- `features/INDEX.md` mit dem neuen Feature aktualisieren
- Empfehlen, `/architecture` als nächsten Schritt auszuführen
-->

### 3. Add shadcn/ui Components (as needed)
<!-- DE: ### 3. shadcn/ui-Komponenten hinzufügen (bei Bedarf) -->

35+ components are pre-installed. Add more as needed:
<!-- DE: Mehr als 35 Komponenten sind vorinstalliert. Bei Bedarf weitere hinzufügen: -->
```bash
npx shadcn@latest add [component-name]
```

### 4. Production Setup (first deployment)
<!-- DE: ### 4. Produktions-Einrichtung (erste Bereitstellung) -->

When you're ready to deploy, the `/deploy` skill guides you through:
- Vercel setup and deployment
- Error tracking with Sentry
- Security headers configuration
- Performance monitoring with Lighthouse
<!-- DE:
Wenn die Bereitstellung bereit ist, führt der `/deploy`-Skill durch:
- Vercel-Einrichtung und Deployment
- Fehler-Tracking mit Sentry
- Konfiguration der Sicherheits-Header
- Performance-Monitoring mit Lighthouse
-->

See `docs/production/` for detailed setup guides.
<!-- DE: Detaillierte Einrichtungsanleitungen in `docs/production/` finden. -->

---

## How It Works Under the Hood
<!-- DE: ## Wie es im Hintergrund funktioniert -->

### Skills (`.claude/skills/`)
<!-- DE: ### Skills (`.claude/skills/`) -->
Each skill is a structured workflow that Claude Code discovers automatically. Skills can run inline (in the main conversation) or as forked sub-agents (isolated context window).
<!-- DE: Jeder Skill ist ein strukturierter Workflow, den Claude Code automatisch erkennt. Skills können inline (im Hauptgespräch) oder als geforkter Sub-Agent (isoliertes Kontextfenster) ausgeführt werden. -->

| Skill | Execution | Why? |
|-------|-----------|------|
| `/requirements` | Inline | Needs live interaction with user |
| `/architecture` | Inline | Short output, user reviews in real-time |
| `/frontend` | Sub-agent (forked) | Heavy file editing, lots of output |
| `/backend` | Sub-agent (forked) | Heavy file editing, SQL, API code |
| `/qa` | Sub-agent (forked) | Systematic testing, lots of output |
| `/deploy` | Inline | Deployment needs user oversight |
| `/help` | Inline | Quick status check and guidance |
<!-- DE:
| Skill | Ausführung | Warum? |
|-------|------------|--------|
| `/requirements` | Inline | Benötigt direkte Nutzerinteraktion |
| `/architecture` | Inline | Kurze Ausgabe, Nutzer prüft in Echtzeit |
| `/frontend` | Sub-Agent (geforkt) | Aufwändige Dateibearbeitung, viel Ausgabe |
| `/backend` | Sub-Agent (geforkt) | Aufwändige Dateibearbeitung, SQL, API-Code |
| `/qa` | Sub-Agent (geforkt) | Systematische Tests, viel Ausgabe |
| `/deploy` | Inline | Deployment benötigt Nutzeraufsicht |
| `/help` | Inline | Schnelle Statusprüfung und Orientierung |
-->

### Rules (`.claude/rules/`)
<!-- DE: ### Rules (`.claude/rules/`) -->
Coding standards that are auto-applied based on which files Claude is working with. No manual loading needed.
<!-- DE: Coding-Standards, die automatisch basierend auf den Dateien angewendet werden, mit denen Claude arbeitet. Kein manuelles Laden erforderlich. -->

### Sub-Agent Configs (`.claude/agents/`)
<!-- DE: ### Sub-Agent-Konfigurationen (`.claude/agents/`) -->
Lightweight configurations that define model, tool access, and turn limits for forked skills.
<!-- DE: Leichtgewichtige Konfigurationen, die Modell, Tool-Zugriff und Turn-Limits für geforkter Skills definieren. -->

### CLAUDE.md
Auto-loaded at every session start. Contains tech stack, conventions, and references to PRD and feature index.
<!-- DE: ### CLAUDE.md
Wird bei jedem Sitzungsstart automatisch geladen. Enthält Tech-Stack, Konventionen und Verweise auf PRD und Feature-Index. -->

---

## Context Engineering
<!-- DE: ## Kontext-Engineering -->

AI agents work best with clean, structured context - not longer prompts. This template is designed around these principles:
<!-- DE: KI-Agents funktionieren am besten mit sauberem, strukturiertem Kontext – nicht mit längeren Prompts. Diese Vorlage basiert auf folgenden Prinzipien: -->

### State lives in files, not in memory
<!-- DE: ### Zustand lebt in Dateien, nicht im Speicher -->

Every skill reads `features/INDEX.md` and the relevant feature spec at start. After context compaction or a new session, nothing is lost - the agent simply re-reads the files. Progress tracking, acceptance criteria, and tech designs all live in markdown files, not in the conversation.
<!-- DE: Jeder Skill liest `features/INDEX.md` und die relevante Feature-Spezifikation beim Start. Nach Kontextkomprimierung oder einer neuen Sitzung geht nichts verloren – der Agent liest die Dateien einfach erneut. Fortschritts-Tracking, Akzeptanzkriterien und Tech-Designs leben in Markdown-Dateien, nicht im Gespräch. -->

### Context is layered
<!-- DE: ### Kontext ist geschichtet -->

Not everything is loaded at once. Information is layered by relevance:
<!-- DE: Nicht alles wird auf einmal geladen. Informationen werden nach Relevanz geschichtet: -->

| Layer | What | When loaded |
|-------|------|-------------|
| `CLAUDE.md` | Tech stack, conventions, commands | Every session (auto) |
| `.claude/rules/` | Coding standards | When editing matching files (auto) |
| Skill `SKILL.md` | Workflow instructions | When skill is invoked |
| Feature spec | Requirements, AC, tech design | On demand (skill reads it) |
| `docs/production/` | Deployment guides | Only when referenced |
<!-- DE:
| Schicht | Inhalt | Wann geladen |
|---------|--------|--------------|
| `CLAUDE.md` | Tech-Stack, Konventionen, Befehle | Jede Sitzung (automatisch) |
| `.claude/rules/` | Coding-Standards | Beim Bearbeiten passender Dateien (automatisch) |
| Skill `SKILL.md` | Workflow-Anweisungen | Wenn der Skill aufgerufen wird |
| Feature-Spezifikation | Anforderungen, AK, Tech-Design | Bei Bedarf (Skill liest sie) |
| `docs/production/` | Deployment-Anleitungen | Nur wenn referenziert |
-->

### Context is isolated
<!-- DE: ### Kontext ist isoliert -->

Heavy implementation skills (`/frontend`, `/backend`, `/qa`) run as **forked sub-agents** with their own context window. Research noise from one skill doesn't pollute another. Each fork starts clean and loads only what it needs.
<!-- DE: Aufwändige Implementierungs-Skills (`/frontend`, `/backend`, `/qa`) laufen als **geforkter Sub-Agents** mit eigenem Kontextfenster. Recherche-Rauschen eines Skills verunreinigt keine anderen. Jeder Fork startet sauber und lädt nur das, was er benötigt. -->

### Context recovery is built in
<!-- DE: ### Kontextwiederherstellung ist eingebaut -->

All forked skills include a **Context Recovery** section: if the context is compacted mid-task, the agent re-reads the feature spec, checks `git diff` for progress, and continues without restarting or duplicating work.
<!-- DE: Alle geforkten Skills enthalten einen **Kontextwiederherstellungs**-Abschnitt: Falls der Kontext mitten in einer Aufgabe komprimiert wird, liest der Agent die Feature-Spezifikation erneut, prüft `git diff` auf Fortschritt und fährt fort, ohne neu zu starten oder Arbeit zu duplizieren. -->

### Always read, never guess
<!-- DE: ### Immer lesen, nie raten -->

A global rule (`rules/general.md`) enforces: always read a file before modifying it, never assume contents from memory, verify import paths and API routes by reading. This prevents hallucinated code references - the most common source of AI coding errors.
<!-- DE: Eine globale Regel (`rules/general.md`) erzwingt: Dateien immer vor der Bearbeitung lesen, Inhalte nie aus dem Gedächtnis annehmen, Import-Pfade und API-Routen durch Lesen verifizieren. Dies verhindert halluzinierte Code-Referenzen – die häufigste Ursache für KI-Coding-Fehler. -->

---

## Customization for Your Team
<!-- DE: ## Anpassung für dein Team -->

This template is designed as a starting point. Customize it for your team:
<!-- DE: Diese Vorlage ist als Ausgangspunkt konzipiert. Für das Team anpassen: -->

1. **Edit CLAUDE.md** - Add your project-specific conventions and build commands
2. **Edit docs/PRD.md** - Define your product vision and roadmap
3. **Edit .claude/rules/** - Adjust coding standards for your team
4. **Edit .claude/skills/** - Modify workflows to match your process
5. **Edit .claude/settings.json** - Configure team permissions
<!-- DE:
1. **CLAUDE.md bearbeiten** – Projektspezifische Konventionen und Build-Befehle hinzufügen
2. **docs/PRD.md bearbeiten** – Produktvision und Roadmap definieren
3. **.claude/rules/ bearbeiten** – Coding-Standards für das Team anpassen
4. **.claude/skills/ bearbeiten** – Workflows an den eigenen Prozess anpassen
5. **.claude/settings.json bearbeiten** – Team-Berechtigungen konfigurieren
-->

---

## Production Guides
<!-- DE: ## Produktions-Anleitungen -->

Standalone guides in `docs/production/`:
<!-- DE: Eigenständige Anleitungen in `docs/production/`: -->

| Guide | Setup Time | What It Does |
|-------|-----------|-------------|
| [Error Tracking](docs/production/error-tracking.md) | 5 min | Sentry integration for automatic error capture |
| [Security Headers](docs/production/security-headers.md) | 2 min | XSS, Clickjacking, MIME sniffing protection |
| [Performance](docs/production/performance.md) | 10 min | Lighthouse checks, image optimization, caching |
| [Database Optimization](docs/production/database-optimization.md) | 15 min | Indexing, N+1 prevention, query optimization |
| [Rate Limiting](docs/production/rate-limiting.md) | 10 min | Upstash Redis for API abuse prevention |
<!-- DE:
| Anleitung | Einrichtungszeit | Was sie tut |
|-----------|-----------------|-------------|
| [Fehler-Tracking](docs/production/error-tracking.md) | 5 Min. | Sentry-Integration für automatische Fehlererfassung |
| [Sicherheits-Header](docs/production/security-headers.md) | 2 Min. | XSS-, Clickjacking-, MIME-Sniffing-Schutz |
| [Performance](docs/production/performance.md) | 10 Min. | Lighthouse-Prüfungen, Bildoptimierung, Caching |
| [Datenbankoptimierung](docs/production/database-optimization.md) | 15 Min. | Indizierung, N+1-Vermeidung, Abfrageoptimierung |
| [Rate-Limiting](docs/production/rate-limiting.md) | 10 Min. | Upstash Redis zur API-Missbrauchsverhinderung |
-->

---

## Scripts
<!-- DE: ## Skripte -->

```bash
npm run dev        # Development server (localhost:3000)
npm run build      # Production build
npm run start      # Production server
npm run lint       # ESLint
```
<!-- DE:
npm run dev        # Entwicklungsserver (localhost:3000)
npm run build      # Produktions-Build
npm run start      # Produktionsserver
npm run lint       # ESLint
-->

---

## Author
<!-- DE: ## Autor -->

Created by **Alex Sprogis** – AI Product Engineer & Content Creator.
<!-- DE: Erstellt von **Alex Sprogis** – KI-Produktingenieur & Content Creator. -->

- [YouTube](https://www.youtube.com/@alex.sprogis)
- [Website](https://alexsprogis.de)

---

## License
<!-- DE: ## Lizenz -->

MIT License - feel free to use for your projects!
<!-- DE: MIT-Lizenz – kann frei für eigene Projekte verwendet werden! -->
