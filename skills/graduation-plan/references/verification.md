# Verification

Run every check. A page that looks right and reconciles wrong is the failure
mode this artifact exists to prevent.

## Arithmetic

- [ ] Passed credits = sum of credit-bearing passed courses. Zero-credit courses
      are listed but add nothing.
- [ ] In-progress credits = sum of current-term courses. Starting total =
      passed + in-progress.
- [ ] Each term's `.term-cr` equals the sum of that term's `.cr` cells.
- [ ] Planned credits = sum of all term totals. Ending total = starting +
      planned. State whether that is unique credits or requirement-credits.
- [ ] Requirement-credits remaining (from the audit) minus deliberate double
      counts equals planned credits.
- [ ] Each ledger row: `data-done` equals the progress doc for that curriculum;
      `data-total` equals the requirement doc; both are repeated in `.lnum` and
      the `aria-label`.
- [ ] The ledger rows are not added anywhere. If a total appears, it comes from
      the audit.
- [ ] Bar segment flex values sum to the planned credits.
- [ ] Bar groups match the key swatches, one label per segment.
- [ ] Every number on the page also appears in `plan-<date>.md` or
      `progress-<date>.md` and traces to the audit or a requirement document.

## Requirements

- [ ] Every unmet requirement has exactly one planned course or one explicit
      substitution.
- [ ] Every planned course satisfies at least one requirement, or is labelled as
      a free elective.
- [ ] Prerequisites are passed or planned in an earlier term. No exceptions.
- [ ] No mutually exclusive pair appears together.
- [ ] Each single-count minimum is met; if met exactly, say so on the page.
- [ ] Each cap on shared credits is respected.
- [ ] Cohort year in the documents matches the student's intake, not the current
      catalog.
- [ ] Offering evidence exists for every course: published section or explicit
      "pattern only" caveat.

## HTML

- [ ] `rg '\{\{' plan.html` returns nothing.
- [ ] One `h1`; one `h2` per section; no heading roles misused.
- [ ] Nav hrefs `path`, `ledger`, `marks`, `week`, `breaks` all have matching ids.
- [ ] `<article class="sheet term` count equals the term count; `.stub` count is
      terms + 1.
- [ ] `.note reveal` count is exactly five.
- [ ] Every `.ticks` has `role="img"`, an `aria-label`, and
      `0 <= data-done <= data-total`.
- [ ] Every course row has four children: `.code`, `.name`, `.tag`, `.cr`.
- [ ] Every tag class is one of `tag`, `tag ai`, `tag pbs`.
- [ ] Every `.term-cr` matches its rows; rotations stay within `-.35deg` and
      `.2deg`.
- [ ] The `<style>` block is unchanged from `assets/template.html` except for
      legitimate component additions. Diff it; do not trust memory.
- [ ] Font URLs still resolve relative to the repo root.

## Content

- [ ] The hero's credit figure matches the plan. If two totals are in play, the
      lede names the one it uses.
- [ ] The stamp date, footer build date, source filenames, and snapshot date
      agree.
- [ ] The ledger note names the deliberate double count and why it is legal.
- [ ] Grade advice is about leverage, not effort theatre; floors are labelled
      minimums.
- [ ] Tripwires are five distinct failure modes, each with a consequence.
- [ ] Nothing claims a future section, grade rule, or approval that is not in a
      source document.
- [ ] Copy passes the voice rules in `content-rules.md`: no filler, no rhetorical
      questions, no triads, no motivational prose.

## Render

Open `plan.html` from disk, not a server.

- [ ] Fonts load offline; no external requests; console clean.
- [ ] 1440px: three term sheets in one row, no horizontal scroll except the week
      at narrow widths.
- [ ] 1020px: hero, terms, and marks collapse to one column; notes become 3-up.
- [ ] 680px: single-column sheets, ledger ticks wrap under the label, week swipes.
- [ ] 430px: notes single-column, no clipped text or tape.
- [ ] Reveal animation runs once, capped at three staggered sheets; reduced
      motion shows everything immediately.
- [ ] Print preview: no tape, stamp, pins, or holes; no clipped sheets.

## Red flags

Any one of these means stop and fix before delivering:

- a leftover `{{PLACEHOLDER}}`
- a term total that does not match its rows
- ledger rows added together as a credit total
- a course planned before its prerequisite
- a claimed offering with no published section
- six or four tripwires
- a new colour, font, or class invented for one section
- a number that exists only in the HTML
