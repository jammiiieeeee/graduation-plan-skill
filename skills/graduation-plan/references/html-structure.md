# plan.html structure

The page is one static document: inline CSS, inline JS, local fonts, no build step.
Read this before filling the template, and again before changing any class.

## Document skeleton

```
<head>
  meta charset / viewport
  <title>            one line, the page's claim
  <style>            design tokens, @font-face, all components
<body>
  <main class="wrap">
    section            hero (no id)
    section#path       three term sheets
    section#ledger     credit ruler + overlap note
    section#marks      grade-weight bar + tactics
    section#week       3 x 7 study grid + four rules
    section#breaks     five pinned tripwires
    footer             provenance + signature
  </main>
  <script>             ticks + reveal
```

The five nav links in the hero are the only navigation. Their `href` values must
match the section ids exactly. Section order is the argument: path, then the
credits behind it, then where grades weight, then the week, then failure modes.

## Section contract

| Section | Element | Required content | Count |
|---|---|---|---|
| Hero | `article.sheet.hero` | 3-line `h1`, `.subject`, `.next` first move, `.lede`, `.stubs`, `.contents` | 1 |
| Path | `article.sheet.term` | `.term-date`, `.term-role`, `.term-cr`, `.courses`, optional `.zero`, `.term-note` | one per remaining term |
| Ledger | `article.sheet.ledger` | `.cap`, one `.lrow` per curriculum, `.ledger-note` | one per curriculum |
| Marks | `article.sheet.marks` | `.big`, `.bar`, `.key`, `.keynote`, `.cap`, `.floor`, tactics list | 1 |
| Week | `article.sheet.week-sheet` | `.week` grid, `.week-legend`, `.rules` | 1 |
| Breaks | `div.notes > div.note` | `.pin`, head, body | exactly 5 |
| Footer | `footer` | provenance paragraph, `.sig` | 1 |

## Component shapes

**Headline.** `h1` holds three spans: `.l1` and `.l2` are plain, `.l3` wraps its
text in `.hl` for the lime mark. The first two lines state the shape of the path;
the third states the constraint or the cost. The stamp sits top-right.

**Term sheet.** `term-cr` is the credit total of that term. Each course is one
`li` with exactly four children in order: `.code`, `.name`, `.tag`, `.cr`.
Tag classes: `tag` (neutral), `tag ai` (lime), `tag pbs` (blue). A zero-credit
requirement goes in `.zero`, never in `.courses` with a 0. `term-note` is one or
two sentences on why this term is shaped the way it is.

**Credit ruler.** `.ticks` carries `data-total` and `data-done`; the script builds
one `span.tick` per credit, `done` for the first N and `plan` for the rest.
`.lnum` repeats the same two numbers as text. `role="img"` plus `aria-label` makes
the ruler audible. One row per curriculum, not one row per credit category.

**Weight bar.** One `div` per group. `flex` is that group's credits. Classes
`m1`–`m3` are the major-average groups, darkest to lightest; `c1`–`c2` are the
CGA-only groups and use hatching. Segment totals must equal the planned credits.
The key swatches are `sw-fyp`, `sw-comp`, `sw-ai`, `sw-c` and must pair with the
segment class they describe.

**Week grid.** Eight columns: a 64px label column and seven days. Three time rows.
Cell classes: `class` (outline), `deep` (lime), `fyp` (blue), `rev` (grey), `buf`
(hatch), `off` (outline). This section is advice, not audit data.

**Tripwire.** Five notes. Head is a date, a number, or a two-word verdict; body is
one sentence naming the failure and its consequence. At most one head carries the
red grease mark (`.mark` + inline SVG ellipse).

## Invariants

- One `h1`, one `h2` per section. Headings carry their own weight; no kickers.
- No new colours, fonts, radii, shadows, or component classes. Reuse the tokens.
- `.reveal` elements may set `--rot` between `-.35deg` and `.2deg`. The script
  staggers the first three only.
- Font paths stay `assets/fonts/*.woff2`; the skill ships the three files, so copy
  them into the output repo. The page must open from disk offline.
- Every `.ticks` has `0 <= data-done <= data-total` and readable numbers.
- Every `.term-cr` equals the sum of its `.cr` cells.
- The bar totals the planned credits, not the whole degree.
- Print and reduced-motion paths stay intact; do not remove their CSS.

## Failure modes this layout exposes

These are structural traps in the design, not hypotheticals.

**The ledger rows do not sum to unique credits.** A course shared between the
major and an extended major appears in both rows. The rows measure requirement
coverage, not a partition of credits. The intro "Every square is one credit"
reads as a partition. Rule: never add the rows; if the page needs a unique total,
take it from the audit and say so.

**Two denominators are easy to mix.** New course credits, requirement-credits,
and unique credits toward the degree are three different numbers. A reader can
take one for another. Name the denominator where the number first appears, or
keep the other totals out of the page.

**The credit ruler needs JS.** Without it the bars are empty. That is acceptable
for an offline artifact with inline JS, but the `aria-label` must carry the
numbers. Always pair it with `role="img"`.

**The week legend reuses `.blk` on a 9px `<i>`.** It works because inline styles
win, but it is a hack. Leave it alone unless you are already editing that block.

**More than three terms.** `.terms` is a 3-column grid; a fourth term wraps to a
second row. Keep the stagger rules for the first three; do not add a column.

**Two terms.** Change `.terms` to `grid-template-columns:repeat(2,1fr)`. This is
the one permitted style edit; the component and tokens stay untouched. One term
uses a single column.
