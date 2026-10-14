---
platform: Gemini
version: 2.1.0-draft
requires: ../core.md
last_reviewed: 2026-10-13
verify_against:
  - https://ai.google.dev/gemini-api/docs/custom-agents
  - https://ai.google.dev/gemini-api/docs/structured-output
  - https://ai.google.dev/gemini-api/docs/tool-combination
  - https://ai.google.dev/api/generate-content
  - https://ai.google.dev/api/agents
---

# Gemini Adapter

Gemini-specific artifact selection, runtime configuration, and handoff guidance only. Mission, workflow, quality hierarchy, and persona semantics come from `../core.md` and `../persona.md`; do not restate them here.

## Product lifecycle

Do not use **Gems** as the durable destination for new Axiom architecture. This repository is intentionally planning beyond their scheduled retirement on November 17, 2026.

Prefer Gemini's durable developer/runtime surfaces and treat consumer UI wrappers as replaceable implementation details.

## Choosing the Gemini artifact

Map the user's need to the smallest Gemini-native construct that owns the behavior:

| Need | Gemini artifact |
| --- | --- |
| One-off, bounded request | Prompt in Gemini / Google AI Studio |
| Persistent model behavior in an application or prototype | System instructions in Google AI Studio / Gemini API |
| Rigid or programmatic response contract | Structured output with JSON Schema |
| Actions against external systems | Function calling / custom tool declarations |
| Fresh web-grounded answers | Google Search grounding |
| Sandboxed computation or data transformation | Code execution |
| Large files, URLs, or indexed knowledge | Native context/file/URL retrieval features appropriate to the runtime |
| Reusable hosted agent with persistent configuration and tools | Gemini managed-agent / Agents API surface when appropriate |
| Enterprise orchestration on Google Cloud | Vertex AI agent/runtime capabilities appropriate to the deployment |

Do not invent a Skill-like package when Gemini's current surface is better represented as system instructions plus runtime configuration, tools, and schemas.

If the target Gemini surface materially changes the implementation, ask or state the assumption before handoff.

## Gemini handoff

Axiom should emit two conceptual layers when adapting an artifact for Gemini:

1. **Behavior payload** — the system instruction or agent definition that carries the durable mission, workflow, constraints, and persona.
2. **Runtime configuration** — only the platform-native capabilities actually needed: structured-output schema, tool declarations, grounding, code execution, retrieval/context features, or managed-agent configuration.

Keep those layers separate so runtime mechanics can change without rewriting the agent's identity.

## System instructions

- Use clear semantic Markdown and direct instructions by default.
- Do not require artificial XML wrappers, mandatory planning blocks, or visible chain-of-thought.
- Negative constraints may be stated directly when they are the clearest instruction; do not mechanically rewrite every prohibition into a positive form.
- Put examples or schemas near the behavior they clarify rather than following a fixed global ordering rule.
- Keep persona concise and subordinate to `../persona.md`'s quality hierarchy.

## Structured outputs

When the output is consumed programmatically or must follow a rigid shape, prefer Gemini's native structured-output support with JSON Schema over asking the model to imitate JSON in free text.

Axiom should specify:

- the semantic meaning of each field;
- required vs. optional fields;
- enums or strong types when useful;
- validation expectations in the calling application.

Treat schema syntax as a runtime concern: Gemini supports a practical subset of JSON Schema, and very large or deeply nested schemas may need simplification.

## Tools and grounding

Map capabilities explicitly to Gemini-native tools when they materially improve the workflow:

- **Google Search** for current or externally grounded information;
- **code execution** for computation, verification, and data manipulation;
- **URL context / file search** when the runtime should retrieve supplied or indexed sources;
- **custom function calling** for actions against the user's own APIs or systems;
- **MCP or other supported agent tools** when using an agent runtime that exposes them.

For custom functions, describe names, purposes, parameter schemas, outputs, and failure behavior clearly enough to produce valid tool declarations.

Do not enable tools merely because they exist. The Axiom specification should state why each capability is needed.

## Long-context guidance

Gemini models can support very large context windows, but limits vary by model and product surface. Verify the selected model's current limits rather than encoding a fixed token count here.

When the material fits comfortably in the available context:

- prefer preserving authoritative source material over prematurely summarizing it;
- avoid unnecessary chunking or retrieval infrastructure solely out of habit;
- separate reference material from execution instructions semantically;
- use retrieval, file search, or external storage when the corpus, reuse pattern, latency, or cost makes direct context impractical.

## Managed agents

Current Gemini developer surfaces include managed-agent capabilities in which system instructions and tools can be configured together, including built-in tools and custom functions.

When the user needs a reusable hosted agent rather than a simple model configuration, Axiom should produce an agent specification and map its capabilities into the current managed-agent/runtime surface instead of forcing the design into a deprecated Gem abstraction.

## Verification rule

Gemini model capabilities and product surfaces evolve quickly. At each `last_reviewed` pass, verify current agent surfaces, tool names, structured-output syntax, context limits, and deployment options against Google's current documentation before changing the durable Axiom core.
