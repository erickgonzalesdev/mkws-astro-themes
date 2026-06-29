# mkws-astro-themes

Minimal Astro themes modeled directly after [mkws](https://mkws.sh/) and its built-in theme collection. Classless CSS, centered single-column layout, no frameworks, no classes needed in content.

## Project structure

```
src/
  layouts/
    BaseLayout.astro      # Root layout — accepts theme prop ("sans" | "sans-dark")
    SansLayout.astro      # Shortcut for theme="sans"
    SansDarkLayout.astro  # Shortcut for theme="sans-dark"
  pages/
    index.astro           # Homepage — uses sans theme
    dark.astro            # Dark theme preview — uses sans-dark theme
  styles/
    sans.css              # Light theme: white bg, #222 text, system sans-serif
    sans-dark.css         # Dark theme: #1a1a1a bg, #d4d4d4 text, same font stack
```

## Themes

| Theme | Layout | Description |
|---|---|---|
| `sans` | `SansLayout.astro` | White `#fff` bg, `#222` text, system sans-serif |
| `sans-dark` | `SansDarkLayout.astro` | Black `#000` bg, `#eee` text — newnight palette (t.mkws.sh/newnight) |

Both themes include a top nav bar styled after mkws.sh — `padding: 2rem 0`, `text-align: right`, plain links with a slide-in underline on hover.

## Using a theme

```astro
---
import SansLayout from "../layouts/SansLayout.astro";
---
<SansLayout title="My page">
  <h1>Hello world</h1>
  <p>No classes needed — just semantic HTML.</p>
</SansLayout>
```

Or via `BaseLayout` with the `theme` prop:

```astro
---
import BaseLayout from "../layouts/BaseLayout.astro";
---
<BaseLayout title="My page" theme="sans-dark">
  <h1>Hello world</h1>
</BaseLayout>
```

## Development

```bash
npm install
npm run dev       # start dev server at http://localhost:4321
npm run build     # static build to dist/
npm run preview   # preview built output
```

When starting the dev server for Claude Code sessions, use background mode so it doesn't block:

```
astro dev --background
```

Manage with `astro dev stop`, `astro dev status`, `astro dev logs`.

## Design decisions

- CSS is embedded inline in `<style>` at build time (via `?raw` import) — same approach mkws uses, no external stylesheet requests.
- No Tailwind, no component libraries, no JavaScript in the browser.
- `BaseLayout` is the single source of truth for the HTML shell; theme layouts are thin wrappers.
- Nav links are hardcoded in `BaseLayout` — edit there to change them globally.

## Modernization (minimal)

Both themes include subtle modern touches that stay invisible during normal reading:

- `scroll-behavior: smooth` — anchor jumps animate
- `text-rendering: optimizeLegibility` + `-webkit-font-smoothing: antialiased` — sharper type
- `::selection` — accent-colored text highlight
- `a { transition: color 0.15s }` — link color fades on hover instead of snapping
- Nav underline slide-in — underline grows left-to-right on hover via `background-size` transition
- `:focus-visible` ring — clean 2px outline for keyboard navigation

## Images

Images use `display: block; max-width: 100%; height: auto; margin-bottom: 1rem` — same block rhythm as paragraphs, no inline baseline gap. No lazy loading is applied automatically; add `loading="lazy"` per image in content.
