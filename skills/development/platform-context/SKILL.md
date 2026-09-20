---
name: platform-context
description: Use when starting or resuming work in this repository that proposes, reviews, or changes platform behavior or an approved artifact, decides domain ownership or a boundary crossing, or configures development tooling, and when a task's scope or governing artifacts have materially changed since the last assessment.
---

# Platform context
> Project status: approved v1.

## Purpose

Establish the approved evidence governing a task in this repository before
substantial work. Report the applicable ownership, prerequisites, and conflicts
without creating new rules or granting approval.

## When it applies

`docs/architecture/skills-strategy.md` and `specs/development-skills-format.md`
require this context before substantial work. Work is substantial when it does
any of the following:

- proposes, designs, reviews, or implements platform behavior
- proposes or makes a change to an approved artifact
- decides, questions, or depends on domain ownership or a boundary crossing
- configures development tooling, Skills, or agent configuration
- resumes work whose scope, governing artifacts, or repository state have
  materially changed since the last assessment

Run the procedure once per work context, then reuse that assessment while its
conditions hold.

It does not apply to:

- a narrow lookup answerable from a named file that assigns no ownership and
  changes no behavior, such as reading one definition or confirming one path
- a follow-up already covered by a current assessment whose scope and relevant
  files are unchanged
- a question that does not depend on this repository's state
- routine repository mechanics, such as inspecting status, log, or diff, that
  precede no change

Reading a file is not itself a trigger. Confirm the reuse conditions still hold
rather than assuming them; reassess when scope or relevant files have changed.
Skipping this Skill never waives repository instructions, which apply regardless.

## Context to read first

All paths below are relative to the confirmed repository root.

- Read `AGENTS.md` and `PROJECT-CONTEXT.md` for every new work context.
- Use `docs/product/domain-map.md` to establish product-domain ownership.
- Select relevant product context from `docs/product/north-star.md`,
  `docs/product/principles.md`, `docs/product/actors.md`,
  `docs/product/experience-map.md`, and `docs/product/glossary.md`.
- Read `docs/architecture/implementation-strategy.md` for development work;
  `docs/architecture/ai-strategy.md` for product AI; and
  `docs/architecture/skills-strategy.md` for Skill-related work.
- Find applicable artifacts in `specs/`, `docs/adr/`, `docs/ux/`, and `plans/`,
  plus business rules and implementation files referenced by those artifacts.
  For Development Skills, read `specs/development-skills-format.md`. Read
  `opencode.json` when the task concerns OpenCode configuration or discovery.

An absent or empty directory is evidence of what is missing, not permission to
invent its contents. Read task-relevant files rather than loading every directory.

## Procedure

1. **Establish the workspace.** Compare the actual working directory and Git
   root with the repository identified by the user. Inspect branch and local
   changes before considering edits. If the intended root is unambiguous and
   accessible, target it explicitly and disclose any default-directory mismatch.
   If identity is uncertain, stop. Preserve existing changes. Do not claim remote
   synchronization from a cached tracking branch; check the live remote when
   synchronization is part of the task, or state that it is unverified.
2. **Define the requested action.** State the outcome and scope: research,
   proposal, review, configuration, or implementation. Separate what the user
   authorized from possible later work. Do not convert a request to review into
   permission to implement, publish, or approve.
3. **Load the governing evidence.** Read the initial context and follow the
   relevant references above. Record artifact paths, approval statuses, and
   versions. Inspect existing code or configuration when discussing current
   behavior. Treat conversations as context to verify, not durable project truth.
4. **Identify ownership.** Name the owning and affected domains from the approved
   domain map and describe relevant contracts or boundary crossings. Distinguish
   Platform Core, the Fishing Domain Pack, and Catch America operator concerns.
   Classify development-tool tasks as development tooling when appropriate; do
   not assign them to AI Runtime simply because an AI agent uses the tool.
5. **Check prerequisites and discrepancies.** Compare the request, approved
   intent, and current behavior. Separate approved artifacts from drafts,
   illustrative examples, and deferred decisions. Determine which requirements,
   business rules, UX approvals, technical designs, ADRs, and plans the requested
   action actually needs. Do not require implementation approval merely to
   produce an authorized proposal. Do not treat that proposal as approved later.
6. **Report the assessment.** Provide the expected output below before affected
   implementation. Surface conflicts rather than silently choosing between code
   and approved documentation or rewriting an approved artifact. If no conflict
   or missing prerequisite prevents the requested action, continue within its
   existing authorization; do not create a redundant permission gate.

Use Superpowers for applicable general development discipline where supported,
as required by `docs/architecture/implementation-strategy.md`. For behavioral
implementation, use `superpowers:test-driven-development` where available;
`AGENTS.md` still requires TDD when that Skill is unavailable. This context Skill
does not reproduce those workflows or treat unavailable tooling as an exemption.

## Required checks

- Repository identity and relevant local changes were inspected.
- The assessment cites files actually read and their observed approval states.
- Ownership comes from approved artifacts, or the ownership gap is explicit.
- Current behavior, approved intent, proposals, and unknowns remain distinct.
- Prerequisites match the requested stage of work and existing authorization.
- Relevant conflicts and missing decisions are reported without invented rules,
  technology choices, or implied approval.

## Stop and escalate

Stop affected work and report to the requesting user or project owner when:

- Repository identity cannot be established.
- The request, this Skill, or current implementation conflicts with `AGENTS.md`
  or another applicable approved artifact.
- Required behavior, business rules, ownership, or approval is missing or
  ambiguous for the action being attempted.
- Implementation would add an undocumented cross-domain dependency or bypass
  the owning domain's contract.
- Proceeding would require silently revising an approved decision.

State the conflicting paths and evidence, the action that cannot proceed, and
the decision or approved artifact needed to resolve it. Do not infer permission
from urgency, a conversation's claim of approval, or the Skill itself. An
explicit request for a proposal may be fulfilled while the affected
implementation remains stopped.

## Expected output

Keep the assessment proportional to the task. Include:

- Repository path, branch, relevant local changes, and any directory mismatch.
- Requested outcome, scope, and stage of work.
- Governing artifact paths with approval status and version.
- Owning and affected domains and relevant boundaries, or development-tool scope.
- Conflicts, missing prerequisites, and relevant deferred decisions.
- The next action supported by current evidence and existing authorization, or
  the specific decision needed before affected work can continue.

An assessment that work can proceed is not a new approval. AI agents may draft,
test, critique, and recommend a Development Skill; human approval and the
repository process defined in `specs/development-skills-format.md` are required
for its approved version.

## Validation

Use the paired scenarios and evidence in [validation.md](validation.md). Run
fresh agent sessions against comparable disposable repository copies, first
without this Skill and then with it explicitly supplied. Keep repository
instructions, task prompts, and permitted effects equivalent in both conditions.

Check observable behavior: loading relevant approved context, naming domain
ownership, stopping on conflicts under pressure, allowing authorized proposals
without premature implementation, and staying proportionate on a narrow lookup
that this Skill excludes. Record baseline successes as successes; do not claim
improvement merely because the treatment passes. Format checks alone do not
validate behavior. Scenario results support human review and do not approve the
Skill.

Validation results and limitations are recorded in validation.md, including the
exact revisions tested. The recorded trials demonstrate the intended behavior in
the tested environment but do not establish improved outcomes over baseline.
Human approval remains required.
