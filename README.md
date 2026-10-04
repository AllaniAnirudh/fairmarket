# FairMarket Protocol

An open protocol for fair digital commerce. Sellers list once at their direct price. Buyers pay that price plus one explicit, capped marketplace fee. Any app can be a storefront.

**This repository is a paper, not a product.** It exists to put the idea into the world in complete, referenceable form so others can criticize it, improve it, or build on it. Nothing here is for sale and nothing is promised beyond the idea itself.

Start with [PAPER.md](PAPER.md): the canonical statement of the idea. The detailed normative specification lives in [spec/](spec/00-overview.md).

## The problem

Marketplace platforms charge sellers 15 to 30 percent commission. Sellers cannot absorb it, so they inflate prices on the platform. Buyers pay more than the direct price for the exact same item. The platform also owns the demand, the seller's identity, and their reputation, so sellers cannot leave. The result is a private tax on every transaction, paid by buyers, blamed on sellers.

This is not specific to food delivery. It is the same on ride hailing, e-commerce, and services. The pattern is identical everywhere: the platform sits between buyer and seller and extracts rent from both sides.

## The idea

Separate the marketplace into a neutral protocol rail and competing apps, the way UPI separated payments from payment apps in India:

- **Sellers** publish their catalog once. It appears on every storefront app. They own their identity and reputation and can move freely.
- **Buyers** pay the seller's direct price plus one explicit marketplace fee, capped by the protocol. No hidden inflation.
- **Storefront apps** compete on experience, not on lock-in. Any developer can build one.
- **The protocol** enforces the fee cap, the payment split, the order lifecycle, and dispute handling. It is neutral infrastructure, not a business.

## Status

**A paper, not a product.** This repository holds the idea in complete, referenceable form: the canonical paper ([PAPER.md](PAPER.md)), the Phase 1 formal specification ([spec/](spec/00-overview.md)), and the project's governance documents. There is no implementation here and none is promised. If the idea has merit, the world will decide what to build with it.

## Repository layout

- `PAPER.md` — the canonical paper: problem, related work, design, economics, adversarial analysis, roadmap, references
- `spec/` — the Phase 1 formal specification (start at `spec/00-overview.md`)
- `rfcs/` — RFC template and future proposals (see `RFC_PROCESS.md`)
- `GOVERNANCE.md`, `CONTRIBUTING.md`, `CODE_OF_CONDUCT.md`, `SECURITY.md`, `VERSIONING.md`, `CHANGELOG.md` — how the project runs
- `LICENSE` — Apache License 2.0

## Contributing

This is early. The most useful contributions right now are criticism of the design: find the holes in the fee model, the dispute process, or the extension system and open an issue. Read [PAPER.md](PAPER.md) first, especially the adversarial analysis and open questions.

## License

Apache License 2.0. See [LICENSE](LICENSE).
