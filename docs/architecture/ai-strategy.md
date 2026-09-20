# AI Strategy

> Status: approved v1.

## Purpose

Define the architecture and operating principles for product and runtime AI
across the platform. This document explains how business domains use AI while
staying model-agnostic, how capabilities, skills, tools, context, models,
providers, evals, and observability fit together, and where authority and
persistent knowledge live.

It is not a provider selection document, a prompt library, a model benchmark, a
feature specification, or an implementation plan. It names no provider, model,
gateway vendor, SDK, or storage technology. Those are later technical decisions.

## Core Principles

AI is a replaceable reasoning dependency of the platform.

AI does not own truth, persistent business memory, business rules, policies,
authority, or domain state.

Durable information belongs in the appropriate platform domain.

## AI Architecture

The conceptual stack:

```
Business Domain / Experience
        |
AI Capability
        |
AI Skill (when a reusable procedure is needed)
        |
Context Builder + Platform Tools
        |
AI Runtime
        |
Routing Policy
        |
Model / Provider
```

Each layer has a distinct job. A business domain names what it wants. A
capability defines the contract. A skill defines the procedure. Context builders
and tools supply grounded information. The Runtime executes. Routing policy
selects. The model produces.

**AI Runtime.** The AI Runtime is the only approved product and runtime path to
external AI models and providers. Feature code must not call a model or provider
SDK directly.

The Runtime owns capability execution, model and provider abstraction, routing
policy, the provider and model registry, versioned instructions and prompts,
tool adapters, structured-output validation, fallback, retries where
appropriate, latency controls, cost and usage controls, AI execution
observability, and eval integration.

The Runtime must not become a substitute for domain ownership. It executes
reasoning; it does not hold business state.

**Model and provider registry.** Models and providers are configuration. The
platform should support multiple providers, multiple models, capability-specific
routing, primary and fallback model configuration, changing models without
changing business-domain code, and organization-level provider restrictions or
preferences where future product requirements justify them.

## Capabilities and Skills

**AI Capability.** A capability describes what the platform wants AI to
accomplish. Candidate examples only, not the approved capability catalog:
fishing assistance, knowledge extraction, claim comparison, social response
suggestion, article drafting, campaign planning, campaign auditing, expert
profile research, classification, and summarization. Actual capability names and
contracts are established in later technical design.

Capabilities have explicit names, define input and output contracts, use
structured output when appropriate, and specify grounding and tool requirements
where appropriate. A capability never names a provider or model in
business-domain code.

Capability contract ownership and approval procedure are defined in AI Runtime
technical design.

**AI Skill.** A skill describes how a capability performs a repeatable job.

Skills are version-controlled artifacts. A skill may define procedure, required
context, tool usage, checks, output expectations, and escalation behavior. A
skill does not contain durable business truth that belongs in a domain, and does
not silently create business rules or policies. It retrieves approved policy,
knowledge, rules, conditions, products, or other domain state as needed. Skills
may be reused across models and providers.

A product skill requires eval coverage before production use when it can
materially affect customer experience, business action, published information,
financial value, access, or platform trust.

**Two separate categories.** Development Skills are procedures used by
development agents to build the platform. Product AI Skills are procedures
executed by product and runtime AI. They are not interchangeable.

## Context, Memory, and Tools

**Context.** Models receive only the context the task requires. Context Builders
assemble relevant information from approved platform domains, which may include
Person and Participant context, Trip or Trip Intent, Location, Knowledge &
Evidence, Field Intelligence, Conditions & Environment, Rules, Access &
Compliance, Content, Products and Commerce, My Gear, Services and Booking, and
conversation context.

Context assembly respects organization boundaries, permissions, privacy, source
and provenance requirements, and data minimization.

The model's conversation context is not durable platform memory.

**Persistent memory.** Anything worth remembering across interactions is written
to the appropriate platform domain through approved behavior. A participant
saying they own a kayak becomes participant profile or My Gear state. An expert
correcting fishing knowledge enters the Contribution and Knowledge workflow. A
customer preference goes to Customer & Personalization. An approved business
policy lives in its owning domain or policy artifact.

Business behavior must not rely on hidden model memory.

**Platform tools.** Tools available to models are platform-owned contracts, not
provider-specific function definitions. Conceptual examples include
`knowledge.search`, `conditions.current`, `rules.applicable`, `content.search`,
`commerce.find`, `services.find`, `booking.availability`, and
`participant.context`. These are illustrations, not approved API or contract
names. Actual platform tool contracts are defined later in technical design.

Provider-specific tool and function formats are adapters underneath the AI
Runtime. Tool authorization follows the permissions and authority of the calling
workflow or user.

## Grounding and Structured Output

**Grounding.** Grounding requirements differ by capability. A regulatory or
access answer requires current applicable Rules data with authoritative source
and provenance. A fishing recommendation should use relevant platform Knowledge
and Field Intelligence where the capability requires it. A simple low-risk copy
transformation may need no domain grounding at all.

Each capability defines its own grounding expectations rather than assuming one
standard covers every task.

**Structured output.** When downstream platform behavior depends on AI output,
prefer explicit schemas and contracts, validate output before another domain
consumes it, preserve uncertainty and unknowns where relevant, and reject,
retry, fall back, or route for review when output does not satisfy the contract.

Free-form prose is appropriate when prose itself is the intended output.

## Human Authority and Workflow

AI may research, extract, classify, summarize, compare, draft, propose, explain,
detect patterns, recommend review, and prepare actions.

AI does not automatically gain authority to create or change business rules,
create or change policies, approve campaigns, issue unapproved discounts, make
unapproved financial decisions, enforce membership or account actions, publish
consequential content, or convert uncertain signals into authoritative truth.
Those actions require approved policies and workflows plus the human or
automated authority defined elsewhere in the platform.

AI participates in Workflow & Automation as a worker. A typical pattern:

```
Trigger
  -> Context
  -> AI Skill / Capability
  -> Structured Finding or Proposal
  -> Approved Workflow / Review
  -> Human or authorized automated decision
  -> Action
  -> Audit / Outcome
```

AI output is not itself authorization.

## Evaluation and Model Changes

AI capabilities that can materially affect customer experience, business action,
published information, financial value, access, or platform trust require
evaluation coverage before production use or rollout. Eval suites test behavior,
not whether the output text reads well.

Dimensions may include correctness, grounding, provenance use, uncertainty
handling, policy compliance, usefulness, structured-output validity, tool use,
latency, cost, and model regression.

Expert corrections and real production failures may become regression and eval
cases. The same eval suite should make it possible to compare different models
and providers for the same capability. A change to an AI capability that meets
the materiality standard above is evaluated before rollout.

Eval suite location, ownership, execution procedure, and pass/fail criteria are
defined in AI Runtime technical design rather than in this strategy.

**Model switching.** Do not switch production models on subjective preference. A
model or provider change for an existing capability considers capability eval
results, latency, reliability, cost, tool and structured-output behavior, and
production feedback where available.

The capability contract stays stable when models change, unless an explicit
product or architecture change is approved.

## Prompts and Conversation

**Prompts and instructions.** Production prompts and instructions are versioned
artifacts associated with a capability, a skill, or both, and are observable in
AI execution metadata as appropriate. They must not contain hidden business
rules that belong elsewhere, and should reference or retrieve approved policy
and knowledge rather than duplicating it. Their final repository layout is a
technical design decision, not a decision made here.

**Conversation.** Conversational experiences such as Max may maintain
conversation state. Conversation history supports interaction continuity and may
be summarized or structured to control latency and cost. It does not become
durable domain memory automatically, and it must not override authoritative
platform state. When durable information surfaces in conversation, approved
workflows persist it to the appropriate domain.

## Multimodal Input

Product experiences may accept voice, text, photo, video, or other supported
modalities. AI may structure natural input to reduce unnecessary forms and data
entry.

Extracted information stays attributable to its source input, remains subject to
confirmation or review where appropriate, and does not become verified knowledge
merely because AI extracted it.

## Routing, Latency, Cost, and Fallback

**Routing.** Routing may eventually consider capability requirements, task
complexity, quality, latency, cost, availability, structured-output support,
tool support, modality requirements, organization policy, and eval performance.
Routing logic is infrastructure and configuration, not product business logic.

**Latency.** AI capabilities do not share one latency requirement. Distinguish
interactive fast, interactive reasoning, and asynchronous or background work.

Where possible, precompute intelligence, prepare context ahead of the
interaction, cache appropriate read models, avoid unnecessary model calls on
critical UI paths, and stream conversational responses when useful. AI must not
make Fishing Mode or other active-use experiences slow by default.

**Cost.** AI cost is an operational input. The platform should support AI usage
and cost attribution at levels useful for operations and finance. Candidate
dimensions may include capability, organization, model and provider, and product
experience. The exact attribution dimensions are a later technical-design
decision. Cost optimization must not silently degrade required quality.

**Fallback and failure.** AI failure degrades gracefully. Depending on the
capability: retry, use the configured fallback, return prepared non-AI
information, route to human review, or explain that current evidence is
insufficient.

Never fabricate missing knowledge because a model, tool, or provider failed.

## Observability and Privacy

The AI Runtime must evolve to record, where applicable:

- capability
- skill and instruction version
- provider and model
- tool calls
- latency
- usage and cost
- retries and fallbacks
- failures
- structured-output validation
- relevant grounding and provenance references
- feedback and eval linkage

All of this is subject to approved privacy, security, and retention controls.

Do not blindly persist full private prompts or sensitive context for debugging.

## Provider Independence

Model agnosticism does not mean every model performs identically.

It means business domains are not coupled to provider APIs, skills and
capability contracts are portable where practical, the platform can
intentionally choose the best model for a job, and provider and model changes
are constrained by contracts, evals, observability, and approved configuration.

**AI gateways.** An external AI gateway may sit underneath the AI Runtime for
provider connectivity, routing, fallback, billing, or observability. It remains
an integration and infrastructure dependency. The AI Runtime and business-domain
contracts must not depend on a specific gateway.
