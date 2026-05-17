# Code-to-SpecKit Codex Plugin Specification

## 1. Overview

Code-to-SpecKit is a repo-local Codex plugin for brownfield analysis. Its purpose is to inspect an existing codebase and turn observed behavior into evidence-backed Spec Kit documentation.

The plugin is intentionally prompt-and-skill driven in `v0.1`.

- No MCP server is required.
- No helper CLI is required.
- Template files provide the canonical output shape.
- The plugin is read-only with respect to application source code by default.

## 2. Problem Statement

Spec-driven workflows are straightforward when requirements are written before implementation. Existing repositories are different: real behavior is spread across routes, handlers, UI flows, services, tests, schemas, and configuration, while documentation is often incomplete or outdated.

Code-to-SpecKit addresses the reverse workflow:

```text
existing codebase
-> bounded navigation
-> repo index
-> architecture map
-> feature inventory
-> feature scope
-> feature trace
-> evidence matrix
-> Spec Kit documentation
-> drift assessment
```

The plugin should behave like a careful technical investigator, not a generic documentation generator.

## 3. Product Goals

### 3.1 Primary goals

- Generate Spec Kit-style documentation from existing code.
- Require source evidence before promoting behavior into requirements.
- Keep large repositories manageable through progressive narrowing.
- Produce Markdown that is useful in plain text and friendly to Obsidian.
- Support drift checks between generated documentation and the current codebase.
- Work as a repo-local Codex plugin composed of skills, templates, and guidance docs.

### 3.2 Non-goals for v0.1

- Editing or implementing product code automatically.
- Replacing the official Spec Kit project.
- Generating one massive full-repository spec in a single pass.
- Requiring a custom runtime, MCP server, or external service.
- Acting as an authoritative source when evidence is weak or missing.

## 4. Primary Users

Code-to-SpecKit is designed for:

- developers inheriting an unfamiliar codebase
- teams documenting brownfield systems before refactors
- maintainers building traceable feature specs from production code
- technical leads preparing migration, audit, or onboarding material
- teams using Obsidian or Markdown-based knowledge systems

## 5. Design Principles

### Evidence first

Every important claim should be backed by code, tests, configuration, schema, routes, or other concrete repository artifacts.

### Narrow before deep

The plugin should scope a feature before attempting a full trace or spec.

### Read-only by default

Application source code should not be modified as part of analysis.

### Plain Markdown first

Generated files should remain readable outside Obsidian even when frontmatter, tags, and wikilinks are added.

### Unknowns stay unknown

When behavior cannot be confirmed safely, the plugin should capture uncertainty in `open-questions.md` or blocked notes rather than inventing requirements.

## 6. Current Implementation

The current implementation is a local plugin at:

`plugins/code-to-speckit`

It is composed of:

- `.codex-plugin/plugin.json`
- `AGENTS.md`
- `README.md`
- `skills/`
- `templates/`
- `examples/`

Repository-level documentation lives in:

- `doc/code-to-speckit-codex-spec.md`
- `doc/installation-guide.md`

### 6.1 Plugin metadata

Current plugin metadata from `.codex-plugin/plugin.json`:

- name: `code-to-speckit`
- version: `0.1.0`
- category: `Productivity`
- capabilities: `Read`, `Write`
- brand color: `#1F6F5F`

### 6.2 Skill set in v0.1

The plugin currently ships these skills:

1. `codebase-navigation`
2. `brownfield-scan`
3. `feature-inventory`
4. `feature-scope`
5. `feature-trace`
6. `evidence-matrix`
7. `generate-speckit-spec`
8. `obsidian-output`
9. `drift-check`

These skills define the real workflow and are the source of truth for `v0.1` behavior.

## 7. Workflow Model

### 7.1 Recommended workflow

The expected sequence for a bounded feature is:

1. `brownfield-scan`
2. `feature-inventory`
3. `feature-scope <feature>`
4. `feature-trace <feature>`
5. `evidence-matrix <feature>`
6. `generate-speckit-spec <feature>`
7. `obsidian-output <feature>`
8. `drift-check <feature>`

### 7.2 Large repository behavior

The repository should be treated as large when one or more of these conditions are true:

- more than 500 source files
- monorepo or multi-app layout
- more than 5 packages or apps
- more than 3 primary languages
- very large generated, vendor, or cache directories

For large repositories, the plugin should stop at navigation and bounded documentation artifacts until one feature is clearly scoped.

## 8. Output Contracts

### 8.1 Repository-level outputs

The plugin may generate:

- `.code-to-speckit/navigation.md`
- `.code-to-speckit/config.md`
- `docs/reverse-engineering/repo-index.md`
- `docs/reverse-engineering/architecture-map.md`
- `docs/reverse-engineering/features-inventory.md`
- `docs/reverse-engineering/scopes/<feature-slug>-scope.md`
- `docs/reverse-engineering/traces/<feature-slug>-trace.md`

### 8.2 Feature-level outputs

The plugin may generate:

- `specs/<feature-slug>/spec.md`
- `specs/<feature-slug>/plan.md`
- `specs/<feature-slug>/tasks.md`
- `specs/<feature-slug>/evidence.md`
- `specs/<feature-slug>/open-questions.md`
- `specs/<feature-slug>/drift-report.md`

### 8.3 Formatting expectations

- Files under `specs/<feature>/` should include YAML frontmatter, tags, and wikilinks.
- Files under `docs/reverse-engineering/` should also include frontmatter and tags in `v0.1`.
- `.code-to-speckit/navigation.md` and `.code-to-speckit/config.md` may stay lighter, but should still follow the templates.

## 9. Skill Responsibilities

### `codebase-navigation`

- prepares safe exploration for large or unfamiliar repositories
- identifies high-signal files and ignore paths
- prevents premature deep analysis

### `brownfield-scan`

- generates initial navigation hints and repo-level architecture artifacts
- should not generate feature specs

### `feature-inventory`

- identifies implemented features with evidence and confidence
- should not list unsupported feature claims as facts

### `feature-scope`

- narrows one feature into included behavior, excluded behavior, key files, and expected evidence

### `feature-trace`

- follows actual code paths through entry points, services, persistence, tests, and integrations
- distinguishes candidate entry points from confirmed ones

### `evidence-matrix`

- converts traced behavior into structured claims
- classifies them as `Confirmed`, `Inferred`, or `Unknown`
- records stable evidence IDs such as `E-001`

### `generate-speckit-spec`

- generates `spec.md`, `plan.md`, `tasks.md`, and `open-questions.md`
- must only promote evidenced behavior into requirements

### `obsidian-output`

- normalizes frontmatter, tags, and wikilinks
- must preserve plain Markdown readability

### `drift-check`

- compares documented behavior with the current codebase
- should report drift instead of silently rewriting specs

## 10. Evidence Model

### 10.1 Evidence sources

Valid evidence may include:

- source files
- route definitions
- handlers and controllers
- services or domain modules
- database schemas and migrations
- tests
- UI components
- configuration
- commands and scripts

### 10.2 Evidence standard

Important claims should include:

- file path
- line or symbol when available
- route, component, function, command, test, or schema name when available
- a short justification for why the artifact supports the claim

### 10.3 Claim states

- `Confirmed`: directly supported by evidence
- `Inferred`: strongly suggested but not fully explicit
- `Unknown`: not safe to derive from the repository

Unknown claims must not become functional requirements.

## 11. Blocking Rules

The plugin must not generate a feature spec when any of these are missing or clearly incomplete:

- `docs/reverse-engineering/features-inventory.md`
- `docs/reverse-engineering/scopes/<feature-slug>-scope.md`
- `docs/reverse-engineering/traces/<feature-slug>-trace.md`
- `specs/<feature-slug>/evidence.md`

Spec generation should also stop when:

- the feature scope is too broad
- the trace contains only candidate entry points
- the evidence matrix does not support the proposed requirements
- repository structure is still unclear after shallow navigation

When blocked, the plugin should explicitly state:

- what is missing
- what should be done next
- what must not be generated yet

## 12. Relationship to Templates

The templates in `plugins/code-to-speckit/templates/` are reference structures for generated outputs. In `v0.1`, the plugin does not enforce them programmatically through code; instead, the skills instruct Codex to use them as the canonical shape.

This means the implementation is:

- lightweight
- easy to install repo-locally
- dependent on disciplined prompting and skill guidance

## 13. Safety and Operating Constraints

- Do not modify application source code unless the user explicitly asks for that separately.
- Do not invent features, requirements, or architectural claims.
- Prefer stopping with documented gaps rather than overclaiming.
- Keep feature specs bounded and traceable.
- Treat drift reports as signals, not as a license to rewrite history without review.

## 14. Validation Strategy

The current documentation and examples imply this manual validation path:

1. Run `brownfield-scan` on a small repository.
2. Generate a feature inventory.
3. Scope a feature such as `authentication`.
4. Trace the feature through code and tests.
5. Build the evidence matrix.
6. Generate the Spec Kit files.
7. Apply Obsidian formatting.
8. Run a drift check after code changes.

Successful validation should show:

- evidence-backed requirements
- explicit unknowns
- no speculative feature behavior
- portable Markdown output
- stable feature-level documentation paths

## 15. Known Limits in v0.1

- The plugin relies on prompt discipline rather than executable enforcement.
- There is no dedicated verification engine beyond Codex workflow behavior.
- There is no automatic repository indexing service.
- There is no native Obsidian plugin integration.
- There is no built-in sync or publish workflow.

These limits are acceptable for `v0.1` because the main goal is a reliable repo-local documentation workflow.

## 16. Summary

Code-to-SpecKit `v0.1` is a repo-local Codex plugin that helps teams reverse-engineer existing software into traceable, evidence-backed Spec Kit documentation. Its current implementation is intentionally simple: a plugin manifest, a set of focused skills, output templates, examples, and guidance documents. The core promise is not automation at any cost, but disciplined reconstruction of what the codebase can actually prove.
