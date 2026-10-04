# Changelog

All notable changes to the FairMarket protocol and this repository are documented here. Format follows Keep a Changelog; versioning follows [VERSIONING.md](VERSIONING.md).

## [Unreleased]

### Added

- PAPER.md: the canonical reference paper (abstract, problem with measured evidence, related work incl. UPI/ONDC/OpenBazaar/co-ops, design principles, system overview, condensed normative core, worked $20-order economic comparison, trust model, extensions, governance, adversarial analysis, phased roadmap, open questions, references, glossary, citation block). ARCHITECTURE.md folded into it and removed.
- Repository reframed explicitly as paper-not-product: the idea exists to be referenced, criticized, and built on; nothing is promised beyond the idea.
- `diagrams/`: Mermaid flow diagrams (transaction/money flow, order lifecycle state machine, layered architecture), embedded in PAPER.md and rendered natively on GitHub.

### Changed

- Fee model revised per research: single flat fee replaced by split marketplace fee (capped) + fulfillment fee (transparent), since a flat 8% cannot fund delivery
- Governance: GOVERNANCE.md, RFC_PROCESS.md with template, CODE_OF_CONDUCT.md (Contributor Covenant 2.1), CONTRIBUTING.md, SECURITY.md
- Licensing: Apache License 2.0, DCO sign-off for contributions
- Versioning policy: SemVer with independent versioning of core and vertical extensions
