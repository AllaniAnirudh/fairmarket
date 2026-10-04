# FairMarket Versioning Policy

The protocol follows Semantic Versioning (SemVer): `major.minor.patch`.

## What the numbers mean for a spec

- **Major.** Breaking changes: removed or renamed fields, changed state machine transitions, changed fee rules, anything that makes an existing compliant implementation non-compliant.
- **Minor.** Backward-compatible additions: new optional fields, new vertical extensions, new fulfillment events, new claim types.
- **Patch.** Clarifications only: wording fixes, new examples, corrected diagrams. A patch never changes what implementations must do.

## Independent versioning

The core protocol and each vertical extension are versioned independently. A change to `food/v1` does not bump the core, and a core major bump does not force every extension to a new major. Each extension declares the core versions it is compatible with.

This rule exists because of a known failure mode (seen in the Beckn protocol's v1.x era): versioning everything as one monolith means a small change in one vertical forces a whole-spec release, which fractures implementations.

## Pre-1.0

While the spec is at v0.x, breaking changes may land in minor releases. The goal is to reach v1.0 of the core with the fee model, order lifecycle, and extension system proven by at least one working implementation.

## Releases

Spec versions are published as GitHub Releases with rendered artifacts. See [CHANGELOG.md](CHANGELOG.md).
