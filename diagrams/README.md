# FairMarket Diagrams

Mermaid diagrams that render natively on GitHub. They are also embedded in [PAPER.md](../PAPER.md) where they belong in the narrative.

## 1. Transaction and money flow

How an order moves through the system and how the money splits. This is the core of the idea.

```mermaid
sequenceDiagram
    participant Buyer
    participant Storefront
    participant Seller
    participant Fulfillment
    participant Rail as Protocol Rail

    Seller->>Rail: publish signed offer<br/>$20 direct price
    Rail-->>Storefront: syndicate offer
    Buyer->>Storefront: discover offer
    Storefront->>Buyer: $20.00 item<br/>+ $1.60 marketplace fee<br/>+ $3.50 fulfillment fee
    Buyer->>Storefront: confirm order
    Storefront->>Rail: order created (signed)
    Note over Rail: atomic payment split
    Rail->>Seller: $20.00 item price
    Rail->>Storefront: $1.60 marketplace fee (capped at 8%)
    Rail->>Fulfillment: $3.50 fulfillment fee (transparent)
    Seller->>Fulfillment: hand off order
    Fulfillment->>Buyer: deliver + tracking events
    Buyer->>Rail: confirm receipt + rate seller
```

## 2. Order lifecycle

The one state machine every vertical uses. Transitions are signed by the responsible actor.

```mermaid
stateDiagram-v2
    [*] --> created
    created --> confirmed : seller accepts
    created --> cancelled
    confirmed --> in_progress : fulfillment starts
    confirmed --> cancelled : per cancellation terms
    in_progress --> fulfilled : declared complete
    in_progress --> disputed : claim filed
    fulfilled --> settled : payment split released
    fulfilled --> disputed : claim filed
    disputed --> resolved : arbiter decision
    resolved --> settled
    resolved --> refunded
    settled --> [*]
    refunded --> [*]
    cancelled --> [*]
```

## 3. Layered architecture

```mermaid
flowchart TB
    subgraph L3["Layer 3 — Applications"]
        BA[Buyer Apps]
        SA[Seller Apps]
        FA[Fulfillment Apps]
    end
    subgraph L2["Layer 2 — Vertical Extensions"]
        E1[food/v1]
        E2[mobility/v1]
        E3[retail/v1]
        E4[services/v1]
    end
    subgraph L1["Layer 1 — Core Protocol"]
        C["Identity · Offers · Orders<br/>Fees · Reputation · Disputes"]
    end
    subgraph L0["Layer 0 — Governance"]
        G["RFC Process · Fee Policy · Stewards"]
    end
    BA & SA & FA --> L2
    L2 --> C
    C --> G
```
