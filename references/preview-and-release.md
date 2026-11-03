# Preview and Release Workflow

Use this workflow whenever the user is still deciding whether the visual style is correct or asks to distill/package/publish the skill.

## 1. Preview first — three variants, one pass

Generate the opening screen in all three palettes at once: `black-red`, `white-blue`, `yellow-green`. Start from `../assets/preview-template.html` and change only the `data-xsnha-palette` attribute so the three previews stay structurally identical.

Do not ask which palette the user prefers before generating them. The whole point of the comparison is to see the same screen in three color directions.

The preview must contain enough system evidence to judge the style:

- top application bar;
- left navigation with an active state in the palette accent;
- three compact KPIs;
- one focal chart using series 1;
- one secondary visualization and one table;
- realistic labels, units, time window, and a source/refresh line.

A single-variant preview is acceptable only when the user explicitly asked for one palette, an image, or a framework component. If the request was "画一个" / "看风格" / a preview image, a high-fidelity raster mockup in one palette is fine — say which palette it uses and offer the other two.

Do not use a theme-aware conversation component for the first fidelity review: host tokens can recolor the palette. If HTML is unavoidable, scope `data-xsnha-palette` locally as `assets/xsnha-data-palettes.css` does.

## 2. Ask for visual confirmation

After presenting all three, ask only about material choices:

- Which palette direction is correct for this product: black-red, white-blue, or yellow-green?
- Should information density stay operational or become simpler?
- Are the shell proportions, chart treatment, and table density correct?

A palette answer is a direction, not a licence to let the unpicked variants drift. If the user picks one, the other two remain available for later comparison and must keep the same structure.

Do not package, publish, or create repositories until the user confirms, unless they explicitly requested those actions in the same step.

## 3. Implement or refine

Apply one focused revision at a time, and re-check it in all three palettes before moving on — a change that only works in one palette is a token bug, not a layout choice.

Recheck against the fidelity gate in `SKILL.md`, the palette rules in `design-system.md`, and the bundled reference image.

## 4. Package independently

When publishing this skill for others, use a dedicated public repository rather than placing it inside a private product repository. Include only the skill folder contents required by Codex:

```text
xsnha-data/
├── SKILL.md
├── agents/openai.yaml
├── assets/
│   ├── xsnha-data-palettes.css
│   ├── xsnha-data-tokens.css
│   ├── preview-template.html
│   └── xsnha-data-finance-reference.png
└── references/
```

Before publishing:

- remove `.DS_Store`, editor state, and any local scratch files;
- confirm every path referenced from `SKILL.md` and `references/` exists in the tree;
- confirm the three palettes and the template still open standalone with no network access;
- confirm no file references a host project's private tokens or assets.

Never copy private product code, credentials, internal screenshots, customer data, or unrelated repository history into the public repository. Confirm repository ownership, visibility, and name before creating or pushing it.
