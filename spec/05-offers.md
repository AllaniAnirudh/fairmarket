# 05 — Offers

## Principle

An offer is a seller's public, signed promise: this item or service, at this price, under these terms. The price in an offer is the seller's direct price. It is the same price the seller charges anywhere else.

## Offer structure

```
offer {
  id,                 // unique, seller-scoped
  seller_id,          // protocol identity
  title,
  description,
  price,              // the seller's direct price
  currency,           // ISO 4217
  terms,              // cancellation policy, SLA, structured terms
  extension_data,     // vertical-specific fields (see 10-extensions)
  valid_from, valid_until,
  signature           // seller's signature over the above
}
```

## Rules

- The `price` field MUST equal the seller's direct price: the price the seller charges for the same item or service outside the protocol. A seller MUST NOT maintain a higher protocol price to offset fees. (The fee model in `07-fees.md` is designed so there is no economic reason to do so.)
- A storefront MUST display the offer price exactly as signed. It MUST NOT modify, round, or re-present the price. Any storefront surcharge MUST appear as a separate fee line item, never folded into the price.
- Offers MUST be signed by the seller's identity key. A storefront MUST verify the signature before displaying an offer and MUST NOT display offers with invalid signatures.
- A seller MAY publish the same offer to any number of storefronts. No storefront SHALL demand exclusivity as a condition of listing. Exclusivity clauses are a protocol violation.
- A seller MAY update or withdraw an offer at any time before it is confirmed in an order. Updates are new signed versions; the old version MUST NOT be displayable after withdrawal.
- Offers MUST carry a `valid_until` timestamp. A storefront MUST NOT accept orders against expired offers.
