# Clara Reed

A reading partner for exploring interpretations, examining ideas, and preserving meaningful personal reflections.

Clara Reed is the canonical identity of this agent. The name is intentionally human and conversational, with a light reading-related wordplay in `Reed` / `read`.

## Repository structure

| File | Responsibility |
| --- | --- |
| `clara-reed/core.md` | Mission, expertise, context, capabilities, workflow, continuity, coverage, quality, outputs, and acceptance scenarios |
| `clara-reed/persona.md` | Identity and interaction style subordinate to core quality |
| `clara-reed/integrations/notion.md` | Library content roles and persistence contract, without connector implementation |
| `clara-reed/platforms/chatgpt.md` | ChatGPT-specific materialization, activation, source loading, tool binding, limitations, handoff, and validation |

Read [core.md](core.md) as the behavioral source of truth, [persona.md](persona.md) for identity and style, [integrations/notion.md](integrations/notion.md) for library persistence, and [platforms/chatgpt.md](platforms/chatgpt.md) only for ChatGPT-specific adaptation.

Each file owns a distinct responsibility. This README is navigation, not another behavioral definition.

The `integrations/` directory isolates external-system contracts from the agent's durable behavior. Notion is a knowledge destination, distinct from the assistant platform that runs the agent.

Platform adapters describe how the canonical definition is materialized for a provider. They do not replace the core, persona, or integration contracts.

## Architecture

Clara Reed follows the repository architecture defined by Axiom. See [`../axiom/`](../axiom/) and [`../docs/architecture.md`](../docs/architecture.md) for the shared architectural rules.

English is the language of the canonical repository definition, not a restriction on conversation language or existing library headings. Clara Reed uses the user's language by default and preserves the conventions of connected systems.

## Current status

The canonical definition and ChatGPT adapter are specified in this directory. Native ChatGPT packaging, installation, and runtime validation remain separate implementation steps.
