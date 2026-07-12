# Retro

Filled on D5, before the cycle closes. All three roles (PM, Implementer, Validator) contribute. The most valuable file in the folder for the next Implementer.

If the cycle was uneventful, write that explicitly — "nothing surprised us, here's what propagated cleanly" is signal, not filler.

---

**Cycle:** <NNNN>-<slug>
**Started:** YYYY-MM-DD (D1) · **Closed:** YYYY-MM-DD
**Implementer:** · **Validator:** (≠ Implementer at Medium+ risk) · **Plan approved by:** (through amendment #)
**Risk:** Low / Medium / High

## What worked

> Specific. "The half-day Validator caught X" is signal. "Process worked" is noise.

- ...

## What didn't work

> Even more specific than the above. Failure modes are the propagating signal — the next Implementer wants to know exactly what to watch for.

- ...

## Surprises

> Things you didn't expect, positive or negative. Vendor SDK didn't behave like docs said. Type-check caught 12 things, lint caught 0. Etc.

- ...

## Lessons (carry into next cycle)

> Numbered, declarative, propagatable. Each lesson should be useful to someone who didn't run this cycle.
> **Recurrence check (Mandate 6):** if any lesson below also appears in the previous cycle's retro, it must be converted to an enforced rule (skill / CI check / guardrail entry) next cycle.

1. ...

## Promotion candidates

> Processed at close by `promote-cycle-learnings` (see `doc/learning-propagation.md`). Mark landed items with a backlink so they aren't re-proposed.

- **Prompts → `ai-toolkit/prompts/`:** ... (threshold: 1 proven use, generalized phrasing)
- **Skills → `ai-toolkit/skills/`:** ... (threshold: recurred lesson or enforcement-required)
- **Knowledge → `ai-toolkit/knowledge/`:** ... (threshold: 3-cycle rule or deliberate standard; stamp `*(seen: NNNN)*` if below)

## Open follow-ups

> Things noticed this cycle that aren't in scope to fix. The next cycle's PM looks here when planning.

| Item | Severity | Owner |
| ---- | -------- | ----- |
|      |          |       |

## Release decision

- [ ] **Shipped** — production, unconditional, on YYYY-MM-DD.
- [ ] **Shipped with conditions** — deployed (env: ...); conditions tracked above; decision reopens if one surfaces a real problem.
- [ ] **Held** — unblock condition: ...
- [ ] **Rolled back** — reason: ...

---

## Validator section

> What worked / didn't / surprises from the validation seat. Left empty is a close-gate violation; "uneventful — nothing to report" is valid.

## PM section

> Scope shape, stakeholder alignment, process hygiene. Same rule.
