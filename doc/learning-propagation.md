# Learning Propagation: the AI Toolkit Layer

**Status:** Adopted (v2.1) · Candidate "Part E" for the methodology paper.
**Provenance:** Generalized from a production AI Toolkit repository (9 cycles, 0001–0009); conventions verified against the source.

---

## 1. Why a second layer

The Cronos cycle (Parts A–D) is a *working-memory* loop: five days, one deliverable, close. But the efficiency model's speedup factor `S` is not a constant — it grows only if what a cycle learns survives the cycle. The empirical finding behind the Recurrence Rule (Mandate 6) is that **retro prose alone does not propagate**: the same formatter lesson was written in cycle 1's retro and violated in cycle 2 by a team that had read it.

The **AI Toolkit** is the long-term-memory layer: a versioned repository (typically a sibling repo, `ai-toolkit/`) that accumulates reusable assets across cycles. In memory terms: the cycle is working memory, the retro is consolidation, the toolkit is long-term storage, and the Recurrence Rule is the forgetting detector.

This compounding can be made explicit in the efficiency model: the per-task speedup in cycle *n* is better modeled as

S(n) = S₀ + κ·K(n)

where `K(n)` is the stock of promoted toolkit assets applicable to the task and `κ` their average marginal contribution. Cronos without a toolkit holds `K` at zero and forfeits the compounding term.

## 2. Toolkit taxonomy — three tiers by generality

```
ai-toolkit/
├── cronos/
│   ├── templates/   # Blank cycle scaffolds (this repo's templates/cycle/)
│   └── cycles/      # One folder per completed cycle — flat, globally numbered
├── prompts/     # Single-shot reusable prompts. One proven use suffices to promote.
├── skills/      # Behavioral agent skills + mechanized automations.
│                # Two roads in: (a) a prompt that earns reuse across 2+ cycles and
│                # consistently outperforms free-form chat; (b) a lesson that must be
│                # ENFORCED, not remembered — Mandate 6 (Recurrence Rule) conversions.
├── agents/      # Agent definitions and system prompts (e.g. a master operating contract).
└── knowledge/   # Org-wide context: conventions, glossaries, vendor gotchas.
                 # Gated by the 3-cycle rule (see §4). Hygiene: an empty placeholder
                 # beats a stale 200-line convention document nobody reads.
```

**Two-repo split.** Keep methodology and substance apart: the framework (cadence, gates, blank templates, sanitized examples) is public; the toolkit (full cycle archives, org prompts, agent system prompts, scan configs) is private. The test: if you're writing the same document into both repos, it belongs in exactly one — methodology → public, substance → private.

**Flat, global cycle numbering.** One folder per cycle (`0001-`, `0002-`, …), never nested by project or team. Lessons cross-pollinate better as siblings; "show me the last five cycles regardless of project" is a one-glance answer. A `Tags:` line in each cycle's overview is how you search by project.

**Prompts** are phrasings that reliably steer an agent: "edit the central type first and walk the compiler errors", "prove the regression test fails on the buggy code before trusting it". Cheap to promote, cheap to retire.

**Skills** are lessons converted into machinery — a path-scoped formatter wrapper, a CI check, an editor rule. A lesson earns skill-hood the second time it is written (Mandate 6).

**Knowledge** is expensive to maintain and easy to bloat, so it carries the highest bar.

## 3. The working prompt log (`02-prompts.md`)

Each cycle keeps a running log of prompts that worked — and prompts that backfired. Two entry types:

- **Working entries:** the actual prompt text (pasted, not summarized), with a per-entry stamp: phase, **model tested against** (prompts drift in effectiveness as models change — the version stamp lets the next reader judge currency), why it worked, what it produced, reuse notes.
- **Cautionary entries:** anti-patterns, kept as negative examples ("recommended an integration before checking the sibling repo"; "fired a multiple-choice question before absorbing pasted context"). Cautionary entries are **never promoted as prompts**; their lessons are captured in the retro's Lessons section instead.

The log is written *during* the cycle, not reconstructed on D5 — a prompt's context evaporates within days.

## 4. The promotion pipeline (`promote-cycle-learnings`)

Run once, at cycle close, against a **closed** cycle (retro filled — see the retro close gate). For each candidate in the retro's "Promotion candidates" section:

| Asset | Threshold | Rationale |
|---|---|---|
| Prompt | **1 proven use** in the closing cycle, phrased generally enough to reuse | Cheap to add, cheap to retire |
| Skill | Lesson has **recurred** (Mandate 6) or requires enforcement to hold | Machinery beats memory |
| Knowledge | **3-cycle rule:** seen in ≥3 cycles' decision logs, OR a deliberate org-wide standard adopted by the PM | Prevents first-cycle noise from calcifying into doctrine |

Rules of the pipeline:

1. **Backlink on promotion.** Each promoted item is marked in the retro with a link to its toolkit location (`✅ promoted → prompts/<name>.md`) so it is never re-proposed by a later cycle.
2. **Held ≠ rejected.** Situational candidates stay in the cycle folder marked "held", with the holding reason. A later cycle that hits the same situation re-evaluates them.
3. **Knowledge candidates below threshold are stamped** with the cycles that have seen them (`*(seen: 0009)*`) so the 3-cycle counter is auditable.
4. **The pipeline runs only against closed cycles** — an unfilled retro blocks the promotion of that cycle's own wins, which is the incentive that keeps retros written.
5. **Promotion is a proposal, not an action.** The agent flags candidates; a human lifts them. Promoted prompt files carry human-readable frontmatter: `name`, `purpose`, `model_tested`, `expected_inputs`, `known_failure_modes`.
6. **Prompt → skill ladder:** a prompt that earns reuse across two or more cycles *and* consistently outperforms free-form chat graduates to a skill.

## 5. The cycle folder

Each cycle is a folder `cycles/<NNNN>-<slug>/` — 4-digit, zero-padded, **globally numbered across all projects** (never per-project subfolders: lessons cross-pollinate better as siblings, and "the last five cycles regardless of project" stays a one-glance answer; use the README's Tags line to find a project's cycles).

| File | Filled | By |
|---|---|---|
| `README.md` | at copy + at close (Outcome) | PM/Implementer |
| `00-kickoff.md` | at kickoff, then frozen | PM |
| `01-plan.md` | D1, before code (Gate 1) | Implementer |
| `02-prompts.md` | as you go — never reconstructed at close | Implementer |
| `03-decisions.md` | as decisions occur | Implementer |
| `04-validation.md` | D5 (Gate 2) | Validator |
| `05-retro.md` | D5 PM — the close gate | all three roles |

**Reading order for the next Implementer** (before opening an editor): retro → decisions → prompts → plan → validation. The kickoff is historical context.

## 6. Prompt vs. skill: the CLI test

If you'd write a CLI for it — clear inputs, clear outputs, repeatable — it's a **skill**. If it's a paragraph you keep retyping into chat, it's a **prompt**. A prompt that earns reuse across two or more cycles and consistently outperforms free-form chat gets lifted to a skill.

Prompt files carry human-readable frontmatter — `name`, `purpose`, `model_tested`, `expected_inputs`, `known_failure_modes` — nothing parses it; it's for the next reader. The model stamp matters: prompts drift in effectiveness as models change, and the stamp lets the reader judge currency.

Skills need not all be homegrown: third-party skills can be vendored (e.g. via a skills package manager) alongside hand-written ones, tracked by a lock file. Pick what earns reuse; don't bulk-import.

## 7. Public / private split

Teams typically run two repos: the **public methodology** (this framework) and the **private toolkit** (cycle archives, filled scaffolds, org knowledge, agent prompts). The dividing rule: *methodology → public; substance → private.* If you find yourself writing the same document into both, it belongs in exactly one of them.

## 8. Consumption: how assets flow back into cycles

- **D1 Initialization:** the Implementer scans `knowledge/` for entries matching the cycle's domain and links applicable ones from the PRD's Technical Constraints.
- **During execution:** `prompts/` entries are pasted as needed; heavily used ones migrate into the project's `.cursorrules`/agent guardrails.
- **Skills** are not optional: once a skill exists for an operation (e.g. narrow-format), invoking the raw operation it replaces is a guardrail violation.

## 6. The reading protocol

Starting cycle N+1 of a project that has run before? **Read the most recent cycle folder end-to-end before opening an editor**, in this order:

1. **Overview `README.md`** — what shipped, how big, who ran it.
2. **`05-retro.md`** — lessons. The most valuable file; read even when skimming the rest.
3. **`03-decisions.md`** — decisions that may still bind.
4. **`02-prompts.md`** — prompts that worked; steal the ones that fit.
5. **`01-plan.md`** — the previous plan, as a reference shape.
6. **`04-validation.md`** — what the Validator caught; look hardest there this time.

The kickoff (`00-kickoff.md`) is historical context — useful if you're new to the project.

Discipline notes: `02-prompts.md` is the file most often skipped and most often regretted — capture prompts the minute they produce output worth keeping. `03-decisions.md` is for decisions that propagate ("we chose X over Y because…"), not naming trivia.

## 7. Hygiene

- The toolkit is versioned and reviewed like code — promotion is a PR, not a wiki edit.
- Every asset names its source cycle(s). An asset that can't cite its evidence is a candidate for deletion.
- A yearly (or every-Nth Technical Health Cycle) prune removes assets unused since promotion: long-term memory also needs forgetting.
