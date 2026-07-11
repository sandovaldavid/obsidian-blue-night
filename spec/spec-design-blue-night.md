---
title: Blue Night Obsidian Theme Specification
version: 3.1.0
date_created: 2026-07-10
tags: [design, app, theme, css]
---

# Introduction

This document specifies the design system, architecture, and requirements for **Blue Night**, a minimalist dark theme for Obsidian with pastel accents. It is designed for software developers, prioritizing low eye strain, clean layout hierarchy, and seamless integration with developer-focused plugins.

## 1. Purpose & Scope

The purpose of the **Blue Night** theme is to provide a unified, responsive, and distraction-free visual environment inside the Obsidian note-taking app. 
The scope covers:
- Core dark/light mode Obsidian themes using CSS variables.
- Optional CSS snippets for extra layout modifiers (`focus-mode.css`, `rainbow-folders.css`, etc.).
- Embedded SVG icons via CSS masks for high-fidelity custom visuals without network requests.

## 2. Definitions

- **Vault**: The directory where Obsidian stores all user notes, settings, attachments, and style configurations.
- **CSS Snippet**: An independent CSS file placed in `.obsidian/snippets` that adds or overrides style layers on top of the active theme.
- **CSS Variable (Custom Property)**: A dynamic token declared inside CSS (e.g., `--color-base-00`) used to control colors, spacing, and styling variables globally.
- **Style Settings Plugin**: A popular community plugin that parses special YAML comments in the theme file to build a GUI in settings, allowing users to toggle features and customize colors.

## 3. Requirements, Constraints & Guidelines

- **REQ-001**: The canvas color palette must use a desaturated night-blue base (`#0f1523` for canvas and `#0b1019` for panels) to reduce visual fatigue. Darker charcoal values (`#090c10`, `#05070a`) are reserved for the Dark Charcoal/OLED preset flavor.
- **REQ-002**: Heading levels (H1 to H6) must support colored variants using pastel accents (blue, lavender, teal, green, yellow, orange).
- **REQ-003**: Search bars must prevent text overlap with the search icon and the delete button by setting a padding-left and padding-right of at least 32px.
- **REQ-004**: The search clear/delete button must be styled with a visible red accent color (`var(--text-error)`) by default with an opacity of 0.65, transitioning to full opacity on hover, instead of remaining dark/invisible.
- **REQ-005**: All custom icons (folders, checkboxes, files) must be embedded locally as URL-encoded SVG variables in the CSS and rendered using CSS mask properties (`-webkit-mask-image`).
- **REQ-006**: Warning and destructive confirmation modal buttons (`button.mod-warning`) must be styled with a solid, high-contrast red background (`var(--color-red)`) and readable text by default, instead of inheriting a transparent dark background.
- **REQ-007**: Metadata property labels and their respective type icons (`.metadata-property-key` and `.metadata-property-icon`) must be unified into a single visual pill by removing the dividing borders and setting matching outer border-radiuses.
- **REQ-008**: Code blocks must display their declared programming language as a stylized, semi-transparent badge (`.code-block-flair`) in the top-right corner, fading out smoothly on hover in Reading View to yield space to the copy button.
- **CON-001**: The theme must function completely offline. No external fonts, icons, or stylesheets can be imported via HTTP/HTTPS URLs.
- **GUD-001**: Focus on a clean, minimal UI. Unnecessary borders should be omitted; layout sections should be distinguished by subtle color depth differences (e.g., base-00 vs base-10).
- **PAT-001**: Maintain compatibility with the Style Settings plugin schema for user customizations.

## 4. Interfaces & Data Contracts

### 4.1. Core Color Variables (Dark Mode Override)
The theme overrides Obsidian's standard design tokens using the following color values:

| Token Name | Color Hex | Description |
| :--- | :--- | :--- |
| `--color-base-00` | `#090c10` | Workspace canvas background |
| `--color-base-10` | `#05070a` | Sidebars and navigation panel background |
| `--color-base-20` | `#10141b` | Secondary panels and inactive tab background |
| `--color-base-30` | `#1e2533` | Border color and inactive checkbox borders |
| `--text-error` | `#f2879b` | Clear button, deletion, and error text |
| `--color-accent-light`| `#8ab4fa` | Light accent color (blue pastel) |

### 4.2. Core Color Variables (Light Mode Override)
For light mode (Latte-style adaptation), the theme uses:

| Token Name | Color Hex | Description |
| :--- | :--- | :--- |
| `--color-base-00` | `#f7f9fc` | Clean bluish white editor background |
| `--color-base-10` | `#eef2f8` | Sidebar and panel backgrounds |
| `--color-base-20` | `#e5ebf4` | Secondary panel backgrounds |
| `--color-base-30` | `#dde5f0` | Outer border outline color |
| `--text-normal` | `#1c2433` | Dark charcoal slate primary text |
| `--text-muted` | `#4b5a75` | Medium gray slate secondary text |
| `--color-accent` | `#2563eb` | Vibrant primary blue accent |

### 4.3. Embedded SVG Masks
Custom vector assets are URL-encoded and stored as variables:
```css
--bn-icon-folder: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' fill='none' stroke='black' stroke-width='1.75' stroke-linecap='round' stroke-linejoin='round'%3E%3Cpath d='M20 20a2 2 0 0 0 2-2V8a2 2 0 0 0-2-2h-7.9a2 2 0 0 1-1.69-.9L9.6 3.9A2 2 0 0 0 7.93 3H4a2 2 0 0 0-2 2v13a2 2 0 0 0 2 2Z'/%3E%3C/svg%3E");
```

### 4.4. Theme Preset Variations
The theme implements variations selectable under Style Settings:
1. **Blue Night (Default)**: Deep night blue editor canvas (`#0f1523`) with neon-pastel accent overlays.
2. **Dark Charcoal / OLED Black**: Pure black canvas (`#000000`) and charcoal panels (`#05070a` / `#090c10`), moving the legacy dark mode snippet directly into a built-in toggle.
3. **Cozy Pastels (Dark)**: Cozy warm lavender/slate base (`#1b1924`) with warm lilac-cream text and soft mauve accents.
4. **Clean Blue (Light Default)**: Pure white with slate accents and night blue text details.
5. **Cozy Pastels (Light)**: Soft creamy lilac base (`#faf4fc`) with dusty violet text and warm purple accents.

### 4.5. Accompanying Snippets
To enhance layout capabilities, the workspace bundles:
- **`colored-headings.css`**: Dual light/dark custom pastel headings (Mocha pastels for dark, Latte pastels for light).
- **`rainbow-folders.css`**: Rotates folder title colors through 8 responsive pastel hues with proper light/dark contrast.
- **`clean-embeds.css`**: Seamless note transclusions by removing border enclosures, padding, and embedded headers.
- **`image-grid.css`**: Responsive flexbox grids for consecutive inline images.
- **`minimal-scrollbar.css`**: Thin, semi-transparent rounded scrollbars that highlight on hover.

## 5. Acceptance Criteria

- **AC-001**: Heading levels H1–H6 must receive their designated pastel colors when `colored-headings.css` is active.
- **AC-002**: When entering text into Obsidian's global search or file search bar, the characters must not overlap with the search magnifying glass icon on the left.
- **AC-003**: The search clear button (X) must show a red tint (`#f2879b` / `#d20f39`) at 65% opacity when text is typed, and must highlight to 100% opacity on hover.
- **AC-004**: The release pipeline version bump must successfully propagate when `npm version` is run, updating `manifest.json` and `versions.json` through the `version-bump.mjs` script.

## 6. Test Automation / Validation Strategy

Since Obsidian themes are client-side CSS files, automated testing focuses on layout validation and syntax linting:
- **Linting**: Prettier is used to validate that the CSS styling is properly formatted and does not contain syntax errors.
- **Manual Verification**: Launch Obsidian with the development theme enabled to visually verify the search layout padding, color visibility of the clear button, and heading colors across various resolutions.

## 7. Rationale & Context

- **Specificity Override**: The heading snippet failed to override theme heading variables because tag-level selector (`body`) has a lower specificity weight than the theme's class-based selector (`.theme-dark`, `.theme-light`). Using `body.theme-dark` with `!important` ensures the snippet overrides any internal active theme options or external variables.
- **Layout Overlap**: Obsidian search icon is positioned absolute on the left inside the container. Overriding padding with a global input declaration resets the padding-left, causing characters to start immediately behind the absolute icon. Forcing `padding-left: 32px !important` guarantees the input text clears the icon boundaries.

## 8. Dependencies & External Integrations

- **EXT-001**: Obsidian App (v1.0.0 or higher) - Required hosting environment.
- **SVC-001**: Style Settings Plugin (optional) - Parses UI configuration tokens defined in theme headers.
- **SVC-002**: Quick Switcher++ (optional) - Third-party plugin, styling adjustments are embedded to match Blue Night UI.

## 9. Examples & Edge Cases

### Specificity Hierarchy
Correct usage to target and override the heading colors within a snippet:
```css
body.theme-dark, body.theme-light {
  --h1-color: rgb(var(--color-blue-rgb, 138, 180, 250)) !important;
}
```

### Search UI Layout Customization
Correct wrapper layout styling:
```css
.theme-dark .search-input-container input[type='search'],
.theme-light .search-input-container input[type='search'] {
  padding-left: 32px;
  padding-right: 32px;
}
```

## 10. Validation Criteria
- Execute `npm run version` using Node.js to verify `version-bump.mjs` works as intended.
- Validate CSS formatting using Prettier rules.
