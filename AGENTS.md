# AGENTS.md

> Status: approved v1. These are the governing instructions for AI agents working in this repository.

## Repository artifacts define project truth

Read the code before you answer questions about it. Approved product
specifications, domain documentation, ADRs, business rules, and approved UX
describe the intended behavior. The code describes the current behavior. When
the implementation and approved documentation disagree, stop and flag the
discrepancy. Do not silently treat either one as correct. Do not rely on memory
of how this project worked in an earlier session.

## Do not invent business rules

If a rule is not written in this repository, you do not know it. Do not guess
thresholds, pricing, eligibility, validation limits, state transitions, or
naming. Ask, and stop until you get an answer. A plausible guess that ships is
worse than a blocked task.

## Respect domain boundaries

Keep each domain's logic inside that domain. Do not reach across a boundary to
read another domain's internals, and do not add a shortcut import to save a
step. If a change seems to need a new boundary crossing, propose it first.

## Use the AI Runtime abstraction for AI work

This rule covers AI functionality we ship in the product and run in production.
It does not cover development agents or developer tooling, which are free to
call whatever they need.

For product AI, all model calls, prompts, embeddings, and tool execution go
through the AI Runtime. Do not call a provider SDK directly from feature code,
and do not add a second path around the Runtime for a one-off case. If the
Runtime cannot do what you need, say so and propose the change to the Runtime.

## Provider schemas are not the domain model

A vendor's request or response shape is a wire format. Map it to our own types
at the edge. Do not let provider field names, enums, or nesting leak into domain
entities, database tables, or public interfaces. We must be able to swap a
provider without touching domain code.

## Approved UX before implementation

Do not build user-facing behavior until someone has approved the UX. That
includes screens, flows, copy, empty states, and error states. If no approved
design exists, produce a proposal and wait.

## Test-driven development

This applies to any change that alters behavior. Documentation-only changes do
not need tests.

For behavioral changes, write a failing test first. Run it and confirm it fails
for the reason you expect. Then write the smallest change that makes it pass.
Then refactor. Do not write implementation code ahead of its test, and do not
delete or weaken a test to make a build go green.

## When you are stuck

Stop and ask. Do not fill a gap with an assumption, a mock that hides the
problem, or a `TODO` that ships.
