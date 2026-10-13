---
platform: ChatGPT / OpenAI
version: 2.1.0-draft
requires: core.md
last_reviewed: 2026-10-13
verify_against:
  - https://help.openai.com/en/articles/20001066-skills-in-chatgpt
  - https://help.openai.com/en/articles/20001256-plugins-in-chatgpt
  - https://help.openai.com/en/articles/10169521-projects-in-chatgpt
  - https://help.openai.com/en/articles/20001143/
  - https://developers.openai.com/learn/agents
  - https://developers.openai.com/cookbook/examples/gpt-5/codex_prompting_guide
---

# ChatGPT / OpenAI Adapter

ChatGPT- and OpenAI-specific artifact selection, packaging, and handoff guidance only. Mission, workflow, quality hierarchy, and persona semantics come from `../core.md` and `../persona.md`; do not restate them here.

## Choosing the OpenAI artifact

Map the user's need to the narrowest surface that owns the behavior:

| Need | OpenAI artifact / surface |
| --- | --- |
| One-off, bounded request | Direct prompt in ChatGPT |
| Lightweight preferences that should apply broadly across chats | Custom Instructions |
| Persistent context, files, and instructions for one body of work | ChatGPT Project |
| Reusable, on-demand workflow or capability | Skill |
| Reusable workflow that also needs connected services, external data, or actions | Plugin containing Skills and/or Apps |
| Repeatable end-to-end team workflow with tools, schedules, or API triggers | ChatGPT Workspace Agent, when available |
| Repository-specific coding guidance | `AGENTS.md` / Codex instructions, optionally combined with Skills or Plugins |
| Agent embedded in a product or service | Responses API and/or Agents SDK; use the current managed agent API when its runtime model fits |

Do not default every reusable behavior to a Skill. A Skill is appropriate for reusable task-scoped guidance. Use a Plugin when the workflow also needs app connections or packaged external capabilities. Use a Workspace Agent when the desired result is a durable autonomous workflow with its own tools, configuration, schedule, or trigger channels.

Custom GPTs are a legacy target during the current transition. Do not choose a new GPT as Axiom's durable default when a Skill, Plugin, Project, or Workspace Agent better represents the use case.

If the user's ChatGPT/OpenAI surface, plan, or workspace permissions materially change the artifact choice, ask or state the assumption before handoff.

## Skill handoff

Axiom specifies the reusable capability; ChatGPT's `skill-creator` should generate, update, test, or troubleshoot the final Skill when available.

Before handoff, provide enough information that the creator does not need to rediscover the intent:

- **purpose** — the repeatable outcome the Skill exists to produce;
- **when useful** — requests and contexts in which the Skill should be selected automatically;
- **non-trigger contexts** — nearby requests that should remain ordinary chat when ambiguity is likely;
- **inputs** — user text, files, project context, or connected information the workflow expects;
- **workflow** — stable steps, decisions, checks, and fallback behavior;
- **resources** — examples, references, templates, or supporting files;
- **scripts/code** — deterministic or repetitive operations better packaged as reusable code;
- **tools/apps** — capabilities or connected services required by the workflow;
- **outputs** — expected deliverables and important format contracts;
- **persona** — concise interaction guidance when useful;
- **test prompts** — 2–3 representative requests when validation would improve confidence;
- **assumptions/open questions** — only unresolved issues that could materially change implementation.

Let `skill-creator` own current Skill packaging details. Do not duplicate volatile file-layout, metadata, installation, or troubleshooting rules in Axiom unless a target surface explicitly requires them.

## Plugin handoff

Use a Plugin when reusable instructions need to travel together with external capabilities.

A Plugin specification should identify:

- which behavior belongs in Skills;
- which external systems require Apps or MCP-backed capabilities;
- read vs. write actions;
- authentication or workspace prerequisites the user must complete;
- approval boundaries for consequential actions;
- surfaces where the plugin must work (Chat, Work, Codex, desktop, web, or mobile) when that matters.

Prefer the native Plugin Creator when available rather than teaching Axiom the full plugin package format.

## Projects and Custom Instructions

Use **Custom Instructions** for lightweight, broadly applicable user preferences rather than task-specific workflows.

Use a **Project** when instructions, files, chats, and connected sources should remain scoped to one ongoing body of work. Project instructions should contain only the behavior that needs to remain active throughout that project; reusable task workflows should stay in Skills so they can be invoked when relevant.

## Workspace Agents

Use a **Workspace Agent** when the user needs a persistent, shareable agent that can own a repeatable end-to-end workflow rather than merely provide reusable instructions.

A Workspace Agent specification may include:

- mission and description;
- instructions and persona;
- model/reasoning requirements only when they materially affect the workflow;
- Skills;
- Apps and tool permissions;
- memory requirements;
- action approval boundaries;
- starter prompts;
- schedules or API trigger channels;
- deployment context such as ChatGPT or Slack.

Keep Skills modular: attach reusable capabilities to the agent rather than expanding one monolithic system instruction.

## Codex

For repository-specific coding behavior, prefer `AGENTS.md` for instructions that should be continuously available within repository scope. Use Skills for task-specific reusable workflows and Plugins when those workflows need external apps or packaged integrations.

Do not add prompt scaffolding for intermediate plans, reasoning traces, or progress messages unless current Codex guidance explicitly calls for it. Native model and harness behavior evolves quickly.

## API and developer runtimes

When the artifact belongs in an application rather than ChatGPT itself, hand off an agent/runtime specification rather than a ChatGPT Skill specification.

Prefer current OpenAI agent primitives such as the Responses API, Agents SDK, supported managed agent APIs, tools, MCP, and structured output mechanisms according to runtime needs. Keep model choice, tool configuration, schemas, state, and deployment concerns in the implementation layer rather than the portable Axiom core.

## Instruction guidance

- Prefer clear headings, explicit steps for multi-stage workflows, and concrete positive instructions.
- Add examples when they disambiguate behavior or classification boundaries.
- Do not require XML or decorative prompt scaffolding by default.
- Do not request visible chain-of-thought. Ask for conclusions, checks, assumptions, concise rationale, or artifacts instead.
- Keep persona subordinate to task quality and the hierarchy in `../persona.md`.

## Verification rule

OpenAI product surfaces are changing rapidly. At each `last_reviewed` pass, verify Skill availability, Plugin semantics, Workspace Agent capabilities, Codex instruction behavior, API agent primitives, and any migration/deprecation notices against current OpenAI documentation before changing the durable Axiom core.