# obsidian-design

A Claude skill for designing Obsidian themes, CSS snippets, and data visualizations that actually render correctly.

## The Problem

I wanted data dashboards in my Obsidian notes. Health metrics, progress bars, sparklines — stuff I could glance at and immediately know where things stand.

Tried the Unicode block elements everyone recommends: `▁▂▃▄▅▆▇█`. All render at the same height in monospace. Tried braille patterns. Noise. Tried shade characters. Indistinguishable.

Built this skill so Claude stops suggesting characters that don't actually work and starts with the ones that do.

## What It Covers

**Data visualization in markdown** — Which Unicode characters actually render distinctly across platforms. Progress bar patterns. Layout templates for metric dashboards. How to handle missing data, inverted metrics, partial-day values.

**Obsidian theming** — CSS custom properties, typography, color systems, snippets. How to build a theme that makes your vault feel refined without being distracting. Light and dark mode. Mobile testing gotchas.

**Combining both** — When your vault has custom themes AND code-block dashboards, the theme's monospace font choice affects whether your progress bars align correctly. The skill covers that intersection.

## Install

Drop the `obsidian-design/` folder into your Claude skills directory:

```bash
# Claude Code
cp -r obsidian-design/ ~/.claude/skills/

# Or wherever you keep your skills
```

## Example Output

What a health dashboard looks like when you stop fighting Unicode:

```
Sleep    7h12m  ████████░  ✓
Deep     1h08m  ██████░░░  ↓
REM      1h40m  ███████░░  ↓
HRV      100ms  █████████  ↑
RHR      56bpm  ████████░  →
Steps    8,241  ████████░  ↑
Cals      809   █████████  ✓
```

Value on the left. Bar in the middle. Trend arrow on the right. Instantly readable. No decoder ring.

## When It Triggers

Ask Claude anything about:
- Making your Obsidian vault look better
- Building a custom theme or CSS snippet
- ASCII/Unicode charts or progress bars in markdown
- Data visualization in notes
- "Why do my sparklines look broken"

## Why This Exists

Design lessons are expensive. This one cost a full iteration cycle of trying every Unicode character set before landing on the obvious answer. Might as well share it.
