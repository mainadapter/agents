---
platform: Gemini
version: 2.0.0-draft
---

# Gemini Adapter

## Role

Translate an Axiom specification into a handoff for the current Gemini ecosystem without coupling the agent definition to a product surface that may disappear or be replaced.

## Product-lifecycle rule

Do not treat **Gems** as the durable destination for new Axiom architecture. This repository explicitly avoids building the v2 design around Gems because their retirement is scheduled for November 17, 2026.

The adapter should target the current supported Gemini-native mechanism available at implementation time. If no durable native agent/skill packaging mechanism is appropriate, produce a provider-specific instruction specification rather than inventing one.

## Handoff expectations

A Gemini-oriented specification should make clear:

- mission and desired outcome;
- inputs and reference context;
- recurring workflow or one-off task shape;
- tools and integrations required;
- quality constraints;
- output contract;
- persona, when useful;
- assumptions that a native creator should resolve.

## Guidance

- Do not require XML, mandatory planning blocks, or visible chain-of-thought as universal Gemini optimizations.
- Prefer direct, unambiguous instructions and strong structure appropriate to the task.
- Keep large reference context and execution instructions clearly separated when that improves comprehension, without hard-coding a single ordering rule for all cases.
- Treat current Gemini product mechanics as an adapter concern, not part of the Axiom core.
- Reassess this file when Google's post-Gems agent/skill workflow is clear.