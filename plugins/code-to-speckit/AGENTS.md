# Code-to-SpecKit Agent Instructions

This repository contains a Codex plugin that reverse-engineers brownfield codebases into evidence-backed Spec Kit documentation.

## Core rules

- Work read-only by default with respect to application source code.
- Do not invent requirements.
- Every requirement must include source evidence.
- Separate Confirmed, Inferred, and Unknown behavior.
- Generate feature-level specs, not one giant project spec.
- For large repositories, generate navigation, index, scope, trace, and evidence before spec.
- Use Obsidian-friendly Markdown.
- Keep generated documentation useful outside Obsidian as plain Markdown.
- If required evidence is missing, stop and record the gap instead of filling it with assumptions.
- Treat missing scope, trace, or evidence files as blockers for spec generation.

## Repository size rules

Treat a repository as large if one or more of the following are true:

- More than 500 source files
- Monorepo or multi-app layout
- More than 5 packages or apps
- More than 3 primary languages
- Very large generated, vendor, or cache directories

For large repositories:

- Do not generate `spec.md` directly from a shallow scan.
- Generate `.code-to-speckit/navigation.md`, `repo-index.md`, `architecture-map.md`, `features-inventory.md`, `feature-scope.md`, `feature-trace.md`, and `evidence.md` first.
- If the user asks for a direct spec, explain that the feature must be bounded first.

## Evidence standard

Minimum evidence detail for important claims:

- file path
- line or symbol when available
- route, test, schema, command, component, or function name when available
- a short reason why the evidence supports the claim
- stable evidence IDs in `evidence.md` when claims are promoted into requirements

## Blocked output pattern

When the workflow must stop, prefer an explicit blocked note with:

- `Blocked because:` short reason
- `Missing or weak evidence:` files, traces, tests, or scope gaps
- `Safest next step:` the smallest reliable follow-up action
- `Do not do yet:` what must not be generated or assumed

## Generated outputs

Preferred output paths in target repositories:

- `.code-to-speckit/navigation.md`
- `.code-to-speckit/config.md`
- `docs/reverse-engineering/repo-index.md`
- `docs/reverse-engineering/architecture-map.md`
- `docs/reverse-engineering/features-inventory.md`
- `docs/reverse-engineering/scopes/<feature>-scope.md`
- `docs/reverse-engineering/traces/<feature>-trace.md`
- `specs/<feature>/spec.md`
- `specs/<feature>/plan.md`
- `specs/<feature>/tasks.md`
- `specs/<feature>/evidence.md`
- `specs/<feature>/open-questions.md`
- `specs/<feature>/drift-report.md`
