# epub-css-baseline

A small, opinionated CSS baseline for reflowable EPUBs (Kindle, Kobo, etc.).
It keeps reader controls intact while setting sane defaults for typography,
spacing, and image behavior.

## Why
- Respect reader controls: relative `font-size` and `line-height`.
- Better readability: hyphenation, paragraph indents, consistent rhythm.
- Safer rendering: avoid awkward breaks after headings; responsive images.

## Design choices
- Reflow first: everything stays relative so device sliders work.
- Indent + margin: classic book rhythm; no indent after headings.
- Justify with hyphens: smoother rag, fewer gaps on small screens.
- Minimal overrides: no fonts or colors; keep it engine-friendly.
- Compatibility: avoid rules that fight reading systems; prefer safe fallbacks.

## What's inside
- `html, body`: reset margins/padding; `line-height: 1.4`; `text-align: justify` (user can override); `hyphens: auto`; `widows`/`orphans`.
- `p`: bottom margin + first-line indent; `overflow-wrap: break-word`; no indent after headings or common blocks.
- `h1-h6`: balanced spacing; avoid page/column breaks after and inside.
- Lists/blockquote: reasonable margins; no indent inside blockquotes.
- `img`: responsive; avoid splitting (`page-break-inside`/`break-inside: avoid`).
- `pre`/`code`: wrap long lines; monospace stack.

Intentionally minimal: no colors, no fonts, no layout gimmicks. Add per‑book
styles on top as needed.

## Use
Option A — include in source
1) Copy `epub-style.css` into your book (e.g., `OEBPS/css/`).
2) Reference it from each XHTML file:

```html
<link rel="stylesheet" href="css/epub-style.css" type="text/css" />
```

3) Avoid inline styles that fight the baseline (especially `text-align`,
`line-height`, `font-size`).

Option B — via Calibre conversion
1) In Calibre select the book → Convert books.
2) Pick your output (EPUB/AZW3/KFX/KEPUB if you use the plugin).
3) Go to Look & feel → Styles → paste the contents of `epub-style.css` into “Extra CSS”.
4) Recommended settings while converting:
   - Leave “Base font size” and “Line height” blank (keeps device controls).
   - Keep Heuristic processing off unless you need fixes.
   - Do not filter style info that removes margins/line-height.
   - Set the book language in metadata so hyphenation works.
5) Convert.

## License
MIT — see `LICENSE`.
