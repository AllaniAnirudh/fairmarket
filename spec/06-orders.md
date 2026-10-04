# 06 — Orders

## Principle

Every order, in every vertical, moves through one state machine. Transitions are signed by the responsible actor and recorded on the shared order log, so any party (and any arbiter) can audit what happened.

## Order structure

```
order {
  id,
  buyer_id, seller_id, storefront_id,
  fulfillment_provider_id,   // optional
  offer_snapshot,            // the signed offer as confirmed
  fee_breakdown,             // see 07-fees
  state,
  state_history,             // signed transitions with timestamps
  extension_data
}
```

The `offer_snapshot` freezes the offer exactly as the buyer confirmed it. Later offer changes MUST NOT affect an order already placed.

## State machine

```
created -> confirmed -> in_progress -> fulfilled -> settled
                   \-> cancelled
    disputed -> resolved -> settled
    disputed -> resolved -> refunded
```

- `created`: buyer has submitted the order. No commitment yet.
- `confirmed`: seller has accepted. Both sides are now committed under the order's terms.
- `in_progress`: fulfillment is underway. Verticals attach their fulfillment events here (picked up, driver arrived, shipped).
- `fulfilled`: the seller or fulfillment provider declares the order complete.
- `settled`: payment has been split and released per `07-fees`. Terminal state.
- `cancelled`: cancelled per the offer's cancellation terms before fulfillment completed.
- `disputed`: a claim has been opened (see `09-disputes`). From here the order can only move to `resolved`.
- `resolved`: the dispute outcome is recorded; the order then moves to `settled` or `refunded`.

## Rules

- Every state transition MUST be signed by the actor responsible for it (buyer confirms creation, seller confirms acceptance, fulfillment provider reports progress) and appended to `state_history`.
- A storefront MUST NOT advance, revert, or forge order states on behalf of another actor.
- Cancellation terms in the offer govern who bears what cost on cancellation. If the terms are silent, the party cancelling after `confirmed` bears the direct costs incurred so far; disputes about this go through `09-disputes`.
- Orders MUST remain queryable by all parties until settlement plus a retention period defined by governance (initial proposal: 2 years) for dispute and audit purposes.
