---
name: obsidian-output
description: Make generated Spec Kit documentation Obsidian-friendly with frontmatter, tags, and wikilinks.
---

# Obsidian Output

Use this skill when writing or updating generated Markdown intended for Obsidian.

## Rules

- Add YAML frontmatter to generated Markdown under `docs/reverse-engineering/` and `specs/`.
- Add stable tags.
- Add relative wikilinks among `spec`, `plan`, `tasks`, `evidence`, and `open-questions`.
- Keep Markdown readable outside Obsidian.
- Avoid plugin-specific Obsidian syntax unless optional.
- Keep `.code-to-speckit/navigation.md` and `.code-to-speckit/config.md` lightweight unless the user wants them formalized too.

## Process

1. Check all generated Markdown files for frontmatter.
2. Normalize tags and feature slug usage.
3. Add or repair wikilinks.
4. Keep headings plain and portable.

## Output guidance

Use the frontmatter and related-link patterns shown in the templates.
