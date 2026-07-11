# Daily Pulse

> **Cronos Framework — async end-of-day update. Not a standup.**
> Posted by the Implementer at the end of every cycle day (D1–D5).
> No scheduled time, no attendance, no discussion required. ~2 minutes to write.
> Post to the team channel, or commit to the cycle folder as `daily/YYYY-MM-DD.md`.

---

## Template

```
Pulse — <cycle-id> — D<n> (YYYY-MM-DD)

Landed:   <what actually reached a working state today — plan row / commit, not intentions>
Next:     <the single next step>
Friction: <anything looping, ambiguous, or smelling like a Reset Trigger — or "none">
```

## Example (uneventful day — this is a complete, valid pulse)

```
Pulse — 0010-invoice-sync — D3 (2026-07-15)

Landed:   Row 6 green (webhook signature verification, commit a1b2c3d)
Next:     Row 7 — retry queue
Friction: none
```

## Example (early-warning day)

```
Pulse — 0010-invoice-sync — D3 (2026-07-15)

Landed:   Nothing merged; row 6 test double keeps failing on the emulator
Next:     Reproduce outside the emulator to isolate
Friction: Agent proposed the same emulator-config fix twice — watching for Circular Hallucination
```

---

## Rules

1. **Three lines, hard.** If the pulse takes more than ~5 minutes to write, it's being over-written.
2. **"Landed" means working state**, not effort. "Worked on X" is not a landed item; "X passes its tests" is. An honest "Landed: nothing" is a valid and useful entry.
3. **"Friction" is the early-warning channel.** Name anything that smells like a Reset Trigger *before* it crosses the mandatory threshold (4h loop / 3× repeated proposal).
4. **PM scan routine:** the PM reads pulses each morning. The same Friction line in **two consecutive pulses** is a soft trigger — check in with the Implementer, don't wait for the hard trigger.
5. **No replies required.** The pulse is a broadcast, not a thread. If discussion is needed, that's a Path Sync topic or an Emergency Sync, per the normal rules.
6. **`Next` doubles as the PRD's current-task pointer.** The pulse is the daily record; the WBS status column stays a pointer. (Teams whose planning tooling has a dedicated next-step field can point it at the latest pulse.)
