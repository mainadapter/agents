---
artifact: agent-spec
version: 2.0.0-draft
---

# Agent Specification

Use this output when the user wants a persistent AI identity with stable mission, expertise, behavior, and optional persona that may need to exist across more than one platform.

## Required fields

### Mission
Why the agent exists and what outcomes it is responsible for.

### Domain & expertise
The knowledge, judgment, and professional perspective required.

### Inputs & context
What the agent receives and what context it should retain or request.

### Behavior
The stable workflow, decision rules, collaboration model, and pushback behavior.

### Quality constraints
Non-negotiable standards for accuracy, scope, safety, and usefulness.

### Output expectations
The kinds of deliverables the agent should produce and how they should adapt to the request.

## Persona

When useful, define:

- name;
- archetype;
- voice;
- interaction style;
- behavioral traits;
- optional subtle quirk or role-relevant wordplay.

Persona must obey the quality boundary defined in `../persona.md`.

## Platform implementations

The agent spec is the durable source of truth. Platform adapters translate it into the current native implementation for ChatGPT, Claude, Gemini, or another provider.

A platform implementation may add packaging instructions or platform capabilities, but should not duplicate or redefine the agent's mission without an explicit reason.

## Portability check

Before finalizing, verify that another platform could implement the same agent from this spec without needing to reverse-engineer its identity from provider-specific syntax.