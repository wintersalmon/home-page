# Architecture Overview

**Updated:** 2026-01-30

## Tech Stack

| Layer | Technology | Version |
|-------|------------|---------|
| Framework | SvelteKit | 2.0 |
| UI | Svelte | 4.2 |
| Language | TypeScript | 5.0 |
| Styling | TailwindCSS | 3.4 |
| Build | Vite | 5.0 |
| Deployment | Static Adapter | SSG |

## Project Structure

```
home-page/
├── src/
│   ├── routes/           # File-based routing
│   │   ├── +layout.svelte    # Root layout
│   │   ├── +page.svelte      # Home page
│   │   ├── Header.svelte     # Nav component
│   │   ├── Counter.svelte    # Demo component
│   │   ├── about/            # /about route
│   │   └── sverdle/          # /sverdle game route
│   ├── lib/              # Shared assets
│   │   └── images/           # SVG, PNG, WebP
│   └── app.d.ts          # Type declarations
├── static/               # Static files (favicon)
├── build/                # Generated output (SSG)
└── config files          # svelte.config.js, tailwind.config.js
```

## Build Configuration

**svelte.config.js**
- Adapter: `@sveltejs/adapter-static` (SSG)
- Fallback: `index.html` (SPA mode)
- Preprocessor: `vitePreprocess()` for TypeScript/PostCSS

**tailwind.config.js**
- Content: `./src/**/*.{html,js,svelte,ts}`
- No custom theme extensions

## Key Patterns

1. **Static Site Generation (SSG)**
   - Pre-rendered at build time
   - SPA fallback for client-side routing

2. **File-based Routing**
   - `+page.svelte` = route component
   - `+page.ts` = client-side load
   - `+page.server.ts` = server-side load/actions
   - `+layout.svelte` = shared layout

3. **Server-side Form Actions**
   - Sverdle game uses form actions for guess validation
   - Cookie-based state persistence

4. **Styling**
   - TailwindCSS utility classes (PostCSS)
   - Scoped component styles (`<style>` blocks)
   - CSS variables for theming (`--color-theme-1`)
