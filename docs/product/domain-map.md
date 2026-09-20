# Domain Map

> Status: approved v1.

## Shared Foundations

These concepts cross domain boundaries. No single domain owns them.

- Person
- Organization
- Identity / Account
- Role & Relationship
- Location
- Activity
- Source & Provenance
- Temporal Validity
- Semantic Association
- Tags & Custom Fields
- Channel
- Entitlement
- Watch

## Platform Domains

**1. Identity & Organizations**

Owns Person, Organization, Identity / Account, Role & Relationship,
organizational membership, teams, permissions, and the relationships connecting
people and organizations. These are shared foundational concepts used across the
platform, but Identity & Organizations owns their meaning and lifecycle.

**2. Knowledge & Evidence**

Owns claims, evidence, observations, signals, inference, verification,
source-awareness, perspective-awareness, corrections, invalidations, and
conflicting viewpoints.

**3. Participation & Contribution**

Owns contributions, contributor attribution, rights and usage permissions,
contribution review, correction, verification, requests, and contribution
lifecycle.

**4. Rewards & Earnings**

Owns cash earning entitlement, reward currencies, credits, wallets and ledgers,
gifting, transfers, redemption, reward purchase, conversion, adjustments and
reversals, and earning policies. Finance owns actual cash movement, settlement,
and accounting.

**5. Customer & Personalization**

Owns participant profiles, declared, observed, inferred, and contextual signals,
interests, intents, Audiences, Candidates, Recommendations, Feedback, and
participant-facing personalization logic.

**6. Content & Learning**

Owns reusable educational and editorial content, assets, learning experiences,
content briefs, versions, content health, and knowledge grounding.

**7. Community & Social**

Owns owned-community interactions plus external social presence, publishing,
conversations, messages, follows, reactions, moderation, social listening, and
social signals.

**8. Marketing**

Owns marketing opportunities, objectives, hypotheses, campaigns, journeys,
communications, offers, channel orchestration, and campaign learning. It
consumes Audiences but does not own Audience definitions.

**9. Commerce**

Owns products, variants, catalogs, categories, collections, bundles, prices,
discounts, promotions, carts, orders, inventory context, and returns, refunds,
and exchanges.

**10. Services & Booking**

Owns providers, services, service offerings, availability, resources, bookings,
participants, cancellations and rescheduling, and service outcomes.

**11. Finance**

Owns financial transactions, payments, receivables, payables, payouts,
settlements, costs, revenue, budgets, reconciliation, multi-currency financial
handling, cost attribution, and margin definitions.

**12. Analytics & Experimentation**

Owns events, metrics, dimensions, measurements, outcomes, attribution, cohorts,
funnels, experiments, assignments, results, and anomaly detection.

**13. Workflow & Automation**

Owns tasks, assignments, workflows, triggers, actions, approvals, policies,
business rules, review queues, warnings and alerts, enforcement cases, findings,
decisions, schedules, escalation, and audit-worthy workflow execution.

**14. AI Runtime**

Owns model-agnostic AI capabilities, capability contracts, routing, prompts and
instructions, context builders, tools, structured outputs, the model and
provider registry, evals, fallback, latency and cost controls, and production AI
execution.

**15. Conditions & Environment**

Owns physical measurements, observations, forecasts, current state, and
environmental time series. Knowledge & Evidence interprets what those conditions
mean.

**16. Rules, Access & Compliance**

Owns regulations, restrictions, inspections, permits, fees, closures, access
requirements, Effective Period, Validity, verification freshness, and
applicability.

**17. Subscriptions & Memberships**

Owns plans, subscriptions, billing cycles, entitlements, allowances, usage,
trials, renewals, upgrades and downgrades, pauses, past-due states, suspensions,
reinstatement, membership policies, policy versions, and acceptance.

**18. Observability & Audit**

Owns operational telemetry, traces, performance, audit records, AI traces,
correlation IDs, and privacy-aware telemetry. It does not replace business
state.

**19. Market & Ecosystem Intelligence**

Owns external market observations, competitor activity, market events and
signals, trends, conversation clusters, monitoring, and research briefs.

## First Domain Pack: Fishing

Fishing is the first domain pack. Its concepts include:

- Species
- Population / Species Presence
- Life Stage
- Stocking Schedule / Stocking Event
- Migration Pattern / Run
- Forage relationships
- Fishing Method
- Technique
- Fishing System
- Setup
- Rig
- Presentation
- Fishing parameters
- Equipment / Gear
- Equipment Category / Specification / Instance / Capability
- My Gear
- Craft
- Fishing Plan
- Fishing Trip
- Trip Segment (optional)
- Fishing Outcome
- Catch Record
- Fishing Report
- Fishing-relevant Location classifications and fishing areas and features

### Fishing Boundary Decisions

- Water is not a platform-core entity. Use Location.
- Angler is not a platform-core entity. Use Participant, with angler as
  fishing-domain language.
- Fishing System is a living, evidence-backed domain object. A Commerce Bundle
  is an optional commercial representation of it.
- Purchase history does not prove ownership, availability, condition, or
  sufficient quantity in My Gear.
- Expert and guide perspectives can legitimately conflict. They stay
  source-aware rather than forced into one canonical answer.
- Plans represent intent. Trips represent actual activity. Outcomes represent
  what happened. Reports represent what someone says about what happened.

## Domain Boundary Principles

- Domains are logical business boundaries, not microservices.
- The intended implementation direction is a modular monolith first.
- Shared foundations may be used across domains while ownership remains
  explicit.
- Domain packs extend the platform core rather than redefining it.
