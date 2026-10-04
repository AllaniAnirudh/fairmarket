# 04 — Identity

## Principle

Identity belongs to the participant, not to any app. A seller verified once is verified on every compliant storefront. A buyer's order history and a seller's reputation move with them.

## Identity format

- Every participant holds a cryptographic identity: a public/private keypair. The public key (or its fingerprint) is the participant's protocol-level identifier.
- Participants MAY attach human-readable profiles (name, avatar, contact) to their identity. Profile data is signed by the identity key.
- Storefront apps MUST NOT require participants to create a separate, non-portable account as a condition of transacting. Apps MAY offer enhanced profiles and features, but the protocol identity MUST remain sufficient to buy and sell.

## Verification tiers

Verification is tiered. Higher tiers unlock higher-trust categories:

- **Tier 0 — self-asserted.** The participant controls the keypair. Sufficient for low-value, in-person, or escrowed transactions.
- **Tier 1 — document-verified.** A government ID or equivalent has been checked by an accredited verifier. Required for sellers in most categories and for fulfillment providers.
- **Tier 2 — business-verified.** Business registration, tax identity, or equivalent checked by an accredited verifier. Required for high-value categories, and RECOMMENDED for all sellers handling other people's money or food.

Verification attestations are signed statements bound to the identity key. A verifier MUST be an accredited protocol participant, and verifiers themselves carry reputation that is slashed for false attestations.

## Rules

- No actor SHALL impersonate another identity. Storefronts MUST display the verification tier of sellers alongside offers.
- Identity keys MAY be rotated. Rotation MUST be signed by the old key, and the rotation record MUST be published so counterparties can follow the chain.
- A compromised key MUST be revocable by the holder through a signed revocation. Orders in flight at revocation time are settled under the dispute process.
