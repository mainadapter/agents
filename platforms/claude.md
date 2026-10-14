---
platform: Claude
version: 2.1.0-draft
requires: core.md
last_reviewed: 2026-10-13
verify_against:
  - https://platform.claude.com/docs/en/agents-and-tools/agent-skills/overview
  - https://platform.claude.com/docs/en/agents-and-tools/agent-skills/best-practices
  - https://platform.claude.com/docs/en/managed-agents/agent-setup
  - https://support.claude.com/en/articles/9517075-what-are-projects
---

# Claude Adapter

Claude-specific artifact selection, packaging, and handoff guidance only. Mission, workflow, quality hierarchy, and persona semantics come from `../core.md` and `../persona.md`; do not restate them here.

## Choosing the Claude artifact

Map the user's need to the Claude surface that best owns the behavior:

| Need | Claude artifact |
| --- | --- |
| One-off, bounded request | Concise prompt in chat |
| Persistent behavior and shared reference material for one body of work | Project instructions + project knowledge |
| Reusable, on-demand workflow or domain capability | Agent Skill (`SKILL.md` + optional supporting files) |
| Always-on repository guidance in Claude Code | Repository/project instructions such as `CLAUDE.md` |
| Delegated specialist or multi-agent workflow | Claude-native subagent / multi-agent configuration |
| Reusable hosted agent with tools, MCP servers, skills, and versioned configuration | Claude Managed Agent |
| Agent embedded in a product or service | Claude API, Agent SDK, or Managed Agents according to runtime needs |

Do not default every reusable request to a Skill. Use a Skill when the desired behavior is an on-demand capability that should load when relevant. Use a persistent agent or project-level instruction when the behavior should remain continuously active for that surface.

If the user's target Claude surface materially changes the artifact choice, ask or state the assumption before handoff.

## Skill handoff

Axiom specifies the capability; Claude's current skill-authoring workflow should materialize, test, and package it when available.

Before handoff, Axiom should provide enough information that the user does not need to re-explain the goal:

- **capability** — what the Skill enables;
- **trigger intent** — what kinds of requests should cause it to load;
- **non-trigger intent** — nearby requests that should not invoke it when ambiguity is likely;
- **expected outputs** — the deliverable and any important format contract;
- **workflow** — stable steps, decisions, and fallback behavior;
- **knowledge/resources** — references, files, or assets that should be available on demand;
- **scripts** — deterministic or repetitive operations that are better represented as executable helpers;
- **tools/integrations** — required external capabilities;
- **persona** — short role-relevant interaction guidance when useful;
- **test prompts** — 2–3 representative requests when realistic validation would improve confidence;
- **assumptions/open questions** — only unresolved items that could materially change the implementation.

When a native or installed Skill creator is available, pass this brief to it rather than duplicating its implementation workflow inside Axiom.

If no creator is available, Axiom may draft the package directly using the conventions below and should make clear that the artifact has not gone through a native creator/testing pass.

When updating an existing Skill, preserve its established name and identity unless the user explicitly asks to rename it.

## Claude Skill conventions

### Trigger metadata

A Claude Skill is a directory whose required entry point is `SKILL.md` with YAML frontmatter containing `name` and `description`.

The `description` is part of Skill discovery and should state both **what the Skill does** and **when it should be used**. Keep persona flavor out of the description unless it is genuinely necessary for invocation; its primary job is discoverability.

### Progressive disclosure

Design Skills so Claude can load only what is needed:

1. metadata (`name`, `description`) for discovery;
2. the `SKILL.md` body after the Skill is relevant;
3. supporting resources only when the workflow needs them.

Keep `SKILL.md` focused and concise. When detailed material grows large or is branch-specific, move it to supporting files and tell Claude when to read them. Anthropic's current guidance recommends keeping the main body under roughly 500 lines when practical.

### Instructions

- Prefer clear, imperative, positive instructions and explain constraints whose purpose is not obvious.
- Use examples where they resolve real ambiguity rather than as decoration.
- Avoid emphatic capitalization and unnecessary absolute language.
- Do not script visible chain-of-thought. Use Claude's native reasoning/thinking controls when deeper reasoning is required.
- XML is optional. Use it when semantic separation of documents, examples, or input blocks materially improves clarity; Markdown is sufficient by default.

### Persona

Keep persona concise and subordinate to `../persona.md`'s quality hierarchy. Put voice and interaction guidance in the Skill body or agent system definition, not in discovery metadata whose main purpose is triggering.

### Tools and files

Name required tools, connectors, file types, scripts, and reference material explicitly so the materialization layer can package or attach them correctly.

## Managed Agents

When the desired result is a reusable, versioned Claude agent rather than an on-demand Skill, consider Claude Managed Agents. A Managed Agent can bind the model, system behavior/persona, tools, MCP servers, Skills, and multi-agent configuration into a versioned resource.

In that case, Axiom should produce an agent specification and treat Skills as modular capabilities attached to the agent rather than collapsing the whole agent into one Skill.

## Verification rule

Claude product surfaces and authoring conventions evolve quickly. At each `last_reviewed` pass, verify artifact names, file-layout requirements, discovery behavior, and supported creation mechanisms against current Anthropic documentation before changing the durable Axiom core.