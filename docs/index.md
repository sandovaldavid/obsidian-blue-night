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
      <p>Choose Blue Night, Lavender, Teal, Pink, or Custom. Every option converges on Obsidian's native <code>--accent-h</code>, <code>--accent-s</code>, and <code>--accent-l</code> variables.</p>
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
    Canvas variants and accent flavors are independent. Mix Blue Night, OLED, or Cozy Pastels surfaces with Blue Night, Lavender, Teal, Pink, or your own custom accent.
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
      <div class="swatch" style="background:#000000">
        <span style="background:#b4befe"></span><span style="background:#8ab4fa"></span><span style="background:#8bd5ca"></span><span style="background:#f5bde6"></span>
      </div>
      <div class="flavor-info">
        <h3>OLED + Lavender</h3>
        <p>Pure black canvas with Lavender as the interactive accent while syntax and semantic colors remain multi-color.</p>
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
      <div class="swatch" style="background:#f7f9fc">
        <span style="background:#f5bde6"></span><span style="background:#1e66f5"></span><span style="background:#147d83"></span><span style="background:#7048c9"></span>
      </div>
      <div class="flavor-info">
        <h3>Clean Blue + Pink</h3>
        <p>Bluish white surfaces with Pink as the interactive accent and high-contrast supporting colors for daylight work.</p>
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
    is independent and avoids <code>!important</code>, so your own snippets can still override it.
  </p>
  <div class="table-wrap">
    <table>
      <thead>
        <tr><th>Snippet</th><th>What it does</th></tr>
      </thead>
      <tbody>
        <tr><td><code>focus-mode.css</code></td><td>Hides ribbon, tabs and status bar until hovered (zen writing)</td></tr>
        <tr><td><code>rainbow-folders.css</code></td><td>Tints each top-level folder with a different pastel</td></tr>
        <tr><td><code>colored-headings.css</code></td><td>Sets heading colors through Obsidian's heading variables</td></tr>
        <tr><td><code>wide-code.css</code></td><td>Lets code blocks, tables and Dataview results exceed line width</td></tr>
        <tr><td><code>clean-embeds.css</code></td><td>Removes borders and padding from note embeds for seamless transclusion</td></tr>
        <tr><td><code>image-grid.css</code></td><td>Lays out consecutive images in a responsive grid</td></tr>
        <tr><td><code>minimal-scrollbar.css</code></td><td>Uses public scrollbar color variables with a slim 6px track</td></tr>
      </tbody>
    </table>
  </div>
</section>
