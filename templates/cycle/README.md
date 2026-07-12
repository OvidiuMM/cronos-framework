# Cycle Folder Convention

Every Cronos cycle lives in its own folder: `cycles/NNNN-<slug>/` (zero-padded, monotonic — the number is never reused, even for abandoned cycles).

| File | Created | Purpose |
|---|---|---|
| `01-plan.md` | D1 | Copy of `templates/agent-ready-prd.md`, filled. THE plan — Gate 1 operates on its Amendment Log (§9). |
| `02-prompts.md` | D1, appended daily | Working prompt log: prompts that worked + cautionary anti-patterns. Feed for promotion. |
| `03-decisions.md` | as decisions occur | Lightweight ADR log. Superseding a decision is cheap when the original + rationale are written down. |
| `04-validation.md` | D5 | The Validator's report (Gate 2): what was run cold, what was traced, verdict. |
| `05-retro.md` | D5 PM | All three roles. **The cycle is not closed until this is filled** — and `promote-cycle-learnings` runs only against closed cycles. |
| `daily/` (optional) | daily | Daily Pulses, if committed rather than posted to chat. |

The folder is the cycle's complete institutional record. The next cycle's PM plans from the previous folder's retro Open Follow-ups table; the next Implementer reads the retro first.
