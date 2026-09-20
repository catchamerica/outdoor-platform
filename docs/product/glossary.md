# Glossary

> Status: approved v1.

Canonical vocabulary for product, domain, UX, and architecture documents. Use
these terms as defined here. This is not a database schema and carries no
implementation detail.

**Activity**

An outdoor activity such as Fishing. Future domain packs may introduce others.

**AI Capability**

A named product or runtime AI function that defines what the platform wants AI
to accomplish, including its input and output contract and any grounding, tool,
or structured-output expectations. Business-domain code requests a capability
rather than a specific model or provider.

**AI Runtime**

The platform abstraction through which all product and runtime AI execution
occurs. It owns model and provider abstraction, capability execution, routing,
tool adapters, structured-output validation, fallback, retries where
appropriate, observability, and related execution concerns without replacing
domain ownership.

**Asset**

A reusable resource used or referenced by the platform, including files, links
and URLs, external media, documents, or other external resources.

**Audience**

A reusable definition of which People qualify for a particular experience,
communication, analysis, or action. Marketing consumes Audiences but does not
own their definition.

**Bundle**

A Commerce object grouping items for sale. A Bundle may represent part or all of
a Fishing System at a point in time, but a Fishing System and a Bundle are not
the same thing.

**Campaign Preflight Audit**

An optional AI-assisted review performed before campaign delivery. It evaluates
an approved campaign against relevant business context, knowledge, products,
audience, finance, brand, technical configuration, and other approved checks,
then returns findings for human review. It does not silently modify or approve
the campaign.

**Catch America**

The first organization and operator proving the platform in the fishing domain.

**Catch Therapy**

Catch America's branded expert-help experience that lets a participant request
or schedule direct help from an appropriate Expert or Guide.

**CatchCash**

Catch America's reward currency. It is one configured implementation within the
platform's Rewards & Earnings domain.

**Channel**

A delivery or interaction surface through which the platform communicates or
publishes, such as website, app, email, SMS, push, Instagram, Facebook, YouTube,
or TikTok.

**Claim**

A proposition that can be supported, contradicted, corrected, invalidated, or
superseded by evidence.

**Collaborator**

Someone working with an organization on content, promotion, research, product
testing, or another project without necessarily being an employee or an Expert.

**Commerce**

The platform domain responsible for commercial behavior, including products,
variants, catalogs, categories, collections, bundles, pricing, discounts,
promotions, carts, orders, inventory context, returns, refunds, and exchanges.
This list is not exhaustive.

**Content Item**

Reusable or publishable material such as an article, guide, lesson, video,
marketing creative, or social content.

**Context Builder**

The component or procedure that assembles only the platform context required for
a specific AI Capability or interaction, subject to permissions, privacy,
organization boundaries, provenance requirements, and data minimization.

**Contributor**

A Person or Organization that supplies content, observations, research,
verification, feedback, or other useful contributions.

**Development Skill**

A version-controlled reusable procedure used by AI development agents to build,
review, or modify the platform consistently with approved project rules and
architecture.

**Domain Pack**

Domain-specific concepts layered onto the platform core. Fishing is the first
domain pack.

**Effective Period**

The time period during which a rule, price, policy, or other time-bound item is
intended to apply.

**Expert**

A contextual role held by a Person with recognized expertise.

**Field Intelligence**

Fresh real-world information from experts, participants, conditions, reports,
catches, and other field sources that helps explain what is happening outdoors
now or recently.

**Fishing Mode**

The on-water participant experience entered while actively fishing. It
aggregates relevant information around the current participant, Location, Trip,
target, conditions, experts, knowledge, plan, and outcomes. It contains no
ecommerce, promotions, campaigns, or selling.

**Fishing System**

A living, evidence-backed fishing-domain approach that can combine target,
method, technique, setup, rig, presentation, operating parameters, knowledge,
expert perspective, and equipment requirements.

**Guide**

A fishing-domain and provider role. A guide may be a Person, while a guide
service may be an Organization containing multiple guides.

**Inference**

A conclusion derived from other information rather than directly observed.

**Location**

A generic real-world place or area. Fishing-specific classifications such as
lake, river, stream, sea, or ocean do not replace the core Location concept.

**Max**

Catch America's AI fishing assistant. Max uses platform knowledge, context,
tools, and approved AI procedures. Max is not itself the platform's source of
truth or persistent knowledge.

**Message**

A communication inside a conversation or thread. Not every Message is a reusable
Content Item.

**My Gear**

The participant's record of equipment they own or have available. Purchase
history may inform My Gear but does not prove current ownership, availability,
condition, or quantity.

**Observation**

Something reported, measured, or observed without necessarily establishing it as
truth.

**Organization**

A business or organized entity such as a brand, guide service, retailer,
outfitter, or manufacturer. An Organization can take part in partnerships with
other organizations.

**Participant**

A Person taking part in an Activity. In the Fishing domain, the participant may
be presented as an angler.

**Partner**

A relationship between organizations.

**Person**

A human represented independently of accounts, roles, or commercial
relationships.

**Platform Core**

Reusable capabilities and concepts that must not be hard-coded to Catch America
or fishing.

**Product AI Skill**

A version-controlled reusable procedure executed by product or runtime AI as
part of an AI Capability. It defines how a repeatable AI job is performed but
does not own business truth, policy, authority, or persistent domain state.

**Provenance**

The traceable history of where information came from, how it was acquired or
transformed, and what downstream information depends on it.

**Provider Organization**

An Organization that offers Services through one or more Providers. In the
Fishing domain, a guide service is a Provider Organization that may include
multiple individual Guides.

**Publication**

Distribution of a Content Item through a Channel such as website, app, email, or
social media.

**Rewards & Earnings**

The platform domain responsible for value earned through participation or
business activity, including cash earnings, reward currencies such as CatchCash,
credits, ledgers, redemption, gifting, transfers, and earning entitlements.
Actual cash settlement remains a Finance responsibility.

**Routing Policy**

Configuration and rules used by the AI Runtime to select an appropriate model or
provider path for an AI Capability based on approved technical criteria such as
capability requirements, quality, latency, cost, availability, modality, tool
support, organization policy, and eval results. Routing Policy is infrastructure
and configuration, not product business logic.

**Signal**

Potentially meaningful information or a pattern that warrants attention or
verification but is not yet established knowledge.

**Skill**

A version-controlled reusable procedure describing how an AI agent performs a
repeatable job. A Skill may define required context, tools, steps, checks,
outputs, and escalation behavior, but it does not own facts, business rules,
policy, permissions, authority, or persistent business memory.

**Source**

Where externally acquired information originated.

**Trip**

An actual outdoor activity instance undertaken by one or more Participants at
one or more Locations and times. In the Fishing domain, a Fishing Trip
represents actual fishing activity and is distinct from Trip Intent, which
represents future intent or consideration.

**Trip Intent**

A participant's expressed possibility or plan to visit a Location at a future
time. It is not proof of presence and is not yet an actual Trip.

**Validity**

Whether the platform should currently rely on a particular record, distinct from
its Effective Period and from when it was last verified.

**Watch**

A participant-requested or system-managed monitoring relationship that tracks a
target or intent for meaningful change, such as a planned trip, product
availability, expert update, or booking availability.
