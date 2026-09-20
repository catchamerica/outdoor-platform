# PROJECT-CONTEXT.md

> Status: approved v1.

Orientation for anyone joining this project, human or AI. Read this first, then
read `AGENTS.md` for the rules you must follow.

## North Star

Build an intelligent operating platform that any fishing or outdoor company can
eventually use. It may in time cover ecommerce, finance, booking, marketing,
content and learning, social and community, personalization, rewards and
earnings, subscriptions, AI, and business operations.

Catch America is the first operator and fishing is the first domain. Neither is
hard-coded into the platform core.

## Why We Are Rebuilding

V1 fragmented across multiple AI conversations and models. It accumulated hidden
and overly complex business rules, had UX problems, caused painful downstream
churn, and the app was too slow.

V2 is a conceptual reset. V1 work may later be classified as keep, migrate,
refactor, or discard, but V1 must not dictate V2 architecture.

## What Catch America Is

Catch America is the first real-world proving ground for the platform. Its
strongest value to participants is fresh first-party field intelligence from
experts and from people actually fishing.

Participants should be able to understand what is happening on the water,
express trip intent, receive meaningful updates as conditions and information
change, use Fishing Mode while actively fishing, contribute catches and reports,
and earn CatchCash for useful participation.

Experts and guides should be able to contribute conversationally by voice, text,
photo, or video and have AI structure that information. They should be able to
publish once and distribute to Catch America and external social channels, build
a persistent expert profile, manage bookings and schedules, provide Catch
Therapy, help verify knowledge, train and correct Max, and earn cash and/or
reward currency.

## Platform Direction

Modular monolith first.

The AI Runtime is model-agnostic.

External systems such as Shopify, Klaviyo, QuickBooks, Meta, weather providers,
and AI providers are integrations and adapters. They are not the domain model.

Knowledge is source-aware, perspective-aware, temporal, and evidence-backed, and
it can hold conflicting valid viewpoints at the same time.

AI does not own truth, memory, business rules, or authority.

## Current Phase

We are not coding product features yet. We are formalizing product intent,
domains, experience architecture, development process, skills, eval strategy,
and implementation strategy before UX and implementation.

## Source of Truth

Approved repository documents, ADRs, business rules, and approved UX define
intended project behavior. The implementation represents current behavior. When
they disagree, stop and flag the discrepancy. Do not silently choose or resolve
either side by assumption. Resolution requires an explicit approved decision or
update. AI conversations are not the durable source of truth.
