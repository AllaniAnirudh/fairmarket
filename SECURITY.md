# Security Policy

## Scope

FairMarket is a protocol specification. Security here covers two distinct layers:

1. **Spec-level vulnerabilities.** Flaws in the protocol design itself: fee enforcement bypasses, identity spoofing, reputation gaming, dispute process exploits, payment split failures. These are the most important reports this project can receive.
2. **Implementation vulnerabilities.** Once reference implementations exist, bugs in that code are in scope too. Each implementation should carry its own security notes; this policy covers the reference implementation maintained here.

Out of scope: vulnerabilities in third-party storefront apps built on the protocol. Report those to the app operators.

## Reporting a vulnerability

Email allanianirudh05@gmail.com with a description of the issue and steps to reproduce it. You will get a reply within 7 days. Do not open a public issue for a suspected vulnerability.

If the issue is confirmed, we will coordinate a fix and a disclosure timeline with you before anything is published. Spec-level fixes may require an RFC and a spec version bump; we will handle that transparently.

## Supported versions

| Version | Supported          |
| ------- | ------------------ |
| spec v0.x (draft) | Yes            |

While the spec is in draft (v0.x), breaking security fixes may change the spec without a deprecation period. After v1.0, security fixes follow the versioning policy in [VERSIONING.md](VERSIONING.md).
