# BLUEPRINT-DESIGN.md — Universal Website Design System

> Drop this file into ANY project folder. Claude Code reads it and every page it builds will come out in this exact style — same fonts, colors, layout patterns, components, animations, and tone. Works for any website: course, portfolio, SaaS landing, blog, docs. Replace only the content, never the design rules.

---

## HOW TO USE

1. Put this file at the root of your project folder.
2. Tell Claude Code: "Read BLUEPRINT-DESIGN.md. Build [your pages] using my content. Follow every rule in the file exactly."
3. Every page will match this design system automatically.

---

## 1. FONTS

Load these from Google Fonts on every page:
```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=VT323&family=Source+Serif+4:ital,opsz,wght@0,8..60,400..700;1,8..60,400..700&family=JetBrains+Mono:wght@400;500;700&display=swap" rel="stylesheet">
```

Use:
- **VT323** → page titles, hero headings, section eyebrows (big, pixel/terminal look)
- **Source Serif 4** → all body text and paragraphs (readable serif)
- **JetBrains Mono** → labels, meta rows, code, buttons, nav links, figure captions

---

## 2. COLORS

### Light theme (default — put in `:root`)
```css
:root {
  --font-display: 'VT323', ui-monospace, 'JetBrains Mono', monospace;
  --font-body: 'Source Serif 4', 'Source Serif Pro', Georgia, serif;
  --font-mono: 'JetBrains Mono', ui-monospace, 'Consolas', monospace;
  --font-heading: var(--font-display);

  --bg: #fafaf5;
  --bg-surface: #f3f1e8;
  --bg-surface-hover: #ece9dc;
  --ink: #1a1a1a;
  --ink-soft: #4a4a4a;
  --ink-mute: #7a7a78;
  --rule: #1a1a1a;
  --rule-soft: rgba(26, 26, 26, 0.16);
  --paper-rule: rgba(26, 26, 26, 0.08);

  --blueprint: #3553ff;
  --blueprint-tint: rgba(53, 83, 255, 0.08);
  --blueprint-tint-strong: rgba(53, 83, 255, 0.18);

  --code-bg: #efece0;
  --header-bg: rgba(250, 250, 245, 0.94);
  --overlay-bg: rgba(26, 26, 26, 0.55);

  --shadow-hard: 3px 3px 0 var(--ink);
  --shadow-hard-lg: 5px 5px 0 var(--ink);

  --motion-press: 160ms;
  --motion-enter: 220ms;
  --ease-out: cubic-bezier(0.23, 1, 0.32, 1);

  --header-offset: 92px;
}
```

### Dark theme
```css
[data-theme="dark"] {
  --bg: #0a0d1a;
  --bg-surface: #131830;
  --bg-surface-hover: #1b2244;
  --ink: #e8e6dc;
  --ink-soft: #a8a6a0;
  --ink-mute: #7a7878;
  --rule: #e8e6dc;
  --rule-soft: rgba(232, 230, 220, 0.18);
  --paper-rule: rgba(232, 230, 220, 0.08);

  --blueprint: #6b8eff;
  --blueprint-tint: rgba(107, 142, 255, 0.12);
  --blueprint-tint-strong: rgba(107, 142, 255, 0.22);

  --code-bg: #131830;
  --header-bg: rgba(10, 13, 26, 0.94);
  --overlay-bg: rgba(10, 13, 26, 0.78);
}
```

**Rule:** Only one accent color — blue (`--blueprint`). Nothing else is colored. Status colors: blue = complete, grey = in-progress, light grey = planned.

---

## 3. BACKGROUND

Every page gets this dotted-grid paper background. Never skip it:
```css
body {
  font-family: var(--font-body);
  font-size: 18px;
  line-height: 1.62;
  color: var(--ink);
  background-color: var(--bg);
  background-image: radial-gradient(var(--paper-rule) 1px, transparent 1px);
  background-size: 16px 16px;
  background-attachment: fixed;
  -webkit-font-smoothing: antialiased;
  hyphens: auto;
  transition: background-color 0.2s, color 0.2s;
}
```

---

## 4. LAYOUT

```
.container { max-width: 1080px; margin: 0 auto; padding: 0 24px; }
```

Page skeleton (use on every page):
```
<header class="site-header">  ← sticky, translucent, blur
  <div class="header-inner">
    logo · nav links · search button · theme toggle
  </div>
</header>

<main id="main" class="container">
  ...content...
</main>

<footer class="site-footer">
  <div class="container footer-inner">
    <p>© 2026 · [your tagline]</p>
    <div class="footer-links"> link | link | link </div>
  </div>
</footer>
```

### Header
```css
.site-header {
  position: sticky; top: 0; z-index: 100;
  background: var(--header-bg);
  backdrop-filter: blur(8px);
  border-bottom: 1px solid var(--rule-soft);
}
.header-inner {
  max-width: 1080px; margin: 0 auto;
  padding: 0 24px; height: 64px;
  display: flex; align-items: center; gap: 20px;
}
.header-nav a {
  font-family: var(--font-mono); font-size: 13px;
  color: var(--ink-soft); text-decoration: none;
  letter-spacing: 0.02em;
}
.header-nav a:hover { color: var(--blueprint); }
```

### Footer
```css
.site-footer { border-top: 1px solid var(--rule-soft); padding: 32px 0; }
.footer-inner { display: flex; justify-content: space-between; align-items: center; }
.footer-links a {
  font-family: var(--font-mono); font-size: 13px;
  color: var(--ink-soft); margin-left: 20px; text-decoration: none;
}
.footer-links a:hover { color: var(--blueprint); }
```

---

## 5. HERO SECTION (top of home page)

Always build the hero in this order:

1. **Meta row** — monospace, small, muted. Figure number + version + license.
   ```html
   <div class="manual-meta-row">
     <span>FIG_000 · [version] · [year]</span>
     <span class="right">[badge] · [badge]</span>
   </div>
   ```

2. **Big title** — VT323 font, large (64–80px), two lines with `<br>`.
   ```css
   .manual-title {
     font-family: var(--font-display);
     font-size: 76px; line-height: 0.95;
     color: var(--ink); margin: 16px 0 12px;
   }
   ```

3. **Tagline** — one sentence, serif, 20–22px.
4. **Attribution** — "Maintained by [name]. [detail]."

5. **CTA buttons** — always two: primary (blue, filled) + secondary (outline).
   ```css
   .masthead-btn {
     display: inline-flex; align-items: center; gap: 8px;
     padding: 10px 18px; border: 1px solid var(--ink);
     background: var(--bg); color: var(--ink);
     font-family: var(--font-mono); font-size: 13px;
     text-decoration: none; box-shadow: var(--shadow-hard);
     transition: transform var(--motion-press), box-shadow var(--motion-press);
   }
   .masthead-btn:active {
     transform: translate(3px, 3px); box-shadow: 0 0 0 var(--ink);
   }
   .masthead-btn--primary {
     background: var(--blueprint); color: #fff; border-color: var(--blueprint);
   }
   .masthead-btn:hover { border-color: var(--blueprint); color: var(--blueprint); }
   .masthead-btn--primary:hover { color: #fff; opacity: 0.9; }
   ```

6. **Terminal block** — grey code window with title bar + copy button.
   ```css
   .masthead-install pre {
     background: var(--code-bg); border: 1px solid var(--rule-soft);
     padding: 16px 20px; font-family: var(--font-mono); font-size: 14px;
     overflow-x: auto; margin: 0;
   }
   .masthead-install-bar {
     display: flex; justify-content: space-between; align-items: center;
     font-family: var(--font-mono); font-size: 12px;
     color: var(--ink-mute); padding: 8px 20px;
     background: var(--bg-surface); border: 1px solid var(--rule-soft);
     border-bottom: none;
   }
   .copy-chip {
     font-family: var(--font-mono); font-size: 11px;
     border: 1px solid var(--rule-soft); background: var(--bg);
     padding: 2px 8px; cursor: pointer; color: var(--ink-soft);
   }
   .copy-chip:hover { color: var(--blueprint); border-color: var(--blueprint); }
   ```

7. **Agent/tool chips** — small monospace pills below the terminal.
   ```css
   .agent-chip {
     font-family: var(--font-mono); font-size: 12px;
     color: var(--ink-mute); border: 1px solid var(--rule-soft);
     padding: 4px 10px; display: inline-flex; align-items: center; gap: 6px;
   }
   ```

8. **Caption** — one italic-ish line below in muted serif.

---

## 6. SECTION COMPONENTS

### Section eyebrow (label above each section)
```css
.section-eyebrow {
  font-family: var(--font-mono); font-size: 12px;
  letter-spacing: 0.14em; color: var(--ink-mute);
  text-transform: uppercase; margin-bottom: 8px;
}
```

### Section heading
```css
.section-heading {
  font-family: var(--font-display); font-size: 40px;
  color: var(--ink); margin-bottom: 16px; line-height: 1.1;
}
```

### Card / surface box
```css
.surface-card {
  background: var(--bg-surface); border: 1px solid var(--rule-soft);
  padding: 24px; transition: background var(--motion-enter);
}
.surface-card:hover { background: var(--bg-surface-hover); }
```

### Code block (inline in content)
```css
code {
  font-family: var(--font-mono); font-size: 0.88em;
  background: var(--code-bg); padding: 2px 6px;
  border: 1px solid var(--rule-soft);
}
```

### Links
```css
a { color: var(--blueprint); text-decoration: none; border-bottom: 1px solid var(--blueprint-tint); }
a:hover { border-bottom-color: var(--blueprint); }
```

### List
```css
ul { padding-left: 20px; }
li { margin-bottom: 8px; line-height: 1.62; }
```

---

## 7. REVEAL ANIMATIONS

Elements fade+slide in with staggered delays. Use the `.reveal` class + `--stagger-delay`:
```css
.reveal {
  opacity: 0; transform: translateY(12px);
  animation: reveal-up var(--motion-enter) var(--ease-out) forwards;
  animation-delay: var(--stagger-delay, 0ms);
}
@keyframes reveal-up { to { opacity: 1; transform: translateY(0); } }

@media (prefers-reduced-motion: reduce) {
  .reveal { opacity: 10; transform: none; animation: none; }
}
```

Usage in HTML:
```html
<p class="reveal">first line</p>
<p class="reveal" style="--stagger-delay: 80ms;">second line</p>
<p class="reveal" style="--stagger-delay: 160ms;">third line</p>
```

---

## 8. THEME TOGGLE

Every page gets this button in the header and this script at the bottom:

**Button:**
```html
<button class="theme-toggle" id="themeToggle" aria-label="Toggle theme" type="button">
  <span class="theme-icon" id="themeIcon">N</span>
</button>
```

**Script (put before `</body>`):**
```html
<script>
(function () {
  var root = document.documentElement;
  var stored = localStorage.getItem('theme');
  if (stored) root.setAttribute('data-theme', stored);
  else if (window.matchMedia && window.matchMedia('(prefers-color-scheme: dark)').matches)
    root.setAttribute('data-theme', 'dark');
  else root.setAttribute('data-theme', 'light');

  function updateIcon() {
    var icon = document.getElementById('themeIcon');
    if (icon) icon.textContent = root.getAttribute('data-theme') === 'light' ? 'N' : 'D';
  }
  updateIcon();
  document.addEventListener('DOMContentLoaded', function () {
    updateIcon();
    var btn = document.getElementById('themeToggle');
    if (btn) btn.addEventListener('click', function () {
      var next = root.getAttribute('data-theme') === 'light' ? 'dark' : 'light';
      root.setAttribute('data-theme', next);
      localStorage.setItem('theme', next);
      updateIcon();
    });
  });
})();
</script>
```

**Button CSS:**
```css
.theme-toggle {
  font-family: var(--font-mono); font-size: 14px;
  border: 1px solid var(--rule-soft); background: var(--bg);
  width: 32px; height: 32px; cursor: pointer;
  color: var(--ink-soft); border-radius: 0;
}
.theme-toggle:hover { color: var(--blueprint); border-color: var(--blueprint); }
```

---

## 9. SEO (on every page)

```html
<title>[Page title] · [Site name]</title>
<meta name="description" content="[One sentence description]">
<link rel="canonical" href="[full URL]">
<meta property="og:title" content="[Page title]">
<meta property="og:description" content="[One sentence]">
<meta property="og:image" content="[image URL]">
<meta property="og:url" content="[page URL]">
<meta property="og:type" content="website">
<meta name="twitter:card" content="summary_large_image">
```

Favicon (inline SVG, blue border + monospace text):
```html
<link rel="icon" href="data:image/svg+xml,<svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 32 32'><rect width='32' height='32' fill='%23fafaf5'/><rect x='2' y='2' width='28' height='28' fill='none' stroke='%233553ff' stroke-width='1.2'/><text x='6' y='22' font-size='14' font-family='monospace' fill='%233553ff'>AI</text></svg>">
```

---

## 10. DESIGN RULES (never break these)

1. **No frameworks.** Plain HTML, CSS, vanilla JS. No React, Tailwind, Bootstrap.
2. **One accent color only** — blue `#3553ff`. Everything else is ink/grey/paper.
3. **Dotted-grid background** on every page. Always.
4. **Hard shadows** on buttons and cards (`3px 3px 0 solid`). No soft shadows, no glow.
5. **VT323 for titles.** Big, pixel, terminal-like. Source Serif for body. Mono for labels.
6. **Blueprint labels.** Figure numbers (FIG_001), monospace meta rows, technical annotations.
7. **Terminal block** on the home page — grey window, title bar, copy button.
8. **Dark mode toggle** on every page. Persists in localStorage. Respects system preference.
9. **Reveal animations** — elements fade in with staggered delays. Quick (220ms), ease-out.
10. **Responsive** — must work on mobile. Stack buttons, reduce font sizes, hide large figures.
11. **Sticky translucent header** with backdrop blur.
12. **Minimal footer** — copyright line + text links.

---

## 11. TONE & VOICE

- Direct, no fluff. Every sentence earns its place.
- Technical but warm. Short declarative sentences.
- No marketing buzzwords. No "revolutionary," "10x," "unlock."
- Honest and plain. Say what it is and why it exists.
- Footer: `© [year] · [tagline]`

---

## 12. BUILD APPROACH

- Every page is a standalone `.html` file.
- One shared `style.css` for all pages.
- Shared JS files for header, search, theme toggle.
- No build step required for basic pages — just open in a browser.
- Deploy: push to GitHub → connect to Vercel or Cloudflare Pages → live.

---

## 13. CLAUDE CODE INSTRUCTION TEMPLATE

When starting a new project with this file, tell Claude Code:

> "Read BLUEPRINT-DESIGN.md. Build a website with these pages: [list pages]. Use my content for all text. Follow every design rule in the file — same fonts, colors, dotted background, hard shadows, terminal block, theme toggle, reveal animations, and tone. No frameworks. Plain HTML/CSS/JS. Start with the home page, I'll review before you continue."

Then iterate: review each page in the browser, give small tweaks, move to the next page.
