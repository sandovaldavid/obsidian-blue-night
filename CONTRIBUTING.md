# Contributing to Blue Night

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

## Project Structure

- `theme.css`: The theme (palette, Style Settings block, embedded SVG assets).
- `manifest.json`: Obsidian theme metadata (version managed by Release Please).
- `versions.json`: Theme version → minimum Obsidian version map (manual, see below).
- `release-please-config.json` + `.release-please-manifest.json`: single-channel Release Please
  config — runs **only on `main`**.
- `.github/workflows/release-please.yml`: cuts releases and attaches `theme.css` +
  `manifest.json` as assets.
- `snippets/`: Standalone snippets usable with any theme.
- `spec/`: Design specification and requirements.
- `docs/`: Jekyll landing page, deployed to
  [GitHub Pages](https://sandovaldavid.github.io/obsidian-blue-night/) on every push to `main`
  that touches this folder.

## Commit Convention

Conventional Commits 1.0.0 with a **required scope** and no emojis, enforced by a commitizen
pre-commit hook: `type(scope): imperative description`.

## Branching & Releasing (Git Flow + Release Please)

- `develop` is the integration branch, `main` is the release branch. **Never commit directly to
  either** — always use an intermediate branch + PR.
- Release Please runs only on pushes to `main`. Merging `develop → main` triggers it; it opens a
  `chore(main): release X.Y.Z` PR; squash-merging that PR publishes the GitHub release with
  `theme.css` and `manifest.json` attached.
- Merged PR branches are deleted automatically; `main` and `develop` are protected against
  deletion and force-pushes by repository rulesets.

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

## Testing changes

Copy `theme.css` and `manifest.json` into a test vault at `.obsidian/themes/Blue Night/` and
reload Obsidian (`Ctrl+R`). Verify both dark and light modes, every preset flavor, and the
Style Settings toggles.
