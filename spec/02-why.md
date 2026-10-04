# 02 — Why an Open Protocol

## Why not reform the incumbents

Incumbents will not voluntarily cut take rates. Their valuation depends on them. Every attempt to negotiate, regulate, or shame platforms into lower fees has produced workarounds: re-layered buyer fees, "enhanced marketing" tiers that bypass caps, exclusive contracts that punish sellers for multi-homing. The incentive structure guarantees this. You cannot fix the tax by asking the tax collector to be generous.

## Why not just build a better app

A cheaper app is still a platform. It still owns discovery, identity, and reputation for its users. If it wins, it becomes the next tax collector; the history of marketplaces is a cycle of undercutting and extraction. The fix has to be structural: separate the marketplace into a neutral rail and competing apps, so no single company can own the chokepoint.

## The precedent: UPI and ONDC

India has already proven the pattern twice:

- **UPI** separated payments from payment apps. Merchants pay near zero, apps compete on experience, and no app can tax a transaction because none of them owns the rail.
- **ONDC**, built on the Beckn protocol, applied the same idea to commerce: an open network where buyer apps and seller apps interoperate. It reached 500 million cumulative transactions and proved the architecture works technically.

ONDC also teaches the hard lessons this spec internalizes: subsidies only rent demand (growth stalled when incentives were cut), and the missing piece users actually punish is trust infrastructure. ONDC's most-cited structural gap is the absence of centralized grievance redressal. That is why disputes and reputation are in FairMarket's core protocol, not left to apps.

## Why these design choices

- **One explicit, capped fee** instead of negotiated commissions: the cap is what makes seller prices honest. If the fee can grow without bound, prices inflate again.
- **Split marketplace and fulfillment fees** instead of one flat rate: research shows a flat 8 percent cannot fund delivery (a $20 order's rider payout alone is ~$3). Pretending otherwise would bankrupt the system or force hidden charges. Honest separation keeps both sides sustainable.
- **Portable identity and reputation** instead of per-app profiles: this is what breaks lock-in. A seller's ratings must follow them everywhere or the protocol has changed nothing.
- **Generic core plus vertical extensions** instead of one vertical's protocol: food, rides, retail, and services share one transaction lifecycle (discover, agree, fulfill, settle, review). Building four separate protocols would fragment the ecosystem before it starts.
- **Disputes in the core** instead of in the apps: trust is the binding constraint on adoption. Users stay where problems get resolved, not where fees are 2 percent lower.

## Why now

AI coding agents and cheap software have collapsed the cost of building storefront apps. The hard part was never the app; it was the rail. What is missing is a credible, neutral specification with a fee model sellers can believe in. That is what this document starts.
