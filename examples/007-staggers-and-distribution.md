# 007 - Staggers and distribution Example

## Goal

Reveal a six-card grid from its center with a consistent gap between each card's start.

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
    <title>Staggers and distribution demo</title>
  </head>
  <body>
    <main class="demo">
      <h1>Staggered grid</h1>
      <div class="tiles">
        <div class="tile">01</div><div class="tile">02</div><div class="tile">03</div>
        <div class="tile">04</div><div class="tile">05</div><div class="tile">06</div>
      </div>
      <button id="replay">Replay</button>
    </main>
    <script type="module" src="/src/main.js"></script>
  </body>
</html>
``

## Styles: src/style.css

``css
:root { font-family: system-ui, sans-serif; color: #172033; background: #eef2f8; }
body { margin: 0; min-height: 100vh; display: grid; place-items: center; }
.demo { width: min(38rem, calc(100% - 2rem)); padding: 2rem; background: white; border-radius: 1rem; }
.tiles { display: grid; grid-template-columns: repeat(3, 1fr); gap: .75rem; }
.tile { min-height: 5rem; display: grid; place-items: center; border-radius: .75rem; color: white; background: #635bdb; }
button { margin-top: 1rem; padding: .6rem 1rem; cursor: pointer; }
@media (max-width: 30rem) { .tiles { grid-template-columns: repeat(2, 1fr); } }
``

## Animation: src/main.js

``js
import "./style.css";
import { gsap } from "gsap";

function revealTiles() {
  gsap.fromTo(".tile",
    { y: 24, autoAlpha: 0 },
    {
      y: 0,
      autoAlpha: 1,
      duration: 0.45,
      ease: "power2.out",
      stagger: { each: 0.08, from: "center", grid: "auto" },
    }
  );
}

revealTiles();
document.querySelector("#replay").addEventListener("click", revealTiles);
``

## Expected result

The six tiles fade and rise in a stagger that begins near the center of the grid. The layout stays responsive; the grid arrangement is determined when the tween is created.

## Practice variation

Change `from` to `"start"`, then compare it with `from: "end"`. Change `each` from 0.08 to 0.2 and observe how the total reveal time grows.

## Common mistakes

- Replaying while the previous stagger is still active can create overlapping tweens; either disable the control temporarily or define an overwrite/replay strategy.
- Forgetting the elements already have visible opacity in CSS, making the initial state less predictable.
- Using a stagger interval so large that the last item appears much later than the first.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous example</th><th>Chapter lesson</th><th>Chapter Q&amp;A</th><th>Next example</th></tr></thead>
  <tbody><tr><td><a href="006-targets-and-dynamic-values.md">006 - Targets and dynamic values example</a></td><td><a href="../lessons/007-staggers-and-distribution.md">Lesson</a></td><td><a href="../qnas/007-staggers-and-distribution.md">Q&amp;A</a></td><td><a href="008-timeline-fundamentals.md">008 - Timeline fundamentals example</a></td></tr></tbody>
</table>
