# Frontend Implementation Checklist
<!-- DE: # Frontend-Implementierungs-Checkliste -->

Before marking frontend as complete:
<!-- DE: Vor dem Abschließen des Frontends: -->

## shadcn/ui
- [ ] Checked shadcn/ui for EVERY UI component needed
- [ ] No custom duplicates of shadcn components created
- [ ] Missing shadcn components installed via `npx shadcn@latest add`
<!-- DE:
- [ ] shadcn/ui auf JEDE benötigte UI-Komponente geprüft
- [ ] Keine eigenen Duplikate von shadcn-Komponenten erstellt
- [ ] Fehlende shadcn-Komponenten via `npx shadcn@latest add` installiert
-->

## Existing Code
<!-- DE: ## Vorhandener Code -->
- [ ] Checked existing project components via `git ls-files src/components/`
- [ ] Reused existing components where possible
<!-- DE:
- [ ] Vorhandene Projektkomponenten via `git ls-files src/components/` geprüft
- [ ] Vorhandene Komponenten wo möglich wiederverwendet
-->

## Design
<!-- DE: ## Design -->
- [ ] Design preferences clarified with user (if no mockups)
- [ ] Component architecture from Solution Architect followed
<!-- DE:
- [ ] Designpräferenzen mit dem Nutzer geklärt (falls keine Mockups vorhanden)
- [ ] Komponentenarchitektur vom Solution Architect befolgt
-->

## Implementation
<!-- DE: ## Implementierung -->
- [ ] All planned components implemented
- [ ] All components use Tailwind CSS (no inline styles, no CSS modules)
- [ ] Loading states implemented (spinner/skeleton during data fetches)
- [ ] Error states implemented (user-friendly error messages)
- [ ] Empty states implemented ("No data yet" messages)
<!-- DE:
- [ ] Alle geplanten Komponenten implementiert
- [ ] Alle Komponenten verwenden Tailwind CSS (keine Inline-Styles, keine CSS-Module)
- [ ] Ladezustände implementiert (Spinner/Skeleton während Datenabruf)
- [ ] Fehlerzustände implementiert (nutzerfreundliche Fehlermeldungen)
- [ ] Leerzustände implementiert („Noch keine Daten"-Meldungen)
-->

## Quality
<!-- DE: ## Qualität -->
- [ ] Responsive: Mobile (375px), Tablet (768px), Desktop (1440px)
- [ ] Accessibility: Semantic HTML, ARIA labels, keyboard navigation
- [ ] TypeScript: No errors (`npm run build` passes)
- [ ] ESLint: No warnings (`npm run lint`)
<!-- DE:
- [ ] Responsiv: Mobil (375px), Tablet (768px), Desktop (1440px)
- [ ] Barrierefreiheit: Semantisches HTML, ARIA-Labels, Tastaturnavigation
- [ ] TypeScript: Keine Fehler (`npm run build` läuft durch)
- [ ] ESLint: Keine Warnungen (`npm run lint`)
-->

## Verification (run before marking complete)
<!-- DE: ## Verifizierung (vor dem Abschluss ausführen) -->
- [ ] `npm run build` passes without errors
- [ ] All acceptance criteria from feature spec addressed in UI
- [ ] `features/INDEX.md` status updated to "In Progress"
<!-- DE:
- [ ] `npm run build` läuft ohne Fehler durch
- [ ] Alle Akzeptanzkriterien aus der Feature-Spezifikation in der UI abgedeckt
- [ ] `features/INDEX.md` Status auf „In Progress" aktualisiert
-->

## Completion
<!-- DE: ## Abschluss -->
- [ ] User has reviewed and approved the UI in browser
- [ ] Code committed to git
<!-- DE:
- [ ] Nutzer hat die UI im Browser geprüft und genehmigt
- [ ] Code in git eingecheckt
-->
