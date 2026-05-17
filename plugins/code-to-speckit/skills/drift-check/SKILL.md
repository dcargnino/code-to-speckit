---
name: drift-check
description: Compare existing generated specs against the current codebase and report possible drift.
---

# Drift Check

Generate or update:

`specs/<feature-slug>/drift-report.md`

## Rules

- Compare existing requirements against current source evidence.
- Check whether referenced files still exist.
- Check whether tests, routes, services, schemas, or components changed.
- Identify documented behavior no longer found.
- Identify new behavior not documented.
- Do not update the spec automatically unless explicitly requested.
- Treat missing evidence references as drift risk, not as permission to rewrite history.

## Stop conditions

- If the target feature has no `spec.md` or `evidence.md`, stop and report that drift cannot be assessed reliably.
- If `plan.md` is missing, continue with drift assessment but report lower confidence and note the missing implementation context.

## Process

1. Read `spec.md`, `evidence.md`, and `plan.md` for the target feature when available.
2. Re-check the referenced source files and tests.
3. Compare documented claims with current source evidence.
4. Write possible drift, missing evidence, and recommended updates.

## Output guidance

Use `templates/drift-report.md` as the report structure. Treat the drift report as a signal, not a source of truth.
