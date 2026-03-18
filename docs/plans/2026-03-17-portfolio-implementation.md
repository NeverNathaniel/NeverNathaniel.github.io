# Portfolio Site Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Build a static 4-page GitHub Pages portfolio with a dark teal-to-purple gradient theme, typewriter font, and typewrite.js heading animation.

**Architecture:** Four standalone HTML files sharing one CSS file and one vendored JS file. No build step. jQuery loaded from CDN; typewrite.js vendored locally. Navigation is a fixed top bar repeated across all pages.

**Tech Stack:** HTML5, CSS3, jQuery 3.x (CDN), typewrite.js (vendored from mrvautin/typewrite)

---

### Task 1: Scaffold file structure

**Files:**
- Create: `css/style.css` (empty)
- Create: `js/typewrite.js` (vendored content)
- Create: `index.html`
- Create: `useful.html`
- Create: `made.html`
- Create: `likes.html`

**Step 1: Create css/style.css**

Create the file with a single comment:
```css
/* portfolio styles */
```

**Step 2: Vendor typewrite.js**

Create `js/typewrite.js` with the full content from:
https://raw.githubusercontent.com/mrvautin/typewrite/master/src/typewrite.js

(jQuery plugin — paste the full IIFE as-is)

**Step 3: Create all four HTML stubs**

Each file gets the same shell — replace PAGE_TITLE and PAGE_HEADING as noted:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>PAGE_TITLE — NeverNathaniel</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link href="https://fonts.googleapis.com/css2?family=Courier+Prime:wght@400;700&display=swap" rel="stylesheet">
  <link rel="stylesheet" href="css/style.css">
</head>
<body>
  <nav>
    <span class="site-name"><a href="index.html">NeverNathaniel</a></span>
    <ul>
      <li><a href="index.html">home</a></li>
      <li><a href="useful.html">useful</a></li>
      <li><a href="made.html">made</a></li>
      <li><a href="likes.html">likes</a></li>
    </ul>
  </nav>

  <main>
    <h1 id="hero"></h1>
    <!-- page content goes here -->
  </main>

  <script src="https://code.jquery.com/jquery-3.7.1.min.js"></script>
  <script src="js/typewrite.js"></script>
  <script>
    $(document).ready(function() {
      $('#hero').typewrite({
        actions: [
          { type: 'PAGE_HEADING' }
        ],
        speed: 40,
        showCursor: true,
        blinkingCursor: true,
        cursor: '_'
      });
    });
  </script>
</body>
</html>
```

Page values:
| File | PAGE_TITLE | PAGE_HEADING |
|------|-----------|--------------|
| index.html | home | hello. |
| useful.html | things I find useful | things I find useful. |
| made.html | things I have made | things I have made. |
| likes.html | things I like | things I like. |

**Step 4: Commit**

```bash
git add css/style.css js/typewrite.js index.html useful.html made.html likes.html
git commit -m "feat: scaffold four-page portfolio structure"
```

---

### Task 2: Write shared CSS

**Files:**
- Modify: `css/style.css`

**Step 1: Replace style.css with full stylesheet**

```css
/* portfolio styles */

*, *::before, *::after {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

:root {
  --c1: #006466;
  --c2: #065a60;
  --c3: #0b525b;
  --c4: #144552;
  --c5: #1b3a4b;
  --c6: #212f45;
  --c7: #272640;
  --c8: #312244;
  --c9: #3e1f47;
  --c10: #4d194d;
  --text: #d6e4e5;
  --text-dim: #7a9ea0;
  --accent: #006466;
  --font: 'Courier Prime', 'Courier New', monospace;
}

html, body {
  min-height: 100%;
}

body {
  font-family: var(--font);
  background: linear-gradient(160deg,
    var(--c1) 0%,
    var(--c4) 20%,
    var(--c6) 40%,
    var(--c8) 65%,
    var(--c10) 100%
  );
  background-attachment: fixed;
  color: var(--text);
  line-height: 1.75;
  font-size: 1rem;
}

/* NAV */

nav {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1rem 2rem;
  background: rgba(0, 0, 0, 0.35);
  backdrop-filter: blur(4px);
  z-index: 100;
}

.site-name a {
  color: var(--text);
  text-decoration: none;
  font-weight: 700;
  letter-spacing: 0.05em;
}

nav ul {
  list-style: none;
  display: flex;
  gap: 2rem;
}

nav ul li a {
  color: var(--text-dim);
  text-decoration: none;
  letter-spacing: 0.05em;
  transition: color 0.2s;
}

nav ul li a:hover,
nav ul li a.active {
  color: var(--c1);
}

/* MAIN */

main {
  max-width: 680px;
  margin: 0 auto;
  padding: 8rem 2rem 4rem;
}

h1#hero {
  font-size: 2.5rem;
  font-weight: 700;
  color: var(--text);
  margin-bottom: 2.5rem;
  min-height: 3.5rem;
  letter-spacing: -0.01em;
}

/* Cursor blink from typewrite.js */
.blinkingCursor {
  color: var(--c1);
  font-weight: 400;
}

/* CONTENT */

h2 {
  font-size: 1.1rem;
  font-weight: 700;
  color: var(--c1);
  margin: 2.5rem 0 0.75rem;
  text-transform: uppercase;
  letter-spacing: 0.1em;
}

p {
  margin-bottom: 1.25rem;
  color: var(--text);
}

ul.content-list {
  list-style: none;
  margin-bottom: 2rem;
}

ul.content-list li {
  padding: 0.4rem 0;
  border-bottom: 1px solid rgba(255,255,255,0.06);
  color: var(--text);
}

ul.content-list li::before {
  content: '> ';
  color: var(--c1);
}

ul.content-list li a {
  color: var(--text);
  text-decoration: none;
  transition: color 0.2s;
}

ul.content-list li a:hover {
  color: var(--c1);
}

/* FOOTER */

footer {
  max-width: 680px;
  margin: 0 auto;
  padding: 0 2rem 3rem;
  color: var(--text-dim);
  font-size: 0.85rem;
}
```

**Step 2: Commit**

```bash
git add css/style.css
git commit -m "feat: add shared stylesheet with palette and layout"
```

---

### Task 3: Add active nav highlighting

Each page needs its own nav link marked active. Add `class="active"` to the matching `<a>` in each file's `<nav>`.

**Files:**
- Modify: `index.html` — `<a href="index.html" class="active">home</a>`
- Modify: `useful.html` — `<a href="useful.html" class="active">useful</a>`
- Modify: `made.html` — `<a href="made.html" class="active">made</a>`
- Modify: `likes.html` — `<a href="likes.html" class="active">likes</a>`

**Step 1: Edit each file's nav**

In each file, find the matching nav link and add `class="active"` to it.

**Step 2: Commit**

```bash
git add index.html useful.html made.html likes.html
git commit -m "feat: highlight active nav link per page"
```

---

### Task 4: Add page content

**Files:**
- Modify: `index.html`
- Modify: `useful.html`
- Modify: `made.html`
- Modify: `likes.html`

Place content between `<h1 id="hero"></h1>` and `</main>`. Add `<footer>` after `</main>` on each page.

**index.html content:**
```html
    <p>
      engineer. tinkerer. occasional photographer.<br>
      based somewhere between the terminal and a good cup of coffee.
    </p>
    <p>
      this site is a loose collection of things — tools i rely on,
      projects i have shipped, and things that hold my attention.
    </p>
    <p>
      no analytics. no cookies. just text.
    </p>
```

**useful.html content:**
```html
    <h2>tools</h2>
    <ul class="content-list">
      <li>placeholder tool — does something useful</li>
      <li>another tool — brief description here</li>
      <li>yet another — one line is enough</li>
    </ul>

    <h2>references</h2>
    <ul class="content-list">
      <li>placeholder reference — link or description</li>
      <li>another reference — keep it short</li>
    </ul>

    <h2>reading</h2>
    <ul class="content-list">
      <li>placeholder book or article</li>
      <li>something worth reading twice</li>
    </ul>
```

**made.html content:**
```html
    <h2>projects</h2>
    <ul class="content-list">
      <li>placeholder project — what it does in one line</li>
      <li>another project — same deal</li>
      <li>something small but useful</li>
    </ul>

    <h2>experiments</h2>
    <ul class="content-list">
      <li>something that worked</li>
      <li>something that didn't, and what i learned</li>
    </ul>
```

**likes.html content:**
```html
    <h2>media</h2>
    <ul class="content-list">
      <li>placeholder film or show</li>
      <li>something worth rewatching</li>
    </ul>

    <h2>music</h2>
    <ul class="content-list">
      <li>placeholder artist or album</li>
      <li>the one album on constant rotation</li>
    </ul>

    <h2>other</h2>
    <ul class="content-list">
      <li>placeholder hobby or interest</li>
      <li>something hard to categorize</li>
    </ul>
```

**Footer (add to all pages before `</body>`):**
```html
  <footer>
    &mdash; NeverNathaniel
  </footer>
```

**Step 1: Add content blocks to each page as above**

**Step 2: Commit**

```bash
git add index.html useful.html made.html likes.html
git commit -m "feat: add placeholder content to all four pages"
```

---

### Task 5: Verify in browser

**Step 1: Open http://localhost:3000 in browser**

Check:
- Gradient background renders correctly
- Courier Prime font loads
- `h1#hero` typewrite animation fires on page load
- Cursor blinks after animation completes
- Nav links are visible; active link is highlighted teal
- Clicking nav links navigates correctly and re-triggers animation

**Step 2: Check all four pages load and animate**

Visit each URL:
- http://localhost:3000/index.html
- http://localhost:3000/useful.html
- http://localhost:3000/made.html
- http://localhost:3000/likes.html

**Step 3: Fix any issues found, then commit**

```bash
git add -A
git commit -m "fix: address any visual issues found in browser review"
```
