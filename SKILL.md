---
name: xsnha-data
description: "Design, preview, and implement analytical web products in the XSNHA visual language. By default, generate runnable HTML in three parallel palette variants—black background with red charts, white background with blue charts, and yellow background with green charts—while keeping layout and data identical for comparison. Use for dashboards, accounting or financial systems, analysis reports, data libraries, admin workspaces, authentication flows, or requests to reproduce this interface style in HTML/CSS, React, Vue, Svelte, or Astro."
---

# XSNHA Data

Build serious, information-dense data products with thin structural rules, compact controls, restrained radii, and legible analytical hierarchy. Default to runnable HTML and show three palette variants at once so the user can compare color direction without layout drift.

## Default deliverable

Unless the user explicitly asks for an image, a framework component, or only one palette:

1. Generate three runnable HTML previews in one pass, starting from [assets/preview-template.html](assets/preview-template.html) so the shell, charts, and table density do not drift between variants.
2. Keep markup, content, data, chart geometry, spacing, and responsive behavior identical across all three.
3. Change only palette tokens:
   - `black-red`: black/charcoal surfaces with red/coral charts and active states.
   - `white-blue`: white/light-gray surfaces with blue charts and active states.
   - `yellow-green`: warm yellow/cream surfaces with green charts and active states.
4. Name files `<slug>-black-red.html`, `<slug>-white-blue.html`, and `<slug>-yellow-green.html` when files are requested or the environment supports HTML previews.
5. Present all three results together. Do not ask the user to choose a palette before generating them.

Use [assets/xsnha-data-palettes.css](assets/xsnha-data-palettes.css) as the canonical palette layer. If a host project needs a single palette, still read the three-variant comparison first so the structural contract is established. Generate raster images only when the user explicitly requests an image, mockup, or screenshot.

## Workflow

1. Inspect the target product, framework, existing tokens, and representative content before editing.
2. Classify each screen as entry/auth, application shell, data library, analysis report, dashboard, form, table, or review flow.
3. Read [references/design-system.md](references/design-system.md) for the structural contract and three palette definitions. Inspect [assets/xsnha-data-finance-reference.png](assets/xsnha-data-finance-reference.png) for shell proportions and density, not as a single mandatory color scheme.
4. When the user is exploring or refining the style, follow [references/preview-and-release.md](references/preview-and-release.md): generate all three HTML variants, present them together, and confirm direction before packaging or broad implementation.
5. For Japanese or mixed Japanese interfaces, also read [references/japanese-typography.md](references/japanese-typography.md). Set `<html lang="ja">` when Japanese is primary.
6. Reuse existing primitives when possible. Scope palette variables to each preview so host theme variables cannot alter the comparison.
7. Build the shell and hierarchy before charts: top bar, sidebar, content bounds, page title, toolbar, then cards and data views.
8. Use real or structurally realistic data. Do not fill an analytical screen with generic marketing copy.
9. Verify at 360, 390, 768, 1280, and 1440 px unless the product explicitly targets desktop only. If desktop-only, document the minimum supported width and prevent accidental half-responsive layouts.
10. Report the structures styled, responsive behavior, accessibility checks, and intentional deviations.

## Fidelity gate

Before calling a result “XSNHA style,” confirm all of the following:

- All three required palettes are present unless the user explicitly requested fewer.
- Each palette follows its named relationship: black/red, white/blue, yellow/green.
- The three versions have identical structure, data, chart geometry, and typography.
- Only palette tokens differ between the three files; the shell, copy, numbers, SVG geometry, and breakpoints match.
- Top navigation and a left analytical rail establish an application shell on desktop.
- Surfaces use 1px rules and restrained 8px corners; they do not look like floating generic cards.
- Information density resembles a real operational dashboard: aligned KPIs, embedded charts, compact legends, metadata, and tables.
- The result avoids glassmorphism, large soft gradients, excessive empty space, oversized radii, and marketing-page composition.

If any item fails, revise before presenting the preview.

## Non-negotiable visual rules

- Preserve surface hierarchy within every palette; do not use one flat background everywhere.
- Use the palette accent for brand, active navigation, primary action, and focal chart data.
- Keep semantic colors semantic. In `yellow-green` the accent is green and in `black-red` it is red, so accent and semantic hue can coincide: the accent owns brand and focal data, the semantic value owns status and deltas, both are always paired with an icon, arrow, or label, and neither is used as decoration. Never invent a fourth hue to escape the overlap. See [references/design-system.md](references/design-system.md).
- Prefer 1 px borders and tonal separation over floating glass effects or heavy shadows.
- Keep corner radii modest: 8 px default, 4–6 px for tags and compact controls, pill radii only for badges or progress.
- Use dense but breathable spacing. Align card edges, chart baselines, headings, and toolbars to a consistent grid.
- Use strong display weight sparingly for the brand, page title, KPI value, and primary action.
- Keep body and supporting text muted; never reduce essential information below accessible contrast.
- Make charts feel embedded in the workspace with subtle grid lines, compact legends, and palette-aware focal series.
- Avoid neon cyberpunk, oversized gradient blobs, excessive glow, glassmorphism, giant marketing type, and rainbow chart palettes.
- Do not make the visual identity host-theme-dependent. Scope the canonical variant values directly.

## Composition patterns

Choose the pattern that matches the task:

- **Application shell:** 86 px top bar, 288 px sidebar, scrollable content region, active states marked by coral rule plus faint coral wash.
- **Dashboard:** title and context, toolbar, KPI row, then 2–3 column chart grid. Allow a high-value chart to span two columns or the full row.
- **Analysis report:** result header, source/status metadata, evidence and findings, embedded charts, recommendations, and follow-up actions.
- **Library:** search/filter toolbar followed by three or four compact asset cards per desktop row.
- **Auth/review:** one centered bordered surface with clear title, explanatory copy, fields or summary rows, and full-width primary action.

Do not force every pattern onto every screen. A sparse state should remain sparse.

## Data visualization rules

- Lead with the question or business meaning, not the chart type.
- Put the KPI value above its delta and comparison period.
- Use the current variant's accent (`--xsnha-series-1`) for the focal series. Derive supporting series from the palette's remaining steps and neutrals.
- Keep semantic color semantic: green for genuinely positive state, red for destructive/error state, amber for warning or debug state. Where the palette accent shares that hue, the accent never occupies a status cell or a delta, and status always carries text in addition to color.
- Include units, time window, source, and refresh state where relevant.
- Prefer line/area for time, bar for ranked comparison, donut only for a small part-to-whole set, and tables for precise lookup.
- Do not use a donut for more than five categories or decorative charts without an analytical claim.

## Typography and content

- Default Latin UI stack: Inter, system UI, `-apple-system`, BlinkMacSystemFont, Segoe UI, sans-serif.
- Use tabular numerals for KPIs and tables.
- Keep headings compact and direct. Use uppercase only for short navigation, eyebrow, or system labels.
- Write concrete labels: `Data refreshed 14:32 JST`, not `Updated recently`.
- Never use `text-align: justify` for Japanese cards, body, FAQ, or mobile copy.
- Never use `word-break: break-all` for normal Japanese copy.

## Accessibility and interaction

- Meet WCAG/JIS contrast: 4.5:1 for normal text and 3:1 for large text and meaningful UI boundaries. Decorative hairlines may sit lower; interactive borders use the palette's strong line.
- Give controls a visible focus state using the palette accent outline without relying on color alone for destructive/positive meaning.
- Keep interactive targets at least 44 px on touch layouts.
- Pair icons with accessible names. Do not ship icon-only ambiguous actions without `aria-label` and tooltip support.
- Respect `prefers-reduced-motion`; the system needs only short fades, progress pulses, and state transitions.
- Keep tables semantic and horizontally scrollable on narrow screens rather than crushing columns.

## Reusable asset

Use [assets/xsnha-data-palettes.css](assets/xsnha-data-palettes.css) as the canonical palette layer for all three variants: scope `data-xsnha-palette="black-red" | "white-blue" | "yellow-green"` on a wrapper and keep component markup unchanged. `assets/xsnha-data-tokens.css` is the same system flattened to the dark palette for host projects that need a single set of variables, with the full role list in [references/design-system.md](references/design-system.md).

Use [assets/preview-template.html](assets/preview-template.html) as the starting skeleton. It already carries the shell, KPI row, chart treatment, table density, and responsive breakpoints, so the three variants stay comparable; replace the sample data instead of rebuilding the layout from scratch.

Use [assets/xsnha-data-tokens.css](assets/xsnha-data-tokens.css) as a starting token layer when the host project needs plain variables rather than palette scoping. Adapt variable names to the host project; do not copy unused component CSS blindly.

Use [assets/xsnha-data-finance-reference.png](assets/xsnha-data-finance-reference.png) as the baseline visual example for shell proportions, black/coral contrast, panel density, chart treatment, and table styling. Match its system, not its financial content.

## Acceptance checklist

- The page reads as an analytical workspace before it reads as a theme demo.
- The palette accent highlights the active path and primary action without flooding the screen.
- Accent and semantic color remain distinguishable; every status or delta carries text, not hue alone.
- All panels share the same border, radius, and surface logic, and each palette keeps its surface ladder rather than flattening to one background.
- KPI, chart, table, status, empty, loading, error, and focus states are represented when relevant.
- No horizontal overflow occurs in the supported viewport range.
- Japanese text follows the alignment and phrase-breaking matrix when present.
- Charts remain understandable without depending on hue alone.
- The implementation retains the target framework's conventions and passes its available checks.
- The user has approved the visual preview before the skill is packaged or published when the task is exploratory.
- All three HTML variants load offline and remain comparable at the same viewport, differing only in `data-xsnha-palette` and the values in `assets/xsnha-data-palettes.css`.
