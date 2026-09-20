# Implementation Strategy

> Status: approved v1.

This document defines how we build the platform and how AI development agents
must work within it. It does not select technologies, define schemas, specify
features, or set a roadmap. Language, frontend framework, database vendor,
hosting, queue technology, vector storage, and cloud vendor are later technical
decisions and are deliberately absent here.

## Goals

- Build the platform so that Catch America proves it through real usage while
  Catch America stays an operator rather than a hard-coded assumption.
- Keep domain boundaries explicit from the first line of code, so extraction
  stays possible later without a rewrite.
- Deliver real participant value in vertical slices instead of completing every
  domain in isolation.
- Keep durable project memory in the repository rather than in AI conversations.
- Make performance, testability, auditability, and provider independence
  properties of the design rather than later cleanup.

## Architecture Approach

Start as a modular monolith.

The approved domains in `docs/product/domain-map.md` are logical business
boundaries, not microservices. Each module has explicit ownership and an
explicit boundary. A module may be extracted later only when a real operational
need justifies it, and extraction is a decision to make then, not a design goal
now.

Do not introduce distributed-system complexity before it is needed.

**Cross-domain interfaces.** A domain may expose an explicit public module
interface, contract, event, or approved query or read model for another domain
to use. The owning domain controls that contract. A new cross-domain dependency
must be documented in the relevant technical design or spec before
implementation, and if it materially changes architecture or domain ownership,
it also requires an ADR. Agents must not reach directly into another domain's
internal implementation or persistence, and must not add a shortcut import to
save a step.

## Delivery Process

Product intent and requirements are locked before implementation. Customer-facing
UX is designed and approved before coding.

Work follows this sequence:

intent, requirements, UX, technical design, implementation plan, TDD execution,
review, release, measurement.

Do not collapse these stages because an AI agent can produce code quickly. Speed
of generation is not evidence that a stage was unnecessary.

Build vertical slices driven by real experiences. Fishing Mode is intended to be
the first major vertical slice and prototype, because it exercises many core
platform concepts while delivering clear participant value.

Guardrail: Fishing-domain concepts must remain inside the Fishing domain pack.
They must not leak into Platform Core merely to make the first slice easier to
implement.

Behavioral changes use test-driven development: write a failing test, confirm it
fails for the expected reason, write the minimal implementation that passes it,
then refactor. Documentation-only changes do not require tests.

Business rules must be explicit and approved before implementation. An agent
must not invent a rule, threshold, default, or state transition to finish a
task. If a rule is missing, stop and ask.

Repository documents are the durable project memory. AI conversations and
individual model memory are not the project source of truth. Read the relevant
approved product docs, domain docs, ADRs, business rules, UX specs, and
implementation plans before doing work that touches them. When approved
documentation and the implementation disagree, stop and flag the discrepancy
rather than silently choosing a side.

**What approved means.** An artifact is approved when its repository status
explicitly says `approved` with a version, such as `Status: approved v1`. An
approved artifact changes only through an explicit revision that updates the
artifact and its version or status as appropriate. An AI agent must not treat
conversational agreement as approval unless the approved repository artifact is
updated. "Locked" in the sequence above means approved in this sense.

**Where artifacts live.**

- Technical designs: `specs/`
- Implementation plans: `plans/`
- UX specifications and design artifacts: `docs/ux/`
- ADRs: `docs/adr/`

**When an ADR is required.** Write an ADR for a decision that materially changes
or establishes architecture direction, domain boundaries or ownership,
cross-domain dependency patterns, major integration strategy, persistence or
data architecture, security or privacy architecture, AI Runtime architecture, or
a technology choice with broad or difficult-to-reverse impact. Routine feature
implementation that follows approved architecture does not require a new ADR.

## AI Development Tooling

Development tooling stays provider-independent where practical. OpenCode is
currently the provider-independent development cockpit. Claude and OpenAI models
may be selected intentionally by task.

Superpowers provides shared workflow discipline across supported coding
environments, and is the primary development workflow discipline where
supported.

The project must not depend on one AI vendor's conversation history for
continuity. Model choice is a task-level decision. It never becomes part of
product business logic.

## Product AI Strategy

Product and runtime AI is reached only through the platform's AI Runtime
abstraction. Feature code must not call OpenAI, Anthropic, Google, Vercel AI
Gateway, or any other model or provider SDK directly.

Business domains request named AI capabilities, not specific models. Capabilities
declare explicit input and output contracts and use structured outputs where
appropriate. Model and provider routing is configuration.

AI tools exposed to models are platform-owned contracts, such as knowledge
search, conditions lookup, rules lookup, content search, commerce search, or
booking availability. Prompts and instructions are versioned artifacts, not
hidden strings scattered through feature code.

Production AI supports evaluation, fallback, latency control, cost control, and
observability.

AI does not become persistent business memory. Information that must last enters
the appropriate platform domain.

**Skills.** Skills define reusable AI procedures: how a capability performs a
job. Skills do not own facts, business rules, policies, or authority. A skill
retrieves approved policy and platform knowledge instead of embedding business
truth in its instructions. Development skills and product or runtime skills are
separate categories and are not interchangeable.

Product skills used for behavior that can materially affect customer experience,
business action, published information, financial value, access, or platform
trust require evaluation coverage before production use.

**Terminology note.** Development Skills, Product AI Skills, AI Capabilities,
and AI Runtime are load-bearing terms that will be documented separately. This
implementation strategy uses them consistently but does not attempt to define
their full specifications.

## Data and Domain Boundaries

Domain ownership is explicit even when several domains share one operational
database. One database does not mean one undifferentiated data model.

Cross-domain semantic relationships may use approved association mechanisms.
Business-critical relationships stay explicitly modeled in the domain that owns
them.

Retain Source and Provenance where approved product principles require it.

Do not silently rewrite historical business or knowledge records when
correction, invalidation, reversal, or supersession is the correct behavior. The
earlier state stays visible alongside what replaced it.

## Integrations

Shopify, Klaviyo, QuickBooks, Meta, Google, weather and data providers, booking
providers, payment providers, and AI providers are integrations and adapters.

Provider request and response schemas stay at the integration boundary. Provider
field names and enums must not become the platform domain model. We must be able
to replace a provider without touching domain code.

Integrate first and replace selectively later, when there is a real reason.

## Background Processing and Performance

Expensive intelligence happens asynchronously whenever possible. Ingestion,
enrichment, research, source monitoring, Field Intelligence synthesis, Market &
Ecosystem Intelligence monitoring, content analysis, personalization
preparation, and similar work run as background jobs rather than blocking an
interactive request.

External APIs generally feed the platform asynchronously instead of being called
serially during every app interaction. The user-facing serving path prefers
prepared data, read models, and caching where appropriate.

Performance is an architectural requirement, not a later optimization.
Interactive experiences avoid unnecessary AI calls in the critical path. Fishing
Mode and other active-use experiences are designed for fast perceived response
and poor connectivity. AI conversational experiences stream or otherwise return
useful feedback quickly.

Performance-sensitive interactive experiences define appropriate performance
expectations or budgets before implementation. Background and non-interactive
work may use different performance expectations.

Observability must make it possible to identify where latency originates.

## Testing

Use the layers that fit the change:

- domain and unit tests
- integration tests
- contract tests
- end-to-end tests
- AI evals
- performance tests

Approved business rules that have executable behavior must be protected by
explicit tests at the appropriate level. Cross-domain contracts are tested so
module boundaries stay enforceable.

Tests must not be weakened or removed to make an implementation pass.

## Observability, Audit, Security, and Privacy

Cross-domain requests, externally triggered workflows, business actions that
create or modify durable business state, financial value, access, published
information, or externally visible effects, and product AI executions should
carry correlation and trace identity where it is needed to reconstruct
execution across components.

The AI Runtime must evolve to record, where applicable:

- capability
- provider and model
- instruction version
- tool usage
- latency
- cost and usage
- failures
- relevant grounding and provenance references

subject to privacy and security controls.

Audit records are distinct from application logs. Business state must never
exist only in logs.

Organization data isolation and authorization are designed explicitly. A partner
relationship does not automatically grant access to another organization's
customer or business data. Sensitive participant information, exact private
locations, financial data, and AI context follow explicit access and privacy
controls.

## V1 Migration

Do not copy V1 architecture into V2 by default. V1 is research and prototype
material.

Existing V1 code, data, and features are later classified as KEEP, MIGRATE DATA,
REFACTOR, REBUILD, or DISCARD.

That classification happens after V2 intent, domain boundaries, UX, and
implementation needs are understood.

## Delivery Principle

Build the minimum platform capability needed to support an approved vertical
experience, while preserving the approved domain boundaries.

Do not build a complete generic platform before Catch America proves the
abstractions through real usage.

Build for Catch America now. Architect so that Catch America is not hard-coded.
