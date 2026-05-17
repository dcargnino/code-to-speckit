---
name: feature-trace
description: Trace a feature through entry points, call flow, data flow, persistence, tests, and integrations.
---

# Feature Trace

Generate:

`docs/reverse-engineering/traces/<feature-slug>-trace.md`

## Rules

- Start from the feature scope.
- Follow real code paths.
- Record files read and skipped.
- Separate candidate entry points from confirmed entry points.
- Capture call flow and data flow.
- Mark gaps and unknowns.
- Use actual routes, handlers, components, commands, services, tests, and schemas when naming the flow.

## Stop conditions

- If `docs/reverse-engineering/scopes/<feature-slug>-scope.md` is missing, do not trace yet.
- If candidate entry points cannot be confirmed from source evidence, stop and keep them under candidate entry points.
- If the flow branches too widely, narrow the scope instead of writing a speculative trace.

## Process

1. Start from the scoped paths and search terms.
2. Confirm entry points from routes, handlers, UI actions, or commands.
3. Follow the runtime path through services, models, and integrations.
4. Record tests and persistence behavior.
5. Capture missing evidence and uncertain branches.

## Output guidance

Use `templates/feature-trace.md` as the canonical structure.
