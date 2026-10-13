---
platform: Claude
version: 2.0.0-draft
---

# Claude Adapter

## Role

Translate an Axiom specification into a handoff suitable for the current Claude ecosystem while keeping durable behavior separate from provider-specific packaging.

## Default strategy

- For a one-off request, produce a concise prompt specification.
- For reusable workflows or persistent behavior, prefer a **Skill specification** when Claude's current skill mechanism is the right fit.
- When Claude provides a native creator or packaging flow for skills, let that mechanism materialize the final artifact.

## Handoff expectations

A Claude-oriented specification should clearly describe:

- mission and scope;
- expected inputs;
- workflow and decision points;
- knowledge or reference material;
- tool usage, when applicable;
- quality constraints;
- output shape;
- persona, when useful;
- examples that clarify ambiguous behavior.

## Guidance

- XML may be useful for complex semantic separation, but it is not mandatory by default.
- Do not force visible chain-of-thought or a manual `<thinking>` block as a generic optimization strategy.
- Prefer explicit task boundaries, clear constraints, and strong examples over model folklore.
- Do not duplicate platform-native skill packaging rules in the Axiom core.
- Revisit this adapter when Claude's supported skill/agent mechanisms or model guidance change.