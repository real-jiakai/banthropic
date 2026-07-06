# Banthropic Codebase Guide

## Project Overview

**Banthropic** is a satirical, single-page Astro static site that parodies Claude's account ban system. It's a joke/parody project (not affiliated with Anthropic) that humorously "scans" users for ban-risk signals (timezone, language, fonts, IP location, payment method, etc.) and displays a fictional "verdict" with a pixel-art police officer. All detection runs locally in the browser; only one IP lookup request is made to external APIs (ipapi.is, ipwho.is, ipapi.co as fallbacks).

## Commands

From `package.json`:

```bash
npm install       # Install dependencies (Astro, Tailwind CSS v4)
npm run dev       # Start dev server → http://localhost:4321
npm run build     # Build static output to dist/
npm run preview   # Preview built site
```

## Architecture

### Static Site Structure
- **Astro 5** with pure static output (no SSR)
- **Tailwind CSS 4** with `@tailwindcss/vite` plugin
- **Language routing:** Root `/` redirects to `/zh/` (Chinese, if `navigator.language` contains "zh") or `/en/` (English) via `src/pages/index.astro`; language-specific pages at `src/pages/zh/index.astro` and `src/pages/en/index.astro`

### i18n (Internationalization)
- All UI text lives in `src/i18n.ts`
- Exports typed language strings: `meta` (title/description), `ui` (page UI), `clientDict` (for client-side JavaScript)
- Split into `zh` and `en` keys; JSON structure mirrors each other
- Type: `type Lang = "zh" | "en"`

### Component & Layout
- `src/layouts/Layout.astro` — Base HTML wrapper, imports global styles, renders `<slot />`
- `src/components/Site.astro` — Main page content (detector card, factors list, notice, FAQ, footer)
- `src/components/Dario.astro` — Pixel-art police officer, SVG-based, rendered at build time from character grids

### Styles
- `src/styles/global.css` — Tailwind imports, custom theme tokens (colors, fonts), animations (blink, doom-shake)
- Tailwind tokens: `--color-cream`, `--color-ink`, `--color-clay`, `--color-safe` (green), `--color-warn` (orange), `--color-alarm` (red), etc.
- Font families: `--font-hei` (CJK sans), `--font-song` (CJK serif), `--font-pixel` (monospace)

## Key Conventions

- **Bilingual edits:** Changes to UI text must update *both* `zh` and `en` entries in `src/i18n.ts` to keep languages in sync
- **Client-side dictionary:** The `clientDict` object is JSON-stringified and inlined into HTML; it powers the scan results log on the page
- **Static-only:** No dynamic API routes; the only network call is the client-side IP lookup (configurable fallback APIs in client code)
- **CSS variables:** All colors and fonts are stored as Tailwind theme tokens; modify `src/styles/global.css` for color or font changes

## File Locations

- Page content: `src/pages/zh/index.astro`, `src/pages/en/index.astro`
- Shared components: `src/components/`
- Styles: `src/styles/global.css`
- Translations: `src/i18n.ts`
