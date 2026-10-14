# Clara Reed

A reading partner for exploring interpretations, examining ideas, and preserving meaningful personal reflections.

Clara Reed is the canonical identity of this agent. The name is intentionally human and conversational, with a light reading-related wordplay in `Reed` / `read`.

![Clara Reed](assets/avatar.png)

## Repository structure

| File | Responsibility |
| --- | --- |
| `agents/clara-reed/core.md` | Mission, expertise, context, capabilities, workflow, continuity, coverage, quality, outputs, and acceptance scenarios |
| `agents/clara-reed/persona.md` | Identity and interaction style subordinate to core quality |
| `agents/clara-reed/assets/avatar.png` | Canonical visual identity |
| `agents/clara-reed/integrations/notion.md` | Library content roles and persistence contract, without connector implementation |
| `agents/clara-reed/platforms/chatgpt.md` | ChatGPT-specific materialization, activation, source loading, tool binding, limitations, handoff, and validation |

Read [core.md](core.md) as the behavioral source of truth, [persona.md](persona.md) for identity and style, [integrations/notion.md](integrations/notion.md) for library persistence, and [platforms/chatgpt.md](platforms/chatgpt.md) only for ChatGPT-specific adaptation.

Each file owns a distinct responsibility. This README is navigation, not another behavioral definition.

The `assets/` directory contains durable identity assets that are part of the canonical agent rather than provider-specific packaging.

The `integrations/` directory isolates external-system contracts from the agent's durable behavior. Notion is a knowledge destination, distinct from the assistant platform that runs the agent.

Platform adapters describe how the canonical definition is materialized for a provider. They do not replace the core, persona, or integration contracts.

## Visual identity

The canonical visual identity is [`assets/avatar.png`](assets/avatar.png). Platform implementations may resize or adapt this asset to native requirements, but should preserve the same recognizable identity unless a new canonical visual is approved.

## Architecture

Clara Reed follows the repository architecture defined by Axiom. See the repository [Axiom core](../../core.md) and [architecture documentation](../../docs/architecture.md) for shared rules.

English is the language of the canonical repository definition, not a restriction on conversation language or existing library headings. Clara Reed uses the user's language by default and preserves the conventions of connected systems.

## Current status

The canonical definition and ChatGPT adapter are specified in this directory. Native packaging and runtime validation are deployment-specific and are not maintained as canonical repository artifacts.
