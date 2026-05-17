# Code-to-SpecKit Installation Guide

This guide explains how to install the `code-to-speckit` plugin as a repo-local Codex plugin.

## Prerequisites

- Codex must be available in your environment.
- The target repository should support repo-local plugins through `.agents/plugins/marketplace.json`.
- You should have permission to edit files inside the target repository.

## Expected layout

Install the plugin so your repository looks like this:

```text
<repo-root>/
  .agents/
    plugins/
      marketplace.json
  plugins/
    code-to-speckit/
```

## Install steps

1. Open the target repository root and confirm that repo-local plugins are expected to live under `plugins/` and be registered through `.agents/plugins/marketplace.json`.
2. If the repository does not already contain a `plugins/` directory, create it at the repository root.
3. Copy the entire `plugins/code-to-speckit/` directory into the target repository so the final path becomes `plugins/code-to-speckit/`.
4. Verify that the copied plugin folder still contains `.codex-plugin/plugin.json`, `AGENTS.md`, `README.md`, `skills/`, `templates/`, and `examples/`.
5. If the repository does not already contain `.agents/plugins/`, create that directory structure.
6. Open `.agents/plugins/marketplace.json` if it already exists. If it does not exist, create it as a JSON file.
7. Register the plugin in the `plugins` array.
8. If the file already contains other plugins, append the new entry without deleting or renaming the existing ones.
9. Point the plugin entry to the repo-local path `./plugins/code-to-speckit`.
10. Save the file and make sure the JSON is still valid, with commas and brackets in the correct places.
11. Reload the repository in Codex, or restart Codex if your environment caches plugin metadata on startup.
12. After reload, verify that Codex can see the plugin and its skills before starting a documentation workflow.

### Detailed procedure

Use this checklist if you want the installation process in a more operational form:

1. From the source repository, copy `plugins/code-to-speckit/`.
2. Paste it into the target repository under `plugins/`.
3. Confirm the final structure matches:

```text
<repo-root>/
  .agents/
    plugins/
      marketplace.json
  plugins/
    code-to-speckit/
      .codex-plugin/
        plugin.json
      AGENTS.md
      README.md
      skills/
      templates/
      examples/
```

4. Open `.agents/plugins/marketplace.json`.
5. If the file is new, create a top-level object with a `plugins` array.
6. Add a local plugin entry for `code-to-speckit`.
7. Save the file and reopen the repository in Codex.
8. Run a simple prompt that explicitly references the plugin to confirm it loads correctly.

## Example marketplace entry

The repository root in this project uses a richer marketplace shape. If your target repository follows the same format, add an entry like this:

```json
{
  "name": "local-repo",
  "interface": {
    "displayName": "Local Repo Plugins"
  },
  "plugins": [
    {
      "name": "code-to-speckit",
      "source": {
        "source": "local",
        "path": "./plugins/code-to-speckit"
      },
      "policy": {
        "installation": "AVAILABLE",
        "authentication": "ON_INSTALL"
      },
      "category": "Productivity"
    }
  ]
}
```

If your Codex setup accepts a simpler marketplace format, a minimal local entry that resolves to the plugin directory can also look like this:

```json
{
  "plugins": [
    {
      "id": "code-to-speckit",
      "path": "./plugins/code-to-speckit"
    }
  ]
}
```

If your repository already contains a marketplace file, add the plugin entry without removing existing plugins.

## Common checks and mistakes

- Do not copy only `skills/` or only `.codex-plugin/`; copy the full `plugins/code-to-speckit/` directory.
- The path in `marketplace.json` should usually be relative to the repository root: `./plugins/code-to-speckit`.
- Keep the folder name and the marketplace path aligned. If you rename the directory, update the path accordingly.
- If Codex does not detect the plugin after installation, first validate `marketplace.json`, then reload the workspace.
- If the plugin loads but skills are missing, re-check that `plugins/code-to-speckit/.codex-plugin/plugin.json` still points to `"skills": "./skills/"`.

## Optional project guidance files

For better results when analyzing a brownfield codebase, you can also create:

- `.code-to-speckit/navigation.md`
- `.code-to-speckit/config.md`

These files help Codex understand project structure, conventions, and documentation preferences.

## Verify the installation

After installation, confirm that the plugin contains:

- `AGENTS.md`
- `README.md`
- `skills/`
- `templates/`
- `examples/`

Then verify behavior in Codex with a small smoke test, for example:

- "Use code-to-speckit and list the available brownfield workflows in this repo."
- "Use code-to-speckit to analyze this codebase in brownfield mode."

If those prompts work, the plugin is installed and discoverable. You can then continue with workflows such as:

- "Use code-to-speckit to analyze this codebase in brownfield mode."
- "Use code-to-speckit to generate the inventory of implemented features."

## Related documentation

- `code-to-speckit-codex-spec.md` for the full plugin specification
- `examples/prompts.md` for prompt examples
- `README.md` for workflow and output expectations
