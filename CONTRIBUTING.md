# Contributing to Blue Night

## Development setup

This project uses `conda` and `pre-commit` for repository quality checks.

### Prerequisites

- Conda or Mamba
- Node.js (for formatting tooling)
- Obsidian 1.12.7 or newer
- A disposable test vault

### Installation

1. Create the environment:

   ```bash
   conda env create -f environment.yml
   conda activate dotfiles
   ```

2. Install pre-commit hooks:

   ```bash
   pre-commit install
   ```

## Project structure

- `theme.css`: production theme, Style Settings metadata, palette, and local SVG assets.
- `manifest.json`: Obsidian theme metadata; the version is managed by Release Please.
- `release-please-config.json` + `.release-please-manifest.json`: single-channel Release Please
  configuration; releases run only from `main`.
- `.github/workflows/release-please.yml`: creates releases and attaches `theme.css` and
  `manifest.json`, matching Obsidian's theme distribution contract.
- `snippets/`: standalone optional snippets usable with Blue Night or other themes.
- `spec/`: current design and compatibility specification.
- `docs/`: Jekyll landing page deployed from `main`.

`versions.json` is intentionally not used. Obsidian documents that fallback map as part of the
community **plugin** compatibility flow. A theme release is distributed through the version in
`manifest.json` plus the matching GitHub release assets.

## CSS architecture rules

Blue Night follows the official Obsidian theme guidance:

01. Prefer documented CSS variables over direct component selectors.
02. Put shared variables under `body`; put mode-specific colors under `.theme-dark` and
    `.theme-light`.
03. Keep selectors low-specificity. Direct DOM selectors are reserved for optional enhancements
    that cannot be expressed with public variables.
04. Never use `!important`. Users must remain able to override the theme with snippets.
05. Keep every asset local. Do not add remote fonts, images, stylesheets, or runtime network calls.
06. Do not override global input padding or other geometry owned by Obsidian unless no public
    variable exists and the selector is narrowly scoped.
07. Do not change vertical margins on CodeMirror/Live Preview lines. Use padding for decorative
    heading spacing to avoid cursor and virtualization issues.
08. Treat classes such as `.workspace-*`, `.cm-*`, `.metadata-*`, and plugin-specific classes as
    implementation details. An upstream class change should disable only the enhancement, not the
    underlying UI.
09. Do not reproduce File Explorer child indentation or guide placement with custom
    `margin`/`padding`/`border` geometry. Use Obsidian's `--nav-item-children-*` and
    `--nav-indentation-guide-*` variables.
10. Bundled snippets must not rely on undocumented custom properties when a documented component
    variable exists. If no variable exists, keep any direct selector narrow and presentation-only.

### Accent contract

`--accent-h`, `--accent-s`, and `--accent-l` are the single runtime source of truth for the
interactive accent.

Style Settings exposes a `class-select` named `bn-accent-flavor` with these choices:

- `bn-accent-blue-night`;
- `bn-accent-sapphire`;
- `bn-accent-lavender`;
- `bn-accent-mauve`;
- `bn-accent-teal`;
- `bn-accent-pink`;
- `bn-accent-peach`;
- `bn-accent-custom`.

Each preset class may set only the native `--accent-h`, `--accent-s`, and `--accent-l` primitives.
Named light-mode variants may lower only `--accent-l` to meet contrast targets while preserving the
same hue/saturation and the same native accent sink. The Custom picker uses `id: bn-custom-accent`
with `format: hsl-split`, producing `--bn-custom-accent-h`, `--bn-custom-accent-s`, and
`--bn-custom-accent-l`. Only `body.bn-accent-custom` maps those custom values into the native accent
primitives.

This arrangement lets presets and a custom picker coexist without competing CSS sources.

Do not reintroduce independently consumed accent systems such as `--color-accent-base`, custom
`--color-accent-1` values, or `--accent-rgb`. If a compatibility alias is ever required, derive it
from the native HSL source of truth.

The Catppuccin-inspired supporting palette (`--bn-blue`, `--bn-purple`, `--bn-cyan`,
`--bn-green`, `--bn-yellow`, `--bn-orange`, `--bn-red`, `--bn-pink`) is separate from the
interactive accent. Switching accents must not flatten syntax or semantic states into one color.
Dark and light modes may use different values for those support tokens so text-level uses remain
legible on their respective canvases.

### Canvas contract

Canvas variants are independent from the selected accent. Dark variants are Blue Night, Midnight
Navy, Storm Blue, Dark Charcoal/OLED, and Cozy Pastels. Light variants are Clean Blue, Blue Mist,
and Cozy Pastels Light.

A canvas class may override background/base palette tokens plus closely related surface tokens such
as `--code-background` and `--glass-bg`. It must not write `--accent-h`, `--accent-s`, or
`--accent-l`. This separation lets every canvas combine with every accent without duplicated preset
classes.

### Contrast contract

For bundled presets, theme-owned normal-sized text roles should target at least **4.5:1** against
the primary, secondary, and elevated surfaces where they appear. Include `--text-faint`, syntax
comments, semantic/support colors used as text, and named accents used for links/tags/selected text.
Custom accent values are user-controlled and are not covered by this guarantee.

### Callout compatibility

Do not wrap `--callout-color` with `rgb(...)`. Obsidian 1.13 changed `--callout-color` from an RGB
triplet to a complete valid CSS color. Blue Night therefore styles callouts through documented
callout variables and leaves icon/color rendering to Obsidian.

## Commit convention

Use Conventional Commits 1.0.0 with a required scope and no emojis, enforced by the repository
commitizen/pre-commit configuration:

```text
<type>(<scope>): imperative description
```

## Branching and releasing

- `develop` is the integration branch and `main` is the release branch. Never commit directly to
  either; use an intermediate branch and PR.
- Release Please runs only on pushes to `main`. Merging `develop → main` opens a
  `chore(main): release X.Y.Z` PR when releasable commits exist.
- The release workflow attaches `theme.css` and `manifest.json` to the GitHub release.
- Merged PR branches are deleted automatically; `main` and `develop` are protected against
  deletion and force-pushes. Both branches allow merge commit and squash only.

Merge method per PR type — never squash a multi-commit integration PR when its individual
Conventional Commit markers need to remain visible to Release Please:

| PR type                                    | Method       |
| ------------------------------------------ | ------------ |
| Feature/fix → `develop` (1-2 commits)      | Squash       |
| Feature/fix → `develop` (many commits)     | Merge commit |
| `develop → main` (sync)                    | Merge commit |
| `main → develop` (catch-up)                | Merge commit |
| Release Please PR (`chore(main): release`) | Squash       |

When a theme change requires a newer Obsidian version, update `minAppVersion` in `manifest.json`
in the same PR and explain the dependency in the PR description.

## Testing changes

Copy `theme.css` and `manifest.json` into a disposable vault at:

```text
.obsidian/themes/Blue Night/
```

Reload Obsidian after CSS changes. Restart Obsidian after changing `manifest.json`.

### Required visual matrix

Verify at minimum:

- dark and light mode;
- Blue Night, Midnight Navy, Storm Blue, Dark Charcoal/OLED, and Cozy Pastels dark canvases;
- Clean Blue, Blue Mist, and Cozy Pastels Light light canvases;
- Blue Night, Sapphire, Lavender, Mauve, Teal, Pink, and Peach accent flavors;
- Custom accent flavor plus multiple custom picker values;
- switching between preset accents and Custom without stale styles;
- switching between canvas variants without changing the selected accent;
- representative cross-axis combinations, including Midnight Navy + Sapphire, Storm Blue + Peach,
  OLED + Mauve, Cozy Pastels + Teal, and Blue Mist + Pink;
- named accent text/selected-state contrast across every light canvas;
- `text-faint`, code comments, supporting semantic colors, checkboxes, and navigation icons across
  every bundled canvas;
- nested File Explorer folders with Folder Indent Guides both enabled and disabled; verify the
  native guide stays aligned at every nesting level;
- syntax and semantic supporting colors remain multi-color under every accent flavor;
- editor Source mode, Live Preview, and Reading view;
- file explorer, tabs, ribbon, prompts, properties, tags, callouts, task states, tables, search,
  Canvas, and status bar;
- each bundled snippet in its intended view/mode, especially compact tables in Reading/Live Preview
  and colored headings/rainbow folders/math in every light canvas;
- keyboard focus and navigation states;
- desktop and mobile-responsive behavior;
- reduced-motion mode;
- PDF/print output;
- theme with Style Settings disabled;
- Dataview and Quick Switcher++ both absent and installed.

### Compatibility matrix

For releases, test against:

1. the latest public Obsidian release;
2. the latest Catalyst build when it contains announced developer/theme breaking changes.

A Catalyst-only regression must not force the public `minAppVersion` upward until the affected
Obsidian version is public, but the theme should be forward-compatible when a safe compatibility
path exists.

### Static checks

Before opening a PR:

```bash
pre-commit run --all-files
```

Also inspect `theme.css` and bundled snippets for accidental `!important`, remote `url(http...)`
assets, independently consumed duplicate accent systems, canvas classes that write native accent
primitives, manual `.nav-folder-children` guide geometry, undocumented custom properties that are
expected to control Obsidian components, and broad global selectors that override native component
geometry.
