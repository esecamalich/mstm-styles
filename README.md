
# mstm-styles

This repository contains the official mstm-styles package (shared CSS tokens, global styles, themes and utility classes) used by Make Stuff That Matters projects.

Repository: https://github.com/esecamalich/mstm-styles

Quick summary:
- Centralized design tokens in `src/tokens/` (colors, spacing, typography, etc.)
- Theme layers in `src/themes/` (base, dark, sage)
- Utility and component primitives in `src/utilities/`
- A single entrypoint `src/global.css` that composes tokens, utilities and themes for a default bundle

## Installation

Install directly from the GitHub repository (recommended for latest changes):

```bash
npm install github:esecamalich/mstm-styles#main
```

If the package is published to a registry in the future, install it as a normal scoped package:

```bash
npm install @mstm/mstm-styles
```

For local development (consume the local copy from another project):

```bash
npm install --save file:../path-to-local/mstm-styles
```

## Usage

The package exposes `src/global.css` as the default convenience bundle. Import it as a side effect in your app's root (JS/TS) or framework entry:

```js
// JavaScript / frameworks
import 'mstm-styles/src/global.css';

/* Or, if installed from GitHub and your bundler resolves package paths: */
import 'github:esecamalich/mstm-styles/src/global.css';
```

You can also import individual token files or theme layers if you want a smaller, composed bundle:

```css
@import 'mstm-styles/src/tokens/colors.css';
@import 'mstm-styles/src/tokens/spacing.css';
@import 'mstm-styles/src/utilities/layout.css';
@import 'mstm-styles/src/themes/sage.css'; /* choose base, dark or sage */
```

Notes:
- Depending on how you install (npm registry vs GitHub source) and your bundler configuration, you may need to reference the `src/` paths directly. The repository ships the raw CSS source files.

## Project structure

Top-level `src/` contains the library source:

- `src/global.css` — main composition file that imports tokens, utilities and themes
- `src/themes/` — theme layer files (`base.css`, `dark.css`, `sage.css`)
- `src/tokens/` — design tokens (`colors.css`, `spacing.css`, `typography.css`, etc.)
- `src/utilities/` — utility classes and small component primitives (`buttons.css`, `layout.css`, `typography.css`)

Use these files as building blocks for composing styles in consuming projects.

## Development

Make edits directly in `src/`. Recommended local workflow:

1. Create a branch for your change: `git checkout -b feat/your-change`.
2. Edit the relevant CSS files inside `src/`.
3. Run any local checks or your app's dev server to verify the styles in-context.
4. Commit and push your branch and open a pull request against `main`.

If you need to test these styles from another local project, use one of the following:

- Install via local path: `npm install --save file:../path-to-local/mstm-styles`
- Or use `npm link` from the `mstm-styles` folder and `npm link mstm-styles` in the consumer project.

## Contributing

Contributions are welcome via pull requests. Please include a short description of the change and any visual diffs if applicable.

Suggested PR checklist:
- Update or add token documentation when changing tokens
- Keep changes focused and small (tokens, utilities, or themes)
- Include a changelog entry in your PR description

## Updating the dependency from consuming repos

If you maintain projects that consume `mstm-styles`, here are recommended steps to update the dependency depending on how the project installed it.

1) Installed from npm registry (future)

- Update package.json in the consuming repo to the new version and run:

```bash
npm install @mstm/mstm-styles@latest
```

- Or run `npm update @mstm/mstm-styles`.

2) Installed directly from GitHub (recommended for latest changes)

- To update to the latest main branch commit:

```bash
npm install github:esecamalich/mstm-styles#main
```

- To update to a specific tag/release replace `#main` with the tag, e.g. `#v1.2.3`.

3) Installed via a Git URL in package.json

- If package.json references a specific commit or branch, update the reference and run `npm install`.

4) Local file install (file:../path)

- Reinstall from the updated local path so npm refreshes the package contents:

```bash
npm install --save file:../path-to-local/mstm-styles
```

- If you prefer a symlinked workflow, use `npm link` (see below).

5) Using npm link (local development)

- In the `mstm-styles` repo root run:

```bash
npm link
```

- In the consuming repo run:

```bash
npm link mstm-styles
```

- When you make local changes in `mstm-styles`, most bundlers will pick them up automatically. If not, rebuild the consumer app or clear caches.

6) Verification after updating

- Clear node_modules and reinstall in the consumer project when in doubt:

```bash
rm -rf node_modules package-lock.json && npm install
```

- Verify the imported CSS is the expected version (search for tokens or theme variables you changed) and run the consumer project's dev server to visually confirm.

Tips and notes
- Prefer pinned tags or released versions for production deployments to avoid accidental breaking changes from main branch updates.
- For CI, prefer installing by tag or from the registry to get reproducible installs.
- If consumers import `src/` paths directly, ensure any changes that rename or move files are reflected in consuming repos.

## License

UNLICENSED — all rights reserved. Contact the repository owner for reuse outside internal projects.
