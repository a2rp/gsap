# 026 - MotionPath and path animation Example

## Goal

Move an arrow-shaped marker along a curved SVG guide and align its center to the path.

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
    <title>MotionPath and path animation demo</title>
  </head>
  <body>
    <main class="demo">
      <h1>Follow a motion path</h1>
      <div class="stage">
        <svg class="route" viewBox="0 0 600 300" aria-label="Curved route">
          <path id="route" d="M 40 220 C 160 20, 360 280, 560 70" />
        </svg>
        <div class="ship" aria-hidden="true"></div>
      </div>
      <button id="start">Start journey</button>
    </main>
    <script type="module" src="/src/main.js"></script>
  </body>
</html>
``

## Styles: src/style.css

``css
:root { font-family: system-ui, sans-serif; color: #172033; background: #eef2f8; }
body { margin: 0; min-height: 100vh; display: grid; place-items: center; }
.demo { width: min(44rem, calc(100% - 2rem)); padding: 2rem; background: white; border-radius: 1rem; }
.stage { position: relative; width: 100%; aspect-ratio: 2 / 1; overflow: hidden; border-radius: 1rem; background: #f5f4ff; }
.route { position: absolute; inset: 0; width: 100%; height: 100%; overflow: visible; }
#route { fill: none; stroke: #b7b2ed; stroke-width: 8; stroke-linecap: round; }
.ship { position: absolute; left: 0; top: 0; width: 0; height: 0; border-top: 12px solid transparent; border-bottom: 12px solid transparent; border-left: 24px solid #635bdb; transform-origin: 50% 50%; }
button { margin-top: 1rem; padding: .6rem 1rem; cursor: pointer; }
``

## Animation: src/main.js

``js
import "./style.css";
import { gsap } from "gsap";
import { MotionPathPlugin } from "gsap/MotionPathPlugin";

gsap.registerPlugin(MotionPathPlugin);

const trip = gsap.to(".ship", {
  duration: 3,
  ease: "power1.inOut",
  motionPath: {
    path: "#route",
    align: "#route",
    alignOrigin: [0.5, 0.5],
    autoRotate: true,
  },
  paused: true,
});

document.querySelector("#start").addEventListener("click", () => trip.restart());
``

## Expected result

Click Start journey. The arrow moves along the visible curve, stays centered on it, and rotates as the curve changes direction.

## Practice variation

Use `autoRotate: 90` if the arrow points sideways. Add `start: 0.2` and `end: 0.8` to use only part of the path.

## Common mistakes

- The path and stage must have matching coordinate geometry; confirm the route is visible before animating.
- If the arrow points backward, use a numeric `autoRotate` offset that matches the artwork.
- After a responsive resize changes the path, alignment is not automatically recalculated; rebuild the tween if exact alignment matters.
- Keep the SVG route decorative or provide a meaningful accessible label if it conveys information.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous example</th><th>Chapter lesson</th><th>Chapter Q&amp;A</th><th>Next example</th></tr></thead>
  <tbody><tr><td><a href="025-flip-and-layout-transitions.md">025 - Flip and layout transitions example</a></td><td><a href="../lessons/026-motionpath-and-path-animation.md">Lesson</a></td><td><a href="../qnas/026-motionpath-and-path-animation.md">Q&amp;A</a></td><td><a href="027-scrollto-and-programmatic-scrolling.md">027 - ScrollTo and programmatic scrolling example</a></td></tr></tbody>
</table>
