# 10 — Vertical Extensions

## Principle

All commerce shares one transaction lifecycle. Vertical specifics are versioned extension packs on top of the core, not forks of it. The core never changes to accommodate one vertical.

## Extension format

Each extension is namespaced and versioned: `food/v1`, `mobility/v1`, `retail/v1`, `services/v1`. An extension defines:

1. **Item schema additions.** Extra fields on offers and orders for the vertical.
2. **Fulfillment events.** Vertical-specific events attached to the order's `in_progress` state.
3. **SLA and terms fields.** Structured service-level terms the vertical needs.
4. **Rating dimensions.** Vertical-specific dimensions added to the core rating schema.
5. **Claim subtypes.** Vertical-specific subtypes of the core claim types.

## Rules

- Extensions MUST declare the core protocol versions they are compatible with.
- The core and each extension are versioned independently (see `../VERSIONING.md`). A change to `food/v1` MUST NOT force a core version bump.
- New extensions are proposed through the RFC process (`../RFC_PROCESS.md`). Anyone MAY propose one.
- Extensions MUST NOT redefine core fields or alter the order state machine. They only add.
- If two extensions conflict on a shared concept, the core definition wins and the extensions MUST be revised.

## food/v1 (sketch)

The first extension to be specified in full. Draft fields:

- **Item additions:** menu structure (items, variants, modifiers, dietary flags), portion sizes.
- **Fulfillment events:** `accepted`, `preparing`, `picked_up`, `arriving`, `delivered`.
- **SLA fields:** prep time estimate, delivery time window, temperature requirements (hot/cold/frozen).
- **Rating dimensions:** food quality, packaging, delivery care, timeliness.
- **Claim subtypes:** `wrong_item.missing_item`, `wrong_item.wrong_variant`, `damaged_or_defective.cold_food`, `damaged_or_defective.spilled`.

## mobility/v1 (sketch)

- **Item additions:** pickup and dropoff coordinates, vehicle class, passenger count.
- **Fulfillment events:** `driver_assigned`, `driver_arriving`, `trip_started`, `trip_completed`.
- **SLA fields:** binding fare estimate (the estimate at confirmation is the maximum charge), ETA, wait time policy.
- **Rating dimensions:** driving safety, vehicle condition, route efficiency, courtesy.
- **Claim subtypes:** `no_show.driver_no_show`, `no_show.rider_no_show`, `quality_dispute.unsafe_driving`.

## retail/v1 (sketch)

- **Item additions:** SKU, inventory count, condition grading (new/used/refurbished), variants.
- **Fulfillment events:** `packed`, `shipped`, `in_transit`, `out_for_delivery`, `delivered`.
- **SLA fields:** shipping options with cost and time, returns policy as structured terms.
- **Rating dimensions:** item as described, shipping speed, packaging quality.
- **Claim subtypes:** `wrong_item.wrong_variant`, `damaged_or_defective.shipping_damage`.

## services/v1 (sketch)

- **Item additions:** scope of work as structured terms, time slot booking, quote flow (an order MAY begin as a non-binding quote request before becoming a binding order).
- **Fulfillment events:** `scheduled`, `professional_en_route`, `work_started`, `work_completed`, `client_accepted`.
- **SLA fields:** arrival window, milestone definitions for large jobs, milestone-based settlement.
- **Rating dimensions:** workmanship, punctuality, communication, cleanliness.
- **Claim subtypes:** `quality_dispute.incomplete_work`, `no_show.professional_no_show`.
