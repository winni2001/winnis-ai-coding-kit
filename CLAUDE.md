# AI Coding Starter Kit
<!-- DE: # KI-Programmier-Starter-Kit -->

> A Next.js template with an AI-powered development workflow using specialized skills for Requirements, Architecture, Frontend, Backend, QA, and Deployment.
<!-- DE: > Eine Next.js-Vorlage mit einem KI-gestützten Entwicklungsworkflow, der spezialisierte Skills für Anforderungen, Architektur, Frontend, Backend, QA und Deployment verwendet. -->

## Tech Stack
<!-- DE: ## Technologie-Stack -->

- **Framework:** Next.js 16 (App Router), TypeScript
- **Styling:** Tailwind CSS + shadcn/ui (copy-paste components)
- **Backend:** Supabase (PostgreSQL + Auth + Storage) - optional
- **Deployment:** Vercel
- **Validation:** Zod + react-hook-form
- **State:** React useState / Context API
<!-- DE:
- **Framework:** Next.js 16 (App Router), TypeScript
- **Styling:** Tailwind CSS + shadcn/ui (Kopier-und-Einfüge-Komponenten)
- **Backend:** Supabase (PostgreSQL + Auth + Storage) – optional
- **Deployment:** Vercel
- **Validierung:** Zod + react-hook-form
- **State:** React useState / Context API
-->

## Project Structure
<!-- DE: ## Projektstruktur -->

```
src/
  app/              Pages (Next.js App Router)
  components/
    ui/             shadcn/ui components (NEVER recreate these)
  hooks/            Custom React hooks
  lib/              Utilities (supabase.ts, utils.ts)
features/           Feature specifications (PROJ-X-name.md)
  INDEX.md          Feature status overview
docs/
  PRD.md            Product Requirements Document
  production/       Production guides (Sentry, security, performance)
```
<!-- DE:
Verzeichnisstruktur:
- src/app/ → Seiten (Next.js App Router)
- src/components/ui/ → shadcn/ui-Komponenten (NIEMALS neu erstellen)
- src/hooks/ → Eigene React Hooks
- src/lib/ → Hilfsfunktionen (supabase.ts, utils.ts)
- features/ → Feature-Spezifikationen (PROJ-X-name.md)
- features/INDEX.md → Feature-Status-Übersicht
- docs/PRD.md → Produktanforderungsdokument
- docs/production/ → Produktionsleitfäden (Sentry, Sicherheit, Performance)
-->

## Development Workflow
<!-- DE: ## Entwicklungsworkflow -->

1. `/requirements` - Create feature spec from idea
2. `/architecture` - Design tech architecture (PM-friendly, no code)
3. `/frontend` - Build UI components (shadcn/ui first!)
4. `/backend` - Build APIs, database, RLS policies
5. `/qa` - Test against acceptance criteria + security audit
6. `/deploy` - Deploy to Vercel + production-ready checks
<!-- DE:
1. `/requirements` - Feature-Spezifikation aus einer Idee erstellen
2. `/architecture` - Technische Architektur gestalten (PM-freundlich, kein Code)
3. `/frontend` - UI-Komponenten bauen (shadcn/ui zuerst!)
4. `/backend` - APIs, Datenbank, RLS-Richtlinien bauen
5. `/qa` - Gegen Akzeptanzkriterien testen + Sicherheitsprüfung
6. `/deploy` - Auf Vercel deployen + Produktionsbereitschaft prüfen
-->

## Feature Tracking
<!-- DE: ## Feature-Verfolgung -->

All features tracked in `features/INDEX.md`. Every skill reads it at start and updates it when done. Feature specs live in `features/PROJ-X-name.md`.
<!-- DE: Alle Features werden in `features/INDEX.md` verfolgt. Jeder Skill liest diese Datei zu Beginn und aktualisiert sie nach Abschluss. Feature-Spezifikationen befinden sich in `features/PROJ-X-name.md`. -->

## Key Conventions
<!-- DE: ## Wichtige Konventionen -->

- **Feature IDs:** PROJ-1, PROJ-2, etc. (sequential)
- **Commits:** `feat(PROJ-X): description`, `fix(PROJ-X): description`
- **Single Responsibility:** One feature per spec file
- **shadcn/ui first:** NEVER create custom versions of installed shadcn components
- **Human-in-the-loop:** All workflows have user approval checkpoints
<!-- DE:
- **Feature-IDs:** PROJ-1, PROJ-2, usw. (fortlaufend)
- **Commits:** `feat(PROJ-X): Beschreibung`, `fix(PROJ-X): Beschreibung`
- **Einzelverantwortlichkeit:** Ein Feature pro Spezifikationsdatei
- **shadcn/ui zuerst:** NIEMALS eigene Versionen installierter shadcn-Komponenten erstellen
- **Mensch im Prozess:** Alle Workflows haben Nutzergenehmigungspunkte
-->

## Build & Test Commands
<!-- DE: ## Build- und Testbefehle -->

```bash
npm run dev        # Development server (localhost:3000)
npm run build      # Production build
npm run lint       # ESLint
npm run start      # Production server
```
<!-- DE:
npm run dev   → Entwicklungsserver (localhost:3000)
npm run build → Produktions-Build
npm run lint  → ESLint-Prüfung
npm run start → Produktionsserver
-->

## Product Context
<!-- DE: ## Produktkontext -->

@docs/PRD.md

## Feature Overview
<!-- DE: ## Feature-Übersicht -->

@features/INDEX.md
