# Frontend Development Rules
<!-- DE: # Frontend-Entwicklungsregeln -->

## shadcn/ui First (MANDATORY)
<!-- DE: ## shadcn/ui zuerst (PFLICHT) -->
- Before creating ANY UI component, check if shadcn/ui has it: `ls src/components/ui/`
- NEVER create custom implementations of: Button, Input, Select, Checkbox, Switch, Dialog, Modal, Alert, Toast, Table, Tabs, Card, Badge, Dropdown, Popover, Tooltip, Navigation, Sidebar, Breadcrumb
- If a shadcn component is missing, install it: `npx shadcn@latest add <name> --yes`
- Custom components are ONLY for business-specific compositions that internally use shadcn primitives
<!-- DE:
- Vor der Erstellung JEDER UI-Komponente prüfen, ob shadcn/ui sie enthält: `ls src/components/ui/`
- NIEMALS eigene Implementierungen erstellen von: Button, Input, Select, Checkbox, Switch, Dialog, Modal, Alert, Toast, Table, Tabs, Card, Badge, Dropdown, Popover, Tooltip, Navigation, Sidebar, Breadcrumb
- Falls eine shadcn-Komponente fehlt, installieren: `npx shadcn@latest add <name> --yes`
- Eigene Komponenten NUR für geschäftsspezifische Kompositionen, die intern shadcn-Primitive verwenden
-->

## Import Pattern
<!-- DE: ## Import-Muster -->
```tsx
import { Button } from "@/components/ui/button"
import { Card, CardHeader, CardTitle, CardContent } from "@/components/ui/card"
```
<!-- DE: Standardimporte für shadcn/ui-Komponenten. -->

## Component Standards
<!-- DE: ## Komponentenstandards -->
- Use Tailwind CSS exclusively (no inline styles, no CSS modules)
- All components must be responsive (mobile 375px, tablet 768px, desktop 1440px)
- Implement loading states, error states, and empty states
- Use semantic HTML and ARIA labels for accessibility
- Keep components small and focused
- Use TypeScript interfaces for all props
<!-- DE:
- Ausschließlich Tailwind CSS verwenden (keine Inline-Styles, keine CSS-Module)
- Alle Komponenten müssen responsiv sein (Mobil 375px, Tablet 768px, Desktop 1440px)
- Lade-, Fehler- und Leerzustände implementieren
- Semantisches HTML und ARIA-Labels für Barrierefreiheit verwenden
- Komponenten klein und fokussiert halten
- TypeScript-Interfaces für alle Props verwenden
-->

## Auth Best Practices (Supabase)
<!-- DE: ## Authentifizierungs-Best-Practices (Supabase) -->
- Use `window.location.href` for post-login redirect (not `router.push`)
- Always verify `data.session` exists before redirecting
- Always reset loading state in all code paths (success, error, finally)
<!-- DE:
- `window.location.href` für die Weiterleitung nach dem Login verwenden (nicht `router.push`)
- Vor der Weiterleitung immer prüfen, ob `data.session` vorhanden ist
- Ladezustand in allen Codepfaden zurücksetzen (Erfolg, Fehler, finally)
-->
