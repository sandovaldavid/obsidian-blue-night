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
  <p class="section-lead">Everything is embedded and offline — no external fonts, icons, or network requests.</p>
  <div class="feature-grid">
    <div class="feature-card" data-accent="blue">
      <h3>Night-blue palette</h3>
      <p>A deep <code>#0f1523</code> canvas with pastel accents in dark mode, and a crisp bluish slate in light mode.</p>
    </div>
    <div class="feature-card" data-accent="teal">
      <h3>Pastel syntax highlighting</h3>
      <p>Catppuccin-style code colors tuned for both dark and light modes, plus a language badge on code blocks.</p>
    </div>
    <div class="feature-card" data-accent="lavender">
      <h3>Minimalist SVG icons</h3>
      <p>Mask-based icons for callouts, checkboxes, explorer folders and files, and the vault name — they follow your accent.</p>
    </div>
    <div class="feature-card" data-accent="green">
      <h3>Extra task states</h3>
      <p>Beyond done: <code>[-]</code> cancelled, <code>[/]</code> in progress, <code>[?]</code> question, <code>[!]</code> important, <code>[&gt;]</code> forwarded.</p>
    </div>
    <div class="feature-card" data-accent="pink">
      <h3>Raycast-style switcher</h3>
      <p>Wide floating glass prompt with visible file paths, keyboard-hint pills, and soft accent selection.</p>
    </div>
    <div class="feature-card" data-accent="yellow">
      <h3>Plugin-aware</h3>
      <p>Extra styling for Style Settings, Dataview, and Quick Switcher++ that activates only when installed.</p>
    </div>
  </div>
</section>

<section id="flavors">
  <h2>Flavors</h2>
  <p class="section-lead">
    Pick your base canvas and accent family from Style Settings — every combination stays readable.
  </p>
  <div class="flavor-row">
    <div class="flavor">
      <div class="swatch" style="background:#0f1523">
        <span style="background:#8ab4fa"></span><span style="background:#b4befe"></span><span style="background:#8bd5ca"></span><span style="background:#f5bde6"></span>
      </div>
      <div class="flavor-info">
        <h3>Blue Night</h3>
        <p>The default deep night-blue canvas with the full pastel accent set.</p>
      </div>
    </div>
    <div class="flavor">
      <div class="swatch" style="background:#000000">
        <span style="background:#8ab4fa"></span><span style="background:#b4befe"></span><span style="background:#8bd5ca"></span><span style="background:#f5bde6"></span>
      </div>
      <div class="flavor-info">
        <h3>Dark Charcoal / OLED</h3>
        <p>Pure black canvas for OLED displays with deeper panels.</p>
      </div>
    </div>
    <div class="flavor">
      <div class="swatch" style="background:#1b1924">
        <span style="background:#cba6f7"></span><span style="background:#f5c2e7"></span><span style="background:#b4befe"></span><span style="background:#f5bde6"></span>
      </div>
      <div class="flavor-info">
        <h3>Cozy Pastels</h3>
        <p>Warm slate and lilac gray with a lavender-mauve accent.</p>
      </div>
    </div>
    <div class="flavor">
      <div class="swatch" style="background:#f7f9fc">
        <span style="background:#2563eb"></span><span style="background:#8ab4fa"></span><span style="background:#8bd5ca"></span><span style="background:#f5bde6"></span>
      </div>
      <div class="flavor-info">
        <h3>Clean Blue (Light)</h3>
        <p>Pure bluish white with night-blue accents for daylight work.</p>
      </div>
    </div>
  </div>
</section>

<section id="install">
  <h2>Installation</h2>
  <ol class="steps">
    <li>
      Download <code>theme.css</code> and <code>manifest.json</code> from the
      <a href="https://github.com/{{ site.repository }}/releases/latest">latest release</a>.
    </li>
    <li>Copy both files into your vault at <code>.obsidian/themes/Blue Night/</code>.</li>
    <li>In Obsidian, open <strong>Settings → Appearance → Themes</strong> and select <strong>Blue Night</strong>.</li>
    <li>
      Optional: install the
      <a href="https://github.com/mgmeyers/obsidian-style-settings">Style Settings</a> plugin to
      unlock flavors, accents, and every feature toggle.
    </li>
  </ol>
</section>

<section id="snippets">
  <h2>Optional snippets</h2>
  <p class="section-lead">
    Each file in <a href="https://github.com/{{ site.repository }}/tree/main/snippets"><code>snippets/</code></a>
    is independent — copy the ones you want into <code>.obsidian/snippets/</code> and enable them
    under <strong>Settings → Appearance → CSS snippets</strong>.
  </p>
  <div class="table-wrap">
    <table>
      <thead>
        <tr><th>Snippet</th><th>What it does</th></tr>
      </thead>
      <tbody>
        <tr><td><code>focus-mode.css</code></td><td>Hides ribbon, tabs and status bar until hovered (zen writing)</td></tr>
        <tr><td><code>rainbow-folders.css</code></td><td>Tints each top-level folder with a different pastel</td></tr>
        <tr><td><code>colored-headings.css</code></td><td>Gives every heading level its own pastel color</td></tr>
        <tr><td><code>wide-code.css</code></td><td>Lets code blocks, tables and Dataview results exceed line width</td></tr>
        <tr><td><code>clean-embeds.css</code></td><td>Removes borders and padding from note embeds for seamless transclusion</td></tr>
        <tr><td><code>image-grid.css</code></td><td>Lays out consecutive images in a responsive grid</td></tr>
        <tr><td><code>minimal-scrollbar.css</code></td><td>Slim, unobtrusive scrollbars that match the palette</td></tr>
      </tbody>
    </table>
  </div>
</section>
