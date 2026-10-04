# 03 — What FairMarket Is

## In one paragraph

FairMarket is an open protocol for commerce. Sellers publish their catalog once at their direct price. Buyers discover offers on any compliant storefront app and pay the seller's price plus one explicit, protocol-capped marketplace fee, plus a separate transparent fulfillment fee where delivery or transport is involved. Identity, listings, and reputation belong to the participants and move with them between apps. The protocol defines the transaction lifecycle, the fee rules, the payment split, and dispute handling. It does not run a storefront, take a cut, or favor any participant.

## Actors

- **Buyer.** Discovers offers and places orders through a storefront app.
- **Seller.** Publishes offers and fulfills orders. Owns their catalog, identity, and reputation.
- **Storefront.** An app that presents offers and takes orders. Earns the marketplace fee, capped by the protocol. Competes on experience and fee level (at or below the cap).
- **Fulfillment provider (optional).** Handles delivery, transport, or logistics as a separate actor with its own transparent fee. May be the seller themselves, an independent provider, or a storefront's logistics arm operating under the same transparency rules.
- **Arbiter.** Resolves disputes that automated rules cannot. Arbiters are registered participants with reputation at stake.

## Layers

```
Layer 3   Applications        Buyer apps, seller apps, fulfillment provider apps
Layer 2   Vertical extensions food/v1, mobility/v1, retail/v1, services/v1
Layer 1   Core protocol       This spec: identity, offers, orders, fees, reputation, disputes
Layer 0   Governance          Spec stewardship, RFC process, fee policy (see ../GOVERNANCE.md)
```

The core (Layer 1) knows nothing about pizzas or rides. It defines the transaction lifecycle every vertical shares. Verticals add domain schemas as versioned extensions (Layer 2). Apps (Layer 3) compete on top.

## What the protocol guarantees

1. The price in an offer is the seller's price. No participant may inflate it.
2. The buyer sees every fee as an explicit line item before confirming. No hidden charges, no post-confirmation increases.
3. Payment splits atomically: seller, storefront, and fulfillment provider are paid in one settlement. No one holds another's money.
4. Identity and reputation are portable across apps.
5. Every order follows one auditable state machine, and disputes follow one defined process.

## What FairMarket is not

- Not a delivery company, a storefront, or a new Uber. It is the rail others build on.
- Not a cryptocurrency project. Settlement uses normal payment rails. The innovation is economic and architectural.
- Not a plan to reform incumbents. They will not adopt this. It competes with them.
- Not a charity. Storefronts, fulfillment providers, and arbiters earn transparent fees. The protocol itself takes nothing.
