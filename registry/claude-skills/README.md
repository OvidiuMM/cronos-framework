# Agent Skills

Drop-in behavioral skills for Claude Code (or any agent runtime that reads `SKILL.md` files). Install by copying into your toolkit repo's `skills/` directory or your project's `.claude/skills/`.

| Skill | Purpose |
|---|---|
| [`cronos/`](cronos/) | Operate inside a Cronos cycle: six modes (Bootstrap → Close), three non-negotiable gates, hard prohibitions, and a failure-mode catalog grown from production retros. |

## The per-mode prompt pattern

Pair the skill with one paste-ready prompt per cycle phase (start → draft plan → amend → verify → validate → close). The prompts don't replace the skill — they invoke it with inputs already structured, so the agent enters the correct mode and stops at the right gate. Recommended file shape: human-readable frontmatter (`name`, `purpose`, `invokes_skill`, `model_tested`, `expected_inputs`, `known_failure_modes`) and intro on top, the paste block **last** between `=== COPY FROM HERE ===` / `=== COPY UNTIL HERE ===` markers, so you scroll once and grab it.
