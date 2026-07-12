# Plan (agent-ready PRD) — excerpt

**PRD ID:** PRD-2026-001 · **Cycle Start (D1):** 2026-03-04 (a Wednesday — D-clock: Wed, Thu, Fri, Mon, Tue)
**PM:** @dana · **Implementer:** @edgar · **Validator:** @omar · **Risk:** Medium (payments touchpoint)
`approved_through_amendment:` 2

## 2. Problem
Merchants can't send payment links by SMS; support creates them manually (11 min avg, error-prone).

## 3. Success criteria
- [x] Link created via one service call; public pay page renders on mobile
- [x] QR generated best-effort; link creation never blocks on QR failure
- [x] Regression suite green; new paths covered

## 5. Constraints (excerpt)
- Sibling-repo check: `billing-backend` has a proven provider SDK integration → reuse pattern (see ADR 2)
- Deployment artifacts: webhook endpoint config, public-page hosting rule — enumerated, verified D5

## 7. WBS (excerpt)
| ID | Task | Day | Status |
|---|---|---|---|
| T-01 | Type-first refactor of PaymentLink types | D1 | ✅ |
| T-02 | Service facade (exactly 4 methods) | D2 | ✅ |
| T-03 | Best-effort QR sidecar | D3 | ✅ |
| T-04 | Fresh-eyes audit + fixes | D4 | ✅ |
| T-05 | Validation (d5-checklist) | D5 | ✅ |

## 9. Amendment log
| # | Date | Class | Change | PM re-approval |
|---|---|---|---|---|
| 1 | D2 | Material | Drop bulk-send from scope (hidden dependency on messaging quota) | ✅ @dana D2 |
| 2 | D4 | Verification-fix | QR error typed as recoverable, not thrown | logged, no re-arm |
