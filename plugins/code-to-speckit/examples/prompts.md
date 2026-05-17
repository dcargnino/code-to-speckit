# Example Prompts

## Brownfield scan

Use code-to-speckit to analyze this codebase in brownfield mode. Generate `.code-to-speckit/navigation.md`, `.code-to-speckit/config.md`, `docs/reverse-engineering/repo-index.md`, and `docs/reverse-engineering/architecture-map.md`. Do not generate specs yet.

## Feature inventory

Use code-to-speckit to generate `docs/reverse-engineering/features-inventory.md`. Each feature must include status, confidence, evidence, tests, and open questions.

## Authentication feature

Use code-to-speckit to create the following for Authentication:

- `docs/reverse-engineering/scopes/authentication-scope.md`
- `docs/reverse-engineering/traces/authentication-trace.md`
- `specs/authentication/evidence.md`
- `specs/authentication/spec.md`
- `specs/authentication/plan.md`
- `specs/authentication/tasks.md`
- `specs/authentication/open-questions.md`

Do not generate `specs/authentication/spec.md` if scope, trace, or evidence are incomplete.

## Drift

Use code-to-speckit to generate or update `specs/authentication/drift-report.md` without changing the spec automatically.

## Large repo with bounded scope

Use code-to-speckit to analyze this large repository in brownfield mode. Do not generate specs yet. First create navigation hints, config guidance, repo index, architecture map, and a feature inventory. Then narrow the work to the feature Billing before any spec generation.

## Incomplete evidence

Use code-to-speckit to investigate the feature Authentication. If scope, trace, or evidence are incomplete, do not generate `spec.md`. Instead, update `open-questions.md` and report the safest next step.

## Drift with missing plan

Use code-to-speckit to check drift for `specs/authentication`. If `plan.md` is missing, continue with lower confidence and note the missing implementation context in the drift report.
