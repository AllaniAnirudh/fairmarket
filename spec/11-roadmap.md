# 11 — Roadmap: The Other Phases

This spec is Phase 1. What follows is what comes after, and what each phase must prove before the next begins.

## Phase 2 — Reference implementation

**Goal:** prove the spec is implementable and coherent by building it.

- Core protocol implemented in code, plus the `food/v1` extension in full.
- One minimal buyer app and one minimal seller app that transact with each other through the protocol.
- Conformance test vectors: a suite any independent implementation can run to prove compliance.
- Success criterion: two independent implementations (the reference plus one more) complete a food order end to end: offer, order, split payment, fulfillment events, rating, and a test dispute.

Language choice is still open. Go matches the founder's stack; TypeScript attracts more contributors. This will be decided by RFC.

## Phase 3 — Pilot: one vertical, one city

**Goal:** prove the economics with real sellers and buyers.

- Food delivery, one metro area. Independent restaurants feel the platform tax most sharply and are organized enough to move together.
- Recruit sellers on one promise: list at your true direct price, keep almost all of it.
- Success criteria: sellers listing at true direct prices; buyers paying less than on incumbent apps for the same order; dispute rate within manageable bounds; sellers renewing after the pilot period.
- Expect incumbent response: price undercutting, exclusive-contract pressure. The pilot needs sellers with enough margin pain to hold the line, and the protocol's anti-exclusivity rules must be enforced visibly from day one.

## Phase 4 — Expansion

**Goal:** prove the generic core by adding verticals without changing it.

- Add `mobility/v1` and run a second pilot. Ride hailing has the same economics but a different fulfillment model; it stress-tests the core's generality.
- Then `retail/v1` and `services/v1`. Open the app ecosystem: multiple buyer apps competing on fee and experience is the moment the model compounds.
- Success criterion: a vertical added with zero changes to the core spec. If the core has to change, the extension system failed and must be fixed first.

## Phase 5 — Protocol maturity

**Goal:** the rail outlives its founders.

- Stewardship transitions to an independent nonprofit foundation funded by grants and membership dues.
- Formal RFC process with elected stewards, third-party audits of fee enforcement, published transparency reports.
- The foundation's charter permanently encodes the one-explicit-fee rule and the fee cap's high-scrutiny change process, so no future steward can quietly become the next tax collector.

## What each phase gates

No phase begins until the previous one's success criteria are met and written up publicly. Skipping ahead (for example, adding verticals before the food pilot proves the economics) is how protocol projects die: they build generality nobody uses. The discipline is: design generic, prove narrow, expand only on evidence.
