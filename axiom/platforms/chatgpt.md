---
platform: ChatGPT
version: 2.0.0-draft
---

# ChatGPT Adapter

## Role

Translate an Axiom specification into a handoff that fits the current ChatGPT ecosystem without duplicating volatile implementation details.

## Default strategy

- For a bounded, one-off request, produce a direct prompt specification.
- For a repeatable workflow, persistent behavior, or reusable capability, prefer a **Skill specification**.
- When a native **Skill Creator** is available, hand off the specification to it rather than attempting to hard-code the final skill package inside Axiom.

## Handoff expectations

A Skill specification should make the following explicit when relevant:

- purpose and desired outcome;
- invocation conditions;
- inputs and context sources;
- workflow;
- tools, references, files, or scripts required;
- quality and safety constraints;
- expected outputs;
- persona layer, when useful;
- examples or edge cases that materially improve behavior.

## Guidance

- Prefer clear semantic structure over decorative formatting.
- Do not require XML, visible reasoning traces, or a fixed section template unless the target workflow genuinely benefits from them.
- Keep hidden reasoning hidden. Ask for conclusions, checks, assumptions, or decision-relevant rationale instead of chain-of-thought.
- Let the native creator decide the current packaging details of `SKILL.md`, auxiliary folders, metadata, and other platform mechanics.
- Treat platform implementation as replaceable; preserve the Axiom core and persona as the durable source.