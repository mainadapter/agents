---
artifact: skill-spec
version: 2.1.0-draft
---

# Skill Specification

Use this output when the user's goal is a reusable workflow or capability that should be packaged by a platform-native skill system.

## Required fields

### Name
Working name for the skill. May include a subtle role-relevant pun when appropriate.

### Purpose
What repeatable outcome the skill exists to produce.

### When to invoke
Conditions that distinguish this skill from a normal prompt or another skill. Include adjacent phrasing or intent boundaries when automatic selection could otherwise be ambiguous.

### Inputs
User input, files, connected data, parameters, or context required.

### Workflow
The stable sequence of actions, decisions, checks, and fallback behavior.

### Quality constraints
Accuracy, safety, domain, scope, and behavioral requirements.

### Outputs
What the skill should produce and how success can be recognized.

## Optional fields

### Tools and integrations
External systems or capabilities the skill may need.

### Knowledge and references
Durable source material, documentation, templates, or files the native creator should package or connect.

### Persona
Reference `../persona.md` for the general contract. Define only role-relevant voice, traits, interaction style, and naming here.

### Examples and edge cases
Include when they materially clarify invocation or behavior.

### Validation scenarios
Provide 2–3 representative requests when a native creator or platform can use them to verify triggering, workflow behavior, or output quality. Include a non-trigger example when invocation boundaries are easy to confuse.

## Handoff contract

This document is a **specification**, not necessarily the final platform package.

The relevant platform adapter should determine the handoff. When a current native skill creator exists, give it this specification and allow it to decide the up-to-date package structure, metadata, scripts, references, tests, and other implementation details.

Do not encode provider-specific packaging rules here.