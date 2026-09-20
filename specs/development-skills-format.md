# Development Skills Format

> Status: approved v3.

## Purpose

Define how Development Skills are stored, structured, versioned, discovered,
reviewed, and used in this repository, so that the first Development Skill,
`platform-context`, can be written without inventing a format ad hoc.

This spec covers Development Skills only, as defined in `docs/product/glossary.md`
and `docs/architecture/skills-strategy.md`. Product AI Skill packaging is a
separate concern and receives its own design later. Nothing here defines a
Product AI Skill format, a model or provider, or any application runtime
technology.

## Canonical Location and Format

**Canonical source.** The canonical source for project-owned Development Skills
is:

```
skills/development/<skill-name>/SKILL.md
```

This is the source of truth. A provider UI, a plugin installation, or a local
agent configuration may consume or adapt a Skill, but none of them is
authoritative. A Skill that exists only inside a chat session or a vendor UI is
not a Skill this project has.

**Format.** Development Skills use the Agent Skills and Superpowers-compatible
`SKILL.md` format:

- a skill directory named for the Skill
- a required `SKILL.md` inside it
- YAML frontmatter containing the supported required fields `name` and
  `description`
- Markdown procedure and instructions in the body
- optional supporting references, scripts, or assets beside `SKILL.md`, only
  when needed

Do not invent additional required YAML frontmatter fields.

**Why `SKILL.md`.** Superpowers and the Agent Skills convention it follows both
require the filename `SKILL.md` with YAML frontmatter. Harnesses discover Skills
by that filename. We adopt it unchanged.

**Why `skills/development/` rather than a flat `skills/`.** Superpowers uses a
flat namespace because its package ships one category of Skill. This repository
will hold two categories that must not be confused, since Development Skills
build the platform and Product AI Skills execute inside it. The extra path
segment is a directory-level choice and does not alter the `SKILL.md` format or
its frontmatter, so it is compatible with the Superpowers convention rather than
an incompatibility with it. Product AI Skills will get their own sibling path
when that design exists.

**Directory name and `name` field must match.** The directory name is the Skill
name. Use lowercase letters, numbers, and hyphens only.

**Harness discovery is separate from canonical storage.** These are different
concerns and must not be conflated. The canonical Skill is the one under
`skills/development/`, whatever a given harness does to find it.

**OpenCode.** OpenCode consumes the canonical Development Skills directly. It
supports explicit additional local Skill sources through the `skills.paths`
array in `opencode.json` or `opencode.jsonc`, and a relative source such as
`./skills/development` resolves from the active OpenCode working directory.
Configuring that source loads our canonical Skills with no copying and no sync
step.

The configuration shape is:

```json
"skills": {
  "paths": [
    "./skills/development"
  ]
}
```

`skills` is an object with a `paths` array, not an array itself. OpenCode
rejects an invalid config rather than degrading, so the shape matters.

OpenCode also discovers project skills natively from `.opencode/skills/`,
`.claude/skills/`, and `.agents/skills/`. Those locations stay valid, but none
of them is required for our canonical Development Skills.

Do not create generated or duplicated OpenCode copies when direct
configured-source discovery is available. A duplicated copy is a second version
that drifts.

**Other harnesses.** Claude Code, Codex, and other development agents may
require their own discovery or adaptation mechanisms. Those mechanisms are
follow-up technical decisions and do not change the canonical repository Skill.
Where a harness needs a generated or copied artifact, that artifact is not the
source of truth and must not be edited directly.

## Required Skill Structure

A Development Skill is a single `SKILL.md` with YAML frontmatter and a Markdown
body.

**Frontmatter.** Two required fields, matching the agent-skills convention:

```yaml
---
name: skill-name
description: Use when <specific triggering conditions>
---
```

- `name`: matches the directory name. Letters, numbers, hyphens.
- `description`: third person, starts with "Use when", states triggering
  conditions only. Do not summarize the procedure in the description. A
  description that summarizes the workflow gives an agent a shortcut it will
  take instead of reading the body.
- Total frontmatter stays under 1024 characters.

Do not add custom YAML fields for project approval or versioning unless the
underlying Skill specification supports them and we explicitly approve their use
later. Project status and version go in the body instead.

**Body.** Required sections, in this order:

1. `# <Skill Name>` heading.
2. `> Project status: <draft for review | approved vN>.` on the line below the
   heading. This carries project version and approval state in the body rather
   than in frontmatter, keeping the frontmatter within the supported
   specification while matching how other approved artifacts in this repository
   declare status.
3. **Purpose.** What job this Skill performs, in one or two sentences.
4. **When it applies.** Concrete triggers and situations, plus when it does not
   apply.
5. **Context to read first.** The approved repository artifacts an agent must
   load before acting, named by path.
6. **Procedure.** Numbered steps. Each step states an observable action or
   decision.
7. **Required checks.** What must be verified before the Skill's work counts as
   done.
8. **Stop and escalate.** Required when the procedure has meaningful ambiguity,
   authority boundaries, missing prerequisites, or unsafe assumptions. It states
   the conditions under which the agent stops, what it surfaces, and to whom.
   Discipline and governance Skills are expected to have explicit stop and
   escalate conditions. A Skill with nothing meaningful to escalate omits the
   section rather than filling it with placeholder text.
9. **Expected output.** What the agent produces or reports when the Skill
   completes.
10. **Validation.** The representative tasks or pressure scenarios used to check
    this Skill, or a pointer to the separate scenario artifacts when they are
    long.

Keep the body focused. Move heavy reference material or reusable scripts into
separate files in the Skill directory rather than inflating `SKILL.md`.

## Relationship to Superpowers

Superpowers supplies general development workflow discipline: brainstorming,
writing plans, TDD, systematic debugging, code review, verification before
completion. `docs/architecture/implementation-strategy.md` already names it the
primary development workflow discipline where supported.

Our Development Skills encode what Superpowers cannot know: this project's
approved architecture, domain boundaries, artifact locations, approval rules,
and escalation behavior.

**Division of labor.**

- Superpowers owns generic process. We do not restate it.
- Our Skills own project-specific procedure and project-specific stop
  conditions.
- Where our Skill needs a generic process, it references the Superpowers skill
  by name and requirement level, for example "REQUIRED: use
  superpowers:test-driven-development", rather than copying its content.
- Where the two conflict, `AGENTS.md` and approved project artifacts win. The
  Skill stops and surfaces the conflict rather than resolving it silently.

**Do not duplicate.** If a behavior already exists in a Superpowers skill and
needs no project-specific change, reference it. Duplication creates two versions
of one procedure that drift apart.

## Governance and Approval

**A Development Skill has no authority of its own.** It does not create product
truth, business rules, policy, permissions, or authority. Approved repository
documents remain authoritative. A Skill retrieves and applies them.

**A Skill change must not silently change approved project behavior.** If
following a Skill would require behavior that differs from an approved artifact,
that is a discrepancy to surface, not a decision the Skill gets to make.

**Conflict handling is mandatory.** A Skill that conflicts with `AGENTS.md` or
any approved project artifact must stop and surface the conflict. This mirrors
the rule already in `AGENTS.md` and `docs/architecture/implementation-strategy.md`:
when approved documentation and behavior disagree, stop and flag it.

**Approval.** A Skill is approved for project use when its canonical repository
`SKILL.md` carries an approved project status and version, such as
`> Project status: approved v1.`, and that revision is committed through the
normal repository review process. Conversational agreement does not approve a
Skill.

Skill approval does not create business authority. `AGENTS.md` and approved
project artifacts remain authoritative.

**Revision.** Changing an approved Skill requires an explicit revision that
updates the body and the version in the project status line. A Skill under
revision may carry `draft for review` until the revision is approved.

**Review ownership.** Development Skill approval follows the normal project
approval process. A human project owner or reviewer approves the canonical Skill
version. AI agents may draft, test, and recommend changes, but do not
self-approve a Skill. The exact code-review tooling is not defined by this spec.

## Portability

Development Skills should stay usable across OpenCode, Claude Code, Codex, and
other compatible development agents where practical.

- Write the procedure in terms of actions, not tool names. Say "read the file",
  not the name of one harness's read tool.
- Keep provider-specific installation, configuration, and adaptation outside the
  Skill's core procedure.
- Core correctness and project truth must not depend on hidden provider memory,
  chat history, or undocumented session state. Everything a Skill relies on must
  be reachable from the repository.
- A Skill may use declared harness-specific capabilities when useful, provided
  those dependencies are explicit and the Skill stays portable or has an
  identified adaptation path where practical.
- Note harness differences in a clearly separated section or a supporting file
  rather than weaving them through the steps.

Portability is a goal, not a guarantee. Harness capabilities differ, and a Skill
that cannot work identically everywhere should say so rather than pretend.

## Validation

Validation for a Development Skill requires evidence that agents using it
produce its intended behavior and respect its limits. Compare against baseline
behavior and report whether the Skill improves outcomes, preserves existing
behavior, or introduces unnecessary work. Baseline success does not disqualify a
Skill, but equivalent results do not establish added benefit. Human approval
must consider the Skill's purpose, observed behavior, maintenance burden, and
evidence limitations.

**Method.** Use representative tasks or pressure scenarios run against an agent,
following the Superpowers approach: establish baseline behavior without the
Skill, then verify behavior with the Skill present. For a Skill that enforces
discipline, include scenarios with realistic pressure to skip the step.

**No universal automated framework.** This spec does not define one, and does
not require one. Validation for Development Skills is scenario-based and
reviewed by a human. Some Skills will warrant scripted checks later; that is a
per-Skill decision.

**Where scenarios live.** Inline in the Skill's Validation section when short,
or in a supporting file in the same Skill directory when long.

Repository-level `evals/` is reserved for reusable evaluation and
pressure-scenario assets. A Development Skill may use `evals/` when separate
scenario or test artifacts are useful. Not every Development Skill is required
to create an eval directory. Product AI capability evaluation location remains
deferred to AI Runtime technical design per
`docs/architecture/ai-strategy.md`.

**Bar for approval.** A Skill is validated when its scenarios have been run and
the observed behavior matches the Skill's stated expected output and stop
conditions. Record enough evidence to understand what was tested and whether
behavior improved. The exact recording format depends on the Skill and the
validation method.

## First Skill: platform-context

`platform-context` is the first Development Skill this format serves. This spec
does not create it.

**Job.** Ensure an agent loads the correct approved project context before
substantial work.

**Expected behavior, per `docs/architecture/skills-strategy.md`.** Read
`AGENTS.md` and `PROJECT-CONTEXT.md`. Identify the relevant approved product,
domain, architecture, and UX documents. Identify relevant ADRs, specs, and
plans. Determine the owning domain or domains. Surface conflicts before changing
code.

**What its validation must prove.** Three things, at minimum:

1. The agent loads approved context rather than working from memory or
   assumption.
2. The agent names the owning domain or domains for the work in front of it.
3. The agent stops and surfaces a conflict instead of resolving it silently,
   including under pressure to keep moving.

The third is the one worth pressure-testing. The first two can be checked with
representative tasks.

**Format application.** `platform-context` lives at
`skills/development/platform-context/SKILL.md`, carries the frontmatter and body
sections required above, and starts at `> Project status: draft for review.`
until it is reviewed and approved. It is a governance Skill, so its stop and
escalate conditions are explicit rather than optional.
