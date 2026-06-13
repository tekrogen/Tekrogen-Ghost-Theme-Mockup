# Changelog

All notable changes to the **Tekrogen Ghost Theme Mockup** project are recorded
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

## [0.10.0] — 2026-06-13

C3 cards migration: the `Claude-DT` mockup's cards now consume the **C3 composites** (registry PR #36).

### Changed
- **Content cards → `tk-content-card`** (6; head/desc/rel slots, data-pillar). **Listing cards →
  `tk-listing-card`** (4). **Pillar buttons → `tk-pillar-button`** (4). **Category cards →
  `tk-category-card`** (6). **Team cards → `tk-team-card`** (2; avatar → `tk-avatar[data-style="mono"]`,
  sized inline). **Manifesto cards → `tk-manifesto-card`** (4). Per-card scoped slot renames
  (`.row`→head, `.desc`/`.rel`/`.ind`/`.label`/`.name`/`.ic`/`.links`/`.role` → slots). Verified on-brand
  (s1 pillar buttons + content cards; s8 manifesto + team cards w/ mono 44px avatar).

### Deferred
- Now-inert bespoke C3 CSS left this pass → shared dead-CSS cleanup. Dashboard `.av` (s9) stays for C7.

## [0.9.0] — 2026-06-13

C2 data & forms migration: the `Claude-DT` mockup consumes the **C2 composites** (registry PR #34).

### Changed
- **Tables → `tk-table`** (bespoke `.tk-table` core removed; registry applies; `.tk-table .chosen`
  kept as a recon helper). **Forms → `tk-form`/`tk-field`/`tk-field-row`** (10 fields, 3 forms).
  **Callouts → `tk-callout`** (2, `data-pillar` where keyed). **CTA blocks → `tk-cta-block`** (2,
  `.row` → `data-tk-slot="actions"`). **Stats → `tk-stat`/`tk-stats`** (4; value now `--tk-fs-h2`
  ≈ 28px vs the old 34px — a minor scale normalization). Verified on-brand (recon table + callout,
  computed-style checks).

### Deferred
- Now-inert bespoke C2 CSS (`.form`/`.field`/`.callout`/`.cta-block`/`.stat`) left this pass —
  folded into the same dead-CSS cleanup as C1.

## [0.8.0] — 2026-06-13

C1 structural migration: the `Claude-DT` mockup's header, footer, section heads, and mono labels
now consume the design-system **C1 composites** (registry PRs #30/#32).

### Changed
- **Header → `tk-site-header[data-style="framed"]`** across all 9 screens (brand/nav/util slots;
  mark sized inline 28px). **Footer → `tk-footer[data-style="nav"]`** (brand + four pillar link
  columns; mark 40px). **Section heads → `tk-section-head`** (12 instances, incl. `data-size="sm"`).
  **Mono labels → `tk-label`** (51: pill-mono→pill, `.chip`→`data-variant="chip"`+pillar,
  `.tag`→`data-variant="tag"`). Header/footer adopt the canonical `tekrogen-org` design (the chosen
  "canonical default") in their framed/nav variants — a deliberate brand-alignment, verified on-brand.

### Deferred
- The now-inert bespoke CSS (`.site-head`/`.site-foot`/`.sec-head*`/`.pill-mono`/`.chip`/`.tag`,
  etc.) is left in place this pass (no matching elements; harmless) — a follow-up cleanup removes it.

## [0.7.0] — 2026-06-13

Component migration: the `Claude-DT` mockup now **consumes the design-system component
registry** (`components/`) instead of bespoke CSS — the first surface to do so, validating
the mockup→theme bridge (ADR-0012).

### Changed
- **`mockups/Claude-DT/index.html` migrated to `.tk-*` registry classes** (v0.5.0): all
  buttons → `tk-button` with the **editorial `data-style="cta"`** variant (sans, mixed-case —
  look preserved) composing `data-pillar` / `data-variant="secondary"` / `data-tk-slot="hint"`;
  badges → `tk-badge[data-pillar]` (tinted pill + dot); inputs → `tk-input`. Default CTAs keep
  following the harness `--wing-accent` knob and form inputs stay full-width via small local
  consumer overrides. Verified visually equivalent to v0.6.0 (only intended deltas: CTA padding
  snapped to `--tk-space-*` ≤2px; inputs adopt the registry's a11y-correct 16px + `--tk-bg-3`).
- **Re-vendored `components/`** from the design system (pillar-aware primitives + button
  `data-style="cta"` / `hint` slot).

### Removed
- The mockup's bespoke `.btn` / `.badge` / `.inp` / `.btn-block` CSS blocks (now provided by the
  registry). `.av` avatars **deferred** to the composites batch (mono-vs-sans initials).

## [0.6.0] — 2026-06-13

Foundation sync to **Tekrogen Brand Design System** parity, brand-integrity fixes, and the
vendored component registry — the base for the upcoming component migration.

### Added
- **Self-hosted font set (ADR-0008).** Full brand weights — Poppins 400–800 + italic
  400/500/600, Manrope 400–700, JetBrains Mono 400–700 — added to `fonts/` as latin-subset
  woff2 (was Regular-only). No remote font dependency.
- **Component registry vendored** from the design system into `components/` (button, card,
  input, badge, avatar + the `tk-components.css` barrel); linked from
  `mockups/Claude-DT/index.html`.

### Changed
- **`colors_and_type.css` brought to full design-system parity** (478 lines / 128 tokens):
  adopts the ADR-0007 rem-fluid type scale (eyebrow/meta now hold the 12px floor; headings
  fluid) and adds 20 previously-missing tokens (`--tk-focus`, `--tk-success-text`,
  `--tk-mark-*`, `--tk-og-*`, `--tk-shell-max`, `--tk-fs-og-title`). This shifts type
  rendering on both surfaces — intended parity, matching the real theme + WCAG 1.4.4.
- **`mockups/README.md` build brief corrected**: Nunito → Manrope (sans-only, ADR-0001/0008);
  "Research Hub" reframed as the Recon hub; "Ratings" removed (no scores — the v0.5.0 Recon
  model).

### Removed
- **Google Fonts CDN** `<link>`/`@import` from `index.html` and `mockups/Claude-DT/index.html`
  — zero remote font dependencies; all weights self-hosted (ADR-0008).

---

## [0.5.0] — 2026-06-05

Content-model overhaul: collapsed the seven content **types** into five top-level
**categories**, introduced **Recon**, and removed scored **Tech Rating**. Rationale and
per-screen plan in `recon-content-model.md`.

### Added
- **Recon** — a new category that unifies the former Research Article + SaaS Evaluation work
  into one qualitative, multi-source "justify the stack" category. Includes a unified Post
  Details reader template (research framing → candidate comparison → sources → chosen stack,
  no scores) and a Recon lane on the Topic page.
- `recon-content-model.md` — decision record for the move to Recon.

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
