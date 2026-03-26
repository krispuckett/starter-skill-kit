---
name: obsidian-design
description: >-
  Design beautiful Obsidian themes, CSS snippets, and ASCII/Unicode data
  visualizations for markdown. Use when building custom Obsidian themes,
  creating CSS snippets for vault styling, designing ASCII charts or progress
  bars for markdown notes, or any request involving "make my vault look good,"
  "Obsidian theme," "CSS snippet," "data visualization in markdown," "progress
  bars in notes," or "ASCII charts." Covers both the visual design layer (CSS
  custom properties, typography, color systems) and the data display layer
  (monospace-safe characters, Unicode rendering, sparklines, progress bars).
  Trigger on any Obsidian visual customization request. NOT for Obsidian plugin
  development (JS/TS), sync configuration, or vault structure/organization.
---

# Obsidian Design — Themes, CSS Snippets & Markdown Data Visualization

You're designing for a tool that people live in. Obsidian is where they think, write, and build their second brain. Every visual decision affects how it *feels* to use — rushed theming or ugly data displays break the spell. Take this seriously.

---

## Part 1: ASCII & Unicode Data Visualization in Markdown

### The Core Problem

Markdown code blocks (`\`\`\``) render in monospace fonts. Most Unicode characters were designed for proportional fonts. What looks perfect in your terminal or code editor may render as unreadable noise in Obsidian, especially on mobile (iOS/Android).

### Character Rendering Rules

**Use freely — render consistently everywhere:**
```
█ ░ ▓       Block elements (full, light shade, medium shade)
─ │ ┌ ┐ └ ┘ ├ ┤ ┬ ┴ ┼   Box drawing (single line)
═ ║ ╔ ╗ ╚ ╝ ╠ ╣ ╦ ╩ ╬   Box drawing (double line)  
→ ← ↑ ↓ ✓ ✗ ·           Arrows, checks, middle dot
● ○ ◆ ◇ ■ □              Basic geometric shapes
```

**Avoid — inconsistent rendering across platforms:**
```
▁▂▃▄▅▆▇   Fractional block heights — most monospace fonts render 
           these at IDENTICAL height. They only vary in theory.
           On macOS Obsidian, iOS, and most terminals, you get
           8 identical-looking rectangles. Useless for sparklines.

⠀⢀⣀⣄⣤⣦⣶⣿  Braille patterns — technically vary by dot density,
           but at typical font sizes (13-16px) the differences are
           imperceptible. Looks like random noise to humans.

╸━         Line weight variations — rendering depends heavily on
           font. Often indistinguishable.
```

**Why fractional blocks fail:** The Unicode block elements ▁▂▃▄▅▆▇█ are designed to fill different vertical portions of the character cell. But monospace fonts in code blocks typically render them all at the same baseline with minimal visible height difference. The *idea* is sound; the *execution* across real fonts is broken. Don't use them for sparklines.

### What Works: Progress Bars

Progress bars using █ (full) and ░ (empty) are the most readable data visualization in monospace markdown. They work because:

1. **Binary contrast** — full vs empty is unmistakable at any font size
2. **Consistent width** — both characters occupy exactly one monospace cell
3. **Intuitive** — everyone understands a filled/unfilled bar
4. **Scannable** — 8-10 character bars are graspable at a glance

#### Progress Bar Pattern

```javascript
function progressBar(value, target, width = 8) {
  const pct = Math.max(0, Math.min(1, value / target));
  const filled = Math.round(pct * width);
  return '█'.repeat(filled) + '░'.repeat(width - filled);
}
```

#### Layout Pattern — Value + Bar + Status

The most readable layout for health/metric dashboards:

```
Label    Value   Bar        Status
─────────────────────────────────
Sleep    7h12m   ████████░  ✓
Deep     0h45m   ████░░░░░  ↓
HRV       32ms   █████░░░░  →
Steps    8,241   ████████░  ↑
```

Design principles:
- **Label** left-aligned, padded to consistent width (5-8 chars)
- **Value** right-aligned with unit, padded to consistent width
- **Bar** fixed width (8 chars recommended), immediately after value
- **Status** trend arrow or check/cross, after bar
- Use 2-space gaps between columns for breathing room

#### Inverted Metrics

Some metrics are "lower is better" (resting heart rate, stress index). For these, invert the bar calculation:

```javascript
// RHR: target is 55, ceiling is 75 (higher = worse)
const invertedPct = (ceiling - value) / (ceiling - target);
```

This way a full bar always means "good" regardless of metric direction.

#### Handling Partial/Missing Data

- Missing day in a time series: show `·` (middle dot) — not a space, not a dash
- Metric with no samples today: show `--` for value, empty bar for visual
- Mid-day partial data (e.g., steps at 2pm): show current value, consider a note like `(midday)` or mark the bar differently

### What Also Works: Simple Tables

For non-time-series data, aligned columns with box drawing:

```
┌─────────┬────────┬────────┐
│ Metric  │ Today  │ 7d Avg │
├─────────┼────────┼────────┤
│ Sleep   │ 7h12m  │ 6h45m  │
│ HRV     │ 32ms   │ 28ms   │
└─────────┴────────┴────────┘
```

Or simpler — just aligned text with consistent padding. Don't over-decorate.

### What Doesn't Work (And Why)

| Approach | Problem |
|---|---|
| Sparklines with ▁▂▃▄▅▆▇ | Identical height in monospace. No visual information. |
| Braille dot density ⠀⢀⣀⣄⣤ | Imperceptible differences at body text size. |
| Emoji-based charts 🟩🟨🟥 | Inconsistent width (emoji are often 2 cells wide). Breaks alignment. |
| Color in code blocks | Code blocks don't support inline color in standard markdown. |
| HTML in code blocks | Rendered as literal text, not markup. |

### Obsidian-Specific: Dataview & Templater

If the user has Dataview or Templater plugins, you can generate dynamic visualizations. But the *rendering* rules are the same — the output still lands in markdown, and the same character constraints apply.

For Dataview inline queries that render outside code blocks, you have access to HTML/CSS and can use actual colored bars via `<span>` elements with inline styles. This is a different (and more powerful) path than code block ASCII art.

---

## Part 2: Obsidian CSS Themes & Snippets

### Theme Architecture

Obsidian themes are single CSS files that override CSS custom properties and add style rules. They live in `.obsidian/themes/` as `ThemeName/theme.css` with a `manifest.json`.

#### manifest.json
```json
{
  "name": "Theme Name",
  "version": "1.0.0",
  "minAppVersion": "1.0.0"
}
```

#### CSS Custom Properties (The Foundation)

Obsidian exposes hundreds of CSS variables. The most impactful ones for theming:

**Colors — Background hierarchy:**
```css
body {
  --background-primary: #1a1a2e;         /* Main editor */
  --background-primary-alt: #16213e;     /* Slightly different alt */
  --background-secondary: #0f3460;       /* Sidebar */
  --background-secondary-alt: #0a2647;   /* Sidebar sections */
  --background-modifier-border: #1a3a5c; /* Borders */
  --background-modifier-hover: rgba(255,255,255,0.05); /* Hover states */
}
```

**Colors — Text hierarchy:**
```css
body {
  --text-normal: #e0e0e0;       /* Body text */
  --text-muted: #888;           /* Secondary text */
  --text-faint: #555;           /* Tertiary text */
  --text-accent: #4fc3f7;       /* Links, accents */
  --text-accent-hover: #81d4fa; /* Accent hover */
  --text-on-accent: #000;       /* Text on accent backgrounds */
  --interactive-accent: #4fc3f7;/* Buttons, toggles, active states */
}
```

**Typography:**
```css
body {
  --font-text-theme: 'Inter', -apple-system, sans-serif;
  --font-monospace-theme: 'JetBrains Mono', 'Fira Code', monospace;
  --font-text-size: 16px;
  --line-height-normal: 1.6;
  --bold-weight: 600;
}
```

**Editor spacing:**
```css
body {
  --file-line-width: 700px;              /* Max editor width */
  --p-spacing: 1rem;                     /* Paragraph spacing */
  --heading-spacing: 0.5em;              /* Space before headings */
  --indentation-guide-width: 1px;        /* Indent guides */
}
```

### Design Principles for Obsidian Themes

**1. Respect the content hierarchy.**
Obsidian is a writing tool. The theme should make text comfortable to read for hours, not compete with it. Background colors should recede. Text contrast should be high enough (WCAG AA minimum) without being harsh.

**2. Design for both light and dark.**
Use `.theme-dark` and `.theme-light` selectors. Many users switch between modes. Don't assume one.

```css
.theme-dark {
  --background-primary: #1e1e2e;
  --text-normal: #cdd6f4;
}
.theme-light {
  --background-primary: #eff1f5;
  --text-normal: #4c4f69;
}
```

**3. Typography makes or breaks it.**
- Body text: 15-18px, line-height 1.5-1.7
- Use a proper text font (Inter, iA Writer, Literata, Source Serif) — not system defaults
- Monospace for code: pick one with good Unicode coverage (JetBrains Mono, Fira Code, Cascadia Code)
- Heading scale should be restrained. H1 doesn't need to be 3x body size.

**4. Subtle is better than loud.**
The best Obsidian themes (Minimal, Things, Prism) share a quality: you barely notice them. They make Obsidian feel *refined* without being distracting. If someone's first reaction to your theme is "wow, look at all the colors" — it's too much.

**5. Code block styling matters.**
Many power users spend significant time in code blocks (dataview queries, templates, actual code). Style them intentionally:

```css
.markdown-rendered pre,
.markdown-source-view .cm-line .cm-inline-code {
  background-color: var(--background-secondary);
  border-radius: 4px;
  padding: 0.8em 1em;
  font-size: 0.9em;
}
```

### CSS Snippets

Snippets live in `.obsidian/snippets/` and are toggled per-vault. They're ideal for targeted customizations without building a full theme.

Common high-value snippets:

**Readable line width override:**
```css
.markdown-source-view.mod-cm6 .cm-content,
.markdown-preview-view {
  max-width: 750px !important;
  margin: 0 auto;
}
```

**Custom checkbox styles:**
```css
input[data-task="!"]:checked {
  --checkbox-color: var(--color-orange);
  --checkbox-marker-color: var(--background-primary);
}
```

**Heading styling:**
```css
.markdown-rendered h1 {
  font-family: 'Instrument Serif', serif;
  border-bottom: 1px solid var(--background-modifier-border);
  padding-bottom: 0.3em;
}
```

### Testing a Theme

1. Write the CSS file
2. Place in `.obsidian/themes/ThemeName/theme.css` with `manifest.json`
3. Activate in Settings → Appearance → Themes
4. Test in both light and dark mode
5. Test on mobile (iOS/Android Obsidian) — font sizes and spacing differ significantly
6. Test with common plugins (Dataview, Calendar, Kanban) — they add their own DOM elements

### Color Palette Design

When building a color palette for an Obsidian theme:

- Start with 2-3 base colors max. Dark themes: a dark neutral + one accent. Light themes: a warm/cool white + one accent.
- Derive the full palette through opacity and lightness shifts, not by picking 15 independent colors
- Test syntax highlighting colors against your background — code readability is non-negotiable
- Graph view colors should be muted versions of your accent palette

---

## Part 3: Combining Both — Data-Rich Vaults

When a vault uses both custom themes AND ASCII data visualizations (dashboards, health trackers, daily notes with metrics), the theme needs to account for code block rendering:

1. **Test your progress bars** in the actual theme's code block styling. Font choice affects character alignment.
2. **Ensure monospace font has good Unicode coverage.** JetBrains Mono and Fira Code handle █░▓ and box drawing well. Some fonts don't.
3. **Code block background contrast** needs to support the visual weight of progress bars without being too dark or too light.
4. **Mobile code blocks** often have different padding and font size. Test the dashboard rendering on both platforms.

---

## Quick Reference: Decision Tree

**User wants data in their notes?**
→ Time series with targets? → Progress bars (█░)
→ Comparison table? → Aligned columns or box drawing
→ Status indicators? → ✓ ✗ → ↑ ↓ ● ○

**User wants their vault to look better?**
→ Quick fix? → CSS snippet
→ Full overhaul? → Custom theme
→ Just typography? → Font snippet + `--font-text-theme` override

**User says "sparklines"?**
→ Explain why fractional blocks don't render distinctly
→ Offer progress bars as the better alternative
→ If they insist on inline sparklines, Dataview + HTML spans with colored backgrounds is the real path
