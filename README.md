# Blue Night — Obsidian Theme

A minimalist night-blue Obsidian theme with pastel accents. Catppuccin-inspired palette over a
deep night-blue base, engineered for low eye strain and a software developer's daily workflow.

## Features

- **Night Blue Palette**: `#0f1523` canvas with pastel accents (blue, lavender, teal, pink) in
  dark mode; crisp bluish slate in light mode. OLED black available as a toggle.
- **Pastel Syntax Highlighting**: Catppuccin-style code colors tuned for both modes.
- **Minimalist SVG Icons**: Embedded (offline, no network) icons for callouts, task checkboxes,
  and file-explorer folders/files — thin 1.75px strokes, mask-based so they follow your accent.
- **Extra Task States**: `[x]` done · `[-]` cancelled · `[/]` in progress · `[?]` question ·
  `[!]` important · `[>]` forwarded.
- **Raycast-Style Palette & Switcher**: Wide floating glass prompt with visible file paths,
  keyboard-hint pills, and soft accent selection.
- **Floating Status Bar**: Glass pill in the bottom-right corner, optional auto-hide.
- **Style Settings Integration**: Accent flavors, OLED mode, and every UI feature is a toggle via
  the [Style Settings](https://github.com/mgmeyers/obsidian-style-settings) plugin.
- **Plugin-Aware**: Extra styling for Dataview (inline fields, tables) and Quick Switcher++
  (paths, mode indicators, heading levels) that activates only when those plugins are installed.
- **Full Native Coverage**: Tables, Canvas (pastel node colors), global search highlights,
  settings modal, mobile adjustments, `prefers-reduced-motion`, and ink-friendly PDF export.

## Installation

### Manual

1. Copy `theme.css` and `manifest.json` into your vault at `.obsidian/themes/Blue Night/`.
1. In Obsidian go to **Settings → Appearance → Themes** and select **Blue Night**.

### As a snippet

If you only want the color tokens on top of another theme, copy `snippets/kodev-blue-night.css`
into `.obsidian/snippets/` and enable it under **Settings → Appearance → CSS snippets**.

### Optional snippets

Each file in `snippets/` is independent — copy the ones you want into `.obsidian/snippets/`:

| Snippet                | What it does                                                    |
| ---------------------- | --------------------------------------------------------------- |
| `kodev-blue-night.css` | Full color-token palette usable on any theme                    |
| `focus-mode.css`       | Hides ribbon, tabs and status bar until hovered (zen writing)   |
| `rainbow-folders.css`  | Tints each top-level folder with a different pastel             |
| `colored-headings.css` | Gives every heading level its own pastel color                  |
| `wide-code.css`        | Lets code blocks, tables and Dataview results exceed line width |

## Recommended plugins

- [Style Settings](https://github.com/mgmeyers/obsidian-style-settings) — unlocks accent flavors,
  OLED mode and all feature toggles.
- [Quick Switcher++](https://github.com/darlal/obsidian-switcher-plus) — note *preview while you
  navigate* the switcher is not possible with CSS alone; this plugin provides it and inherits the
  theme's prompt styling. The native Page Preview (hover a result with `Ctrl`/`Cmd`) is styled by
  the theme as a closer built-in alternative.

## Development Setup

This project uses `conda` and `pre-commit` for quality control.

### Prerequisites

- Conda or Mamba
- Node.js (for Prettier)

### Installation

1. Create the environment:

   ```bash
   conda env create -f environment.yml
   conda activate dotfiles
   ```

1. Install pre-commit hooks:

   ```bash
   pre-commit install
   ```

### Project Structure

- `theme.css`: The theme (palette, Style Settings block, embedded SVG assets).
- `manifest.json`: Obsidian theme metadata (version managed by Release Please).
- `versions.json`: Theme version → minimum Obsidian version map (manual, see below).
- `release-please-config.json` + `.release-please-manifest.json`: single-channel Release Please
  config — runs **only on `main`**.
- `.github/workflows/release-please.yml`: cuts releases and attaches `theme.css` +
  `manifest.json` as assets.
- `snippets/`: Standalone snippets usable with any theme.
- `themes/baseline.css`: Development reference only (not distributed).

### Branching & Releasing (Git Flow + Release Please)

- `develop` is the integration branch, `main` is the release branch. **Never commit directly to
  either** — always use an intermediate branch + PR.
- Release Please runs only on pushes to `main`. Merging `develop → main` triggers it; it opens a
  `chore(main): release X.Y.Z` PR; squash-merging that PR publishes the GitHub release with
  `theme.css` and `manifest.json` attached.

Merge method per PR type (prevents spurious version bumps from concatenated squash bodies):

| PR type                                    | Method       |
| ------------------------------------------ | ------------ |
| Feature/fix → `develop` (1-2 commits)      | Squash       |
| Feature/fix → `develop` (many commits)     | Rebase       |
| `develop → main` (sync)                    | Merge commit |
| `main → develop` (catch-up)                | Rebase       |
| Release Please PR (`chore(main): release`) | Squash       |

`versions.json` is updated by hand, and only when `minAppVersion` changes: add a
`"<new-theme-version>": "<min-app-version>"` entry in the same PR that changes the manifest.

## Customization

Install the **Style Settings** plugin in Obsidian to customize:

- Accent flavor (Night Blue / Lavender / Teal / Pink) and principal accent color
- Editor backgrounds per mode, plus OLED Black Mode
- UI features: Raycast prompt, minimalist explorer, metadata card, folder guides
- Content: premium headers, accent bullets, pill tags, circular checkboxes, IDE blockquotes
- Status bar: floating pill and auto-hide
