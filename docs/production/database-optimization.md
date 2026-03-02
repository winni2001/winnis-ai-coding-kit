# Database Optimization
<!-- DE: # Datenbankoptimierung -->

## 1. Indexing
<!-- DE: ## 1. Indizierung -->

Create indexes on columns used in WHERE, ORDER BY, or JOIN clauses:
<!-- DE: Indizes für Spalten erstellen, die in WHERE-, ORDER BY- oder JOIN-Klauseln verwendet werden: -->

```sql
-- Without index: ~500ms at 100k rows
SELECT * FROM tasks WHERE user_id = 'abc123' ORDER BY created_at DESC;

-- After creating index: <10ms
CREATE INDEX idx_tasks_user_id_created ON tasks(user_id, created_at DESC);
```
<!-- DE: Ohne Index: ~500ms bei 100.000 Zeilen. Nach dem Erstellen des Index: unter 10ms. -->

**Rule of thumb:** If a column appears in WHERE or ORDER BY and the table will have >1000 rows, add an index.
<!-- DE: **Faustregel:** Wenn eine Spalte in WHERE oder ORDER BY vorkommt und die Tabelle mehr als 1.000 Zeilen haben wird, einen Index hinzufügen. -->

Always include indexes in your migration SQL alongside CREATE TABLE.
<!-- DE: Indizes immer zusammen mit CREATE TABLE in das Migrations-SQL aufnehmen. -->

## 2. Avoid N+1 Queries
<!-- DE: ## 2. N+1-Abfragen vermeiden -->

The most common performance problem with ORMs and query builders:
<!-- DE: Das häufigste Performance-Problem bei ORMs und Query-Buildern: -->

```typescript
// Bad: N+1 (1 query for users + N queries for tasks)
const { data: users } = await supabase.from('users').select('*')
for (const user of users) {
  const { data: tasks } = await supabase
    .from('tasks')
    .select('*')
    .eq('user_id', user.id)
}

// Good: Single query with join (1 query total)
const { data } = await supabase
  .from('users')
  .select('*, tasks(*)')
```
<!-- DE: Schlecht: N+1 (1 Abfrage für Nutzer + N Abfragen für Aufgaben). Gut: Einzelne Abfrage mit Join (insgesamt 1 Abfrage). -->

## 3. Always Limit Results
<!-- DE: ## 3. Ergebnisse immer begrenzen -->

Never return unbounded results from the database:
<!-- DE: Niemals unbegrenzte Ergebnisse aus der Datenbank zurückgeben: -->

```typescript
// Bad: Returns ALL rows
const { data } = await supabase.from('tasks').select('*')

// Good: Returns max 50 rows
const { data } = await supabase.from('tasks').select('*').limit(50)

// Better: Paginated
const { data } = await supabase
  .from('tasks')
  .select('*')
  .range(0, 49)  // First 50 rows
```
<!-- DE: Schlecht: Gibt ALLE Zeilen zurück. Gut: Gibt maximal 50 Zeilen zurück. Besser: Paginiert (erste 50 Zeilen). -->

## 4. Caching Strategy
<!-- DE: ## 4. Caching-Strategie -->

For data that changes rarely (dashboard stats, config, categories):
<!-- DE: Für Daten, die sich selten ändern (Dashboard-Statistiken, Konfiguration, Kategorien): -->

```typescript
import { unstable_cache } from 'next/cache'

export const getCategories = unstable_cache(
  async () => {
    const { data } = await supabase.from('categories').select('*')
    return data
  },
  ['categories'],          // Cache key
  { revalidate: 3600 }    // Refresh every hour
)
```
<!-- DE: Daten, die sich selten ändern, mit unstable_cache von Next.js cachen. Cache-Key und stündliche Aktualisierung konfigurieren. -->

**When to cache:**
- Data that changes less than once per hour
- Expensive aggregation queries
- Data shared across all users (not user-specific)
<!-- DE:
**Wann cachen:**
- Daten, die sich seltener als einmal pro Stunde ändern
- Aufwändige Aggregationsabfragen
- Daten, die von allen Nutzern geteilt werden (nicht nutzerspezifisch)
-->

**When NOT to cache:**
- User-specific data that changes frequently
- Real-time data (use Supabase Realtime instead)
<!-- DE:
**Wann NICHT cachen:**
- Nutzerspezifische Daten, die sich häufig ändern
- Echtzeit-Daten (stattdessen Supabase Realtime verwenden)
-->

## 5. Select Only What You Need
<!-- DE: ## 5. Nur benötigte Spalten abfragen -->

```typescript
// Bad: Fetches all columns
const { data } = await supabase.from('users').select('*')

// Good: Fetches only needed columns
const { data } = await supabase.from('users').select('id, name, avatar_url')
```
<!-- DE: Schlecht: Ruft alle Spalten ab. Gut: Ruft nur die benötigten Spalten ab. -->
