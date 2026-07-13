# Cycle <NNNN>: <slug>

> This file becomes the cycle's overview when you copy `templates/cycle/` into `cycles/<NNNN>-<slug>/`. Fill it in right after the copy. For the folder convention and how the files fit together, see `doc/learning-propagation.md` §5.

**Project:** <name>
**Project doc:** <link to `docs/projects/<name>/` in the product repo>
**Cycle dates:** YYYY-MM-DD (D1) → YYYY-MM-DD (D5)
**Risk tier:** Low / Medium / High
**Tags:** <comma-separated — cycles are globally numbered, not grouped by project; tags are how you find a project's cycles>

## People
- **Implementer:** <name>
- **Validator:** <name — ≠ Implementer at Medium+ risk>
- **PM / plan approver:** <name>

## Repos touched
- `<repo-1>` — <one-line summary of what changed there>

## Scope (one line per change)
- ...

## Outcome
> Fill at cycle close. One paragraph: what shipped, what was deferred, the release decision (four states).

## Reading order for the next Implementer
1. [`05-retro.md`](05-retro.md) — lessons. Read this even if you skim the rest.
2. [`03-decisions.md`](03-decisions.md) — decisions that may bind your work.
3. [`02-prompts.md`](02-prompts.md) — prompts to steal.
4. [`01-plan.md`](01-plan.md) — what last cycle's plan looked like, as a reference shape.
5. [`04-validation.md`](04-validation.md) — what the Validator caught; look hardest there this time.

The kickoff (`00-kickoff.md`) is historical context — read it if you're new to the project.
