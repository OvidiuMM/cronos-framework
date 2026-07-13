# Phase Prompts — paste-ready invocations, one per mode

Six short prompts that invoke the `cronos` skill in the right mode with structured inputs. They don't replace the skill; they enter it at the right gate. Fill the bracketed fields, paste into a Claude Code session. Convention: stamp each with the model you tested it against — prompts drift as models change.

## 1 · Bootstrap (D1, pre-kickoff)
> Run /cronos in Bootstrap mode. Project: `<name>`. Scaffold the next cycle folder from `templates/cycle/`, pre-fill the README (Implementer `<name>`, Validator `<name>`, risk `<tier>`, tags `<tags>`), and read the previous cycle of this project if one exists — surface its retro lessons and binding decisions. Stop before Kickoff; do not code.

## 2 · Mission Control (D1, post-kickoff)
> Run /cronos in Mission Control mode and draft `01-plan.md`. Inputs: PRD at `<path>`, kickoff at `<cycle>/00-kickoff.md`, previous cycle's `03-decisions.md` at `<path>` (if any). Read everything cold first. File-level table required; map every scope item to a PRD acceptance criterion — if one doesn't map, stop and tell me the PRD needs fixing. Post the plan and wait for my approval. No code.

## 3 · Amend the plan (D2–D3)
> Run /cronos in Implementation mode. The plan needs an amendment: `<describe the change>`. Add a dated row to the Amendment Log, propose its class (Material / Verification-fix / Cosmetic) with one line of reasoning, and if Material, stop until I re-approve. Do not continue building on the amended scope before that.

## 4 · Verification gate (D4)
> Run /cronos in Verification mode. Run all suites plus the explicit type-check; treat any suite-level failure with zero failing assertions as a compile error and confirm in-band. Confirm every regression guard was observed red on the buggy code. Tests must trace to PRD acceptance criteria. Tell me explicitly what you could NOT verify (e.g., browser flows). End with a ready-for-Validator yes/no and why.

## 5 · Validation (D4 PM / D5 AM — run by the Validator, not the Implementer)
> Run /cronos in Validation mode on cycle `<NNNN>`. You are not the Implementer. Read `01-plan.md` §Validator pre-brief and `03-decisions.md`, run the suites cold from a fresh checkout, walk the D5 checklist, and attack: bypass the UI, replay malformed input, race writes. Verdict must be one of approve / approve with conditions / held / blocked — fill `04-validation.md`.

## 6 · Close (D5 PM)
> Run /cronos in Close mode for cycle `<NNNN>`. Draft `05-retro.md` with me (all three role sections). Then run promotion against the retro's candidates: prompts (1 proven use), skills (recurred lessons), knowledge (3-cycle rule) — with backlinks on anything promoted. Update the cycles index. Hand me the release decision; do not push or open PRs.
