# 09 — Disputes

## Principle

Trust is the binding constraint on adoption. Users stay where problems get resolved. Dispute handling is therefore core protocol infrastructure, not an app feature. (This is the structural gap most cited in the ONDC experience, and this spec does not repeat it.)

## Claim types

Standard across verticals. Extensions MAY add vertical-specific subtypes.

- `not_delivered` — the order never arrived or the service never happened
- `wrong_item` — materially different from the confirmed offer
- `damaged_or_defective` — arrived damaged, defective, or unusable
- `no_show` — a party failed to appear at the agreed time and place
- `quality_dispute` — the outcome does not meet the described standard

## Process

1. **Filing.** Either party opens a claim against the order, citing a claim type and attaching evidence (photos, messages, tracking data, timestamps). Filing moves the order to `disputed`. Frivolous or abusive filing is itself a reputation event.
2. **Automated rules.** Clear cases resolve without humans: tracking data showing non-delivery, timestamps proving a no-show, photo evidence matching defined criteria. The rule set is published and versioned.
3. **Arbitration.** Cases the rules cannot decide go to a registered arbiter. Arbiters are protocol participants with verification tier 1 or higher and their own reputation at stake. Either party MAY request arbitration; the arbiter's decision is binding.
4. **Resolution.** One of: release payment to the seller, partial refund, full refund, or redo at the seller's expense. The outcome is recorded on the order and affects the reputation of the party at fault.

## Rules

- A dispute MUST be filed within the window defined by the offer's terms, or a protocol default (initial proposal: 7 days after fulfillment).
- Evidence submitted by either party MUST be visible to the other party and to the arbiter.
- Arbiters MUST disclose conflicts of interest and MUST NOT arbitrate orders involving their own affiliated storefronts or accounts.
- While an order is `disputed`, settlement MUST NOT release funds except per the resolution.
- The dispute process, rule set, and arbiter accreditation criteria are set by governance and MUST be published. Secret rules are a protocol violation.

## Funding arbitration

Unresolved: who pays for human arbitration. Candidate models include a tiny per-order dispute insurance pool and loser-pays. This is listed as an open question in the architecture and will be settled by RFC before v1.0.
