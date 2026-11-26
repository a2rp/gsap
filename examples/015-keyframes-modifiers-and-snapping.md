# 015 - Keyframes, modifiers, and snapping Example

## Goal

Animate a box through three states and quantize its horizontal position to a 10-pixel grid.

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
    <title>Keyframes, modifiers, and snapping demo</title>
  </head>
  <body>
    <main class="demo">
      <h1>Keyframes and modifiers</h1>
      <div class="stage"><div class="box">Move</div></div>
      <button id="play">Play path</button>
    </main>
    <script type="module" src="/src/main.js"></script>
  </body>
</html>
``

## Styles: src/style.css

``css
:root { font-family: system-ui, sans-serif; color: #172033; background: #eef2f8; }
body { margin: 0; min-height: 100vh; display: grid; place-items: center; }
.demo { width: min(42rem, calc(100% - 2rem)); padding: 2rem; background: white; border-radius: 1rem; }
.stage { height: 13rem; padding: 1rem; background: #e7e9f2; border-radius: 1rem; }
.box { width: 5rem; height: 5rem; display: grid; place-items: center; color: white; border-radius: .8rem; background: #635bdb; }
button { margin-top: 1rem; padding: .6rem 1rem; cursor: pointer; }
``

## Animation: src/main.js

``js
import "./style.css";
import { gsap } from "gsap";

const path = gsap.to(".box", {
  keyframes: [
    { x: 180, duration: 0.65 },
    { x: 180, y: -48, duration: 0.4 },
    { x: 0, y: 0, duration: 0.65 },
  ],
  ease: "power1.inOut",
  modifiers: { x: gsap.utils.snap(10) },
  paused: true,
});

document.querySelector("#play").addEventListener("click", () => path.restart());
``

## Expected result

The box moves to the right, lifts, then returns to the start. Its horizontal positions are rounded to the nearest 10 pixels by the modifier.

## Practice variation

Replace the modifier with `snap: { x: 20 }` and compare. Try using a timeline with three `.to()` children if you want to name each beat.

## Common mistakes

- If the box clips vertically, increase the stage height or reduce the negative y value.
- Avoid a large snap increment when the distance is small; the path may appear stuck.
- Do not put labels or callbacks inside the keyframe objects unless the documented keyframe syntax explicitly supports the desired behavior; use a timeline for richer sequencing.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous example</th><th>Chapter lesson</th><th>Chapter Q&amp;A</th><th>Next example</th></tr></thead>
  <tbody><tr><td><a href="014-svg-and-attribute-animation.md">014 - SVG and attribute animation example</a></td><td><a href="../lessons/015-keyframes-modifiers-and-snapping.md">Lesson</a></td><td><a href="../qnas/015-keyframes-modifiers-and-snapping.md">Q&amp;A</a></td><td><a href="016-utilities-and-reusable-effects.md">016 - Utilities and reusable effects example</a></td></tr></tbody>
</table>
