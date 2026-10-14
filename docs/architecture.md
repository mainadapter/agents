# Repository Architecture

This repository is Axiom: an AI instruction architecture system and the canonical home for the reusable artifacts it designs.

The design goal is to preserve durable intent and behavior independently from any single provider while allowing each platform to use the implementation style that fits it best.

## Why artifact-first

The repository began as a prompt collection and later accumulated provider-first directories such as `chatgpt/`, `claude/`, and `gemini/`. That structure made the implementation platform the primary organizing principle and encouraged duplicated definitions.

Axiom now classifies the underlying need first and stores canonical artifacts by type:

- **Prompt** — a bounded instruction worth preserving and reusing.
- **Skill** — a reusable capability or workflow.
- **Agent** — a durable entity with stable mission, behavior, judgment, context policy, and optional persona.

The platform is an implementation target, not the identity of the artifact.

## Axiom at the root

Axiom defines the architecture of this repository, so its own canonical files live at the repository root rather than under an `axiom/axiom`-like nested directory.

- `core.md` — Axiom's durable behavior and workflow.
- `persona.md` — policy for designing personas; not a requirement that Axiom itself be strongly personified.
- `platforms/` — provider-specific adaptation and materialization guidance.
- `outputs/` — intermediate Prompt, Skill, and Agent specification formats.
- `integrations/` — durable contracts for systems Axiom uses to manage canonical artifacts and catalogs.

## Canonical artifact organization

```text
/
├── core.md
├── persona.md
├── platforms/
│   ├── chatgpt.md
│   ├── claude.md
│   └── gemini.md
├── outputs/
│   ├── prompt-spec.md
│   ├── skill-spec.md
│   └── agent-spec.md
├── integrations/
│   ├── github.md
│   └── notion.md
├── agents/
│   └── <agent-name>/
├── skills/
│   └── <skill-name>/
├── prompts/
│   └── <prompt-name>/
├── docs/
│   └── architecture.md
├── chatgpt/                 # Legacy provider-first material during migration
├── claude/                  # Legacy provider-first material during migration
├── gemini/                  # Legacy provider-first material during migration
├── README.md
└── LICENSE
```

A Skill that exists only as one capability of an Agent may live under `agents/<agent-name>/skills/<skill-name>/` instead of the global `skills/` directory.

Not every artifact needs every optional file or directory. Prefer the smallest canonical representation that preserves the actual behavior.

## Conceptual layers

### Prompt definition

A canonical Prompt captures a reusable bounded instruction and only the context, inputs, constraints, and output contract required to execute it reliably.

A truly one-off request does not need repository publication. Store a Prompt only when the user wants it preserved as a reusable artifact.

### Skill definition

A canonical Skill defines a reusable capability or workflow, including invocation boundaries, inputs, behavior, quality constraints, outputs, and any durable tools or integration semantics it needs.

A platform may package the Skill in a native format, but that package does not redefine the canonical capability.

### Agent core

Defines what a durable Agent is and does:

- mission;
- domain expertise;
- durable workflow;
- decision rules;
- context policy;
- quality constraints;
- inputs and outputs.

Core content should change because the Agent changes, not because a provider changed its prompting guidance.

### Persona

Defines optional human-facing identity:

- name;
- archetype;
- voice;
- interaction style;
- behavioral traits;
- subtle quirks or role-relevant wordplay.

Persona is subordinate to competence. Style may change how an answer feels, but not whether it is correct or useful.

The root `persona.md` is Axiom's policy for designing personas for generated artifacts; it does not imply that Axiom requires a strong persona of its own.

### Visual identity and assets

A durable Agent may optionally include canonical visual assets when they materially support recognition or personification.

Canonical assets belong under the Agent rather than inside one provider's generated package. Platform-specific icons or transformed variants may derive from them without becoming the source of truth.

A visual asset should be promoted to the repository only when it is intentionally part of the Agent's durable identity. Do not version every native icon or automatically generated image merely because a platform produced it.

### Integration contract

Defines durable semantics for an external system without embedding one provider's connector or runtime implementation.

An integration contract may define:

- the external system's role;
- semantic destinations and content roles;
- read/write expectations;
- preservation and authorization rules;
- failure and verification behavior;
- implementation requirements that any platform binding must satisfy.

Workspace IDs, credentials, connector-specific commands, private bindings, and other environment details belong to deployment configuration, not the public canonical integration contract.

Root-level integration contracts such as `integrations/github.md` and `integrations/notion.md` describe systems used by Axiom itself. Artifact-specific integrations stay with that artifact, for example `agents/clara-reed/integrations/notion.md`.

### Platform adapter

Defines how a canonical artifact should be handed off to a provider's current ecosystem.

Adapters may describe:

- preferred native artifact type;
- handoff to a native creator;
- provider-specific capabilities;
- packaging considerations;
- platform limitations or product lifecycle notes;
- which canonical files are runtime authority versus build-time guidance;
- validation expectations for a materialized deployment.

Adapters should avoid freezing temporary model folklore into canonical behavior.

### Deployment artifacts

Native creators may generate files such as Skill entry instructions, manifests, package metadata, app bindings, platform icons, installation state, or runtime configuration.

These files are execution/build output unless deliberately promoted to canonical architecture or identity. They may be regenerated when canonical source changes and do not need to be maintained in this repository merely because a platform requires them.

```text
Canonical source
├── behavior / persona
├── integration contracts
├── optional assets
└── platform adapter
        ↓
Native creator / builder
        ↓
Deployment artifacts
├── entry instructions
├── manifests / metadata
├── private bindings
└── provider-specific icons/config
```

## Canonical GitHub workflow

GitHub is the reviewed source of truth for durable artifacts.

For creation or durable modification:

```text
Natural intent
   ↓
Axiom discovery + classification
   ↓
Canonical definition
   ↓
Focused branch
   ↓
Draft pull request
   ↓
User review + iteration
   ↓
Explicit merge by the user
   ↓
Approved canonical `main`
```

Axiom should not write durable changes directly to `main` when this workflow is available, and it must never merge its own pull request without explicit user authorization.

See [`../integrations/github.md`](../integrations/github.md).

## Notion catalog

Notion may provide a human-friendly discovery layer over canonical artifacts.

The catalog may contain lightweight metadata such as artifact name, type, purpose, category, repository path, and GitHub link. It should not maintain an independent full copy of Prompt, Skill, or Agent behavior.

During migration, legacy prompt text may remain temporarily until equivalent canonical GitHub artifacts exist. Preservation is more important than achieving the target catalog schema immediately.

See [`../integrations/notion.md`](../integrations/notion.md).

## Native creator principle

When a provider offers a maintained mechanism for creating Skills or Agents, use it as the final materialization layer.

```text
Approved canonical definition
   ↓
Platform adapter
   ↓
Materialization handoff
   ↓
Native creator / current platform mechanism
   ↓
Deployment artifact
   ↓
Runtime validation
```

The platform adapter is build-time guidance. Canonical behavior, persona, and applicable integration contracts remain runtime authority. A native creator may package snapshots or references to those sources, but should not invent a competing behavioral definition.

## Canonical update flow

When an installed artifact needs a durable change:

```text
Desired change
   ↓
Edit the responsible canonical layer
   ↓
Branch + draft PR
   ↓
Review + explicit merge
   ↓
Rebuild or update platform deployment
   ↓
Validate affected behavior
```

Examples:

- workflow or judgment change → Agent core or Skill definition;
- interaction identity or tone → persona;
- durable external-system semantics → `integrations/...`;
- provider-specific materialization → `platforms/...`;
- canonical visual identity → `assets/...` plus a lightweight reference when useful;
- discovery/catalog metadata → Notion catalog without redefining canonical behavior.

Generated deployment files should normally be regenerated rather than manually maintained as a second source of truth.

## Adapter validation

Platform adapters are intentionally more volatile than canonical behavior.

For each adapter:

1. review implementation guidance against current official platform documentation;
2. when practical, validate using the target platform rather than relying only on another model's interpretation;
3. record a `last_reviewed` date and authoritative sources;
4. keep target-specific findings inside the adapter unless they reveal a genuinely platform-neutral architectural rule;
5. revalidate when product surfaces, native creators, tool APIs, or artifact formats materially change.

## Migration policy

Legacy provider-first directories remain temporarily as reference implementations.

Recommended migration sequence:

1. maintain Axiom's current architecture at the root;
2. classify each legacy implementation from the underlying need;
3. create equivalent canonical Prompt, Skill, or Agent definitions;
4. validate relevant platform materializations;
5. remove provider-first legacy copies only after equivalent canonical definitions are confirmed or the user explicitly approves removal.

## Design rules

- Classify the need before choosing repository placement or provider syntax.
- Prefer one canonical definition over synchronized copies.
- Keep platform-specific rules out of canonical behavior.
- Keep deployment-specific identifiers and private bindings out of public canonical sources.
- Use branch + draft PR review for durable repository changes.
- Never merge without explicit user authorization.
- Preserve useful differences between platform implementations.
- Validate adapters against the target platform and current official documentation.
- Treat native creator output as generated unless deliberately promoted.
- Use Notion as a discovery catalog when useful, not as a second source of behavioral truth.
- Do not expose or require chain-of-thought as a generic optimization technique.
- Keep personality optional but first-class when it improves long-term interaction.
- Favor maintainability, reviewability, and portability over prompt cleverness.
