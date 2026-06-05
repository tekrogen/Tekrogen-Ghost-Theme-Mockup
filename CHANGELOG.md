# Changelog

All notable changes to the **Tekrogen Ghost Theme Mockup (v04)** project are recorded
here. Format follows [Keep a Changelog](https://keepachangelog.com/); this is a design
mockup project, so versions track design milestones rather than shipped software.

> **Note on dates:** earlier milestones predate this changelog and their exact dates were
> not recorded — they are marked *(date not recorded)*. Everything from the
> brand-compliance pass onward is dated accurately.

## [Unreleased]

### Pending (awaiting go-ahead)
- **Polish #8 — tokenize hardcoded hexes.** Map inline pillar hexes and hardcoded
  Paper-mode neutrals (`#e6ebef`, `#f3f5f7`, `#0a0d12`) to their `--tk-*` tokens to
  remove palette-drift risk. Visually invisible.
- **Polish #9 — keyboard accessibility.** Give nav links real `href`s and convert
  search / chips / anchors from `<div>`s to real links/buttons so they are focusable
  and the brand focus ring applies.

---

## [0.5.0] — 2026-06-05

Content-model overhaul: collapsed the seven content **types** into five top-level
**categories**, introduced **Recon**, and removed scored **Tech Rating**. Rationale and
per-screen plan in `admin/features/recon-content-model.md`.

### Added
- **Recon** — a new category that unifies the former Research Article + SaaS Evaluation work
  into one qualitative, multi-source "justify the stack" category. Includes a unified Post
  Details reader template (research framing → candidate comparison → sources → chosen stack,
  no scores) and a Recon lane on the Topic page.
- `admin/features/recon-content-model.md` — decision record for the move to Recon.

### Changed
- **Seven types → five categories** across every screen: Use Case Study · Recon · Product ·
  Demo / POC · Documentation. Reworked the Home feed, Topics dropdown, Topic page, Library
  (now "Index of Five"), and Post Details accordingly.
- Library grid rebalanced to a clean 6-cell 3×2 layout (5 category cards + 1 merged CTA).

### Removed
- **Tech Rating** and all numeric scoring (six-axis rubric, `x.x/10` scores, score bars) —
  Tekrogen does not rate evaluated resources; the stack decision belongs to stakeholders.
- Standalone **Research Article** and **SaaS Evaluation** types — folded into Recon.

### Notes
- `.score-mini` / `.score-panel` CSS is now unused; retained for a later cleanup pass.

---

## [0.4.2] — 2026-06-03

### Changed
- Generalized `CLAUDE.md` Rule 1 to ban any `Co-Authored-By: Claude Opus …`
  co-author trailer (previously named only the `4.7 (1M context)` variant).
- Bumped the `index.html` version meta to `v0.4.2`.

---

## [0.4.1] — 2026-06-03

Repository restructure — flattened the project layout and added standard project
metadata. No design changes.

### Changed
- Retired the `tekrogen/` working directory and flattened its contents into
  top-level folders: foundations CSS to the repo root (`colors_and_type.css`),
  web fonts to `fonts/`, runtime scripts to `scripts/` (`image-slot.js`,
  `palette.js`), and brand marks to `assets/` (`tekrogen-icon-256.svg`,
  `tekrogen-mark.svg`).

### Added
- `LICENSE` — MIT License (© 2025 Tekrogen).
- `.gitignore` — OS, editor, and tooling ignore rules.
- `.gitattributes` — `* text=auto` for cross-platform LF normalization.
- `CLAUDE.md` — repository guide for Claude Code (architecture, conventions, brand rules).

### Removed
- Duplicate `tekrogen/favicon.svg` — the canonical copy lives at
  `assets/favicon.svg`.

---

## [0.4.0] — 2026-06-03

Housekeeping + canonical entry point.

### Changed
- Promoted the corrected mockup to **`index.html`** as the canonical Ghost-theme entry
  point (formerly `Ghost Theme Mockup v03.html`); cleared the version suffix from
  `<title>`.
- Renamed the four review screens to plain, prefix-free labels — **Home Page**,
  **Topic Page**, **Library Page**, **Post Details Page** — across the tab bar and the
  `data-screen-label` attributes. Internal `data-dir` routing keys (A–D) and the LOCKED
  badge on Home Page were preserved.

### Added
- `CHANGELOG.md` (this file).

### Moved
- Archived `Ghost Theme Mockup v02.html` (pre-compliance baseline) to `archive/`.
- Archived `Ghost Theme Wireframes.html` (low-fi homepage-layout sketch) to `archive/`.

---

## [0.3.0] — 2026-06-03

Brand-compliance pass against the Tekrogen Brand Design System. Produced from v02;
shipped as v03 (now `index.html`). Full audit in `Brand Compliance Checklist.md`.

### Fixed
- **Wordmark** — publication header and footer now use the mixed-case **Tekrogen**
  wordmark (Poppins 600, `-0.01em`), not the locked all-caps `TEKROGEN` (which the brand
  reserves for marketing surfaces).
- **Iconography** — removed off-vocabulary glyphs `★ ✱ ▶`; spotlight tags now read as
  words (*Featured / Product / Live demo*) and the comparison table uses the approved
  `✓` glyph.
- **Elevation** — the Topics dropdown now uses the sanctioned `var(--tk-shadow-2)`
  recipe instead of an ad-hoc `0 20px 50px` shadow.
- **Radii** — off-scale `14px` corners (browser frame, hero image, post cards) snapped
  to `var(--tk-radius-xl)` (12px).

### Changed
- **Default surface → Ink.** The mockup now opens in Ink (the brand's primary surface);
  Paper remains one click away via the header toggle and Tweaks panel.
- **Default author → M. Dolce** across all bylines, the `MD` avatar, the citation block,
  and the copyright line.

### Added
- `Brand Compliance Checklist.md` — the full audit with per-item status.

### Confirmed (no change)
- **One cyan per surface** is satisfied by design: `--wing-accent` is swapped to each
  entity's pillar color per surface; House cyan is the `.org`/default lead, demonstrated
  via the Tweaks panel.
- Token layer matches the canonical Tekrogen palette value-for-value (no drift).

---

## [0.2.0] — *(date not recorded)*

### Added
- `Ghost Theme Mockup v02.html` — the high-fidelity mockup: four IA directions
  (Home / Topic / Library / Post Details), the seven content types, the Ink/Paper
  surface toggle, and the Tweaks panel (wing accent · surface · density). Built on the
  Tekrogen design tokens (`tekrogen/colors_and_type.css`).
- `README.md` — project overview.

---

## [0.1.0] — *(date not recorded)*

### Added
- `Ghost Theme Wireframes.html` — low-fidelity wireframes used to define the homepage
  layout and compare the candidate directions before the hi-fi pass.
