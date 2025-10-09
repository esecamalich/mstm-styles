# @mstm/mstm-styles

Shared CSS tokens, global styles, and utilities for Make Stuff That Matters projects. Install it wherever you need consistent theming, spacing, and component primitives.

## Installation

### From this monorepo

```bash
npm install --save file:packages/mstm-styles
```

### From a remote Git source

```bash
npm install github:esecamalich/makeStuffThatMatters#main -- @mstm/mstm-styles
```

If you publish the package to a private registry, install it as you would any scoped dependency:

```bash
npm install --save @mstm/mstm-styles
```

## Usage

The package default export is `src/global.css`, which already imports all tokens and utilities. In Astro, add a side-effect import in your root layout:

```astro
---
import '@mstm/mstm-styles';
---
```

### Themes

Core theme variables live in `src/themes/`. `global.css` imports every theme so they are all available by default. If you want to include only one theme layer or compose your own bundle:

```css
@import '@mstm/mstm-styles/src/tokens/colors.css';
@import '@mstm/mstm-styles/src/tokens/spacing.css';
@import '@mstm/mstm-styles/src/utilities/layout.css';
@import '@mstm/mstm-styles/src/themes/sage.css'; /* or dark.css, base.css */
```

### Direct exports

An exports map is configured so you can reach common sub-entries without touching internal paths:

```css
@import '@mstm/mstm-styles/themes/dark';
@import '@mstm/mstm-styles/tokens/colors';
@import '@mstm/mstm-styles/utilities/layout';
```

If you want to compose a custom bundle, mix and match from these public entry points.

## Development

### Working locally

1. Make CSS changes inside `packages/mstm-styles/src/` (this is the single source of truth).
2. In the root project, reinstall the dependency so it picks up local edits:
   ```bash
   npm install --save file:packages/mstm-styles
   ```
3. Import the bundle in your Astro layout:
   ```astro
   ---
   import '@mstm/mstm-styles';
   ---
   ```
4. Run `npm run dev` to verify the consuming app renders correctly.

### Release checklist

Run these steps from `packages/mstm-styles/` whenever you’re ready to share updates:

1. `npm test` (currently a no-op) — replace with real lint/build checks when available.
2. `npm pack` — confirms only the right files are included.
3. `npm version patch|minor|major` — choose the appropriate bump.
4. Commit the changes, push, and tag as needed.
5. Publish or distribute:
   - Private registry: `npm publish --access=restricted`
   - Git/tarball consumers: push the tag and reinstall using the tag or generated `.tgz`

### Updating consuming projects

- Using a published version: run `npm install @mstm/mstm-styles@latest` (or `npm update`) in each project.
- Using a Git source: reinstall with the new tag, e.g. `npm install github:esecamalich/makeStuffThatMatters#v0.1.1`.
- Using a local file link: rerun `npm install file:packages/mstm-styles` so npm refreshes the symlinked package.

Keep all edits centralized here; downstream projects should never modify their own copies of these styles.

## License

UNLICENSED – All rights reserved. Contact Sergio Camalich for usage outside internal projects.
