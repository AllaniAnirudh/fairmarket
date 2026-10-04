# FairMarket Protocol: Architecture (v0.1 draft)

## 1. Problem statement

On every major marketplace the economics work the same way:

1. The platform charges the seller a commission of 15 to 30 percent.
2. The seller raises prices on the platform to cover it. The platform price is higher than the direct price for the identical item or service.
3. The buyer pays the difference. The seller takes the blame.
4. The platform owns customer demand, seller identity, and reputation history, so neither side can leave without starting over.

This holds for food delivery (Uber Eats, DoorDash), ride hailing (Uber, Lyft), e-commerce (Amazon), and services. The vertical changes; the extraction does not.

Price parity clauses and regulation have tried to fix the symptoms. They do not fix the structure: whoever controls discovery and identity can tax every transaction.

## 2. Vision

A neutral, open protocol for commerce on which anyone can build a storefront. The protocol guarantees three things:

- **Sellers list at their direct price, everywhere, once.** One catalog, published to the protocol, visible on every compliant storefront app.
- **Buyers see one explicit fee.** The seller's price plus a single platform fee line item, capped by the protocol. Nothing hidden, nothing inflated.
- **No lock-in.** Identity, listings, and reputation belong to the participants, not to any app. A seller or buyer can switch apps without losing anything.

The model is UPI for payments and ONDC/Beckn for commerce in India: a shared rail, competing apps. FairMarket generalizes that pattern to every vertical.

## 3. Design principles

1. **Participants own their data.** Identity, catalogs, order history, and reputation are portable. Apps are interchangeable views.
2. **Fees are explicit and capped.** The protocol sets a maximum platform fee. Apps may charge less to compete, never more. The fee appears as its own line item on every order.
3. **The rail is neutral.** The protocol does not run a storefront, take a cut, or favor any participant. Anyone can implement it.
4. **Generic core, vertical extensions.** All commerce shares one transaction lifecycle. Vertical specifics (menus, ETAs, SKUs) are versioned extensions, not forks.
5. **Trust is shared infrastructure.** Ratings, verification, and dispute resolution live on the protocol so new apps and sellers do not start from zero.
6. **Build narrow, design generic.** The protocol is specified for everything; the first implementation proves it on one vertical in one place.

## 4. Layered architecture

```
Layer 3   Applications        Buyer apps, seller apps, fulfillment providers
Layer 2   Vertical extensions food/v1, mobility/v1, retail/v1, services/v1
Layer 1   Core protocol       Identity, offers, orders, payments, disputes, reputation
Layer 0   Governance          Spec stewardship, RFC process, fee cap policy
```

**Layer 1, the core protocol**, is the heart of the system. It defines the transaction lifecycle every vertical shares: discover, agree, fulfill, settle, review. It knows nothing about pizzas or rides.

**Layer 2, vertical extensions**, add domain schemas on top of the core. Each extension is namespaced and versioned. An extension defines the item schema additions, fulfillment events, and service-level fields its vertical needs.

**Layer 3, applications**, are what users touch. A buyer app, a seller app, or a fulfillment provider app all speak the core protocol plus the extensions they support. Competition happens here, on experience and price.

## 5. Core protocol (draft)

### 5.1 Actors

- **Buyer.** Purchases goods or services.
- **Seller.** Lists offers and fulfills orders.
- **Storefront.** An app that presents offers and takes orders. Earns the platform fee, capped by the protocol.
- **Fulfillment provider.** Optional. Handles delivery, transport, or logistics as a separate actor with its own transparent fee.
- **Arbiter.** Resolves disputes. Can be automated rules, a human service, or both.

### 5.2 Identity

Every participant holds a portable, cryptographic identity. Verification is tiered: self-asserted, document-verified, and business-verified. A seller verified once is verified on every app. Identity theft or impersonation is handled at this layer, not per app.

### 5.3 Offers

An offer is the atomic unit of commerce:

```
offer {
  id, seller_id,
  title, description,
  price, currency,
  terms (cancellation, SLA),
  extension_data (vertical-specific),
  signature (seller)
}
```

The price in an offer is the seller's direct price. The protocol forbids the storefront from modifying it. Offers are signed by the seller so any app displaying them can prove authenticity.

### 5.4 Order lifecycle

Every order moves through one state machine, regardless of vertical:

```
created -> confirmed -> in_progress -> fulfilled -> settled
                  \-> cancelled
   disputed -> (resolved -> settled | refunded)
```

Transitions are signed by the responsible actor and recorded on the shared order log. Verticals add their own fulfillment events (order picked up, driver arrived) as extension events attached to `in_progress`.

### 5.5 Fee model and payment split

This is the economic core of the protocol. Research into marketplace unit economics shows a single flat fee cannot work: on a $20 food order the rider payout alone is about $3 (15%), so an 8% all-in cap cannot fund delivery. The protocol therefore separates the two kinds of cost explicitly instead of pretending one fee covers everything.

- Each order carries an explicit `fee_breakdown` with separate line items: the seller's price, the **marketplace fee**, and where applicable the **fulfillment fee**. Every line item is visible to the buyer before confirmation. Nothing may be folded into the item price.
- The **marketplace fee** covers discovery, ordering, payments, support, and dispute handling. It is capped by protocol policy (initial proposal: 8 percent). A storefront may charge less to compete. It may never charge more.
- The **fulfillment fee** covers delivery, transport, or logistics. It is set by the fulfillment provider, must be shown as its own line item, and is subject to transparency rules (no drip pricing, no post-confirmation increases) rather than a fixed cap, because real fulfillment costs differ by vertical and geography. For mobility, the fare estimate shown at confirmation is binding: the maximum charged.
- The protocol **forbids fee stacking tricks**: no more than these line items, no duplicate charges under different names, no seller exclusivity clauses that punish multi-homing. One explicit marketplace fee is the rule; violations are a governance matter.
- Payment settles atomically: the seller's amount routes to the seller, the marketplace fee to the storefront, the fulfillment fee to the fulfillment provider. No party can hold another's money hostage.
- Because the marketplace fee is small, explicit, and capped, sellers have no reason to inflate the base price. The direct price and the protocol price are the same by construction, which is the entire point of the system.

### 5.6 Reputation

Ratings are signed statements bound to the participant's identity, not to the app where the transaction happened. A restaurant's 4.8 stars follow it to every storefront. The protocol defines the rating schema and anti-gaming rules (one rating per completed order, both sides rate, Sybil resistance through verified identity). Apps may display reputation differently but cannot alter or withhold it.

### 5.7 Disputes

Standard claim types across verticals: not delivered, wrong item, damaged or defective, no-show, quality dispute. The flow:

1. Either party opens a claim with evidence attached to the order record.
2. Automated rules resolve the clear cases (for example, fulfillment tracking shows non-delivery).
3. Unclear cases go to an arbiter. Arbiters are registered protocol participants with their own reputation at stake.
4. Resolution is one of: release payment, partial refund, full refund, or seller redo. The outcome is recorded and affects reputation.

## 6. Vertical extensions (draft sketches)

Each extension is a namespaced, versioned schema pack. Version 1 of each is sketched here; details belong in `spec/`.

**food/v1.** Menu structure with items, variants, and modifiers. Prep time estimates. Fulfillment events: accepted, preparing, picked up, arriving, delivered. Perishability and temperature requirements as optional fields.

**mobility/v1.** Pickup and dropoff coordinates. Vehicle class. Live location stream during `in_progress`. Fare estimate binding rules: the estimate shown at `confirmed` is the maximum charged.

**retail/v1.** SKU and inventory counts. Shipping options with cost and time. Returns policy as structured terms. Condition grading for used goods.

**services/v1.** Time slot booking. Quote flow: the order can start as a quote request before becoming a binding order. Scope of work as structured terms. Milestone-based settlement for large jobs.

New verticals follow the same pattern: define the item additions, the fulfillment events, and the SLA fields. Nothing in the core changes.

## 7. Trust, safety, and fraud

- **Verification tiers** from section 5.2 gate what a seller can do. High-value categories require business verification.
- **Escrow** is available for high-value or made-to-order transactions: buyer funds are held until fulfillment is confirmed.
- **Fraud signals** (chargeback rates, dispute rates, fake review patterns) are computed at the protocol level and shared with all apps, so a bad actor banned on one storefront cannot start clean on another.
- **Content and safety policy** for listings is set by governance, enforced by apps, and appealable through the dispute process.

## 8. Governance

The protocol needs a steward that cannot become the next rent extractor. Options, in order of preference:

1. **Independent nonprofit foundation**, funded by grants and membership dues, with a public RFC process. (The UPI/ONDC model.)
2. **Seller cooperative**, where the merchants who depend on the rail govern it.
3. **Venture-backed steward** with the fee cap and neutrality written into a binding charter. Weakest option; charters get rewritten.

The RFC process governs: core protocol changes, new vertical extensions, the fee cap value, and arbiter accreditation. All decisions and rationales are public.

## 9. Rollout plan

**Phase 0: Spec and reference.** Finalize the core protocol spec and build a reference implementation: core plus the food extension, one buyer app, one seller app. Open source everything.

**Phase 1: One vertical, one city.** Pilot with independent restaurants in one metro area. Restaurants feel the platform tax most sharply and are organized enough to move together. Success metric: sellers listing at true direct prices and buyers paying less than on incumbent apps for the same order.

**Phase 2: Mobility.** Add the mobility extension and run a second pilot. Ride hailing has the same economics and a different fulfillment model, which stress-tests the generic core.

**Phase 3: Retail and services.** Add extensions, open the app ecosystem. Multiple buyer apps competing on fee and experience is the moment the model compounds.

**Phase 4: Protocol maturity.** Independent foundation, formal RFC process, third-party audits of the fee enforcement.

## 10. Open questions

These are unresolved and need answers before the spec is final:

1. **Fee cap value.** 8 percent is a starting proposal for the marketplace fee; fulfillment is priced separately and transparently (see 5.5). Too high and sellers still inflate; too low and no one builds storefront apps. It may need to differ by vertical.
2. **Who pays for arbitration?** Options include a tiny per-order dispute insurance pool or loser-pays. Undecided.
3. **Fulfillment interface.** The protocol coordinates fulfillment but does not own fleets. The interface for independent delivery and logistics providers needs design.
4. **Funding the rail.** Reference implementation and early operations need funding before the ecosystem is self-sustaining.
5. **Regulatory posture.** Money transmission, food safety liability, and transport regulation differ by jurisdiction. The protocol must stay on the right side of being infrastructure, not the merchant of record.
6. **Incumbent response.** Expect price undercutting and exclusive contracts during the pilot phase. The pilot needs sellers with enough margin pain to hold the line.

## 11. What this is not

- Not a new delivery company or a new Uber. It is the rail others build on.
- Not a cryptocurrency project. Settlement uses normal payment rails; the innovation is economic and architectural, not monetary.
- Not a plan to reform incumbents. They will not adopt this. It competes with them.
