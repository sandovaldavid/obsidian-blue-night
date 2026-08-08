---
layout: default
title: Blue Night
---

<section class="hero">
  <h1>Blue Night</h1>
  <p>
    A minimalist night-blue theme for Obsidian with Catppuccin-inspired pastel accents.
    Engineered for low eye strain and a developer's daily workflow.
  </p>
  <div class="hero-actions">
    <a class="btn btn-primary" href="https://github.com/{{ site.repository }}/releases/latest">Download latest release</a>
    <a class="btn btn-ghost" href="https://github.com/{{ site.repository }}">View on GitHub</a>
  </div>
  <div class="hero-screenshot">
    <img src="{{ '/assets/img/screenshot.png' | relative_url }}" alt="Blue Night theme screenshot showing the night-blue editor with pastel syntax highlighting" />
  </div>
</section>

<section id="features">
  <h2>Features</h2>
  <p class="section-lead">Built on Obsidian's public CSS variables, fully offline, and designed to stay override-friendly.</p>
  <div class="feature-grid">
    <div class="feature-card" data-accent="blue">
      <h3>Night-blue palette</h3>
      <p>A deep <code>#0f1523</code> canvas with pastel accents in dark mode, and a crisp bluish slate in light mode.</p>
    </div>
    <div class="feature-card" data-accent="teal">
      <h3>Selectable accent flavors</h3>
      <p>Choose Blue Night, Sapphire, Lavender, Mauve, Teal, Pink, Peach, or Custom. Every option converges on Obsidian's native <code>--accent-h</code>, <code>--accent-s</code>, and <code>--accent-l</code> variables.</p>
    </div>
    <div class="feature-card" data-accent="lavender">
      <h3>Catppuccin-inspired support colors</h3>
      <p>Blue, lavender, cyan, green, yellow, peach, red, and pink remain available for syntax and semantic states regardless of the selected accent.</p>
    </div>
    <div class="feature-card" data-accent="green">
      <h3>Extra task states</h3>
      <p>Beyond done: <code>[-]</code> cancelled, <code>[/]</code> in progress, <code>[?]</code> question, <code>[!]</code> important, <code>[&gt;]</code> forwarded.</p>
    </div>
    <div class="feature-card" data-accent="pink">
      <h3>Raycast-style switcher</h3>
      <p>A floating glass treatment layered over Obsidian's documented prompt sizing and border variables.</p>
    </div>
    <div class="feature-card" data-accent="yellow">
      <h3>Forward-compatible</h3>
      <p>Core styling is variable-driven. DOM selectors are isolated to optional enhancements so upstream markup changes do not break the base UI.</p>
    </div>
  </div>
</section>

<section id="flavors">
  <h2>Canvas and accent combinations</h2>
  <p class="section-lead">
    Canvas variants and accent flavors are independent. Dark mode offers Blue Night, Midnight Navy,
    Storm Blue, OLED, and Cozy Pastels; light mode offers Clean Blue, Blue Mist, and Cozy Pastels
    Light. Mix any of them with Blue Night, Sapphire, Lavender, Mauve, Teal, Pink, Peach, or your own custom accent.
  </p>
  <div class="flavor-row">
    <div class="flavor">
      <div class="swatch" style="background:#0f1523">
        <span style="background:#8ab4fa"></span><span style="background:#b4befe"></span><span style="background:#8bd5ca"></span><span style="background:#f5bde6"></span>
      </div>
      <div class="flavor-info">
        <h3>Blue Night</h3>
        <p>The default deep night-blue canvas with the Blue Night accent and pastel supporting colors.</p>
      </div>
    </div>
    <div class="flavor">
      <div class="swatch" style="background:#080d18">
        <span style="background:#7dc4e4"></span><span style="background:#8ab4fa"></span><span style="background:#b4befe"></span><span style="background:#8bd5ca"></span>
      </div>
      <div class="flavor-info">
        <h3>Midnight Navy + Sapphire</h3>
        <p>A deeper blue canvas paired with a cool sapphire accent without crossing into pure-black OLED territory.</p>
      </div>
    </div>
    <div class="flavor">
      <div class="swatch" style="background:#161b2a">
        <span style="background:#f5a97f"></span><span style="background:#7dc4e4"></span><span style="background:#a6da95"></span><span style="background:#c6a0f6"></span>
      </div>
      <div class="flavor-info">
        <h3>Storm Blue + Peach</h3>
        <p>Desaturated blue-gray surfaces with a warm peach accent for contrast during long writing sessions.</p>
      </div>
    </div>
    <div class="flavor">
      <div class="swatch" style="background:#000000">
        <span style="background:#c6a0f6"></span><span style="background:#8ab4fa"></span><span style="background:#8bd5ca"></span><span style="background:#f5bde6"></span>
      </div>
      <div class="flavor-info">
        <h3>OLED + Mauve</h3>
        <p>Pure black canvas with a richer violet accent while syntax and semantic colors remain multi-color.</p>
      </div>
    </div>
    <div class="flavor">
      <div class="swatch" style="background:#1b1924">
        <span style="background:#8bd5ca"></span><span style="background:#b4befe"></span><span style="background:#eed49f"></span><span style="background:#f5bde6"></span>
      </div>
      <div class="flavor-info">
        <h3>Cozy Pastels + Teal</h3>
        <p>Warm slate and lilac-gray surfaces with Teal as the shared interactive accent.</p>
      </div>
    </div>
    <div class="flavor">
      <div class="swatch" style="background:#f1f5fb">
        <span style="background:#f5bde6"></span><span style="background:#1e66f5"></span><span style="background:#147d83"></span><span style="background:#7048c9"></span>
      </div>
      <div class="flavor-info">
        <h3>Blue Mist + Pink</h3>
        <p>A softer blue-tinted light canvas with Pink as the interactive accent and high-contrast support colors.</p>
      </div>
    </div>
  </div>
</section>

<section id="install">
  <h2>Installation</h2>
  <ol class="steps">
    <li>Use Obsidian <strong>1.12.7 or newer</strong>.</li>
    <li>
      Download <code>theme.css</code> and <code>manifest.json</code> from the
      <a href="https://github.com/{{ site.repository }}/releases/latest">latest release</a>.
    </li>
    <li>Copy both files into your vault at <code>.obsidian/themes/Blue Night/</code>.</li>
    <li>In Obsidian, open <strong>Settings → Appearance → Themes</strong> and select <strong>Blue Night</strong>.</li>
    <li>
      Optional: install the
      <a href="https://github.com/obsidian-community/obsidian-style-settings">Style Settings</a> plugin to
      expose accent flavors, custom accent color, canvas variants, custom backgrounds, and feature toggles.
    </li>
  </ol>
</section>

<section id="snippets">
  <h2>Optional snippets</h2>
  <p class="section-lead">
    Each file in <a href="https://github.com/{{ site.repository }}/tree/main/snippets"><code>snippets/</code></a>
    is independent, avoids <code>!important</code>, and stays as variable-driven and low-specificity as its feature allows.
  </p>
  <div class="table-wrap">
    <table>
      <thead>
        <tr><th>Snippet</th><th>What it does</th></tr>
      </thead>
      <tbody>
        <tr><td><code>focus-mode.css</code></td><td>Dims desktop chrome until hover or keyboard focus</td></tr>
        <tr><td><code>rainbow-folders.css</code></td><td>Tints top-level folders with Blue Night/Catppuccin-inspired pastels</td></tr>
        <tr><td><code>colored-headings.css</code></td><td>Sets heading colors through Obsidian's heading variables</td></tr>
        <tr><td><code>wide-code.css</code></td><td>Lets code blocks, tables and Dataview results exceed readable line width</td></tr>
        <tr><td><code>wide-note.css</code></td><td>Opt-in <code>wide-note</code> cssclass for a wider whole-note layout</td></tr>
        <tr><td><code>clean-embeds.css</code></td><td>Makes note embeds seamless while preserving the source-note affordance</td></tr>
        <tr><td><code>image-grid.css</code></td><td>Opt-in <code>image-grid</code> cssclass for responsive galleries</td></tr>
        <tr><td><code>compact-tables.css</code></td><td>Reduces table padding and density through table variables</td></tr>
        <tr><td><code>compact-callouts.css</code></td><td>Makes native callouts denser without replacing their colors or icons</td></tr>
        <tr><td><code>math-accent.css</code></td><td>Adds a restrained Blue Night accent to MathJax and editor math</td></tr>
        <tr><td><code>minimal-scrollbar.css</code></td><td>Uses public scrollbar color variables with a slim 6px track</td></tr>
      </tbody>
    </table>
  </div>
  <p class="section-lead">
    <code>wide-note.css</code> and <code>image-grid.css</code> are per-note modifiers. Add
    <code>wide-note</code> and/or <code>image-grid</code> to the note's <code>cssclasses</code>
    property. The gallery's <code>:has()</code> selector is therefore evaluated only in notes that explicitly opt in.
  </p>
</section>
