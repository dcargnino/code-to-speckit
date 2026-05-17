---
name: codebase-navigation
description: Navigate large codebases safely before generating brownfield Spec Kit documentation.
---

# Codebase Navigation

Use this skill before generating documentation from an existing codebase, especially when the repository is large, unfamiliar, or a monorepo.

## Rules

- Do not try to understand the whole repository deeply in one pass.
- Start shallow, then go deep only on bounded feature areas.
- Identify generated, vendor, build, dependency, and cache directories before reading deeply.
- Prefer high-signal files: manifests, routes, handlers, services, schemas, tests, config, README, CI.
- Avoid low-signal files: compiled output, generated code, snapshots, lockfiles, minified assets.
- Create or update `.code-to-speckit/navigation.md` when useful.
- For large repos, require `repo-index.md`, `feature-scope.md`, `feature-trace.md`, and `evidence.md` before generating `spec.md`.
- Treat the repo as large if any of these are true: more than 500 source files, monorepo or multi-app layout, more than 5 packages or apps, more than 3 primary languages, or very large generated directories.
- If the repo is large, stop after bounded navigation artifacts unless the user explicitly narrows to one feature.

## High-signal files

- README files
- package manifests
- workspace manifests
- app entry points
- route definitions
- controller or handler files
- service or domain modules
- database schema or migrations
- validators
- tests
- CI configuration

## Default ignore paths

- node_modules
- vendor
- dist
- build
- coverage
- .next
- .nuxt
- out
- target
- .gradle
- __generated__
- generated
- snapshots
- minified assets

## Output guidance

Use `templates/navigation.md` as the reference for `.code-to-speckit/navigation.md`.
