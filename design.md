# Design system — "The Ledger"

This is the single source of truth for visual decisions on this site. Read it before making
any design change; update it the moment a decision changes, so it never drifts out of sync
with `src/styles/global.css`.

## Concept

Öjerviks gård isn't "a nice Swedish farm" — it's the actual setting for Selma Lagerlöf's
magical-realist folklore (the farm is "Sjö" in *Gösta Berlings saga*), a family that's
recited the same poem crossing into Värmland for generations, and a documented 700-year
chronology (Bronze Age graves through the present owner). The design treats the site like
the farm's own land-record book — an archival ledger, not a hospitality brochure.

**Guardrail**: avoid the three current AI-design clichés — (1) warm cream + high-contrast
serif + terracotta accent, (2) near-black + single neon accent, (3) newspaper hairline-rule
broadsheet layout. This system intentionally differs from all three (see palette below).

## Palette

Defined as CSS custom properties in `src/styles/global.css` (`:root`). Reused verbatim in
any new page or component — never introduce a one-off color.

| Token | Hex | Use |
|---|---|---|
| `--paper` | `#ede9df` | Page background — warm greige, not cream |
| `--paper-raised` | `#f6f3ea` | Cards, panels, anything "on top of" the page |
| `--ink` | `#16221f` | Body text — near-black forest-teal, not flat black |
| `--falu` | `#8c2f1c` | Primary accent — real historic Falu-red pigment, not terracotta. Links, CTAs, borders that need emphasis |
| `--dusk` | `#d98c74` | Secondary accent, pulled from the actual sky color in the farm's drone photography. Used sparingly |
| `--moss` | `#5b6b4f` | Tertiary accent — fact-card title bars, nature-adjacent emphasis |
| `--border` | `#c9c2ae` | Hairlines, card borders |
| `--muted` | `#5c5a4e` | Secondary/caption text |

## Typography

Self-hosted via `@fontsource/*` packages (never Google Fonts CDN — avoids sending EU visitor
IPs to Google, relevant for a Swedish site). Imported at the top of `global.css`.

- **Display** (`--font-display`, "Fraunces"): all headings (`h1`/`h2`/`h3`), the `.signature`
  block, poem blocks. Weight 500/600, used at large sizes only — never body text.
- **Body** (`--font-body`, "Inter"): all running text, default on `<body>`.
- **Mono** (`--font-mono`, "IBM Plex Mono"): anything data-like — dates, distances, nav links,
  footer, `.entry-meta`, `.breadcrumb`, `.cta` buttons. Gives factual metadata a "log entry"
  feel that's distinct from prose.

## Layout components (class reference)

All defined in `src/styles/global.css` — reuse these rather than inventing new patterns:

- `.site-header` / `.site-footer` — global nav and footer (mono type, uppercase nav links)
- `.hero` / `.hero-caption` — full-bleed image with overlaid title, used at the top of a page
- `.page-header` — standard title + intro for any non-hero page
- `.lede` — a single emphasized intro paragraph
- `.cards` / `.card` — image-led link tiles (used for section hubs: homepage, Activities index)
- `.prose` — long-form article body copy (History, article pages)
- `.entry-list` / `.entry-title` / `.entry-meta` — reference-style lists (Activities category
  pages). `.entry-meta` renders as a small red pill/stamp for distances and times
- `.factcard` / `.factcard-title` — a floated "quick facts" card for article pages (type,
  location, distance, etc.) — moss-green title bar
- `.breadcrumb` — mono, muted trail at the top of nested pages (`Activities › Category › Page`)
- `.gallery` / `.amenities` / `.floorplans` — photo grids and spec lists (Farm page)
- `.cta` — the single accent-colored action button style (Falu red, mono type)
- `.ledger` / `.ledger-entry` / `.ledger-year` / `.ledger-note` — see Signature element below

## Signature element: the marginalia ledger

A vertical timeline component (`src/components/Ledger.astro`) listing real dated facts from
the farm's own documented history (Bronze Age → 1457 → the Sandelin story → ownership
changes → 2020). Rows fade in on scroll via a small `IntersectionObserver` script inside the
component — this is the **one** deliberate motion moment on the site. Currently used on the
homepage and the History page. Don't add more animation elsewhere; this is the site's one
orchestrated gesture, not a pattern to repeat per-page.

## Motion rules

- Exactly one animated moment: the ledger scroll-reveal.
- Everything else is static. No hover-lift cards, no scroll parallax, no page-load sequences.
- `@media (prefers-reduced-motion: reduce)` is respected globally (see top of `global.css`).

## Section structure

- **Farm site** (`/`, `/farm`, `/celebrate`, `/history`): uses `Layout.astro` + `global.css`.
- **Activities** (`/activities/*`): 14 pages — a hub (4 category tiles, no "featured" section
  by design), 4 category pages, 9 article pages with `.factcard` sidebars. Uses the *same*
  `Layout.astro` and `global.css` as the farm site — there is deliberately no separate layout
  or stylesheet for this section anymore (an earlier Wikipedia-styled version was merged in
  and retired; don't reintroduce a second design system).
- Emoji: used sparingly, if at all. An earlier draft of the Activities pages leaned on them
  heavily and it read as cluttered next to the restrained ledger aesthetic — avoid reverting
  to that.

## Open / upcoming

- Article and category pages in `/activities/*` don't have photography yet — imagery pass is
  planned as a follow-up, then a design tightening pass once real images are in place.
