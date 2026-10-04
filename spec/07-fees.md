# 07 — Fees and Payment Split

## Principle

The buyer pays the seller's direct price plus explicit fees. Fees are always visible line items, never hidden in the price, never added after confirmation. The protocol caps what the marketplace can take and demands transparency for the rest.

## The two fees

Every order's `fee_breakdown` contains up to three line items:

1. **Item price.** The seller's direct price from the signed offer. Untouchable.
2. **Marketplace fee.** Covers discovery, ordering, payments, support, and dispute handling. Goes to the storefront.
3. **Fulfillment fee (when applicable).** Covers delivery, transport, or logistics. Goes to the fulfillment provider.

## Marketplace fee rules

- The marketplace fee is capped by protocol policy. Initial cap: **8 percent** of the item price.
- A storefront MAY charge less than the cap to compete. It MUST NOT charge more.
- There MUST be exactly one marketplace fee line item per order. Duplicate charges under different names ("service fee" plus "platform fee" plus "convenience fee") are a protocol violation.
- The fee MUST be shown to the buyer before confirmation and MUST NOT change after confirmation.

## Fulfillment fee rules

- The fulfillment fee is set by the fulfillment provider and MUST be shown as its own line item before confirmation.
- It MUST NOT increase after confirmation. For mobility, the fare estimate shown at confirmation is binding: it is the maximum the buyer can be charged.
- No drip pricing: all mandatory charges MUST be in the pre-confirmation breakdown. Optional extras (priority delivery, larger vehicle) MUST be opt-in and priced separately.
- Where the seller fulfills directly (in-store pickup, digital delivery), there is no fulfillment fee line item.

## Why two fees instead of one

A single flat fee cannot work across verticals: on a $20 food order the rider payout alone is about $3 (15%), so an 8 percent all-in cap could not fund delivery without hidden charges or bankruptcy. Separating the fees keeps the marketplace fee small and honest while letting fulfillment be priced at its real, visible cost.

## Payment split

- Settlement MUST be atomic: in one operation, the item price routes to the seller, the marketplace fee to the storefront, and the fulfillment fee to the fulfillment provider.
- No party SHALL be able to hold another party's funds hostage. If settlement cannot complete atomically, the order MUST NOT advance to `settled`.
- For high-value or made-to-order transactions, the buyer's payment MAY be held in escrow until fulfillment is confirmed, with release governed by the order state machine and the dispute process.

## Anti-circumvention

- No storefront SHALL require, incentivize, or reward sellers for maintaining higher protocol prices than direct prices.
- No storefront SHALL demand exclusivity or penalize sellers (in ranking, visibility, or terms) for listing on other storefronts.
- Fee policy changes follow the highest scrutiny track in `../RFC_PROCESS.md` and `../GOVERNANCE.md`. The cap moves slowly, publicly, or not at all.
