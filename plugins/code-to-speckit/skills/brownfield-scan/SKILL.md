---
name: brownfield-scan
description: Generate a high-level repo index and architecture map for an existing codebase.
---

# Brownfield Scan

Analyze the repository in read-only mode and generate:

- `.code-to-speckit/navigation.md` if it does not exist
- `.code-to-speckit/config.md` if it does not exist
- `docs/reverse-engineering/repo-index.md`
- `docs/reverse-engineering/architecture-map.md`

## Rules

- Do not modify application source code.
- Do not generate feature specs yet.
- Do not invent system behavior.
- Use source evidence for architectural claims.
- Keep the repo index concise.
- Mark uncertainty explicitly.
- Treat `.code-to-speckit/config.md` as the local policy reference and create it when missing.
- For large repos, stay shallow and create navigation, repo index, and architecture map without attempting deep feature reconstruction.

## Process

1. Identify project type and stack.
2. Identify package or app layout.
3. Identify likely entry points.
4. Identify routing, API, and UI surfaces.
5. Identify data layer and integrations.
6. Identify tests and existing documentation.
7. Identify ignore paths.
8. Produce navigation hints, config guidance, repo index, and architecture map.

## Stop conditions

- If the repository layout is still unclear after the first pass, stop and record unknowns instead of guessing architecture.
- If likely generated or vendor directories dominate the repo, refine ignore paths before continuing deeper.

## Output guidance

- Use `templates/navigation.md` for navigation hints.
- Use `templates/config.md` for local policy guidance.
- Use `templates/repo-index.md` and `templates/architecture-map.md` as reference structures.
- If the repo is large, stay shallow and record unknowns instead of over-reading.
