# Reading Companion

A reading partner for exploring interpretations, examining ideas, and preserving meaningful personal reflections.

## Definition and status

This directory is the proposed English repository representation of the approved Reading Companion Agent Spec, version 1.0.0, dated 2026-10-13. The approved behavior is preserved; the file organization is proposed for review. This package has not been committed to `main`, published, installed, or tested as a platform implementation.

The durable abstraction is an agent. Its previous Skill format supplies requirements but does not constrain classification.

## Repository structure

All paths are relative to the repository root.

| File | Responsibility |
| --- | --- |
| `reading-companion/README.md` | Entry point, composition, provenance, and source mapping |
| `reading-companion/core.md` | Mission, expertise, context, capabilities, workflow, continuity, coverage, quality, outputs, and acceptance scenarios |
| `reading-companion/persona.md` | Identity and interaction style subordinate to core quality |
| `reading-companion/integrations/notion.md` | Library content roles and persistence contract, without connector implementation |
| `reading-companion/platforms/chatgpt.md` | ChatGPT-specific materialization, activation, source loading, tool binding, limitations, handoff, and validation |

Read [core.md](core.md) as the behavioral source of truth, [persona.md](persona.md) for style, [integrations/notion.md](integrations/notion.md) for library persistence, and [platforms/chatgpt.md](platforms/chatgpt.md) only for ChatGPT-specific adaptation. Each file owns a distinct responsibility; this README is navigation and provenance, not another behavioral definition.

The `integrations/` directory extends the repository's agent-first layout to isolate an external knowledge contract. Notion is a knowledge destination, distinct from the assistant platform that runs the agent.

The ChatGPT adapter does not install a Plugin or Skill. Native packaging remains a later implementation step.

## Provenance

Behavioral source: the user-approved Reading Companion Agent Spec, version 1.0.0, dated 2026-10-13. The materialization uses that approved specification rather than importing additional rules from the older provider-specific implementation.

Architectural reference: `mainadapter/agents` `main`, after the Axiom 2.1.1-draft reclassification update. The Axiom persona file is a policy for designing personas, not a persona to copy into Reading Companion.

## Source mapping

| Approved specification section | Canonical destination |
| --- | --- |
| Mission | Core: Mission |
| Classification and scope | Core: Classification and scope |
| Domain and competencies | Core: Domain and expertise |
| Inputs and context policy | Core: Inputs and context |
| Persona | Persona: Identity, Interaction style, Quality boundary |
| Capabilities | Core: Capabilities |
| Behavior and reflection workflow | Core: Behavior and reflection workflow |
| Continuity across sessions | Core: Continuity across sessions |
| Persistence and library integration | Notion integration contract; core links to its authoritative rules |
| Coverage, pausing, and completion | Core: Coverage, pausing, and completion |
| Quality constraints | Core: Quality constraints |
| Outputs and success criteria | Core: Output expectations and success criteria |
| Behavioral validation scenarios | Core: Behavioral acceptance scenarios |
| Portability and future handoff | Core: Portability and future handoff; platform adapters handle implementation |

## Review scope

The English definition preserves the approved mission, default post-reading focus, support for in-progress reading and rereading, proportional retrieval, knowledge layers, finite reflection map, sufficient-depth criteria, continuity, persistence preference, and coverage-based closure.

English is the language of the canonical definition, not a restriction on conversations or stored page headings. Reading Companion uses the user's language, and the integration preserves existing library conventions.

Validation at this stage is document-level: separation of responsibilities, relative-link consistency, preservation of the acceptance scenarios, and adapter fidelity. No Plugin, Skill, platform behavior, or Notion operation has been installed or runtime-validated by this repository change.
