# CARE Lab Website — Guide for Claude Code

## Overview

Static website for the **CARE Lab** (Child, Adolescent, Resilience, and Ecology Lab) at Texas Tech University, directed by **Dr. Wonjung Oh**. The entire site is a single file: `index.html` — all CSS, content, and JavaScript live there. There is no build step, no framework, no dependencies.

The site is a hash-routed single-page app: every "page" (Home, Research, Publications, People, News, Join, Contact) is a `<div class="page" id="page-...">` inside the same file, shown/hidden by a small JS router (`#/research`, `#/people`, etc.).

## Deployment

Push to `main` → GitHub Pages redeploys automatically, usually live within a minute. There is no build process (`.nojekyll` disables Jekyll). To check: `curl -sI https://<owner>.github.io/care-lab/ | head -1`.

## Design system

All design tokens are CSS variables defined in `:root` near the top of `index.html`:

| Variable | Value | Role |
|---|---|---|
| `--red` | `#D8121B` | Primary accent (TTU red) — links, buttons, eyebrows |
| `--red-dark` | `#A50E14` | Hover state for primary buttons |
| `--ink` | `#16130F` | Main text |
| `--ink-soft` | `#3E3933` | Secondary text |
| `--muted` | `#5F5A54` | Captions, meta text |
| `--line` | `#E7E2DC` | Borders, dividers |
| `--paper` | `#F8F6F3` | Alternate section background |
| `--white` | `#FFFFFF` | Base background |
| `--display` | Space Grotesk | Headings, nav, buttons, labels |
| `--body` | Source Serif 4 | Body text |
| `--maxw` | `1080px` | Content max width |
| `--pad` | `24px` | Horizontal page padding |

**When changing colors or spacing, edit these variables first** instead of hardcoding values in individual rules — most of the site derives from them. Fonts load from Google Fonts (see `<link>` tags in `<head>`).

Recurring patterns: `.eyebrow` (red uppercase label with diamond), `.section` / `.section.alt` (white / paper bands), `.btn` / `.btn.primary` (outline / red buttons), `.reveal` (scroll-in animation). The Join and Contact pages use a dark inverted theme.

## Structure map (approximate line numbers)

| Lines | What |
|---|---|
| 1–297 | `<head>` + all CSS (grouped by `/* ---------- name ---------- */` banners) |
| 298–327 | Fixed top nav |
| 329–382 | Home (`#page-home`) — hero + about merged; recruiting banner chip |
| 384–436 | Research (`#page-research`) — research themes |
| 438–550 | Publications (`#page-publications`) — filterable list |
| 552–672 | People (`#page-people`) — faculty / grad students / alumni / collaborators |
| 674–717 | News (`#page-news`) — timeline, includes recruiting notice |
| 719–758 | Join (`#page-join`, dark) — recruiting info + contact CTA |
| 760–801 | Contact (`#page-contact`, dark) |
| 803–830 | Footer |
| 832–897 | JS: hash router, mobile menu, publication filters, reveal animations |

Frequently edited spots are wrapped in `<!-- ✏️ EDIT: ... START/END -->` markers (recruiting banner, publications list, people, news recruiting item, join note) — search for `✏️ EDIT` to jump to them. Keep these markers when editing.

## Working principles

- Content and design edits are both welcome — change whatever the request calls for.
- Before a large change (layout overhaul, new section, redesign), show a summary of the planned changes first, then proceed.
- Commit messages: one line, in English.
