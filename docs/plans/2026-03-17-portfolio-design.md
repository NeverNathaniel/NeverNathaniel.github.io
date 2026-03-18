# Portfolio Site Design — 2026-03-17

## Goal
Static GitHub Pages personal portfolio. Dramatic, text-only aesthetic with typewriter animation on page headings.

## Structure
Four separate HTML files, one shared CSS, one vendored JS.

```
/
├── index.html
├── useful.html
├── made.html
├── likes.html
├── css/style.css
└── js/typewrite.js
```

## Pages
- `index.html` — main landing / intro
- `useful.html` — things I find useful
- `made.html` — things I have made
- `likes.html` — things I like

## Visual
- Palette: `#006466` → `#4d194d` gradient background (teal to deep purple)
- Font: monospace/typewriter (Courier Prime or Special Elite via Google Fonts)
- Layout: centered column, max 680px, generous spacing
- Nav: fixed top bar, site name left, links right, active page highlighted
- Body text: off-white/light gray
- No images, no icons, no cards — pure text

## Animation
- typewrite.js (vendored from mrvautin/typewrite)
- Fires on `<h1>` hero heading on each page load
- Cursor blink after completion
- Body content appears immediately (no animation)
