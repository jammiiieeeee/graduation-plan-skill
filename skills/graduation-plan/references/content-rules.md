# Derivation and copy rules

The page is downstream of two source documents: the progress snapshot (what the
student has) and the plan (what remains). Resolve the data there first; the HTML
only renders the result.

## 1. Resolve requirements against the intake cohort

Use the catalog year the student entered, not the year they declared a minor and
not the current catalog. One curriculum can be declared later without moving
forward: HKUST AR 4.3 fixes the curriculum at year of entry.

For each requirement record:

| Field | Value |
|---|---|
| Curriculum | Major / Common Core / Extended Major / Minor |
| Group | the document's own grouping (Fundamental, Required, Elective, area) |
| Credits required | from the cohort document |
| Satisfied by | course(s) already passed or in progress |
| Status | done, in progress, planned, not started |
| Single-counted? | yes / no / shared, when the curriculum has a minimum |

Rules that decide the assignment:

- **Single-count minimum.** An extended major or minor may require N credits that
  count for nothing else. Track that number separately from the total.
- **Exclusions.** Courses listed as mutually exclusive can never both appear.
  Check the pair, not just the individual course.
- **Maximum sharing.** If the document caps shared credits, the cap plus the
  single-count minimum is the real budget. State the cap in the ledger note.
- **Free electives.** A passed course that satisfies nothing is not an error; it
  still counts toward the 120. List it in the audit, not as a requirement.
- **Zero-credit requirements** still consume a term slot and appear in `.zero`.

Completion: every requirement in every curriculum has a status and a named
course or a planned slot. No course is claimed twice where the rules forbid it.

## 2. Build the remaining terms

Constraints, in priority order:

1. **Prerequisites** must be passed or planned earlier.
2. **Offering evidence** beats preference. Check the last four published terms;
   a course with no section in any of them is not a plan.
3. **Credit load.** Fit the student's stated maximum per term. Do not silently
   add a summer term; the default is regular terms only.
4. **Single-count budget.** A swap can preserve total credits while breaking the
   single-count minimum. Check the minimum after every swap.
5. **Difficulty spread.** Put the heaviest technical courses in a term without
   the final-year project, when the plan allows it.

For every course keep the evidence line: prerequisite met, exclusion checked,
term pattern (Fall-only, Spring-only, both), and whether that is confirmed or
pattern-only. Pattern-only belongs in the footer caveat.

Completion: each term's credits equal the target, every unmet requirement has a
course, every prerequisite has an earlier or passed source, and each course has
an offering status.

## 3. The ledger

One row per curriculum. `done` = passed + in progress, in that curriculum's own
currency. `total` = the curriculum's requirement credits.

- Shared courses appear in more than one row. That is correct; the rows measure
  coverage, not a partition.
- **Never sum the rows.** The unique-credit total comes from the audit.
- A row can show `done` above the single-counted requirement total; the minimum
  is a constraint on the plan, not on the row.
- Put the one deliberate overlap in the ledger note: which course, which two
  requirements, and why the single-count rule still holds.

## 4. Grade weighting

Split the remaining credits into two buckets:

- **Counts toward the major average** — final-year project, major required and
  elective courses, extended-major courses that are not reused elsewhere.
- **Counts only toward the overall average** — Common Core and minor courses.

The bar shows both buckets; filled segments are the major-average groups, hatched
segments are overall-only. The statement above the bar names the share that
carries the leverage, not the total. The floors are credential minima from the
requirement documents; label them as minimums, never as targets. Do not invent
honours bands or grade thresholds.

If the audit carries no grades, do not estimate averages: show the weighting and
the credential floors, and leave the student's current average off the page.

## 5. The hero

- **Three lines.** Shape, load, constraint. Examples: "Three terms. / Eighteen
  credits each / No summer." Keep each line under six words.
- **Stamp.** Snapshot date, `D Mon YYYY` or `DD.MM.YY`, matching the file date.
- **First move.** The earliest irrevocable action, with a date and the exact
  courses or forms involved. Not "plan ahead".
- **Lede.** One sentence: the size of what remains and the one trade-off the plan
  makes. Name the denominator if two credit totals are in play.
- **Stubs.** One per term with credits and year/term, then one for graduation.

## 6. Copy

The voice is a senior student's margin note: concrete, numeric, unimpressed.

- One claim per sentence. Prefer a number to an adjective.
- Use the second person for advice ("your major average"); use the third person
  for rules ("a fail costs a term").
- Short verdicts are allowed as headings: "No slack." "Counted twice."
- Name the consequence. "FYP bidding. Choose an AI project" is weaker than
  "FYP bidding. EMIA 4990 must approve it as AI-integrated."
- No motivational filler, no "journey", no "remember to", no exclamation marks.
- No rhetorical questions, no "not just X, but Y", no triads.
- Do not claim a course runs in a term unless it is published. "Pattern only" is
  an honest note and belongs in the footer.

## 7. Tripwires

Choose five constraints that can actually invalidate the plan:

1. A credit rule met exactly (single-count, cap, minimum).
2. A dated administrative deadline (bidding, add/drop, approval).
3. A repeating zero-credit or residency requirement.
4. The last chance to declare or lock a credential.
5. The recovery path if a course is failed or not offered.

Each body is one sentence with the failure and its cost. If the plan has slack,
say where the slack is; do not manufacture a fifth risk.

## Calibration

Useful as a scale reference, not as defaults:

- Requirement-credits remaining minus deliberately shared credits equals new
  course credits. The shared credits still satisfy both requirements.
- Unique credits held plus new unique credits equals the graduation total. A
  curriculum can ask for more than the degree minimum.
- Split the new credits into major-average and overall-only totals; the two must
  add up to the planned load.
- Credential floors come from the requirement documents and are minimums.
