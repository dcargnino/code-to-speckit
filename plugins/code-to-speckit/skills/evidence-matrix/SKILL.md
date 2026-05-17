---
name: evidence-matrix
description: Build a requirement-to-source traceability matrix for a brownfield feature.
---

# Evidence Matrix

Generate:

`specs/<feature-slug>/evidence.md`

## Rules

- Every claim must have status and confidence.
- Valid statuses: Confirmed, Inferred, Unknown.
- Unknown claims must become open questions, not requirements.
- Every confirmed requirement must reference source evidence.
- Use stable evidence IDs such as `E-001`.
- Prefer evidence references with file path plus line, symbol, route, test, or schema name when available.

## Stop conditions

- If the feature trace is missing, do not build the final evidence matrix yet.
- If a claim cannot be supported, downgrade it to Unknown and move it toward open questions.

## Process

1. Start from the feature scope and trace.
2. Extract concrete claims about behavior.
3. Classify each claim as Confirmed, Inferred, or Unknown.
4. Attach code, test, route, schema, config, or UI evidence.
5. Record evidence gaps and files reviewed.
6. Reuse evidence IDs when those claims are referenced in `spec.md`.

## Output guidance

Use `templates/evidence.md` as the canonical structure.
