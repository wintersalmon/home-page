# Frontend Structure

**Updated:** 2026-01-30

## Route Hierarchy

```
/                 +page.svelte      Home page
├── /about        +page.svelte      About page
└── /sverdle      +page.svelte      Wordle game
    └── /how-to-play  +page.svelte  Game instructions
```

## Layout

**+layout.svelte** (root)
- Imports `Header.svelte` and `app.css`
- Flexbox layout: header, main (slot), footer
- Max-width: 64rem centered

## Components

| Component | Location | Purpose |
|-----------|----------|---------|
| Header.svelte | src/routes/ | Navigation bar with SvelteKit/GitHub links |
| Counter.svelte | src/routes/ | Animated counter demo using Svelte spring |

### Header.svelte
- Uses `$app/stores` page store for active route
- Links: SvelteKit docs, GitHub profile
- Nav items: Welcome, To, My Page

### Counter.svelte
- Spring animation via `svelte/motion`
- Reactive statements (`$:`) for animation offset
- Increase/decrease buttons with SVG icons

## State Management

1. **Svelte Reactivity**
   - `$:` reactive statements (Counter.svelte)
   - Component-local state (`let count = 0`)

2. **Svelte Stores**
   - `$app/stores`: page store for routing state
   - `reduced_motion`: readable store for accessibility

3. **Server State**
   - Cookie-based game state (Sverdle)
   - Form actions for mutations

## Styling Approach

**TailwindCSS**
- PostCSS integration
- Utility classes in markup
- `theme()` function in scoped styles

**Scoped Styles**
- Component `<style>` blocks
- CSS variables: `--color-theme-1`, `--color-bg-1`

**Global Styles**
- `src/app.css`: Tailwind directives, base styles
- `:global()` selector for HTML element styles

## Assets

Located in `src/lib/images/`:
- `svelte-logo.svg` - SvelteKit logo
- `github.svg` - GitHub icon
- `svelte-welcome.webp/.png` - Welcome image
