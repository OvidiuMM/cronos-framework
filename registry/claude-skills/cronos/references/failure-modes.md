# Failure Modes — Catalog from Production Retros

Patterns that recur across Cronos cycles. Each entry: the failure, what surfaces it, the discipline that prevents it. When the agent senses itself drifting toward one, it names it and course-corrects.

## Vibe drift — implementation diverges from plan
**Failure:** Mid-cycle, files not in the plan are being touched; unplanned decisions are being made.
**Surfaces as:** the retro asks "did the diff match the plan?" and the answer is "mostly."
**Prevention:** the plan's file table is the truth. A change not in the table means stop and amend (Material amendments re-arm Gate 1). Don't free-ride on an approved scope.

## Author's bias — "the diff looks fine"
**Failure:** the Implementer reviews their own confident-looking output and ships; subtle logic and security gaps survive.
**Surfaces as:** a production bug, or a Validator's post-hoc "how did this ship?"
**Prevention:** Gate 2. The Validator is not the Implementer.

## Skipped plan gate
**Failure:** "I'll just try it real quick." Hours later the implementation has a shape that doesn't fit the system and is hard to undo.
**Surfaces as:** the plan written *after* the code, retroactively justifying it.
**Prevention:** plan, approval, then code. Exempt: bug fixes and small refactors that don't cross repo boundaries.

## Tests-pass-as-validation
**Failure:** "all tests pass, ship it" — but the agent wrote the tests to pass against its own assumptions.
**Surfaces as:** production breaking in ways the tests didn't cover.
**Prevention:** tests written against PRD acceptance criteria, not the code. Regression guards must be observed red on the buggy code before they count.

## Green build that's lying
**Failure:** a parallel test runner silently drops a suite with a compile error; "94 passed" while the build is red.
**Surfaces as:** a suite-level failure with zero failing assertions, or the failing suite changing between runs.
**Prevention:** the verify command runs the type-check explicitly; any zero-assertion suite failure is treated as a compile/load error and confirmed in-band.

## Wide formatter overreach
**Failure:** a repo-root format alias reformats dozens of unrelated files; reviewers can't see the change through the noise.
**Surfaces as:** surprise diff size at PR open.
**Prevention:** format only edited paths. Pre-existing format debt is a Technical Health Cycle, not a free rider.

## Pre-existing debt smuggled in
**Failure:** "while I'm in here" fixes to unrelated lint/type/dead-code issues; the PR is half feature, half cleanup, hard to review as either.
**Surfaces as:** review friction; fixes hiding inside reformats.
**Prevention:** catalog debt, surface it to the human, don't fix it in the same PR.

## Spec-driven scaffolding
**Failure:** endpoints/services built because the spec lists them, before any caller exists; they ship dormant or get deleted.
**Surfaces as:** a fresh-eyes audit finding dormant code.
**Prevention:** just-in-time construction — build when the first caller exists.

## Silent defaults on required parameters
**Failure:** a missing env/parameter silently defaults, misrouting behavior (e.g., to the wrong environment).
**Surfaces as:** correct-looking behavior against the wrong target.
**Prevention:** loud-fail — throw on missing, never default.

## Diagnosis-by-assumption on "stuck" UI
**Failure:** a resolved-but-discarded response looks identical to a hang from the UI; the agent patches the assumed cause.
**Surfaces as:** the fix not fixing it; the diagnosis flipping under evidence.
**Prevention:** get the request status and server log before editing code.

## Audit findings treated as facts
**Failure:** a fresh-eyes audit asserts a bug that isn't there; time is spent "fixing" working code.
**Surfaces as:** a fix that changes nothing observable.
**Prevention:** audits are claims. Verify each finding against the actual code before acting.
