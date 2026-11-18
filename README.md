# graduation-plan

An agent skill that turns a student's study history into one static, self-contained
graduation plan page: remaining terms, a credit ledger, grade weighting, a week
template, and the constraints that can break it.

Designed for [OpenCode](https://opencode.ai), compatible with any agent that reads
`SKILL.md`.

## Install

```bash
npx skills@latest add jammiiieeeee/graduation-plan-skill \
  --skill graduation-plan -g -a opencode --copy -y
```

Requires Node 22.20 or later.

- `-g` installs for every project. Drop it to install into the current project.
- `-a opencode` targets OpenCode. Omit it to choose agents interactively.
- `--copy` avoids symlinks (useful on Windows). Omit it to link.

Verify with:

```bash
npx skills list -g
```

## Use

Open a project and ask for the skill by name, then supply the audit:

- intake cohort and current term
- major, extended major, minor, Common Core home area
- passed courses: code, title, credits, term
- in-progress courses
- the cohort's official requirement documents
- credit-load limits and whether summer is allowed

The skill writes `progress-<date>.md` and `plan-<date>.md` first, then renders
`plan.html`, then runs the verification checklist.

## What is inside

| Path | Purpose |
|---|---|
| `skills/graduation-plan/SKILL.md` | Six-step procedure: audit, requirements, path, sources, page, verify |
| `references/content-rules.md` | Cohort rules, single-counting, ledger semantics, grade weighting, copy voice |
| `references/html-structure.md` | Section contract, component shapes, structural failure modes |
| `references/verification.md` | Arithmetic, requirement, HTML, content, and render checks |
| `assets/template.html` | Complete design system, CSS, and JS with placeholders |
| `assets/fonts/` | Archivo, Archivo Black, and Literata (SIL OFL 1.1 — see `OFL.txt`) |

The template expects the fonts at `<project>/assets/fonts/`. The skill copies them
from its own `assets/fonts/` when it builds the page.

## Scope

The pipeline and page are general. The rule references — cohort year, single-count
minimums, MCGA/CGA, credential floors — are HKUST-specific. For another university,
adapt `references/content-rules.md`; the audit and rendering steps still apply.

The skill produces an advisory plan, not an official degree audit. It checks
prerequisites, exclusions, and published offerings, and marks anything unconfirmed
as pattern-only.
