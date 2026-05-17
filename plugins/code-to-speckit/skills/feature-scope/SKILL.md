---
name: feature-scope
description: Define the boundaries of a single feature before tracing or generating a spec.
---

# Feature Scope

Generate:

`docs/reverse-engineering/scopes/<feature-slug>-scope.md`

## Rules

- Define included behavior.
- Define excluded behavior.
- Identify primary and secondary paths.
- Identify search terms.
- Identify required evidence.
- Do not generate `spec.md` until scope is clear.
- Keep the scope narrow enough to trace in one pass.

## Stop conditions

- If the requested feature name maps to multiple unrelated behaviors, split it before tracing.
- If no likely entry points, files, or tests can be identified, stop and record an unresolved scope instead of pretending the feature is bounded.

## Process

1. Start from one feature named by the user or inventory.
2. Decide what behavior is included and excluded.
3. Identify the highest-signal files and tests to inspect next.
4. Record evidence that must exist before spec generation.

## Output guidance

Use `templates/feature-scope.md` as the reference structure.
