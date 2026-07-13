# Mission Control Plan

The "rigorous plan." Written by the **Implementer** on D1, *after* Kickoff and *before any code*. Approved by the PM before implementation starts (Gate 1). This is a separate artifact from the PRD: the PRD (see `templates/agent-ready-prd.md`) is the PM's spec; this plan is the Implementer's file-level answer to it.

---

**Implementer:** · **Validator:** (≠ Implementer at Medium+ risk) · **Risk tier:** Low / Medium / High
`approved_through_amendment:` 0

## 1. Scope (in)
- ...

## 2. Scope (out — explicitly)
> Things considered and not done this cycle. Anchors against scope drift.
- ...

## 3. PRD coverage
> Every scope item maps to a PRD acceptance criterion. If something doesn't map, stop and fix the PRD — don't invent justification.

| Scope item | PRD § | Acceptance criterion |
|-----------|-------|----------------------|

## 4. File-level changes
> The table is non-negotiable. "I'll touch the user service" is not a plan.

| Repo | File | Change | Why |
|------|------|--------|-----|

## 5. Schema / contract changes
- **DB schema:** · **API contract:** · **Auth / claims:** · **Rules / permissions:** · **Backwards compatibility:** ...

## 6. Test approach
| Layer | What we'll test | Tool / location |
|-------|-----------------|-----------------|
| Unit | | |
| Integration | | |
| E2E / UI | | |
| Security | | |

## 7. Deployment artifacts (release-critical)
> Security rules, IAM grants, lifecycle rules, env config, feature flags — enumerated here, verified at D5 (checklist §7).
- ...

## 8. Hot spots
> Brought forward from `00-kickoff.md`, refined. The Validator looks hardest here.
- ...

## 9. Validator pre-brief
> One paragraph the Validator reads cold on D4 PM. What changed, what to challenge, what to ignore.

## 10. Amendment log (Gate 1)
> Every dated change after approval, classified. **Material** blocks code until the PM re-approves (bump the counter above). Verification-fix and Cosmetic are logged, no re-arm. Implementer proposes the class; Validator can contest.

| # | Date (D<n>) | Class (Material / Verif-fix / Cosmetic) | Change | PM re-approval |
|---|-------------|------------------------------------------|--------|----------------|

## next_step
> One line, always current: the single next action. Doubles as the Daily Pulse's "Next" line. A pointer, not a record — history lives in the pulses.
