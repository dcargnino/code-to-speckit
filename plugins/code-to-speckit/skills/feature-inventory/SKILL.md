---
name: feature-inventory
description: Generate an inventory of implemented features from a brownfield codebase.
---

# Feature Inventory

Use repo index, architecture map, tests, routes, UI surfaces, and source files to identify implemented features.

Generate:

`docs/reverse-engineering/features-inventory.md`

## Rules

- List only features with evidence.
- Separate implemented, partially implemented, and unclear features.
- Include confidence level.
- Include source evidence and tests.
- Do not generate feature specs yet.
- If a feature candidate has no direct evidence, leave it out or mark it as unclear with explicit gaps.

## Stop conditions

- If repo index or architecture map is missing, create them first.
- If feature boundaries remain too fuzzy, stop at candidate listing and ask for scope selection rather than inventing a cleaned-up inventory.

## Process

1. Review repo index and architecture map.
2. Group real behavior into feature candidates.
3. Keep only candidates with direct evidence.
4. Mark uncertainty with status and confidence.
5. Capture open questions per feature.

## Output guidance

Use `templates/features-inventory.md` as the reference structure.
