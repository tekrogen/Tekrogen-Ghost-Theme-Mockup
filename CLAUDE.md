# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

High-fidelity design mockups for a custom **Ghost** publishing theme for **Tekrogen** (a
four-entity practice publishing under one mark across `.org`, `.studio`, `.com`, `.net`).
The deliverable is a self-contained HTML mockup used to **review and lock** information
architecture and visual design *before* the theme is implemented in Ghost. It is not a
runnable application and has no build, test, or lint tooling.

## Working in this repo

- **Preview:** open `index.html` directly in a browser (`open index.html`). No server or
  build step.
- **Host-runtime features are inert locally.** The Tweaks panel and `<image-slot>`
  persistence only function inside the Claude design host ("omelette" runtime) that
  serves these files. The Tweaks panel is shown/hidden by `postMessage` (`__activate_edit_mode`
  / `__deactivate_edit_mode`) from the parent frame; image-slot drops persist via a sidecar
  the host bridge only allows at the project root. Opening `index.html` from disk shows the
  default state with these features dormant — that is expected, not a bug.
- **Versioning — bump every marker together.** The project version uses the `vX.Y.Z` tag
  format (matching GitHub tags/releases) and is duplicated in several places. When releasing,
  update **all** of these in one commit so they never drift:
  1. `index.html` `<meta name="version" content="vX.Y.Z"/>` (line ~7) — canonical marker.
  2. `index.html` harness badge — `.shell-bar .ver` (`vX.Y.Z · HI-FI`).
  3. `README.md` H1 title — `(vX.Y.Z)`.
  4. `Brand Compliance Checklist.md` H1 title — `vX.Y.Z`.
  5. New `CHANGELOG.md` entry (Keep a Changelog format), then `git tag vX.Y.Z` + GitHub release.
  Do **not** touch the fictional in-content product versions (e.g. "Spine v0.4", the roadmap
  card) — those are deliberate mock data, not the project version. Leave `archive/*` frozen.
  Versions track design milestones, not shipped software.

## Architecture

### `index.html` is two layers in one file

The single ~3200-line file is split by comment banners into:

1. **APP CHROME — the mockup harness** (top of the file, explicitly marked *NOT part of the
   Ghost theme*): the top bar, screen tabs, surface toggle, density control, and Tweaks
   panel. This is review scaffolding. **Do not treat harness markup/CSS/JS as theme code to
   port into Ghost.**
2. **GHOST THEME**: the actual templates being designed.

The harness JS lives in the single inline `<script>` at the bottom of the file.

### `--wing-accent` is the theme's one accent knob

The entire theme keys its accent color off the single CSS variable `--wing-accent`
(default `var(--tk-cyan)`). The Tweaks "Wings" swatches override it by setting
`--wing-accent` inline on `documentElement`. This implements the brand's **"one cyan per
surface / per-pillar accent"** rule — each Tekrogen entity gets its pillar color swapped in
as the single lead accent. When adding themed UI, color it via `--wing-accent`, not a
hardcoded hex.

### Harness mechanics (all in the bottom `<script>`)

- **Screen routing:** four `.direction` blocks tagged `data-dir` A–D, switched by
  `.shell-tab` buttons via `aria-selected` / `aria-current`. Routing keys stay A–D
  internally; user-facing tab labels (Home / Topic / Library / Post Details Page) are
  prefix-free. There are no real URLs.
- **Surface (Ink/Paper):** `applySurface()` toggles `.theme-paper` on `#stage` and
  `data-tk-theme="paper"` on `<html>`; the header toggle and the Tweaks panel are kept in
  sync. Ships in **Ink** (brand primary) by default.
- **Density:** sets the `--tk-space-rh` vertical-rhythm multiplier (spacious/balanced/dense).

### Token layer: `colors_and_type.css` + `scripts/palette.js`

`colors_and_type.css` (loaded by `index.html`, lives at repo root) holds the design tokens
(`--tk-*`) — palette, type scale, spacing. The palette values inside the
`/* TK-PALETTE-BEGIN */ … /* TK-PALETTE-END */` markers are **generated** and mirror
`scripts/palette.js`, the canonical JS source of truth (it also populates `window.TK_TOKENS`
at runtime for any consumer; load it before consumers). **Keep the two in parity** — if you
change a pillar/surface hex, change it in `scripts/palette.js` and mirror it into the CSS
block. (The `tokens/sync.mjs` script and `adr/` referenced in those files' comments are
aspirational — they do not exist in this repo, so parity is currently maintained by hand.)
`@font-face` `src:` paths in `colors_and_type.css` are relative to repo root, i.e. `fonts/…`.

### `scripts/image-slot.js`

Defines the `<image-slot>` web component — a user-fillable image placeholder filled by
drag/drop. See its header comment for attributes (`id`, `shape`, `radius`, `mask`, …). Each
slot needs a distinct `id` to persist; persistence requires the host runtime and the HTML at
project root (see "Host-runtime features" above).

## Brand compliance

`Brand Compliance Checklist.md` is the authority for brand rules and records each item's
status. Locked rules worth knowing before editing the theme: mixed-case **Tekrogen** wordmark
in Poppins 600 (all-caps `TEKROGEN` is reserved for marketing surfaces only); approved glyph
vocabulary (`✓` only — no `★ ✱ ▶`); sanctioned `var(--tk-shadow-*)` and `var(--tk-radius-*)`
tokens rather than ad-hoc values; and "one cyan per surface."

## Files & layout

`index.html` is the main deliverable. `archive/` holds frozen prior snapshots (v02 mockup,
wireframes) — do not modify them as part of unrelated changes. `assets/` (marks, icon,
favicon), `fonts/` (self-hosted Poppins/Manrope/JetBrains Mono), `scripts/`, and
`colors_and_type.css` sit at repo root. `uploads/` is user-supplied source material.

## Rules

These must be followed with no exceptions:

1. Do not ever include `Co-Authored-By: Claude Opus  <noreply@anthropic.com>` in commits in this code base.
2. **Check files first, assume nothing.** When there is any confusion, contradiction, or ambiguity — especially about what this project *is*, what it references, or how it relates to other projects — verify against the documents, the data, and the codebase (README, CLAUDE.md, `git remote -v`, `git log`, `grep`) *before* answering or acting. Treat the repository's own files as authoritative over anything stated in chat, including loosely-worded inputs and your own prior statements. Report what the files say, then reason. Never carry an unverified claim from conversation forward as fact.
