---
title: Blue Night Obsidian Theme Specification
version: 4.0.0
date_created: 2026-07-10
date_updated: 2026-08-07
tags: [design, app, theme, css, obsidian]
---

# Blue Night theme specification

## 1. Purpose

Blue Night is a minimalist Obsidian theme for software-development and long-form note-taking
workflows. It provides a deep night-blue dark palette, a high-contrast light palette, pastel code
syntax colors, optional interface enhancements, and Style Settings customization without replacing
Obsidian's own CSS architecture.

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

### 3.3 Keep assets offline

All theme-owned icons must be embedded locally as URL-encoded SVG data. The production theme must
not load remote fonts, images, stylesheets, or other runtime network resources.

## 4. Accent contract

The accent has one source of truth:

```css
--accent-h
--accent-s
--accent-l
```

The Style Settings accent picker uses:

```yaml
id: accent
type: variable-color
format: hsl-split
```

That makes Style Settings write directly to the variables Obsidian consumes. Blue Night-specific
transparent accents are derived from those same HSL values.

Do not reintroduce a parallel system such as `--color-accent-base`, custom accent-flavor classes,
or independent `--accent-rgb` values unless an upstream API requires it.

Canvas presets may alter background/base tokens but must not replace the selected accent.

## 5. Palette requirements

### 5.1 Dark default

| Token | Value | Role |
| --- | --- | --- |
| `--color-base-00` | `#0f1523` | editor/workspace canvas |
| `--color-base-10` | `#0b1019` | sidebars and recessed panels |
| `--color-base-20` | `#151d2e` | elevated surfaces |
| `--color-base-30` | `#232e45` | borders |
| `--text-normal` | `#cdd9f0` | primary text |
| `--text-muted` | `#9db0d0` | secondary text |

Dark canvas variants:

1. Blue Night — default night-blue palette.
2. Dark Charcoal / OLED — black and near-black surfaces.
3. Cozy Pastels — warm slate/lilac surfaces.

### 5.2 Light default

| Token | Value | Role |
| --- | --- | --- |
| `--color-base-00` | `#f7f9fc` | editor/workspace canvas |
| `--color-base-10` | `#eef2f8` | sidebars and recessed panels |
| `--color-base-20` | `#e5ebf4` | elevated surfaces |
| `--color-base-30` | `#d7e0ec` | borders |
| `--text-normal` | `#1c2433` | primary text |
| `--text-muted` | `#4b5a75` | secondary text |

Light canvas variants:

1. Clean Blue — default bluish white palette.
2. Cozy Pastels Light — soft lilac/cream surfaces.

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

### 6.4 File explorer icons

Folder/file/vault icons are optional SVG-mask enhancements. They may target current explorer DOM
classes, but their failure must only remove the decoration. Core file/folder text, selection,
indentation, and navigation must remain driven by Obsidian variables.

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

## 7. Style Settings contract

Style Settings is optional. Blue Night must render correctly without the plugin.

Exposed settings:

- accent color through native HSL variables;
- custom dark/light editor background;
- dark and light canvas variants;
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

Class-based settings must alter only their named feature.

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
- all canvas variants;
- custom accent changes through Style Settings;
- theme with Style Settings disabled;
- Source mode, Live Preview, Reading view;
- search inputs and clear buttons;
- file explorer and navigation states;
- tabs, ribbon, prompts, properties, tags, callouts, tasks, tables, Canvas, status bar;
- keyboard focus states;
- mobile-responsive behavior;
- reduced-motion mode;
- PDF/print output;
- Dataview and Quick Switcher++ absent and installed.

Static review must also confirm:

- no `!important`;
- no remote runtime assets;
- no duplicate accent source of truth;
- no `rgb(var(--callout-color))`;
- no broad global input padding override;
- no Live Preview vertical-margin override.

## 12. References

- Obsidian Developer Documentation — Theme guidelines
- Obsidian Developer Documentation — Build a theme
- Obsidian Developer Documentation — CSS variable reference
- Obsidian Developer Documentation — Submit your theme
- Style Settings — setting-definition documentation
- Obsidian 1.13 developer changelog for the callout-color and CodeMirror changes
