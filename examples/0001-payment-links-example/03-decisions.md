# Decision Log — 0001-payment-links-example

## ADR 1 — QR generation is best-effort, decoupled from link creation
- **Status:** Accepted
- **Decision:** Link creation must succeed independently; QR is an async sidecar that degrades to "no QR" on failure.
- **Rationale:** external QR API is failable; a payment link without a QR is degraded, a blocked link is broken.
- **Consequences:** pattern reusable for any augmented-data-on-critical-doc pair (thumbnails, search indexes).

## ADR 2 — Reuse billing-backend's provider SDK pattern (supersedes initial raw-REST lean)
- **Status:** Accepted (reversal of the D1 research-based direction)
- **Decision:** Copy the JWT + SDK integration proven in the sibling repo instead of the raw REST approach web research suggested.
- **Rationale:** proven in-org code against the same provider beats first-principles research.

## ADR 3 — Bulk-send descoped
- **Status:** Accepted (amendment 1, Material)
- **Decision:** Bulk send moves to a future cycle; hidden messaging-quota dependency would breach the 72-hour chunk rule.
