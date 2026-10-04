# 08 — Reputation

## Principle

Reputation belongs to the participant, not the app. A seller's ratings follow them to every storefront. This is what makes leaving a bad app possible, which is what keeps every app honest.

## How it works

- Ratings are signed statements bound to the rater's and ratee's protocol identities.
- One rating per completed order, per side: the buyer rates the seller (and fulfillment provider, if any), and the seller rates the buyer.
- Ratings are submitted after `settled` (or after dispute resolution) and become part of the participant's portable reputation record.
- The protocol defines the rating schema: an overall score, structured dimensions per vertical (defined in extensions), and optional text. The schema is fixed so ratings are comparable across apps.

## Rules

- A storefront MUST submit ratings it collects to the participant's protocol reputation record. It MUST NOT withhold, alter, or selectively display ratings to misrepresent a participant.
- Apps MAY display reputation differently (averages, badges, filters) but MUST NOT fabricate scores or hide negative ratings they have collected.
- Only parties to a completed order MAY rate each other for that order. Ratings from anyone else MUST be rejected.
- **Sybil resistance.** Rating weight SHOULD account for the rater's verification tier and history. Governance defines the exact anti-gaming rules; at minimum, unverified identities MUST NOT be able to mass-rate.
- Dispute outcomes affect reputation: a resolved claim against a seller is recorded alongside ratings, with the outcome (not just the claim) shown.

## Fraud signals

Protocol-level fraud signals (chargeback rates, dispute rates, fake-review patterns, ban history) are computed across all apps and shared with every storefront. A bad actor removed from one app MUST NOT be able to start clean on another. The exact signals and thresholds are set by governance and published openly.
