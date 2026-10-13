---
artifact: prompt-spec
version: 2.0.0-draft
---

# Prompt Specification

Use this output when the user's need is bounded, usually one-off, and does not justify a persistent skill or agent.

## Required fields

### Goal
What the user wants the model to accomplish.

### Context
Only the information needed to perform the task well.

### Inputs
What the user will provide at execution time.

### Task
The concrete action the model should perform.

### Constraints
Quality, scope, safety, tone, or formatting boundaries that materially matter.

### Output contract
The expected deliverable and its structure.

## Optional fields

Include only when useful:

- role or expertise;
- examples;
- evaluation criteria;
- tool usage;
- assumptions;
- platform notes.

## Rule

A prompt spec should remain simple. If it starts accumulating persistent workflow, invocation logic, tool dependencies, reusable knowledge, or a stable persona, re-evaluate whether the artifact should instead be a skill or agent specification.