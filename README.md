# FairMarket Protocol

An open protocol for fair digital commerce. Sellers list once at their direct price. Buyers pay that price plus one explicit, capped platform fee. Any app can be a storefront.

## The problem

Marketplace platforms charge sellers 15 to 30 percent commission. Sellers cannot absorb it, so they inflate prices on the platform. Buyers pay more than the direct price for the exact same item. The platform also owns the demand, the seller's identity, and their reputation, so sellers cannot leave. The result is a private tax on every transaction, paid by buyers, blamed on sellers.

This is not specific to food delivery. It is the same on ride hailing, e-commerce, and services. The pattern is identical everywhere: the platform sits between buyer and seller and extracts rent from both sides.

## The idea

Separate the marketplace into a neutral protocol rail and competing apps, the way UPI separated payments from payment apps in India:

- **Sellers** publish their catalog once. It appears on every storefront app. They own their identity and reputation and can move freely.
- **Buyers** pay the seller's direct price plus one explicit platform fee, capped by the protocol. No hidden inflation.
- **Storefront apps** compete on experience, not on lock-in. Any developer can build one.
- **The protocol** enforces the fee cap, the payment split, the order lifecycle, and dispute handling. It is neutral infrastructure, not a business.

## Status

Spec draft v0.1. The `spec/` directory now holds the full Phase 1 formal specification: the problem, the rationale, the system overview, and the normative core (identity, offers, orders, fees, reputation, disputes), plus the extension system and the roadmap for the phases after. See [spec/00-overview.md](spec/00-overview.md) to start reading. Reference implementation comes next.

## Repository layout

- `ARCHITECTURE.md` — the full design: principles, layered architecture, core protocol, extension system, fee model, trust and disputes, governance, rollout plan
- `spec/` — the Phase 1 formal specification (start at `spec/00-overview.md`)
- `rfcs/` — RFC template and future proposals (see `RFC_PROCESS.md`)
- `GOVERNANCE.md`, `CONTRIBUTING.md`, `CODE_OF_CONDUCT.md`, `SECURITY.md`, `VERSIONING.md`, `CHANGELOG.md` — how the project runs
- `LICENSE` — Apache License 2.0

## Contributing

This is early. The most useful contributions right now are criticism of the design: find the holes in the fee model, the dispute process, or the extension system and open an issue. Read [ARCHITECTURE.md](ARCHITECTURE.md) first, especially the open questions section.

## License

Apache License 2.0. See [LICENSE](LICENSE).
