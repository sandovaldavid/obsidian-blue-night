# Blue Night

A minimalist night-blue theme for Obsidian with Catppuccin-inspired pastel accents. Engineered
for low eye strain and a software developer's daily workflow.

![Blue Night theme screenshot](https://raw.githubusercontent.com/sandovaldavid/obsidian-blue-night/main/screenshot.png)

**Website**: [sandovaldavid.github.io/obsidian-blue-night](https://sandovaldavid.github.io/obsidian-blue-night/)

## Features

- **Night Blue Palette** — deep `#0f1523` canvas with pastel accents (blue, lavender, teal,
  pink) in dark mode; crisp bluish slate in light mode.
- **Preset Flavors** — dark canvas variants (Blue Night, Dark Charcoal/OLED, Cozy Pastels) and
  light variants (Clean Blue, Cozy Pastels Light).
- **Pastel Syntax Highlighting** — Catppuccin-style code colors tuned for both modes, with a
  language badge on code blocks.
- **Minimalist SVG Icons** — embedded, fully offline icons for callouts, task checkboxes,
  file-explorer folders/files, and the vault name. Thin 1.75px strokes, mask-based so they
  follow your accent color.
- **Extra Task States** — `[x]` done · `[-]` cancelled · `[/]` in progress · `[?]` question ·
  `[!]` important · `[>]` forwarded.
- **Raycast-Style Palette & Switcher** — wide floating glass prompt with visible file paths,
  keyboard-hint pills, and soft accent selection.
- **Floating Status Bar** — glass pill in the bottom-right corner, with optional auto-hide.
- **Plugin-Aware** — extra styling for Dataview (inline fields, tables) and Quick Switcher++
  (paths, mode indicators, heading levels) that activates only when those plugins are installed.
- **Full Native Coverage** — tables, Canvas (pastel node colors), global search highlights,
  settings modal, mobile adjustments, `prefers-reduced-motion`, and ink-friendly PDF export.

## Installation

### From the community theme store

Search for **Blue Night** under **Settings → Appearance → Themes → Manage** (once the theme is
published to the gallery).

### Manual

1. Download `theme.css` and `manifest.json` from the
   [latest release](https://github.com/sandovaldavid/obsidian-blue-night/releases/latest).
1. Copy both files into your vault at `.obsidian/themes/Blue Night/`.
1. In Obsidian go to **Settings → Appearance → Themes** and select **Blue Night**.

## Customization

Install the [Style Settings](https://github.com/mgmeyers/obsidian-style-settings) plugin to
customize:

- Accent flavor (Night Blue / Lavender / Teal / Pink) and principal accent color
- Preset canvas variants — dark: Blue Night, Dark Charcoal/OLED, Cozy Pastels; light: Clean Blue,
  Cozy Pastels Light — plus custom editor backgrounds per mode
- UI features: Raycast prompt, minimalist explorer, metadata card, folder guides, vault name icon
- Content: premium headers, accent bullets, pill tags, circular checkboxes, IDE blockquotes
- Status bar: floating pill and auto-hide

## Optional snippets

Each file in [`snippets/`](https://github.com/sandovaldavid/obsidian-blue-night/tree/main/snippets)
is independent — copy the ones you want into `.obsidian/snippets/` and enable them under
**Settings → Appearance → CSS snippets**:

| Snippet                 | What it does                                                    |
| ----------------------- | --------------------------------------------------------------- |
| `focus-mode.css`        | Hides ribbon, tabs and status bar until hovered (zen writing)   |
| `rainbow-folders.css`   | Tints each top-level folder with a different pastel             |
| `colored-headings.css`  | Gives every heading level its own pastel color                  |
| `wide-code.css`         | Lets code blocks, tables and Dataview results exceed line width |
| `clean-embeds.css`      | Removes borders and padding from note embeds (seamless)         |
| `image-grid.css`        | Lays out consecutive images in a responsive grid                |
| `minimal-scrollbar.css` | Ultra-thin rounded scrollbars that blend into the theme         |

## Recommended plugins

- [Style Settings](https://github.com/mgmeyers/obsidian-style-settings) — unlocks accent flavors,
  preset canvas variants and all feature toggles.
- [Quick Switcher++](https://github.com/darlal/obsidian-switcher-plus) — note *preview while you
  navigate* the switcher is not possible with CSS alone; this plugin provides it and inherits the
  theme's prompt styling. The native Page Preview (hover a result with `Ctrl`/`Cmd`) is styled by
  the theme as a closer built-in alternative.

## Contributing

Development setup, project structure, and the branching/release flow are documented in
[CONTRIBUTING.md](https://github.com/sandovaldavid/obsidian-blue-night/blob/main/CONTRIBUTING.md).

## License

[MIT](https://github.com/sandovaldavid/obsidian-blue-night/blob/main/LICENSE)
