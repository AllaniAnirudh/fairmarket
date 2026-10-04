# Changelog

All notable changes to the FairMarket protocol and this repository are documented here. Format follows Keep a Changelog; versioning follows [VERSIONING.md](VERSIONING.md).

## [Unreleased]

### Added

- Phase 1 formal spec in `spec/`: 00-overview (conformance language), 01-problem, 02-why (rationale, UPI/ONDC precedent), 03-what (actors, layers, non-goals), 04-identity (portable identity, verification tiers), 05-offers (signed offers, direct-price rule, no exclusivity), 06-orders (state machine, signed transitions), 07-fees (split marketplace/fulfillment fees, 8% cap, atomic split, anti-circumvention), 08-reputation (portable ratings, fraud signals), 09-disputes (claim types, arbitration), 10-extensions (system + food/mobility/retail/services sketches), 11-roadmap (phases 2-5 with success criteria)

### Changed

- Fee model revised per research: single flat fee replaced by split marketplace fee (capped) + fulfillment fee (transparent), since a flat 8% cannot fund delivery
- Governance: GOVERNANCE.md, RFC_PROCESS.md with template, CODE_OF_CONDUCT.md (Contributor Covenant 2.1), CONTRIBUTING.md, SECURITY.md
- Licensing: Apache License 2.0, DCO sign-off for contributions
- Versioning policy: SemVer with independent versioning of core and vertical extensions
