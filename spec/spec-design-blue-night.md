---
title: Blue Night Obsidian Theme Specification
version: 4.3.0
date_created: 2026-07-10
date_updated: 2026-08-10
tags: [design, app, theme, css, obsidian]
---

# Blue Night theme specification

## 1. Purpose

Blue Night is a minimalist Obsidian theme for software-development and long-form note-taking
workflows. It provides a deep night-blue dark palette, a high-contrast light palette, a
Catppuccin-inspired supporting pastel palette, selectable accent flavors, optional interface
enhancements, and Style Settings customization without replacing Obsidian's own CSS architecture.

The primary engineering goal is **forward-compatible theming**: core behavior must depend on
Obsidian's documented CSS variables, while DOM-specific selectors are allowed only for optional
visual enhancements whose failure cannot make the underlying UI unusable.

## 2. Supported Obsidian versions

- Minimum public version: **Obsidian 1.12.7**.
- Catalyst builds are tested when they announce theme/developer breaking changes.
- Obsidian 1.13 compatibility is required for the announced callout color contract, Settings
  redesign, and CodeMirror upgrade.

`minAppVersion` in `manifest.json` is the source of truth for the minimum supported public build.

## 3. Architecture principles

### 3.1 Prefer the public CSS-variable API

Shared variables belong under `body`. Mode-specific colors belong under `.theme-dark` and
`.theme-light`.

The theme must prefer Obsidian variables for:

- backgrounds and text;
- tabs and navigation;
- prompts;
- properties/metadata;
- tags and pills;
- checkboxes;
- syntax highlighting;
- links and graph colors;
- tables;
- scrollbars;
- callouts;
- title bar and status bar.

Direct selectors may be used for decorations such as the explorer SVG icons, Raycast-style prompt
surface, metadata shadow, or floating status bar, but those features must degrade safely when an
upstream class changes.

### 3.2 Low specificity and user overrides

- Do not use `!important` in `theme.css` or bundled snippets.
- Do not build selectors around deep DOM nesting when a variable exists.
- User snippets must remain able to override Blue Night.
- Avoid global element geometry overrides such as changing every `input[type='search']` padding.
- Do not duplicate component geometry already represented by documented variables. In particular,
  navigation child indentation and indentation-guide placement remain owned by Obsidian.

### 3.3 Keep assets offline

All theme-owned icons must be embedded locally as URL-encoded SVG data. The production theme must
not load remote fonts, images, stylesheets, or other runtime network resources.

## 4. Accent contract

All accent choices converge on one Obsidian-native sink:

```css
--accent-h
--accent-s
--accent-l
```

Blue Night exposes these Style Settings accent flavors:

1. Blue Night — `218 / 92% / 76%`.
2. Sapphire — `199 / 66% / 69%` (`#7dc4e4`).
3. Lavender — `232 / 97% / 85%`.
4. Mauve — `267 / 83% / 80%` (`#c6a0f6`).
5. Teal — `171 / 47% / 69%`.
6. Pink — `316 / 74% / 85%`.
7. Peach — `21 / 86% / 73%` (`#f5a97f`).
8. Custom — user-selected HSL values.

The preset selector is a `class-select`. Each preset class may set **only** the native
`--accent-h`, `--accent-s`, and `--accent-l` primitives. It must not introduce a second accent
system.

Named presets may use mode-specific lightness values while preserving their hue/saturation identity
and the same native HSL sink. In light mode the bundled presets use these contrast-tuned lightness
values:

| Accent     | Light-mode `--accent-l` |
| ---------- | ----------------------: |
| Blue Night |                   `40%` |
| Sapphire   |                   `29%` |
| Lavender   |                   `51%` |
| Mauve      |                   `46%` |
| Teal       |                   `25%` |
| Pink       |                   `34%` |
| Peach      |                   `30%` |

This is not a second accent system: the light-mode rules still write only `--accent-l` and all
consumers continue to resolve through the native `--accent-h/s/l` primitives. Custom remains
user-controlled and therefore cannot be guaranteed to meet the bundled contrast targets.

The custom picker is intentionally separate:

```yaml
id: bn-custom-accent
type: variable-color
format: hsl-split
```

Style Settings therefore generates:

```css
--bn-custom-accent-h
--bn-custom-accent-s
--bn-custom-accent-l
```

Those custom variables are consumed only by `body.bn-accent-custom`, which maps them into
Obsidian's native `--accent-h`, `--accent-s`, and `--accent-l` primitives. This prevents the custom
picker from overriding preset classes when Custom is not selected.

Blue Night-specific transparent accent tokens such as `--bn-accent-soft` must derive from those
same native HSL primitives.

Do not reintroduce independently consumed accent sources such as `--color-accent-base`, custom
`--color-accent-1` values, or `--accent-rgb`. Compatibility aliases are acceptable only if an
upstream API requires them and they are derived from the native HSL source of truth.

Canvas presets may alter background/base tokens but must never replace the selected accent.

## 5. Palette requirements

### 5.1 Dark default

| Token             | Value     | Role                            |
| ----------------- | --------- | ------------------------------- |
| `--color-base-00` | `#0f1523` | editor/workspace canvas         |
| `--color-base-10` | `#0b1019` | sidebars and recessed panels    |
| `--color-base-20` | `#151d2e` | elevated surfaces               |
| `--color-base-30` | `#232e45` | borders                         |
| `--text-normal`   | `#cdd9f0` | primary text                    |
| `--text-muted`    | `#9db0d0` | secondary text                  |
| `--text-faint`    | `#788bae` | subdued but readable text/icons |

Dark canvas variants:

1. Blue Night — default night-blue palette.
2. Midnight Navy — deeper blue surfaces without becoming pure black.
3. Storm Blue — desaturated blue-gray surfaces for reduced visual intensity.
4. Dark Charcoal / OLED — black and near-black surfaces.
5. Cozy Pastels — warm slate/lilac surfaces.

Reference surface tokens for the additional variants:

| Variant       | Canvas    | Sidebar   | Surface   | Border    |
| ------------- | --------- | --------- | --------- | --------- |
| Midnight Navy | `#080d18` | `#060a12` | `#101827` | `#1d2a40` |
| Storm Blue    | `#161b2a` | `#111622` | `#1d2435` | `#313a52` |

### 5.2 Light default

| Token             | Value     | Role                            |
| ----------------- | --------- | ------------------------------- |
| `--color-base-00` | `#f7f9fc` | editor/workspace canvas         |
| `--color-base-10` | `#eef2f8` | sidebars and recessed panels    |
| `--color-base-20` | `#e5ebf4` | elevated surfaces               |
| `--color-base-30` | `#d7e0ec` | borders                         |
| `--text-normal`   | `#1c2433` | primary text                    |
| `--text-muted`    | `#4b5a75` | secondary text                  |
| `--text-faint`    | `#54667f` | subdued but readable text/icons |

Light canvas variants:

1. Clean Blue — default bluish white palette.
2. Blue Mist — softer blue-tinted surfaces for lower contrast against white surroundings.
3. Cozy Pastels Light — soft lilac/cream surfaces.

Blue Mist reference tokens:

| Token   | Value     |
| ------- | --------- |
| Canvas  | `#f1f5fb` |
| Sidebar | `#e8eef7` |
| Surface | `#dde6f2` |
| Border  | `#cad6e6` |

### 5.3 Catppuccin-inspired supporting palette

The supporting palette is part of Blue Night's visual identity and remains available regardless of
the selected interactive accent. Light mode uses darker counterparts rather than reusing pastel
dark-mode values as text colors.

| Token         | Dark value | Light value | Typical role                                |
| ------------- | ---------- | ----------- | ------------------------------------------- |
| `--bn-blue`   | `#8ab4fa`  | `#0a53e5`   | functions, properties, blue semantic states |
| `--bn-purple` | `#b4befe`  | `#6f46c9`   | keywords, secondary emphasis                |
| `--bn-cyan`   | `#8bd5ca`  | `#116c71`   | operators, informational states             |
| `--bn-green`  | `#a6da95`  | `#24701e`   | strings, success                            |
| `--bn-yellow` | `#eed49f`  | `#8d5400`   | warning/highlight                           |
| `--bn-orange` | `#f5a97f`  | `#a54300`   | values, important states                    |
| `--bn-red`    | `#f2879b`  | `#c20e35`   | errors/tags                                 |
| `--bn-pink`   | `#f5bde6`  | `#9f388b`   | decorative/special states                   |

Choosing Sapphire, Lavender, Mauve, Teal, Pink, Peach, or a custom accent changes the interactive
accent family. It must not flatten syntax highlighting or semantic states into a single color.

### 5.4 Canvas/accent matrix

Canvas and accent selection are independent axes. With five dark canvases and eight accents, Blue
Night supports 40 dark combinations. With three light canvases and eight accents, it supports 24
light combinations. These are compositional combinations, not 64 separately maintained themes.

Canvas classes may override `--color-base-*` and directly related surface tokens such as
`--code-background` and `--glass-bg`. Canvas classes must not set `--accent-h`, `--accent-s`, or
`--accent-l`.

### 5.5 Contrast targets

For bundled presets, normal-sized text roles that Blue Night owns — including `--text-faint`,
syntax comments, semantic support colors, and named interactive accents used as text — target at
least **4.5:1** against the primary, secondary, and elevated surfaces on which they are used.
Interactive outlines/icons that communicate state should also avoid disappearing into their
surface; prefer already contrast-tuned semantic text tokens when a darker base token is too faint.

The target applies to the bundled named accents and palettes. User-selected Custom accent values are
explicitly outside that guarantee.

## 6. Component contracts

### 6.1 Inputs and search

Blue Night may set public input variables such as radius or border width. It must not globally
replace native input padding because search inputs contain app-owned icons and clear buttons whose
geometry can change between Obsidian releases.

Acceptance criterion: typing in global/file search must never overlap the search icon or clear
button because of theme CSS.

### 6.2 Live Preview headings

Reading-view headings may use normal block margins. CodeMirror/Live Preview heading decorations
must use padding rather than vertical margins so cursor positioning and virtualized line geometry
remain controlled by Obsidian.

### 6.3 Callouts

Blue Night uses documented callout variables and retains Obsidian's native callout icon rendering.

Obsidian 1.13 changed `--callout-color` from an RGB triplet to a complete valid CSS color. Therefore
Blue Night must never use:

```css
rgb(var(--callout-color))
```

The theme must remain valid whether the app provides legacy or new callout internals by avoiding
manual conversion of that variable.

### 6.4 File explorer icons and indentation guides

Folder/file/vault icons are optional SVG-mask enhancements. They may target current explorer DOM
classes, but their failure must only remove the decoration. Core file/folder text, selection,
indentation, and navigation must remain driven by Obsidian variables.

Folder indentation guides must use Obsidian's documented navigation contract:

```css
--nav-item-children-padding-start
--nav-item-children-margin-start
--nav-indentation-guide-width
--nav-indentation-guide-color
```

Blue Night must not reproduce the guide by assigning `margin-inline-start`, `padding-inline-start`,
and `border-inline-start` directly to `.nav-folder-children`. The app owns that geometry so the guide
stays aligned when File Explorer spacing changes upstream.

### 6.5 Custom task states

Blue Night supports:

- `[x]` complete;
- `[-]` cancelled;
- `[/]` in progress;
- `[?]` question;
- `[!]` important;
- `[>]` forwarded.

The custom marks are local SVG masks. Standard checkbox size, radius, border, completion color, and
decoration use Obsidian checkbox variables.

### 6.6 Prompts

Prompt width, maximum width/height, input height, and border use the documented prompt variables.
The Raycast-style effect may add surface blur, shadow, selected-item decoration, and spacing without
replacing core prompt sizing behavior.

### 6.7 Scrollbars

Scrollbar colors use:

```css
--scrollbar-bg
--scrollbar-thumb-bg
--scrollbar-active-thumb-bg
```

The theme/snippet may directly set scrollbar thickness because Obsidian does not expose a public
width variable.

### 6.8 Tables and bundled snippets

Bundled snippets must use documented component variables when available. A direct selector is
acceptable only for a narrowly scoped presentation property with no documented variable and must
fail safely if upstream markup changes.

For example, Obsidian exposes table line-height/text/header sizing variables but does not currently
document cell-padding variables. `compact-tables.css` therefore uses the documented sizing
variables and a narrow `th`/`td` padding rule instead of inventing unsupported custom-property names.

## 7. Style Settings contract

Style Settings is optional. Blue Night must render correctly without the plugin.

The root Style Settings identifier is `kodev-blue-night`. Keep it stable to preserve persisted user
preferences across theme updates.

Exposed settings:

- accent flavor: Blue Night, Sapphire, Lavender, Mauve, Teal, Pink, Peach, or Custom;
- custom accent color, active only through the Custom accent class;
- custom dark/light editor background;
- dark canvas: Blue Night, Midnight Navy, Storm Blue, Dark Charcoal/OLED, or Cozy Pastels;
- light canvas: Clean Blue, Blue Mist, or Cozy Pastels Light;
- Raycast prompt;
- minimalist explorer;
- metadata card;
- folder guides;
- vault icon;
- premium headings;
- custom bullets;
- pill tags;
- circular/custom task states;
- IDE blockquotes;
- floating status bar;
- fade-until-hover status bar.

Class-based settings must alter only their named feature. Accent flavor classes are the exception
only in the sense that they intentionally feed the shared native accent primitives consumed across
Obsidian; they must not change canvas/background palettes.

## 8. Optional plugin styling

Blue Night may provide inert styling for:

- Dataview;
- Quick Switcher++.

Plugin-specific selectors must not affect core Obsidian components when the plugin is absent.

## 9. Accessibility and responsive behavior

- Respect `prefers-reduced-motion`.
- Hover-only features must also expose keyboard focus where applicable.
- Mobile disables expensive backdrop blur and desktop-only floating status-bar positioning.
- Text and interactive states must remain legible in dark and light palettes.
- Bundled named accents and theme-owned normal-sized text colors target 4.5:1 on their intended
  bundled surfaces.
- Print/PDF mode uses an ink-friendly light surface.

## 10. Release contract

A community theme release consists of:

- `manifest.json` committed at the repository default branch;
- a GitHub release whose tag matches the manifest version;
- `manifest.json` attached to that release;
- `theme.css` attached to that release.

The project does not use `versions.json`; that fallback map belongs to Obsidian's community plugin
compatibility flow.

Release Please owns the theme version. Do not document or add a separate `npm version` /
`version-bump.mjs` release path unless the repository actually adopts it again.

## 11. Validation matrix

Before release, manually verify:

- latest public Obsidian build;
- latest Catalyst build when relevant;
- dark/light modes;
- Blue Night, Midnight Navy, Storm Blue, Dark Charcoal/OLED, and Cozy Pastels dark canvases;
- Clean Blue, Blue Mist, and Cozy Pastels Light light canvases;
- Blue Night, Sapphire, Lavender, Mauve, Teal, Pink, and Peach accent flavors;
- Custom accent selection and picker changes;
- switching repeatedly between presets and Custom without stale accent variables;
- switching canvas variants without changing the selected accent;
- representative cross-axis combinations: Midnight Navy + Sapphire, Storm Blue + Peach,
  Dark Charcoal/OLED + Mauve, Cozy Pastels + Teal, and Blue Mist + Pink;
- bundled named accent text/selected-state contrast on every light canvas;
- faint text, syntax comments, semantic support colors, and navigation icons on every canvas;
- nested File Explorer folders with Folder Indent Guides enabled and disabled; guide position must
  follow Obsidian's native indentation and remain centered at every nesting level;
- supporting syntax/semantic colors remain multi-color under every accent flavor;
- theme with Style Settings disabled;
- Source mode, Live Preview, Reading view;
- search inputs and clear buttons;
- file explorer and navigation states;
- tabs, ribbon, prompts, properties, tags, callouts, tasks, tables, Canvas, status bar;
- every bundled snippet, including Reading/Live Preview coverage where relevant;
- keyboard focus states;
- mobile-responsive behavior;
- reduced-motion mode;
- PDF/print output;
- Dataview and Quick Switcher++ absent and installed.

Static review must also confirm:

- no `!important`;
- no remote runtime assets;
- every accent preset converges on `--accent-h/s/l`;
- Custom is the only consumer of `--bn-custom-accent-h/s/l`;
- canvas preset classes never write `--accent-h/s/l`;
- no independently consumed duplicate accent source of truth;
- no `rgb(var(--callout-color))`;
- no broad global input padding override;
- no manual `.nav-folder-children` indentation/guide geometry;
- bundled snippets do not depend on undocumented custom properties when a documented contract is
  available;
- no Live Preview vertical-margin override.

## 12. References

- Obsidian Developer Documentation — Theme guidelines
- Obsidian Developer Documentation — Build a theme
- Obsidian Developer Documentation — CSS variable reference
- Obsidian Developer Documentation — Navigation CSS variables
- Obsidian Developer Documentation — Table CSS variables
- Obsidian Developer Documentation — Callout CSS variables
- Obsidian Developer Documentation — Submit your theme
- Style Settings — setting-definition documentation
- Obsidian 1.13 developer changelog for the callout-color and CodeMirror changes
