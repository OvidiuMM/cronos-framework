---
name: cronos
description: Operate inside a Cronos engineering cycle — hold the gates, follow the D1–D5 cadence, capture artifacts. Invoke when starting a new cycle, working mid-cycle, running validation on someone else's cycle, or closing a cycle.
---

# Cronos

Run engineering work inside the Cronos framework — five-day cycles (D1–D5, any start day), a plan gate before code, half-day adversarial validation before ship.

This skill is **behavioral**, not generative. Invoking it doesn't produce output on its own; it shapes how you approach the work for the rest of the conversation.

## When to use
- The user says "start a cycle" / "kick off cycle N for project X".
- The repo's `CLAUDE.md` or agent guardrails mention Cronos, Mission Control, or "cycle" in a methodology sense.
- The user asks you to validate, review, or audit a diff produced by a Cronos cycle.
- The user is mid-cycle and needs planning, prompting, decision capture, verification, or close-out.

## When *not* to use
- One-shot bug fixes, small refactors, local edits. Cronos is heavyweight relative to those.
- Repos that don't follow Cronos — don't retrofit; ask first.
- Pure discovery work with no PRD yet. Cronos starts after the PM has an agent-ready PRD.

## Operating modes

You enter exactly one mode per invocation. If unclear, ask which applies.

### Mode 1: Bootstrap — start a new cycle (D1, pre-kickoff)
1. Confirm the project; check for a project doc (`docs/projects/<name>/`).
2. Find the next cycle number (highest 4-digit prefix in `cycles/`; globally ordered, never reused).
3. Copy `templates/cycle/` → `cycles/<NNNN>-<slug>/`; pre-fill the README (people, repos, risk, tags).
4. If a previous cycle of this project exists, read it end-to-end — surface its retro lessons and binding decisions.
5. Hand off: the human runs Kickoff and fills `00-kickoff.md`. **Do not start coding.**

### Mode 2: Mission Control — draft the plan (D1, post-kickoff)
1. Read the PRD, project doc, and `00-kickoff.md` cold. Read the previous cycle's `03-decisions.md` — decisions may bind.
2. Draft `01-plan.md`: the file-level table is non-negotiable ("I'll touch the user service" is not a plan).
3. Map every scope item to a PRD acceptance criterion. If one doesn't map, **stop and fix the PRD** — never invent justification.
4. Surface hot spots for the Validator.
5. Post the plan and **wait for explicit approval before any code**. This is the cheapest hour of the cycle.

### Mode 3: Implementation (D2–D3)
1. Capture prompts in `02-prompts.md` **as you use them** — the most-skipped, most-regretted file.
2. Capture propagating decisions in `03-decisions.md` (naming a function doesn't qualify; a rules-vs-secrets trade-off does).
3. Verify every assumption about SDKs, versions, env vars before relying on it.
4. One concept per change. Flag unrelated bugs; don't quietly fix them.
5. If the plan changes, add a dated row to the plan's Amendment Log and classify it: **Material** (new file / contract / dependency / design) blocks code until the PM re-approves; Verification-fix and Cosmetic are logged only.
6. Post the three-line Daily Pulse at end of day (Landed / Next / Friction) if the team runs it.

### Mode 4: Verification (D4)
1. Generation stops; verification starts. Run all suites — never claim "tests pass" without running them, and run the type-check explicitly: a parallel test runner can silently drop a suite with a compile error and report green.
2. Tests are generated against **PRD acceptance criteria**, not against the code you wrote.
3. Any regression-guard test must be **observed failing** on the buggy code before it counts.
4. For UI changes, **say explicitly if you could not run the browser** — type-checks verify code correctness, not feature correctness.
5. Surface anything noticed during implementation that wasn't fixed.

### Mode 5: Validation — adversarial half-day (D4 PM / D5 AM)
You are reviewing someone else's diff. You are **not** the Implementer.
1. Read `01-plan.md` and `03-decisions.md` for intent; read the Validator pre-brief.
2. Walk the D5 checklist line by line; run the suites cold on a fresh checkout.
3. Execute as an attacker: bypass the UI, replay malformed input, race two writes.
4. Verdict: approve / approve with conditions / held / blocked. There is no "looks good but…".
5. Fill `04-validation.md`.

### Mode 6: Close (D5 PM)
1. Help draft `05-retro.md` — all three role sections; an explicit "uneventful" entry is valid, an empty section is not. The cycle is not closed without it.
2. Run promotion: candidates from `02-prompts.md` and the retro lift to the toolkit (prompts: 1 proven use; skills: recurred lesson; knowledge: 3-cycle rule). Mark promoted items with backlinks.
3. Update the cycles index.
4. Hand the release decision (four states) to the human. **Do not push or open PRs unless explicitly told.**

## The non-negotiable gates
1. **Plan before code** (Gate 1). No non-trivial implementation without an approved `01-plan.md`. Material amendments re-arm the gate.
2. **Validator ≠ Implementer** (Gate 2) at Medium+ risk. Solo high-risk cycles are named, time-bounded deviations — never the norm.
3. **The agent does not push or open PRs.** Close hands off to the human, who owns the release decision.

If the user asks you to violate a gate, restate the rule and ask for explicit confirmation. Don't silently comply.

## Hard prohibitions
- **Never self-grant permissions.** Don't write to your own permission/settings files. If broader autonomy is needed, give the human the config to paste.
- **Never run wide formatters.** Scope to the paths you edited; repo-wide format aliases balloon PRs with unrelated noise.
- **Never amend commits unless explicitly asked.** When a hook fails, the commit didn't happen — `--amend` rewrites the *previous* commit.
- **Never commit `.env` or credentials.** Even if staged, refuse and flag.

## References (load on demand)
- [`references/failure-modes.md`](references/failure-modes.md) — catalog of recurring failure modes from production retros.
- [`references/phase-prompts.md`](references/phase-prompts.md) — paste-ready invocation prompts, one per mode.
