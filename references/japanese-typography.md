# Japanese Typography for XSNHA Data

Use these rules when Japanese is primary or materially present. They combine the XSNHA visual system with production Japanese typography and JIS X 8341-3 accessibility concerns.

## Baseline

```css
:lang(ja) {
  font-family: "Hiragino Sans", "Hiragino Kaku Gothic ProN",
    "Yu Gothic", YuGothic, Meiryo, "Noto Sans JP", system-ui, sans-serif;
  font-feature-settings: "palt" 1, "kern" 1;
  letter-spacing: 0.02em;
  line-height: 1.75;
  line-break: strict;
  overflow-wrap: anywhere;
  text-align: left;
}

:lang(ja) :is(h1, h2, h3, h4, .card-title) {
  overflow-wrap: normal;
  word-break: normal;
  word-break: auto-phrase;
  line-break: strict;
  letter-spacing: 0.01em;
  line-height: 1.4;
}
```

Use at least 16 px for Japanese body copy when practical. Use explicit available font weights; avoid synthetic bold that crushes complex glyphs.

## Alignment and phrase-breaking matrix

| Surface | Alignment | Phrase break |
|---|---|---|
| Hero/section heading | Left or center | ON |
| Card/FAQ title | Left or center | ON |
| Centered short lead | Center | ON |
| Left lead/body/card description | Left | OFF |
| FAQ answer/article body | Left | OFF |
| Compact button | Center | OFF; keep label intact |
| Table cell | Left | `auto-phrase` only, with cell overrides |

Never justify Japanese body, card, FAQ, or narrow mobile copy. Japanese justification inserts visible inter-character gaps and leaves the last line ragged.

`word-break: auto-phrase` works in Blink, but not WebKit or Gecko. If correct phrase boundaries on iPhone/Safari/Firefox are a requirement, ask before adding build-time BudouX. Apply BudouX only to headings, titles, centered short leads, and other deliberate short display copy—not left-aligned long text.

## Protected phrases

- Wrap prices, numbers plus units, dates, and short product names in a reusable `.nowrap` utility.
- Protect short quoted phrases such as `「分析結果」` inside phrase-broken headings.
- For long names or compounds, insert `<wbr>` at safe boundaries instead of forcing `nowrap` and causing overflow.
- Reserve `<br>` for authored display copy; never structure body, FAQ, or article text with forced breaks.
- Mark inline English with `lang="en"` and allow `hyphens: auto`.

## Tables

Body-level `overflow-wrap: anywhere` must not leak into cells:

```css
.table-ja-wrap { overflow-x: auto; }
.table-ja { width: 100%; min-width: 880px; table-layout: fixed; }
.table-ja th,
.table-ja td {
  overflow-wrap: normal;
  word-break: normal;
  word-break: auto-phrase;
  line-break: strict;
  text-align: left;
}
.table-ja th.is-compact {
  white-space: nowrap;
  word-break: keep-all;
}
```

Use `<colgroup>` widths based on the longest cell in each column. Do not solve bad table wrapping with hard-coded `<br>` elements.

## Japanese UI accessibility

- Use `<ruby><rp>（</rp><rt>...</rt><rp>）</rp></ruby>` for necessary readings.
- Use concrete link text rather than `こちら` or `ここ`.
- Provide Japanese `aria-label` text for icon buttons and menu state.
- Test iOS Safari because all iPhone browsers use WebKit.
- Verify 360, 390, 768, and 1280 px with real Japanese copy, not Latin placeholders.

## Final check

- No stranded particles or punctuation at line starts.
- No justified character gaps.
- No `break-all` on ordinary content.
- Titles and quoted phrases break intentionally.
- Left-aligned descriptions use natural wrapping.
- Tables preserve useful column widths and scroll when needed.
- All Japanese text remains readable against the dark surfaces.
