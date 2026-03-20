# Plugin Authoring Skill (Playground)

Use this skill to bootstrap a new JupyterLab plugin inside **Plugin Playground** and iterate quickly.

## Goal

Produce a working plugin source file that can be loaded with `Load Current File As Extension`, using extension points and examples already available in the running environment.

## Inputs

- Desired behavior (what the plugin should do)
- Optional UI target (command palette, sidebar, status bar, notebook, etc.)
- Optional package constraints (JupyterLab-only APIs vs external AMD modules)

## Workflow

1. Discover available extension points

- Run `plugin-playground:list-tokens` to get available tokens.
- Run `plugin-playground:list-commands` to get available commands.
- Use optional `query` argument to narrow results:
  - `app.commands.execute('plugin-playground:list-tokens', { query: 'status' })`
  - `app.commands.execute('plugin-playground:list-commands', { query: 'notebook' })`

2. Discover reference examples

- Run `plugin-playground:list-extension-examples`.
- Filter by topic with `query` (for example `toolbar`, `commands`, `widget`, `notebook`).
- Open the selected example code/README from the sidebar for implementation details.

3. Scaffold plugin code

- Start from a minimal `const plugin = { id, autoStart, activate }` shape.
- Add `requires` tokens only after confirming token availability from step 1.
- Add commands with stable IDs (`<namespace>:<action>`).

4. Load and iterate

- Run `Load Current File As Extension`.
- Validate behavior in UI.
- If reloading same plugin ID, ensure cleanup is handled by plugin `deactivate()` where needed.

5. Imports and module safety

- Prefer JupyterLab/Lumino imports first.
- For external packages, ensure AMD-compatible import targets are used.
- Avoid Node/Webpack-only modules that are not AMD-compatible.

## Output expectations

- Single plugin source file (`.ts`)
- Clear command IDs and labels
- Minimal required tokens
- No unused imports

## References

- JupyterLab Extension Tutorial:
  - https://jupyterlab.readthedocs.io/en/stable/extension/extension_tutorial.html
- JupyterLab Extension Examples:
  - https://github.com/jupyterlab/extension-examples
