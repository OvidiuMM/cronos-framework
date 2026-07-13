# Kickoff Notes — 0001-payment-links-example

**Date:** 2026-03-03 · **Attendees:** @dana (PM), @edgar (Implementer), @omar (Validator), merchant-support lead

## Project context
Support creates payment links manually (11 min avg, error-prone). One cycle to give merchants self-serve link creation with an SMS-ready public pay page.

## This cycle's scope (from PRD)
- "A merchant can create a payment link in one service call" (PRD §3.1)
- "The public pay page renders on mobile" (PRD §3.2)
- "A QR code accompanies each link when generation succeeds" (PRD §3.3)

## Hot spots flagged
- The provider webhook: signature scheme is under-documented — Validator to attack this on D5.
- QR vendor API has a 2% observed failure rate — must not block link creation.

## Validator assignment
@omar — available D4 PM + D5 AM.

## Action items
- [x] PM: PRD §3.3 wording ("best-effort") confirmed with stakeholder.
- [x] Implementer: draft `01-plan.md` D1.
