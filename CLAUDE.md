# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Political campaign website for Prince Olisa Okwuchukwu Eze's 2027 election campaign (Dunukofia, Njikoka, and Anaocha constituencies, Nigeria). It is a **single self-contained HTML file** — no build system, no package manager, no dependencies.

**Main file:** `excellency_hifi.html` (~4,500 lines)

## Development

No build process. Open `excellency_hifi.html` directly in a browser. All CSS and JavaScript are embedded inline in the file.

## Architecture

The file is structured in three blocks:
1. `<head>` — meta tags, Google Fonts preconnect, and the entire `<style>` block (design system + responsive CSS)
2. `<body>` — 8 major sections plus nav, footer, and floating UI elements
3. Closing `<script>` — all interactivity

### Page Sections (by anchor `id`)
| ID | Section |
|----|---------|
| `home` | Hero with headline, CTAs, email signup |
| `about` | Candidate story/narrative |
| `impact` | Achievement cards with animated counters |
| `vision` | Policy pillars grid |
| `gallery` | Photo carousel |
| `join` | CTA + signup form |
| `testimonials` | Quote cards |
| `footer` | Links, social icons, membership signup |

### Design System (CSS Variables)
All tokens are defined at `:root`. Key values:
- **Colors:** Forest Green `#1D6A38` (accent), Campaign Red `#C0392B` (CTAs), Gold `#B8860B`, Navy `#0C1B29` (hero bg)
- **Spacing:** `--sp-1` through `--sp-10` (4px base scale)
- **Shadows:** `--shadow-xs` through `--shadow-xl`
- **Transitions:** `--t-fast` (150ms), `--t-base` (250ms), `--t-slow` (400ms)
- **Typography:** SF Pro Display/Text (system), Instrument Serif (editorial, via Google Fonts)
- **Breakpoints:** xs 320px / sm 481px / md 768px / lg 1024px / xl 1280px / 2xl 1440px

### JavaScript Modules (all in the single `<script>` block)
- `initPageLoad()` — hero entrance animations (staggered)
- `initScrollReveal()` — Intersection Observer for card reveal
- `initCounters()` — animated number counters (easeOutQuart)
- `initCardInteractions()` — 3D tilt hover on achievement cards, gallery zoom
- `initFormInteractions()` — floating label logic, validation, focus states
- `initButtonInteractions()` — ripple effects and press states
- `initSmoothNav()` + `initScrollObservers()` — smooth scroll + active nav sync
- `initHamburger()` — mobile menu toggle
- `initNavScroll()` — nav style change on scroll
- `initWAFloat()` — WhatsApp float button
- `showToast()` — toast notifications for form feedback
- `updateProgress()` — scroll progress bar

Performance patterns used: RAF throttling for scroll events, `prefers-reduced-motion` detection, `will-change` hints on animated elements.
