---
name: generate-speckit-spec
description: Generate Spec Kit-style brownfield documentation for one feature from trace and evidence files.
---

# Generate Spec Kit Spec

Generate:

- `specs/<feature-slug>/spec.md`
- `specs/<feature-slug>/plan.md`
- `specs/<feature-slug>/tasks.md`
- `specs/<feature-slug>/open-questions.md`

## Required inputs

- `docs/reverse-engineering/features-inventory.md`
- `docs/reverse-engineering/scopes/<feature-slug>-scope.md`
- `docs/reverse-engineering/traces/<feature-slug>-trace.md`
- `specs/<feature-slug>/evidence.md`

If any required input is missing, stale, or obviously incomplete, do not generate `spec.md` yet.

## Rules

- Do not invent requirements.
- Do not include Unknown claims as requirements.
- Mark Inferred requirements clearly.
- Every functional requirement needs evidence.
- Keep implementation details in `plan.md`, not `spec.md`.
- Generate tasks for documentation, missing tests, drift checks, optional refactors, and product questions.
- Reference evidence IDs from `evidence.md` inside requirements when possible.
- If evidence is incomplete, generate or update `open-questions.md` instead of writing speculative requirements.

## Stop conditions

- Missing required input files
- Scope too broad for one feature
- Trace that still contains only candidate entry points
- Evidence matrix missing confirmed or inferred claims tied to real source artifacts

## Process

1. Read the required inputs in full.
2. Validate that the required inputs are sufficient.
3. Convert only evidenced behavior into requirements.
4. Move uncertainty into open questions.
5. Document the current implementation in `plan.md`.
6. Generate actionable, verifiable follow-up tasks.

## Output guidance

Use `templates/spec.md`, `templates/plan.md`, `templates/tasks.md`, and `templates/open-questions.md` as reference structures.
