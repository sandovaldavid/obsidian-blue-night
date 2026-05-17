# Blue Night (Kodev) Obsidian Theme

An elegant blue-themed Obsidian theme inspired by macOS UI/UX. Engineered for absolute focus, zero light bleed, and high cognitive efficiency.

## Features

- **macOS Aesthetic**: San Francisco-inspired typography, rounded corners, and glassmorphism.
- **Blue Night Palette**: Deep blue tones for dark mode and crisp slate for light mode.
- **Style Settings Integration**: Full customization via the [Style Settings](https://github.com/mgmeyers/obsidian-style-settings) plugin.
- **Productivity Focused**: Raycast-style command palette, circular checkboxes, and minimal status bar.

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

- `theme.css`: The main theme file containing all styles and Style Settings definitions.
- `manifest.json`: Obsidian theme metadata.
- `.pre-commit-config.yaml`: Configuration for linters and formatters.
- `environment.yml`: Conda environment definition.

## Customization

Install the **Style Settings** plugin in Obsidian to customize:

- Accent colors
- Background depths
- UI features (Raycast prompt, minimal sidebar, etc.)
