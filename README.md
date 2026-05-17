```text
  ______          __        ______            _____                 __   _ __
 / ____/___  ____/ /__     /_  __/___       / ___/____  ___  _____/ /__(_) /_
/ /   / __ \/ __  / _ \     / / / __ \      \__ \/ __ \/ _ \/ ___/ //_/ / __/
/ /___/ /_/ / /_/ /  __/    / / / /_/ /     ___/ / /_/ /  __/ /__/ ,< / / /_
\____/\____/\__,_/\___/    /_/  \____/     /____/ .___/\___/\___/_/|_/_/\__/
                                               /_/
```

# Code-to-SpecKit

Code-to-SpecKit is a repo-local Codex plugin that reverse-engineers existing codebases into evidence-backed Spec Kit documentation with Obsidian-friendly Markdown output.

![plugin](https://img.shields.io/badge/plugin-Code--to--SpecKit-2f6f60)
![version](https://img.shields.io/badge/version-v0.1.0-c97b63)
![repo-local](https://img.shields.io/badge/install-repo--local-6b7280)
![codex](https://img.shields.io/badge/Codex-compatible-0f766e)
![spec-kit](https://img.shields.io/badge/Spec%20Kit-brownfield-8b5cf6)
![obsidian](https://img.shields.io/badge/Obsidian-friendly-7c3aed)
![markdown](https://img.shields.io/badge/output-Markdown-2563eb)

It is built for brownfield work: understanding what a repository actually does today, scoping one feature at a time, tracing behavior through real code and tests, and only then generating documentation.

## What This Plugin Does

Code-to-SpecKit helps you document an already-existing codebase without inventing behavior that is not supported by the repository.

- Scans the repository and builds navigation hints for brownfield analysis
- Maps implemented features before deep-diving into any single area
- Traces one feature through code, tests, routes, schemas, and configuration
- Converts findings into Spec Kit documentation backed by explicit evidence
- Produces Markdown that remains readable in plain text and works well in Obsidian
- Flags uncertainty as open questions instead of promoting guesses into requirements

## What this repository contains

This repository contains:

- the plugin itself in `plugins/code-to-speckit/`
- repository-level documentation in `doc/`
- examples, templates, and skill definitions used by the plugin

The current plugin version is `0.1.0`.

## How it works

The plugin is intentionally lightweight in `v0.1`.

- No MCP server is required.
- No helper CLI is required.
- Skills define the workflow.
- Templates define the expected output structure.
- Application source code is treated as read-only by default.

The recommended workflow is:

1. `brownfield-scan`
2. `feature-inventory`
3. `feature-scope <feature>`
4. `feature-trace <feature>`
5. `evidence-matrix <feature>`
6. `generate-speckit-spec <feature>`
7. `obsidian-output <feature>`
8. `drift-check <feature>`

## Repository structure

```text
.
|- doc/
|  |- code-to-speckit-codex-spec.md
|  `- installation-guide.md
|- plugins/
|  `- code-to-speckit/
|     |- .codex-plugin/plugin.json
|     |- AGENTS.md
|     |- README.md
|     |- examples/
|     |- skills/
|     `- templates/
`- .agents/
   `- plugins/marketplace.json
```

## Key principles

- Evidence first: requirements must be tied to real repository artifacts.
- Bounded scope: document one feature at a time.
- Plain Markdown first: generated docs should stay readable outside Obsidian.
- Unknowns stay explicit: missing evidence becomes an open question, not a fake requirement.

## Outputs

Code-to-SpecKit is designed to generate:

- `.code-to-speckit/navigation.md`
- `.code-to-speckit/config.md`
- `docs/reverse-engineering/...`
- `specs/<feature-slug>/...`

Typical feature outputs include `spec.md`, `plan.md`, `tasks.md`, `evidence.md`, `open-questions.md`, and `drift-report.md`.

## Documentation

- [Plugin specification](C:/DEV/code-to-speckit/doc/code-to-speckit-codex-spec.md)
- [Installation guide](C:/DEV/code-to-speckit/doc/installation-guide.md)
- [Plugin README](C:/DEV/code-to-speckit/plugins/code-to-speckit/README.md)
- [Plugin agent guidance](C:/DEV/code-to-speckit/plugins/code-to-speckit/AGENTS.md)

## Installation

Install the plugin repo-locally by placing `plugins/code-to-speckit/` inside the target repository and registering it in `.agents/plugins/marketplace.json`.

Full instructions are in [doc/installation-guide.md](C:/DEV/code-to-speckit/doc/installation-guide.md).

## Status

The implementation is aligned with the current `v0.1` plugin structure:

- 9 documented skills
- template-driven outputs
- repo-local installation
- no external runtime dependencies

The main limitation is that enforcement is workflow-based rather than hard-coded, so reliability depends on following the documented skill sequence and evidence rules.
