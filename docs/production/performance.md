# Performance Monitoring
<!-- DE: # Performance-Monitoring -->

## Lighthouse Check (after every deployment)
<!-- DE: ## Lighthouse-Prüfung (nach jeder Bereitstellung) -->

1. Open Chrome DevTools (F12)
2. Go to Lighthouse tab
3. Select: Performance, Accessibility, Best Practices, SEO
4. Generate Report for both Mobile and Desktop
5. **Target: Score > 90** in all categories
<!-- DE:
1. Chrome DevTools öffnen (F12)
2. Zum Lighthouse-Tab wechseln
3. Auswählen: Performance, Barrierefreiheit, Best Practices, SEO
4. Bericht für Mobil und Desktop generieren
5. **Ziel: Score > 90** in allen Kategorien
-->

## Common Performance Issues
<!-- DE: ## Häufige Performance-Probleme -->

### Unoptimized Images
<!-- DE: ### Nicht optimierte Bilder -->
```tsx
// Bad - unoptimized, no lazy loading
<img src="/large-image.jpg" />

// Good - Next.js Image component
import Image from 'next/image'
<Image src="/large-image.jpg" width={800} height={600} alt="Description" />
```
<!-- DE: Schlecht: nicht optimiert, kein Lazy Loading. Gut: Next.js Image-Komponente verwenden. -->
Next.js Image automatically: resizes, lazy-loads, serves WebP format.
<!-- DE: Next.js Image verkleinert automatisch, lädt lazy und liefert das WebP-Format. -->

### Large JavaScript Bundle
<!-- DE: ### Großes JavaScript-Bundle -->
Use dynamic imports for heavy components that aren't needed on initial load:
<!-- DE: Dynamische Importe für schwere Komponenten verwenden, die beim ersten Laden nicht benötigt werden: -->
```tsx
import dynamic from 'next/dynamic'

const HeavyChart = dynamic(() => import('./HeavyChart'), {
  loading: () => <p>Loading chart...</p>,
})
```
<!-- DE: Schwere Komponenten erst bei Bedarf laden (Code Splitting) mit next/dynamic. -->

### Missing Loading States
<!-- DE: ### Fehlende Ladezustände -->
Always show feedback during data fetching:
<!-- DE: Beim Datenabruf immer Feedback anzeigen: -->
```tsx
// Use shadcn Skeleton component
import { Skeleton } from "@/components/ui/skeleton"

if (isLoading) return <Skeleton className="h-12 w-full" />
```
<!-- DE: Die shadcn Skeleton-Komponente für Ladezustände verwenden. -->

### No Caching Strategy
<!-- DE: ### Keine Caching-Strategie -->
Cache slow database queries with `unstable_cache`:
<!-- DE: Langsame Datenbankabfragen mit `unstable_cache` cachen: -->
```typescript
import { unstable_cache } from 'next/cache'

export const getStats = unstable_cache(
  async () => {
    const { data } = await supabase.from('stats').select('*')
    return data
  },
  ['dashboard-stats'],
  { revalidate: 3600 } // Refresh every hour
)
```
<!-- DE: Datenbankabfragen mit unstable_cache von Next.js cachen und stündlich aktualisieren. -->

## Quick Wins Checklist
<!-- DE: ## Checkliste für schnelle Verbesserungen -->
- [ ] All images use `next/image` component
- [ ] Heavy components use dynamic imports
- [ ] Loading states show skeleton/spinner
- [ ] Fonts loaded with `next/font`
- [ ] No unnecessary client-side JavaScript (`"use client"` only when needed)
<!-- DE:
- [ ] Alle Bilder verwenden die `next/image`-Komponente
- [ ] Schwere Komponenten verwenden dynamische Importe
- [ ] Ladezustände zeigen Skeleton/Spinner
- [ ] Schriftarten werden mit `next/font` geladen
- [ ] Kein unnötiges clientseitiges JavaScript (`"use client"` nur wenn nötig)
-->

## Automated Monitoring
<!-- DE: ## Automatisiertes Monitoring -->
- **Vercel Analytics** - Automatic on Pro plan, shows Core Web Vitals
- **Vercel Speed Insights** - Real user performance data
<!-- DE:
- **Vercel Analytics** – Automatisch im Pro-Plan, zeigt Core Web Vitals
- **Vercel Speed Insights** – Performance-Daten echter Nutzer
-->
