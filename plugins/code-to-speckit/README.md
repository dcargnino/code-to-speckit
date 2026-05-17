# Code-to-SpecKit

Code-to-SpecKit is a repo-local Codex plugin that reverse-engineers existing codebases into evidence-backed Spec Kit documentation with Obsidian-friendly Markdown output.

## What it is

This plugin is intentionally implemented as a prompt and skill pack for brownfield analysis.

- No MCP required in v0.1
- No helper CLI required in v0.1
- Read-only with respect to application source code by default
- Template files act as textual references that skills should follow

## Install repo-local

Expected layout:

```text
<repo-root>/
  .agents/plugins/marketplace.json
  plugins/code-to-speckit/
```

The marketplace entry in this repository already points to:

```text
./plugins/code-to-speckit
```

Recommended local guidance files in the analyzed repository:

```text
.code-to-speckit/navigation.md
.code-to-speckit/config.md
```

## Plugin contents

```text
plugins/code-to-speckit/
  .codex-plugin/plugin.json
  AGENTS.md
  README.md
  skills/
  templates/
  examples/
```

## Documentation

- `../../doc/code-to-speckit-codex-spec.md`
- `../../doc/installation-guide.md`

## Output policy

All generated Markdown should remain readable as plain Markdown.

- Files under `specs/<feature>/` must include YAML frontmatter, tags, and wikilinks.
- Files under `docs/reverse-engineering/` should also include YAML frontmatter and tags in v0.1 for consistency.
- `.code-to-speckit/navigation.md` and `.code-to-speckit/config.md` may stay lightweight, but should still follow the plugin templates.

## Main workflow

Recommended flow on an existing repository:

1. `brownfield-scan`
2. `feature-inventory`
3. `feature-scope <feature>`
4. `feature-trace <feature>`
5. `evidence-matrix <feature>`
6. `generate-speckit-spec <feature>`
7. `obsidian-output <feature>`
8. `drift-check <feature>`

## Blocking rules

Do not generate a feature spec if any of these are missing:

- `docs/reverse-engineering/features-inventory.md`
- `docs/reverse-engineering/scopes/<feature-slug>-scope.md`
- `docs/reverse-engineering/traces/<feature-slug>-trace.md`
- `specs/<feature-slug>/evidence.md`

If evidence is weak or incomplete, generate or update `open-questions.md` instead of inventing requirements.

## Failure modes

When the plugin cannot safely continue:

- Missing scope: create or refine the feature scope first.
- Missing trace: inspect entry points and produce a real feature trace before spec generation.
- Missing evidence: build the evidence matrix and capture gaps explicitly.
- Large repo, unclear feature: stop at navigation, index, inventory, and scope.
- Ambiguous behavior: write it to `open-questions.md`, not `spec.md`.

## Manual validation

Recommended validation target:

- A small local repo with one clear feature such as `authentication` or `todo`
- At least one route or entry point
- At least one test
- A data model, schema, or persistence layer
- A README or basic project manifest

Suggested validation sequence:

1. Run `brownfield-scan`
2. Run `feature-inventory`
3. Run `feature-scope authentication`
4. Run `feature-trace authentication`
5. Run `evidence-matrix authentication`
6. Run `generate-speckit-spec authentication`
7. Run `obsidian-output authentication`
8. Run `drift-check authentication`

Expected outputs:

- `.code-to-speckit/navigation.md`
- `.code-to-speckit/config.md`
- `docs/reverse-engineering/repo-index.md`
- `docs/reverse-engineering/architecture-map.md`
- `docs/reverse-engineering/features-inventory.md`
- `docs/reverse-engineering/scopes/authentication-scope.md`
- `docs/reverse-engineering/traces/authentication-trace.md`
- `specs/authentication/spec.md`
- `specs/authentication/plan.md`
- `specs/authentication/tasks.md`
- `specs/authentication/evidence.md`
- `specs/authentication/open-questions.md`
- `specs/authentication/drift-report.md`

Validation checklist:

- Every requirement in `spec.md` points to evidence.
- Unknown behavior is captured in `open-questions.md`, not promoted into requirements.
- Repo-level docs remain concise and evidence-backed.
- Wikilinks and frontmatter are present where expected.
- Drift check does not silently rewrite the spec.

## Glossary

- `Feature`: a bounded slice of implemented product behavior.
- `Scope`: what is included and excluded before tracing.
- `Trace`: the concrete path through code, tests, data, and integrations.
- `Claim`: a statement about current system behavior.
- `Evidence`: source material supporting a claim.
- `Confirmed`: directly supported by source evidence.
- `Inferred`: strongly suggested, but not fully explicit.
- `Unknown`: not safely derivable from the codebase.

## Example prompts

### Initial scan

Use code-to-speckit to analyze this codebase in brownfield mode. First generate navigation hints, config guidance, repo index, and architecture map. Do not generate specs yet.

### Feature inventory

Use code-to-speckit to generate the inventory of implemented features. Each feature must include evidence and confidence.

### Feature docs

Use code-to-speckit to create scope, trace, evidence matrix, and Spec Kit docs for the feature Authentication.

### Obsidian output

Use code-to-speckit to make the Authentication documentation Obsidian-friendly.

### Drift check

Use code-to-speckit to check for drift between `specs/authentication` and the current codebase.
