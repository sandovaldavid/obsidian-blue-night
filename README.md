# Blue Night

A minimalist night-blue theme for Obsidian with Catppuccin-inspired pastel accents. Engineered
for low eye strain and a software developer's daily workflow.

![Blue Night theme screenshot](https://raw.githubusercontent.com/sandovaldavid/obsidian-blue-night/main/screenshot.png)

**Website**: [sandovaldavid.github.io/obsidian-blue-night](https://sandovaldavid.github.io/obsidian-blue-night/)

## Compatibility

Blue Night targets **Obsidian 1.12.7 or newer**. The theme is built primarily on Obsidian's
public CSS variables and keeps DOM-dependent selectors isolated to optional visual enhancements.
This reduces breakage when Obsidian changes internal markup or component nesting.

The theme also avoids the legacy `rgb(var(--callout-color))` pattern so callouts remain compatible
with the CSS-color contract introduced in Obsidian 1.13.

## Features

- **Night Blue Palette** — deep `#0f1523` canvas with pastel accents in dark mode and a crisp
  bluish slate palette in light mode.
- **Selectable Accent Flavors** — Blue Night, Sapphire, Lavender, Mauve, Teal, Pink, Peach, or
  Custom. Every choice feeds the same native `--accent-h`, `--accent-s`, and `--accent-l`
  variables used by Obsidian, so tabs, links, graph focus, tags, prompts, and Blue Night
  enhancements stay synchronized. Named light-mode presets keep their hue while using
  contrast-tuned lightness values.
- **Catppuccin-Inspired Supporting Palette** — blue, lavender, cyan, green, yellow, peach, red, and
  pink remain available for syntax highlighting and semantic states regardless of the selected
  interactive accent. Light mode uses darker counterparts so text-level uses stay readable.
- **Preset Flavors** — dark canvas variants (Blue Night, Midnight Navy, Storm Blue, Dark
  Charcoal/OLED, Cozy Pastels) and light variants (Clean Blue, Blue Mist, Cozy Pastels Light)
  without replacing the selected accent.
- **Pastel Syntax Highlighting** — Catppuccin-inspired code colors tuned for both modes.
- **Minimalist SVG Icons** — embedded, fully offline icons for task checkboxes, file-explorer
  folders/files, and the vault name. Callouts intentionally retain Obsidian's native icon system
  for forward compatibility.
- **Extra Task States** — `[x]` done · `[-]` cancelled · `[/]` in progress · `[?]` question ·
  `[!]` important · `[>]` forwarded.
- **Raycast-Style Palette & Switcher** — floating prompt styling layered on top of Obsidian's
  documented prompt variables.
- **Floating Status Bar** — glass pill in the bottom-right corner on desktop, with optional fade.
- **Plugin-Aware** — extra styling for Dataview and Quick Switcher++ that remains inert when those
  plugins are not installed.
- **Responsive & Accessible** — contrast-tuned bundled palettes, mobile adjustments,
  keyboard-focus-aware states, `prefers-reduced-motion`, and ink-friendly PDF export.

## Installation

### From the community theme store

Search for **Blue Night** under **Settings → Appearance → Themes → Manage** once the theme is
published to the gallery.

### Manual

1. Make sure you are running Obsidian **1.12.7 or newer**.
1. Download `theme.css` and `manifest.json` from the
   [latest release](https://github.com/sandovaldavid/obsidian-blue-night/releases/latest).
1. Copy both files into your vault at `.obsidian/themes/Blue Night/`.
1. In Obsidian go to **Settings → Appearance → Themes** and select **Blue Night**.

## Customization

Install the [Style Settings](https://github.com/obsidian-community/obsidian-style-settings) plugin
to customize:

- Accent Flavor: Blue Night, Sapphire, Lavender, Mauve, Teal, Pink, Peach, or Custom
- Custom Accent Color, used only when `Accent Flavor = Custom`
- Preset canvas variants — dark: Blue Night, Midnight Navy, Storm Blue, Dark Charcoal/OLED, Cozy
  Pastels; light: Clean Blue, Blue Mist, Cozy Pastels Light — plus custom editor backgrounds per
  mode
- UI features: Raycast prompt, minimalist explorer, metadata card, folder guides, vault name icon
- Content: premium headers, accent bullets, pill tags, circular checkboxes, IDE blockquotes
- Status bar: floating pill and optional fade-until-hover behavior

Accent flavors and canvas variants are intentionally independent. For example, you can use
Midnight Navy with Sapphire, Storm Blue with Peach, Dark Charcoal/OLED with Mauve, or Blue Mist
with Teal. The selected accent changes interactive emphasis while the Catppuccin-inspired
supporting palette remains multi-color.

Blue Night still works without Style Settings; the plugin only exposes the optional controls.

## Optional snippets

Each file in [`snippets/`](https://github.com/sandovaldavid/obsidian-blue-night/tree/main/snippets)
is independent — copy the ones you want into `.obsidian/snippets/` and enable them under
**Settings → Appearance → CSS snippets**:

| Snippet                 | What it does                                                               |
| ----------------------- | -------------------------------------------------------------------------- |
| `focus-mode.css`        | Dims desktop chrome until hover or keyboard focus for distraction-free work |
| `rainbow-folders.css`   | Tints each top-level folder with a Blue Night/Catppuccin-inspired pastel   |
| `colored-headings.css`  | Gives every heading level its own pastel color                             |
| `wide-code.css`         | Lets code blocks, tables and Dataview results exceed readable line width   |
| `wide-note.css`         | Opt-in `wide-note` cssclass that increases the whole note line width       |
| `clean-embeds.css`      | Makes note embeds seamless while preserving the source-note link           |
| `image-grid.css`        | Opt-in `image-grid` cssclass for responsive multi-image galleries          |
| `compact-tables.css`    | Reduces table sizing and cell padding with a narrowly scoped fallback      |
| `compact-callouts.css`  | Makes native callouts denser without replacing their colors or icons       |
| `math-accent.css`       | Applies a restrained Blue Night accent to rendered and editor math         |
| `minimal-scrollbar.css` | Ultra-thin rounded scrollbars that use Obsidian scrollbar vars             |

The bundled snippets avoid `!important` so users can still override them with their own CSS. DOM-
dependent selectors are kept isolated, and the only bundled `:has()` usage is scoped to notes that
explicitly enable the `image-grid` cssclass. Snippets prefer documented Obsidian variables; direct
selectors are reserved for presentation details that do not have a public variable.

`wide-note.css` and `image-grid.css` are intentionally opt-in per note. Add the corresponding class
to Properties/frontmatter, for example:

```yaml
---
cssclasses:
  - wide-note
  - image-grid
---
```

## Recommended plugins

- [Style Settings](https://github.com/obsidian-community/obsidian-style-settings) — exposes accent
  flavors, custom accent color, canvas variants, backgrounds, and feature toggles.
- [Quick Switcher++](https://github.com/darlal/obsidian-switcher-plus) — note *preview while you
  navigate* the switcher is not possible with CSS alone; this plugin provides it and inherits the
  theme's prompt styling. The native Page Preview remains the closest built-in alternative.

## Theme architecture

Blue Night follows three rules for maintainability:

1. Prefer documented Obsidian CSS variables for core colors, typography, tabs, navigation,
   metadata, prompts, tables, checkboxes, scrollbars, and callouts.
2. Use direct DOM selectors only for optional enhancements that cannot be represented by a public
   variable. If one of those selectors changes upstream, the enhancement should disappear rather
   than break the underlying UI.
3. Do not use `!important`; snippets and user styles must remain able to override the theme.

Accent presets are not a second color system: each preset only sets Obsidian's native
`--accent-h`, `--accent-s`, and `--accent-l` values. Named presets may use a darker lightness in
light mode while keeping the same native HSL contract. The Custom picker writes separate
`--bn-custom-accent-*` values that are mapped into those native variables only when Custom is
selected.

Canvas variants form a second, independent axis. They override background/base palette tokens only;
they never redefine the selected accent. This keeps the theme maintainable while allowing 40 dark
and 24 light canvas/accent combinations without implementing 64 separate themes.

## Contributing

Development setup, project structure, compatibility checks, and the branching/release flow are
documented in
[CONTRIBUTING.md](https://github.com/sandovaldavid/obsidian-blue-night/blob/main/CONTRIBUTING.md).

## License

[MIT](https://github.com/sandovaldavid/obsidian-blue-night/blob/main/LICENSE)
