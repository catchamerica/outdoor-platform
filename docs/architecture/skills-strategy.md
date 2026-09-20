# Skills Strategy

> Status: approved v1.

## Purpose

Define how this project uses Skills, what types of Skills exist, how a Skill
differs from an AI Capability, a business rule, a policy, a prompt, and a
workflow, and which initial Skills we expect to create.

This is a strategy and catalog document. It is not the Skill implementations, a
Skill file format decision, or a commitment to build every Skill listed here.

## Skill vs Capability vs Workflow

A Skill defines how an AI agent performs a repeatable job.

A Skill does not own facts, domain state, business rules, policies, permissions,
authority, or persistent business memory. Skills retrieve and operate on
approved platform context.

**Development Skill.** A reusable procedure used by AI development agents to
build, review, or modify the platform.

**Product AI Skill.** A reusable procedure executed by product or runtime AI as
part of an AI Capability.

**AI Capability.** Defines what the platform wants AI to accomplish, plus the
input and output contract.

**Prompt / Instruction.** The model-facing instruction used by a Capability, a
Skill, or both.

**Workflow.** Coordinates tasks, approvals, triggers, human review, and
authorized actions.

**Business Rule / Policy.** Approved business behavior or authority. A Skill may
consume these. A Skill must not create them.

## Skill Principles

A Skill should:

- be version-controlled
- have a narrow, clear job
- identify when it applies
- define required inputs and context
- define required platform tools where applicable
- define procedural steps and checks
- define expected output
- define uncertainty and escalation behavior where appropriate
- stay model and provider portable where practical
- avoid duplicating domain knowledge
- avoid embedding hidden business rules
- avoid direct provider-specific APIs

## Development Skills

The initial Development Skill catalog. These are cataloged here, not created by
this document.

**1. platform-context**

Ensure an agent loads the correct approved project context before substantial
work. Read `AGENTS.md` and `PROJECT-CONTEXT.md`, identify the relevant approved
product, domain, architecture, and UX documents, identify relevant ADRs, specs,
and plans, determine the owning domain or domains, and surface conflicts before
changing code.

**2. domain-change**

Guide changes that modify domain behavior or ownership. Identify the owning
domain, identify affected domains, identify approved business rules, identify
Source and Provenance implications where relevant, identify cross-domain
contracts, determine whether an ADR is required, require approved behavior
before implementation, and require appropriate tests.

**3. ux-feature**

Guide implementation of customer-facing behavior. Confirm approved UX exists,
read the relevant experience and UX specs, and include loading, empty, error,
permissions, offline and connectivity, and responsive states where applicable.
Do not redesign approved UX during implementation. Escalate UX gaps rather than
inventing them.

**4. cross-domain-feature**

Guide features that span multiple domains. Identify each participating domain,
preserve ownership boundaries, document new cross-domain dependencies in the
technical design, use approved public contracts, events, or read models,
determine whether an ADR is required, and prevent shortcut imports or
shared-state coupling.

**5. ai-capability**

Guide creation or modification of a Product AI Capability. Define the capability
contract, identify the owning and consuming domains, identify grounding
requirements, identify required tools and context, define structured output
where appropriate, identify Skill usage, define eval needs, define
observability, and preserve provider and model independence.

**6. integration-adapter**

Guide integration with an external provider or system. Keep provider schemas at
the edge, map external data into platform domain concepts, retain Source and
Provenance where required, define failure and retry behavior, define sync
direction and system-of-record assumptions explicitly, and avoid leaking
provider-specific types into domains.

**7. migration-safety**

Guide schema and data migrations safely. Preserve approved historical and audit
semantics, avoid silent destructive transformations, define forward and backward
compatibility where relevant, define a rollback and recovery strategy, test
migration behavior, and distinguish migration of V1 data from adoption of V1
architecture.

## Product AI Skill Candidates

These are candidate Skill names only. They do not define an approved Skill
catalog. An actual Skill is created only when an approved experience or
capability needs it. A candidate may be renamed, merged, split, or dropped
during technical design. Do not create these Skills upfront.

**Fishing and Participant**

- plan-fishing-trip
- update-living-trip-plan
- fishing-mode-assistant
- structure-catch-report
- troubleshoot-fishing
- prepare-catch-therapy-brief

**Expert and Field Intelligence**

- research-expert-profile
- structure-field-report
- process-expert-correction
- identify-profile-updates
- prepare-social-derivatives

**Knowledge**

- extract-knowledge
- evaluate-claim
- review-conflicting-evidence
- assess-source-change

**Content**

- research-content-brief
- draft-learning-content
- refresh-stale-content
- audit-content

**Marketing**

- detect-marketing-opportunity
- build-campaign-brief
- audit-campaign
- analyze-campaign

**Community and Social**

- triage-community-inbox
- suggest-community-response
- extract-field-signal
- identify-ugc
- detect-content-opportunity

**Market & Ecosystem Intelligence**

- monitor-market-change
- analyze-competitor-change
- cluster-community-conversation
- prepare-market-brief

## Skill Lifecycle

First-pass lifecycle:

```
Need identified
  -> Skill intent defined
  -> Skill procedure drafted
  -> representative scenarios / evals created
  -> review
  -> approved version
  -> production use
  -> production feedback and corrections
  -> revised version
```

Not every Skill uses the same testing machinery. A Development Skill and a
Product AI Skill are verified differently, and the lifecycle above describes the
shape of the path rather than one shared toolchain.

## Storage and Portability

Canonical Skills live in the repository. A Skill must not exist only inside a
provider UI or a chat session.

The final Skill directory layout, file format, and packaging are technical
design decisions and are not made here.

Skills should be portable across models and providers where practical.
Portability is constrained by capability, tool, and model differences. Evals
determine whether a Skill performs acceptably on a given model. Switching models
does not change a Skill's business authority.

## Governance and Evaluation

Product AI Skills used for behavior that can materially affect customer
experience, business action, published information, financial value, access, or
platform trust require eval coverage before production use.

Development Skills should be testable through realistic pressure scenarios or
representative tasks where practical.

A Skill never gains authority by being executed. Authority stays with approved
policies, workflows, and the human or automated decision-makers defined
elsewhere in the platform.
