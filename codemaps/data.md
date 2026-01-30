# Data Models

**Updated:** 2026-01-30

## Game State (Sverdle)

**Location:** `src/routes/sverdle/game.ts`

```typescript
class Game {
  index: number      // Word index in dictionary
  guesses: string[]  // Player's guesses (6 slots)
  answers: string[]  // Letter match results per guess
  answer: string     // Target word to guess
}
```

### Answer Format
Each answer string uses characters:
- `x` = exact match (correct position)
- `c` = close match (wrong position)
- `_` = no match

### Methods

| Method | Purpose |
|--------|---------|
| `constructor(serialized?)` | Parse cookie or init new game |
| `enter(letters[])` | Submit guess, returns validity |
| `toString()` | Serialize for cookie storage |

### Serialization Format
```
{index}-{guesses joined by space}-{answers joined by space}
```

## Server Data Flow

**+page.server.ts**

```
Load:
  cookies.get('sverdle') → Game → { guesses, answers, answer? }

Actions:
  update: Handle keypress (backspace/letter)
  enter:  Submit guess, validate, update answers
  restart: Delete game cookie
```

## Type Definitions

**src/app.d.ts**
```typescript
declare global {
  namespace App {
    // interface Error {}
    // interface Locals {}
    // interface PageData {}
    // interface PageState {}
    // interface Platform {}
  }
}
```
Default SvelteKit type stubs (not customized).

## Stores

**reduced_motion** (`src/routes/sverdle/reduced-motion.ts`)
```typescript
readable<boolean>
// Respects prefers-reduced-motion media query
// SSR-safe: returns false on server
```

## Data Sources

| Source | Type | Location |
|--------|------|----------|
| Word list | `string[]` | `words.server.ts` |
| Allowed words | `Set<string>` | `words.server.ts` |

Note: Word lists are server-only (`.server.ts`) to prevent cheating.
