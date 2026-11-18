---
name: graduation-plan
description: Build or regenerate the pinned-sheet graduation plan HTML (plan.html) from a student's study history. Use when a degree audit, transcript, USThing snapshot, or updated passed/in-progress course list should become the final one-page plan — term path, credit ledger, grade weighting, week template, and tripwires — or when an existing plan.html must be refreshed after grades, course changes, or a new snapshot. Requires the intake cohort's requirement documents.
---

# Graduation plan

A study history is not a plan. This skill resolves the student's passed and
in-progress courses against their **cohort's** requirements, chooses the remaining
terms, and renders the result as a pinned noticeboard of printed sheets.

The page is the last step. If the arithmetic is wrong, a beautiful page is worse
than no page.

## 1. Assemble the audit

Collect, from the student or their tracker:

- intake cohort (the year they entered, e.g. 2024-25) and current term
- programs: major, extended major, minor, Common Core home area
- every passed course: code, title, credits, term; include zero-credit courses
- every in-progress course
- the cohort's official requirement documents — PDFs or catalog pages for that
  year, not the current year's
- constraints: maximum credits per term, whether summer is allowed, target
  graduation date

Normalize the course list into one table. If a missing input can change the plan
— cohort year, a program, whether a course is passed or in progress — ask for it.
Do not fill the gap with a plausible guess.

**Done when** the course credits sum to the student's reported total, every
in-progress course has a credit value, and no input that changes the plan is
unknown.

## 2. Resolve the requirements

Follow `references/content-rules.md` §1. For each curriculum, map every
requirement to the courses that satisfy it, with status and credits. Apply the
cohort rule, exclusions, caps on sharing, and single-count minimums.

**Done when** every requirement in every curriculum has a status and a named
course or an empty slot, every passed course is assigned or deliberately left as
a free elective, and no forbidden pair or double count survives.

## 3. Build the remaining path

Follow `references/content-rules.md` §2. Fill the gaps term by term: prerequisites
first, then offering evidence, then the stated credit load, then the single-count
budget. Keep a swap option for every fragile slot.

**Done when** every gap has a planned course, each term hits the target load,
every prerequisite is passed or planned earlier, every course has an offering
status, and each single-count minimum is met (say so on the page if met exactly).

## 4. Write the sources before the page

Write the two markdown documents next to the artifact:

- `progress-<YYYY-MM-DD>.md` — audit tables, passed courses, in-progress courses,
  totals
- `plan-<YYYY-MM-DD>.md` — why the credit count is what it is, term tables,
  requirement audit, rules that decided the picks, sequencing, and what slips

Update the README tables to match, if the repo has them. Then build the HTML from
those documents.

**Done when** every number that will appear on the page exists in one of the two
documents, and the "why N credits" arithmetic adds up.

## 5. Fill the page

If the repo already has a `plan.html`, read it first as the worked example to
calibrate copy density and term-sheet shape. Then copy `assets/template.html` over
it as the new `plan.html`, or create the file if there is none. The template
already carries the full design system, fonts, components, script, and section
order.

Copy the three `.woff2` files from this skill's `assets/fonts/` into the output
repo's `assets/fonts/` before opening the page. The template's `@font-face` URLs
are relative to `plan.html`; without them the design falls back to Georgia and
system sans.

Keep verbatim:

- the `<style>` block, the script, every class name, colour, font, and section id
  (the one exception: `.terms` column count when the plan has two terms)
- the five nav links and their order
- the component shapes in `references/html-structure.md`

Replace:

- every `{{PLACEHOLDER}}`; there are no optional leftovers
- repeat blocks: one term article per remaining term, one course `li` per course,
  one stub per term plus graduation, one ledger row per curriculum, one bar
  segment and one key item per grade group, one tactic per line, one note per
  tripwire (exactly five)
- copy in the voice of `references/content-rules.md` §6

The week grid is advice, not audit data. Keep it as the default study template;
swap its two blue `.fyp` blocks for `.deep` only when the plan has no final-year
project.

**Done when** `rg '\{\{' plan.html` is empty, the counts match the plan, and the
section order and ids are intact.

## 6. Verify

Work through `references/verification.md` end to end. Do not sample it.

**Done when** every arithmetic, requirement, HTML, content, and render box is
checked, and the page opens from disk with no console errors.

## Guardrails

- **The cohort wins.** A later declaration does not move the curriculum forward.
- **Trace every number.** If it is not in the audit or a requirement document, it
  does not go on the page.
- **Ledger rows do not sum.** They measure requirement coverage; shared courses
  appear in more than one. Take unique totals from the audit.
- **Name the denominator.** Requirement-credits and unique credits are different
  numbers; the page may use both only if it says which is which.
- **Advice stays advice.** Term notes, tactics, the week, and tripwires may be
  stable across students; they must never contradict the audit.
- **No invented offerings or thresholds.** Future sections are pattern-only until
  published; credential floors are minimums, not targets.
- **Change the system in one place.** Where the repo has `DESIGN.md`, it is the
  contract and `assets/template.html` is its executed form; otherwise the template
  is the contract. A design change lands there first, then in the page — never in
  a single section.
