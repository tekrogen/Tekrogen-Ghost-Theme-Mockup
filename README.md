# Tekrogen — Ghost Theme Mockup (v04)

High-fidelity design mockups for a custom **Ghost** publishing theme for **Tekrogen**, a
four-entity practice ("four wings, one pursuit") publishing under a single mark across
`.org`, `.studio`, `.com`, and `.net`. The theme is organized around **seven content
types**: Use Case Study, SaaS Evaluation, Tech Rating, Product Page, Demo / POC,
Documentation, and Research Article.

## Purpose

These files explore and lock the information architecture and visual design for the
theme's key templates *before* implementation. Each mockup presents several candidate
**directions** as tabs so they can be compared side by side, with one direction marked
**LOCKED** as the chosen path.

## Templates explored (the four directions)

| Tab | Template | Route | Notes |
|-----|----------|-------|-------|
| **B** | Homepage — *Editorial Feed* | `/` | **LOCKED.** Chronological river: a featured note on top, the rest in a numbered list; the 7 types live in a *Topics* dropdown. |
| **C** | Topic page — *Library Hub* | `/topics/:slug` | Landing page after picking a topic; featured note + curated lanes of related work. |
| **A** | Library — *Index of Seven* | `/library` | Full library: a uniform grid of the 7 content types, each a doorway to its recent items. |
| **D** | Post details — *Post templates* | `/:slug` | Per-type article templates (scored ratings, comparison tables, product CTAs, etc.). |

A built-in **Paper / Ink** surface toggle previews each direction in light and dark modes.

## Files

- **`index.html`** — the current high-fidelity mockup (all four directions + Ink/Paper toggle, defaults to Ink). *Main deliverable* (formerly `Ghost Theme Mockup v03.html`). Brand-compliance pass applied — see `Brand Compliance Checklist.md`.
- **`archive/Ghost Theme Mockup v02.html`** — prior version, kept for reference (pre-compliance pass).
- **`Brand Compliance Checklist.md`** — audit of the mockup against the Tekrogen Brand System, with each item's status.
- **`archive/Ghost Theme Wireframes.html`** — low-fidelity wireframes used to define the homepage layout. Archived; not an active deliverable.
- **`tekrogen/`** — brand design tokens consumed by the mockup: `colors_and_type.css` (palette + type scale), fonts, favicon, and the Tekrogen mark/icon SVGs.
- **`assets/`** — supporting assets.
- **`uploads/`** — user-supplied source material.

## Design system

Built on the Tekrogen tokens in `tekrogen/colors_and_type.css`:

- **Type:** Poppins (display/sans), Manrope (body), JetBrains Mono (meta/labels).
- **Color:** cyan accent (`--tk-cyan`) over ink/paper neutrals, with per-pillar accent
  colors. Paper-mode muted tokens are darkened in the mockup so small mono meta text
  clears WCAG-AA contrast.

> The app chrome (top bar, tabs, direction headers, surface toggle) is a presentation
> harness for reviewing options — it is **not** part of the Ghost theme itself.
