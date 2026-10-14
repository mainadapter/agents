# Axiom

Axiom is an AI instruction architect and the canonical system for designing, versioning, and materializing reusable AI artifacts.

This repository stores Axiom itself at the root and the artifacts it produces under explicit type directories. The goal is to preserve durable intent and behavior independently from any one provider while still allowing each platform to use its native implementation model.

## Artifact model

Axiom classifies the underlying need before choosing implementation syntax:

- **Prompt** — an instruction for a bounded task.
- **Skill** — a reusable capability or workflow.
- **Agent** — a durable entity with stable mission, behavior, judgment, context policy, and optional persona.

The repository is the canonical source of truth for these artifacts. Native ChatGPT Skills, plugins, manifests, bindings, provider icons, and similar files are deployment outputs unless deliberately promoted to canonical identity or architecture.

## Repository structure

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
│   └── clara-reed/
├── skills/
├── prompts/
├── docs/
│   └── architecture.md
├── chatgpt/                 # Legacy provider-first material during migration
├── claude/                  # Legacy provider-first material during migration
├── gemini/                  # Legacy provider-first material during migration
├── LICENSE
└── README.md
```

A Skill used only by one Agent may live under that Agent instead of `skills/`. Not every artifact needs every optional layer.

## Axiom flow

```text
Natural intent
   ↓
Axiom understands and asks only high-impact questions
   ↓
Artifact classification
   ↓
Canonical definition
   ↓
Repository branch + draft PR
   ↓
Review and manual merge
   ↓
Platform adapter
   ↓
Native materialization
   ↓
Runtime validation
```

Axiom should hide this architecture during ordinary use. The user can describe what they need naturally; Axiom owns classification, structure, placement, and handoff.

## Canonical repository workflow

When an artifact is created or durably changed, Axiom should work on a branch and open a draft pull request. `main` represents approved canonical state. Axiom must not merge its own PR unless the user explicitly requests it.

Repository placement follows classification:

- `agents/<agent-name>/` — standalone durable agents;
- `skills/<skill-name>/` — standalone reusable skills;
- `prompts/<prompt-name>/` — reusable bounded prompts;
- `agents/<agent-name>/skills/<skill-name>/` — skills owned exclusively by one agent.

See [`integrations/github.md`](integrations/github.md) for the repository contract.

## Notion catalog

Notion may act as a human-friendly catalog for canonical Axiom artifacts. It is an index, not a second behavioral source of truth.

Catalog entries may identify an artifact's name, type, short purpose, repository path, and GitHub link. Prompt, Skill, or Agent content should remain canonical in GitHub rather than being independently maintained in both places.

See [`integrations/notion.md`](integrations/notion.md) for the catalog contract.

## Architecture principles

- Keep canonical behavior separate from provider packaging.
- Prefer one source of truth over synchronized copies.
- Treat platform adapters as build guidance rather than competing behavioral definitions.
- Treat native deployment output as generated unless deliberately promoted.
- Keep deployment-specific identifiers and private bindings out of public canonical files.
- Ask only questions whose answers materially change the artifact.
- Let native creators own volatile package formats.
- Keep persona optional but first-class when it improves long-term interaction.
- Favor maintainability and portability over prompt cleverness.

Read [`core.md`](core.md) for Axiom's canonical behavior, [`persona.md`](persona.md) for persona-design policy, and [`docs/architecture.md`](docs/architecture.md) for the full repository architecture.

## Migration

The legacy provider-first directories remain temporarily as evidence and migration references. Existing implementations should be reclassified from their underlying need before being migrated; their historical format is not authoritative.

## License

This project is licensed under the **GNU General Public License v3.0**. See [`LICENSE`](LICENSE) for details.
