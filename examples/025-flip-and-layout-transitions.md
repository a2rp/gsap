# 025 - Flip and layout transitions Example

## Goal

Expand a featured grid card with a smooth transition while the remaining cards reposition.

## Prerequisites and setup

Use Node.js, npm, and the project created in Chapter 002. If you need a fresh project, run:

``bash
npm create vite@latest gsap-demo -- --template vanilla
cd gsap-demo
npm install
npm install gsap
npm run dev
``

Keep the development server running. Put the markup in index.html, the styles in src/style.css, and the JavaScript in src/main.js. This example uses the local development server because the GSAP package is imported as an ES module.

## Markup: index.html

``html
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Flip and layout transitions demo</title>
  </head>
  <body>
    <main class="demo">
      <h1>Flip between layout states</h1>
      <button id="toggle" aria-expanded="false">Expand first card</button>
      <div class="grid" id="grid">
        <article class="tile tile--feature"><h2>Featured</h2><p>This card changes its grid area.</p></article>
        <article class="tile"><h2>Card two</h2></article><article class="tile"><h2>Card three</h2></article>
        <article class="tile"><h2>Card four</h2></article><article class="tile"><h2>Card five</h2></article>
      </div>
    </main>
    <script type="module" src="/src/main.js"></script>
  </body>
</html>
``

## Styles: src/style.css

``css
:root { font-family: system-ui, sans-serif; color: #172033; background: #eef2f8; }
body { margin: 0; min-height: 100vh; display: grid; place-items: center; }
.demo { width: min(48rem, calc(100% - 2rem)); padding: 2rem; background: white; border-radius: 1rem; }
.grid { display: grid; grid-template-columns: repeat(3, 1fr); grid-auto-rows: minmax(7rem, auto); gap: .75rem; margin-top: 1rem; }
.tile { padding: 1rem; border-radius: .8rem; background: #e9e7ff; }
.tile--feature { background: #d8d4ff; }
.grid.is-expanded .tile--feature { grid-column: span 2; grid-row: span 2; }
button { padding: .6rem 1rem; cursor: pointer; }
@media (max-width: 34rem) { .grid { grid-template-columns: repeat(2, 1fr); } }
``

## Animation: src/main.js

``js
import "./style.css";
import { gsap } from "gsap";
import { Flip } from "gsap/Flip";

gsap.registerPlugin(Flip);

const grid = document.querySelector("#grid");
const toggle = document.querySelector("#toggle");

function toggleLayout() {
  const state = Flip.getState(".tile");
  const expanded = grid.classList.toggle("is-expanded");
  toggle.setAttribute("aria-expanded", String(expanded));
  toggle.textContent = expanded ? "Restore grid" : "Expand first card";

  Flip.from(state, {
    duration: 0.55,
    ease: "power1.inOut",
    absolute: true,
    stagger: 0.04,
  });
}

toggle.addEventListener("click", toggleLayout);
``

## Expected result

Each click captures the current positions, toggles the featured card's grid area, and animates all cards into the new layout. The button's accessible expanded state follows the class state.

## Practice variation

Remove `absolute: true` and compare how the grid calculates space during movement. Add `fade: true` and matching `data-flip-id` values when swapping two distinct elements.

## Common mistakes

- Capturing state after toggling the class.
- Giving a transition a `duration` but forgetting to register Flip.
- Using `absolute: true` in a layout where removing cards from flow causes visible collapse.
- Not updating `aria-expanded` when the UI's expanded/collapsed state changes.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous example</th><th>Chapter lesson</th><th>Chapter Q&amp;A</th><th>Next example</th></tr></thead>
  <tbody><tr><td><a href="024-observer-and-input-driven-motion.md">024 - Observer and input-driven motion example</a></td><td><a href="../lessons/025-flip-and-layout-transitions.md">Lesson</a></td><td><a href="../qnas/025-flip-and-layout-transitions.md">Q&amp;A</a></td><td><a href="026-motionpath-and-path-animation.md">026 - MotionPath and path animation example</a></td></tr></tbody>
</table>
