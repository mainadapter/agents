# AI Agents Repository

A versioned collection of AI agents, skills, personas, and platform adaptations designed to preserve durable behavior across changing AI ecosystems.

This repository began as a prompt library. As AI platforms evolved beyond simple prompt configuration into skills, agents, tools, and provider-native artifacts, the repository evolved with them.

The current direction is **agent-first** rather than **platform-first**: define what an agent is and how it should behave once, then adapt that definition to ChatGPT, Claude, Gemini, or another platform as needed.

## Why this repository exists

AI providers evolve quickly. Product surfaces, model behavior, recommended prompting patterns, and packaging formats can change in months.

Keeping one fully independent prompt per provider creates drift and makes portability expensive. This repository instead aims to separate:

- **Core behavior** — mission, expertise, workflow, inputs, outputs, and quality constraints.
- **Persona** — name, voice, interaction style, and optional role-relevant personality.
- **Platform adaptation** — how the durable definition should be materialized in a provider's current ecosystem.

The goal is not to force every model through the same prompt. The goal is to preserve the same agent while allowing each platform to implement it appropriately.

## Axiom

**Axiom** is the meta-agent at the center of this architecture.

Axiom is no longer defined merely as a prompt optimizer. It is an **AI instruction architect** that transforms raw intent into a structured specification for the smallest suitable AI artifact.

Depending on the request, Axiom may produce:

- a direct prompt specification for a bounded request;
- a modular skill specification for a reusable capability or workflow;
- a portable agent specification for a durable identity that may own multiple capabilities;
- a handoff for another platform-native artifact when the provider offers a better fit.

When a platform provides a maintained native creator for skills or agents, Axiom should define the artifact clearly and delegate final packaging to that mechanism rather than duplicating volatile implementation rules.

See [`axiom/core.md`](axiom/core.md) for the canonical definition and [`docs/architecture.md`](docs/architecture.md) for the repository design.

## Repository structure

The new structure is organized around agents:

```text
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
├── docs/
│   └── architecture.md
│
├── chatgpt/                 # Legacy provider-first structure during migration
├── claude/                  # Legacy provider-first structure during migration
├── gemini/                  # Legacy provider-first structure during migration
├── LICENSE
└── README.md
```

The provider-first directories remain temporarily as reference implementations while agents are migrated incrementally.

## Architecture principles

### Core before platform

An agent's mission and quality bar should not change simply because the provider changed.

### Platform-specific implementation still matters

Portability does **not** mean using one universal prompt everywhere. Each platform adapter may use different packaging, structure, tools, or native creation mechanisms.

Adapters should be reviewed against current official documentation and, when practical, validated using the target platform itself. Platform-specific discoveries stay in the adapter unless they reveal a genuinely provider-neutral rule.

### Native creators own volatile packaging

When ChatGPT, Claude, Gemini, or another provider offers a maintained way to create a skill or agent, prefer handing it a clear specification over teaching Axiom every implementation detail permanently.

### Personality is optional but first-class

Long-lived agents can have recognizable names and personalities. This is especially useful for tutors, companions, reviewers, architects, and other recurring roles.

Personality may influence tone and interaction style, but never accuracy or task competence. A light pun or wordplay in an agent name is welcome when it fits naturally — examples in the repository include names such as **Dotty Nett**, **Artie Board**, **Becky Logër**, **Paige Turner**, and **Yusef Fect**.

`axiom/persona.md` defines how Axiom designs persona for generated artifacts; it does not mean Axiom itself needs a strong character persona.

### Avoid model folklore in the core

Do not hard-code techniques such as mandatory XML, visible `<thinking>` blocks, or fixed reasoning scaffolds as universal truths. Provider guidance belongs in replaceable adapters and should be revisited as models evolve.

## Axiom flow

```text
Raw intent
   ↓
Axiom core
   ↓
Artifact selection
   ↓
Portable specification
   ↓
Platform adapter
   ↓
Native creator / current platform mechanism
   ↓
Final artifact
```

## Legacy agents

The repository already contains agents and platform-specific definitions such as:

- **Aline Aguiar** — calendar scheduling agent;
- **Artie Board** — UX/UI co-creation specialist;
- **Audrey Tor** — documentation auditor;
- **Becky Logër** — product owner for solo builders;
- **Dotty Nett** — .NET software architect;
- **Paige Turner** — document analysis specialist;
- **Yusef Fect** — React Native architect.

These files are useful migration references. Multi-platform agents will gradually move toward canonical agent-first definitions with platform adapters rather than independent duplicated prompts.

## Migration plan

1. Establish Axiom v2 and the agent-first architecture.
2. Migrate one existing multi-platform agent to validate the pattern.
3. Migrate the remaining agents incrementally.
4. Remove legacy provider-first copies only after the canonical definitions are validated.

## Contributing

When adding or evolving an agent:

1. Define durable behavior separately from platform mechanics.
2. Keep persona subordinate to quality and competence.
3. Add platform adaptation only where it provides real value.
4. Validate platform adapters against current official guidance and, when practical, the target platform itself.
5. Prefer current native platform mechanisms over copied historical prompt patterns.
6. Test the resulting artifact on the intended platform.
7. Document meaningful behavioral or architectural changes.

## License

This project is licensed under the **GNU General Public License v3.0**. See [`LICENSE`](LICENSE) for details.

The GPL v3 license allows use, modification, and redistribution under the terms described in the license, including the corresponding copyleft obligations for distributed derivative works.

---

**Architecture transition:** Axiom v2 / agent-first repository model.