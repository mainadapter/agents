# Repository Architecture

This repository stores versioned AI agent definitions and platform adaptations.

The design goal is to keep durable behavior independent from any single provider while still allowing each platform to use the implementation style that fits it best.

## Why agent-first

The previous structure grouped files primarily by provider (`chatgpt/`, `claude/`, `gemini/`). That worked while the repository was mostly a prompt collection, but it created duplication as the same agent began to exist on multiple platforms.

The new direction makes the **agent** the primary unit. A platform becomes an implementation target of that agent rather than the top-level category.

## Conceptual layers

### Core

Defines what the agent is and does:

- mission;
- domain expertise;
- durable workflow;
- decision rules;
- quality constraints;
- inputs and outputs.

Core content should change because the agent changes, not because a provider changed its prompting guidance.

### Persona

Defines the optional human-facing identity:

- name;
- archetype;
- voice;
- interaction style;
- behavioral traits;
- subtle quirks or role-relevant wordplay.

Persona is subordinate to competence. Style may change how an answer feels, but not whether it is correct or useful.

For Axiom itself, `axiom/persona.md` is the policy Axiom uses when designing personas for generated artifacts; it does not imply that Axiom requires a strong persona of its own.

### Platform adapter

Defines how the durable specification should be handed off to a provider's current ecosystem.

Adapters may describe:

- preferred native artifact type;
- handoff to a native skill/agent creator;
- provider-specific capabilities;
- packaging considerations;
- platform limitations or product lifecycle notes.

Adapters should avoid freezing temporary model folklore into the agent core.

### Adapter validation

Platform adapters are intentionally more volatile than the core and should be treated as platform-owned knowledge.

For each adapter:

1. review the implementation against current official platform documentation;
2. when practical, validate the guidance using the target platform itself rather than relying only on another model's interpretation;
3. record a `last_reviewed` date and the authoritative sources used for verification;
4. keep target-specific findings inside the adapter unless they reveal a genuinely platform-neutral architectural rule;
5. revalidate the adapter when product surfaces, native creators, tool APIs, or artifact formats materially change.

This allows ChatGPT, Claude, Gemini, or another platform to differ significantly in implementation without causing their temporary conventions to leak into the canonical agent definition.

### Output specification

Defines the intermediate artifact Axiom should produce before platform materialization.

Current specification types:

- `prompt-spec.md` — bounded, usually one-off requests;
- `skill-spec.md` — modular reusable workflows or capabilities that should load when relevant;
- `agent-spec.md` — durable identities and behaviors that may own multiple capabilities or Skills and span sessions, deployments, or providers.

## Target structure

```text
/
├── axiom/
│   ├── core.md
│   ├── persona.md
│   ├── platforms/
│   │   ├── chatgpt.md
│   │   ├── claude.md
│   │   └── gemini.md
│   └── outputs/
│       ├── prompt-spec.md
│       ├── skill-spec.md
│       └── agent-spec.md
│
├── <agent-name>/
│   ├── core.md
│   ├── persona.md
│   └── platforms/
│       └── ...
│
├── docs/
│   └── architecture.md
├── README.md
└── LICENSE
```

Not every agent needs every file. A simple single-platform artifact may remain smaller when that is the clearest representation.

## Axiom's role

Axiom is a meta-agent and instruction architect.

It should:

1. understand the user's intent;
2. diagnose ambiguity and missing constraints;
3. choose the smallest suitable artifact type;
4. produce a portable specification;
5. apply the relevant platform adapter;
6. delegate final packaging to a native creator when one exists.

Axiom should not attempt to permanently encode the implementation internals of every provider.

## Native creator principle

When a provider offers a maintained mechanism for creating skills or agents, use it as the final materialization layer.

Conceptually:

```text
Raw intent
   ↓
Axiom
   ↓
Portable specification
   ↓
Platform adapter
   ↓
Native creator / current platform mechanism
   ↓
Final artifact
```

This reduces maintenance and makes platform changes less likely to require rewriting the agent itself.

## Migration policy

The legacy provider-first directories remain temporarily during the Axiom v2 transition. They are reference implementations and should not be deleted until the new architecture has been validated against real agents.

Recommended migration sequence:

1. establish Axiom v2 and repository architecture;
2. migrate one multi-platform agent as a proof of the pattern;
3. migrate remaining agents incrementally;
4. remove provider-first legacy files only after equivalent agent-first definitions are confirmed.

## Design rules

- Prefer one canonical definition over synchronized copies.
- Keep platform-specific rules out of core files.
- Preserve useful differences between platform implementations.
- Validate adapters against the target platform and current official documentation.
- Do not expose or require chain-of-thought as a generic optimization technique.
- Treat provider guidance as revisable.
- Keep personality optional but first-class when it improves long-term interaction.
- Favor maintainability and portability over prompt cleverness.