---
name: Axiom GitHub Integration Contract
version: 1.0.0-draft
language: en
description: Canonical repository workflow for versioned AI artifacts designed and maintained through Axiom.
---

# GitHub Integration Contract

## Purpose and boundary

GitHub is the canonical versioned store for durable AI artifacts designed through Axiom.

This contract defines repository semantics and review workflow. It does not prescribe credentials, connector-specific commands, local Git configuration, or provider deployment packaging.

## Canonical placement

Place an artifact according to its underlying classification:

- `agents/<agent-name>/` for standalone durable agents.
- `skills/<skill-name>/` for standalone reusable skills.
- `prompts/<prompt-name>/` for reusable bounded prompts.
- `agents/<agent-name>/skills/<skill-name>/` for a skill owned exclusively by one agent.

A historical file location or provider-specific package is migration evidence, not authority over the new classification.

Keep Axiom's own canonical definition at the repository root.

## Change workflow

For creation or durable modification of a canonical artifact:

1. Start from the current approved `main` unless the user explicitly chooses another base.
2. Create or reuse a focused branch for the change.
3. Write the canonical files on that branch.
4. Open a draft pull request describing the intent, architectural decisions, and validation scope.
5. Iterate on the same branch while the user reviews the change.
6. Mark the pull request ready for review only when the user considers the definition ready for final review or explicitly requests that transition.
7. Treat the merged `main` revision as approved canonical state.

Do not write durable artifact changes directly to `main` when the branch-and-review workflow is available.

**Never merge a pull request unless the user explicitly requests the merge.** Approval of content, completion of validation, or a statement that a feature is ready does not by itself authorize Axiom to merge.

## Pull request quality

A draft pull request should make review easy without duplicating the canonical files. Include only useful context such as:

- what artifact is being created or changed;
- why its classification and repository placement fit;
- important architectural decisions;
- migration or compatibility implications;
- what was actually validated and what remains deployment-specific.

Avoid transient implementation history in canonical README files when that history belongs naturally in the pull request and Git history.

## Canonical vs deployment state

Repository canonical files define durable intent and behavior. Native package files such as manifests, private bindings, credentials, installation state, and provider-generated entry files remain deployment artifacts unless deliberately promoted.

When materializing an artifact, prefer an approved merged revision. If the user intentionally materializes from an unmerged branch, identify that source revision as provisional and do not describe it as the approved `main` definition.

When durable behavior changes after deployment:

```text
canonical edit
   ↓
branch + draft PR
   ↓
review + explicit merge by the user
   ↓
rebuild or update deployment
   ↓
validate affected behavior
```

## Safety and preservation

- Do not commit credentials, private workspace identifiers, tokens, or secrets to the public canonical repository.
- Preserve unrelated files and history during migrations.
- Prefer moves and focused edits over recreating content when repository history can be retained.
- Do not delete legacy implementations until equivalent canonical definitions have been validated or the user explicitly approves removal.
- Verify branch and pull-request state after structural changes before reporting completion.
