# XSNHA Data Design System

## Contents

1. Character
2. Visual source of truth
3. Tokens
4. Palette variants
5. Layout
6. Components
7. Charts
8. Responsive behavior
9. Anti-patterns

## Character

The system is a precise, restrained analytical workbench rather than a cinematic theme. Information density comes from alignment and repetition. Thin rules create structure; one palette accent creates focus.

## Visual source of truth

Inspect `../assets/xsnha-data-finance-reference.png` before producing a high-fidelity preview or implementation. It establishes:

- a dark top bar plus left navigation rail;
- exact black-to-charcoal layer separation;
- coral brand, active navigation, icon, number, and focal-series usage;
- compact KPI panels and dense chart/table composition;
- thin borders, restrained radii, minimal shadow, and no glass effect.

The image is a style reference, not a fixed template. Change labels, metrics, chart types, and information architecture to suit the product while retaining this visual grammar.

Do not substitute generic theme variables for the canonical palette in preview work. A host variable such as `--primary` is acceptable only if it resolves to `#ffa796`; otherwise define scoped XSNHA variables and use them directly.

## Tokens

### Color

The table below is the `black-red` default in full detail; the other two palettes are defined role-for-role in [Palette variants](#palette-variants).

| Role | Value | Use |
|---|---|---|
| Canvas | `#0f0f0f` | Page background |
| Deep chrome | `#0a0a0a` | Sticky top bar |
| Panel | `#171717` | Cards and modal surfaces |
| Raised panel | `#1d1d1d` | Inputs, nested surfaces |
| Primary text | `#ffffff` | Titles, KPI values |
| Muted text | `#a7a7a7` | Body and metadata |
| Faint text | `#6f6f6f` | Secondary hints only |
| Structural line | `#333333` | Borders, dividers, grids |
| Coral | `#ffa796` | Brand, active, primary action |
| Coral pressed | `#e78f7f` | Hover/pressed or second series |
| Positive | `#68c36b` | Positive semantic state |
| Warning | `#ffd166` | Warning/debug state |
| Danger | `#ff574f` | Error/destructive state |

These canonical values define the identity of the dark variant. An XSNHA preview must not silently turn coral into another hue, swap in a host accent, or flatten the black surface hierarchy — and the light palettes must keep the same roles and hierarchy rather than degrading into flat white.


Coral tints:

- Active wash: `rgba(255, 167, 150, 0.14)`
- Information wash: `rgba(255, 167, 150, 0.08)`
- Accent border: `rgba(255, 167, 150, 0.42–0.70)`

### Structural line vs interactive border

`#333` is the decorative rule: it separates surfaces and draws chart grids, and it is allowed to sit below 3:1 contrast. Anything a user must find and hit — input borders, non-primary button borders, segmented controls — uses a stronger rule (`#6a6a6a`, ≈3.2:1) so the boundary clears the 3:1 non-text contrast requirement. Both roles carry over to the light palettes as `--xsnha-line` and `--xsnha-line-strong`.

### Shape and elevation

- Default radius: `8px`
- Compact radius: `4–6px`
- Cards: `1px solid #333`
- Primary card background: `linear-gradient(180deg, rgba(25,25,25,.90), rgba(16,16,16,.94))`
- Card shadow: `0 18px 60px rgba(0,0,0,.20)`
- Large/auth shadow: `0 20px 80px rgba(0,0,0,.34)`

Do not stack strong borders, shadows, and glows on the same surface.

### Spacing

Use a 4 px base grid. Common steps: 8, 12, 14, 18, 22, 24, 28, 32, 38, 52, 60.

- Compact chip gap: 6–8 px
- Card grid gap: 14–18 px
- Card padding: 22–24 px
- Result/report padding: 30–34 px
- Desktop content padding: 38 px top, 52 px sides, 60 px bottom

### Type

- Brand: 24 px / 900 / 3 px tracking
- Page title: 40 px / 900 / 1.1
- Section title: 20–24 px / 700–800
- Body: 16–18 px / 1.5–1.75
- Metadata: 12–14 px / 1.4–1.6
- KPI value: 32 px / 700–800 with tabular numerals
- Button: 15–18 px / 700–800

## Palette variants

Three palettes are first-class deliverables, not themes. `../assets/xsnha-data-palettes.css` is the canonical implementation: it scopes every token under `[data-xsnha-palette="…"]`, so a preview is immune to host theme variables. Generate all three unless the user asks for fewer.

| Token | `black-red` | `white-blue` | `yellow-green` |
|---|---|---|---|
| Canvas | `#0f0f0f` | `#f4f6f9` | `#f7efdc` |
| Chrome (top bar / rail) | `#0a0a0a` | `#ffffff` | `#fdf8ea` |
| Panel | `#171717` | `#ffffff` | `#fffdf6` |
| Raised panel | `#1d1d1d` | `#eef1f6` | `#f3e9d0` |
| Primary text | `#ffffff` | `#0b1220` | `#1d1a10` |
| Muted text | `#a7a7a7` | `#55637a` | `#5c5340` |
| Faint text | `#6f6f6f` | `#8794a8` | `#8f8468` |
| Structural line | `#333333` | `#d7dde8` | `#ddd0ae` |
| Interactive border | `#6a6a6a` | `#8194ab` | `#9c8f70` |
| Accent | `#ffa796` | `#1f5fef` | `#4a7c2f` |
| Accent pressed | `#e78f7f` | `#164dd0` | `#3c6626` |
| On-accent text | `#0f0f0f` | `#ffffff` | `#fffdf6` |
| Positive | `#68c36b` | `#1a7f43` | `#1e7a3c` |
| Warning | `#ffd166` | `#b45309` | `#8a5a00` |
| Danger | `#ff574f` | `#c92a2a` | `#b3261e` |
| Chart series 1–5 | `#ffa796` `#e78f7f` `#b9786e` `#7b5b56` `#57504d` | `#1f5fef` `#4d84f6` `#7fa6f4` `#a9c2ee` `#94a3b8` | `#4a7c2f` `#6f9a4a` `#93b273` `#b9cb9f` `#a89b78` |
| Grid / axis | `rgba(255,255,255,.09)` | `rgba(15,23,42,.08)` | `rgba(60,46,10,.10)` |

### What must not change between variants

Only the token values above move. Markup, DOM order, copy, data values, chart geometry, SVG viewBox, breakpoints, and spacing stay byte-identical. If a variant needs a different layout to work, the layout is wrong.

Surface ladder must survive translation. The light palettes are not flat white: chrome and panel are both near-white but separated by a rule, and raised panels step down into the canvas tint. Fill ratio and hierarchy stay the same across all three.

### Semantic colors take precedence over the accent

The `yellow-green` variant makes green both the accent and the positive semantic color, and `black-red` makes red both the accent and the danger color. Resolve it this way:

1. Accent drives brand, active navigation, primary action, and the focal chart series.
2. Semantic colors keep fixed meaning and are never reused decoratively. Positive is always paired with an arrow, icon, or label; danger is always paired with text — color alone never carries the sign.
3. Where a semantic value would collide with the accent, the semantic value wins inside data rows and status tags, and the accent stays out of those exact cells.
4. Do not invent a fourth green/red to escape the collision. If a chart needs more than five distinguishable series, add a second visualization instead.

### Per-variant checks

- Every text and background pairing listed above clears 4.5:1 for body text and 3:1 for large text and interactive borders. Recompute after any hex change.
- `--xsnha-on-accent` is used for text on filled accent buttons; never assume white.
- Focus outlines use the accent and stay visible on both dark and light canvases (2 px outline, 2 px offset).
- Chart series must remain distinguishable in grayscale or with a legend; the light palettes replace the warm mid-tones with progressively lighter tints, which is expected.
- Light palettes carry lower shadow values by design; do not reuse the dark shadow tokens on white or cream.


## Layout

### Desktop shell

```text
┌──────────────────────── top bar 86 ────────────────────────┐
├──── sidebar 288 ────┬──────── scrollable content ──────────┤
│ navigation          │ title / context                     │
│                     │ toolbar                             │
│                     │ KPI + charts / reports / library    │
└─────────────────────┴─────────────────────────────────────┘
```

Cap content near 1500 px. Keep the navigation chrome fixed or sticky while the content region scrolls.

### Grids

- KPI: 3 columns normally; 1 narrow KPI rail plus a chart area is valid for executive dashboards.
- Charts: 3 columns desktop; allow `span 2` and `span full` for important views.
- Asset library: 4 columns for compact analysis cards, 3 for dashboard previews.
- Forms: prefer explicit label/input/action columns on wide screens, then stack on narrow screens.

## Components

### Navigation

Top tabs use a 3 px coral bottom rule. Sidebar items use a 4 px coral left rule and a faint left-to-right coral wash. Do not use a filled coral nav button.

### Buttons

- Primary: coral vertical gradient, near-black text, no border.
- Secondary: transparent/dark surface, coral border and text.
- Danger: transparent/dark surface, red border and text.
- Compact controls: minimum 38 px desktop; touch layouts minimum 44 px.

### Cards and panels

Use the shared panel treatment. Nested chart canvases may use `rgba(255,255,255,.025)` with the same structural line. Avoid independent decorative styles for every card type.

### Tags and statuses

Use compact outlined rectangles. Pills are reserved for counts, verified states, or progress. Status color must be paired with readable text.

### Tables

Use horizontal dividers rather than a boxed grid for every cell. Left-align text, right-align numbers, use tabular numerals, keep headers muted and semibold. Wrap the table in an overflow container on mobile.

### Empty, loading, and errors

- Empty: one outlined icon, direct title, one sentence, one primary next action.
- Loading: restrained coral pulse or progress line; honor reduced motion.
- Error: explain the failed stage and recovery action. Do not show raw provider errors as the main message.

## Charts

### Palette

Use `--xsnha-series-1` through `--xsnha-series-5` from the active palette. Series 1 is the accent and carries the focal claim; series 2–5 step toward the palette's neutrals. Use semantic positive/warning/danger only when the sign is meaningful, and see [Semantic colors take precedence over the accent](#semantic-colors-take-precedence-over-the-accent) when a palette makes the accent collide with a semantic hue.

### Treatment

- Plot background: transparent or the palette's inset wash
- Grid/axis: `--xsnha-grid`
- Labels: `--xsnha-muted`
- Tooltip: `--xsnha-panel-raised`, 1 px `--xsnha-line`, 8 px radius
- Line: 2 px `--xsnha-series-1`, optional low-opacity area fill
- Bar: `--xsnha-series-1` fill with consistent corner treatment
- Legend: compact, wrapping, muted text, 10 px markers


Always show the time window and units. Add source/refresh metadata below the visualization when it affects interpretation.

## Responsive behavior

Preferred behavior below 980 px:

- Collapse multi-column report, KPI, evidence, and chart grids to one column.
- Convert the fixed sidebar to a drawer or compact navigation; do not keep a 288 px rail on a 390 px viewport.
- Allow toolbars and action groups to wrap or stack.
- Make tables scroll horizontally with a deliberate minimum width.
- Preserve 16–24 px page padding and 44 px targets.

If the product is intentionally desktop-only, set and document a meaningful minimum width (the source product uses 1100 px) and provide an explicit unsupported-device message instead of a broken compressed shell.

## Anti-patterns

- Pure `#000` applied to every layer
- Coral used for all text or every chart series
- Large glass blur, bloom, glow, or neon outlines
- Rounded 20–32 px SaaS cards
- Marketing hero layouts inside operational screens
- Hidden labels relying on icon recognition
- Charts without units, comparison period, or source context
- Light-gray low-contrast body copy on black
- `text-align: justify` or `word-break: break-all` in Japanese UI
- Theme-variable previews where the host's default accent replaces the palette accent
- Palette variants that drift in layout, copy, data, or chart geometry
- Light palettes flattened into one white surface with no rule or tonal separation
- Semantic green/red used as decoration, or a fourth hue invented to dodge an accent/semantic collision
- Conversation widgets that flatten the sidebar, top bar, or dense panel hierarchy into generic cards
