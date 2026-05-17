# Privacy Policy

Code-to-SpecKit is distributed as a repo-local Codex plugin.

## Data handling

- The plugin is designed to operate on the files available in the repository where it is installed.
- In `v0.1`, the plugin does not require a dedicated backend service or MCP server.
- Output is generated as Markdown files inside the target repository.

## Responsibilities

- Repository owners are responsible for deciding which codebases and documents are analyzed with this plugin.
- Users should avoid running the plugin on repositories that contain data they are not authorized to inspect.
- Any network behavior is determined by the Codex runtime or hosting environment, not by this plugin bundle itself.

## Stored data

- This repository does not include a standalone data collection service.
- Generated documents are stored only where the user chooses to save them.

## Contact

For repository-specific questions, use the repository homepage or maintainer contact listed in `.codex-plugin/plugin.json`.
