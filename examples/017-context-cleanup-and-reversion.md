# 017 - Context, cleanup, and reversion Example

## Goal

Scope two repeated card selectors to one stage and provide a cleanup control that reverts their entrance.

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
    <title>Context, cleanup, and reversion demo</title>
  </head>
  <body>
    <main class="demo">
      <h1>Scoped setup and cleanup</h1>
      <section class="stage" id="stage">
        <div class="box">First card</div><div class="box">Second card</div>
      </section>
      <button id="cleanup">Revert stage animation</button>
    </main>
    <script type="module" src="/src/main.js"></script>
  </body>
</html>
``

## Styles: src/style.css

``css
:root { font-family: system-ui, sans-serif; color: #172033; background: #eef2f8; }
body { margin: 0; min-height: 100vh; display: grid; place-items: center; }
.demo { width: min(40rem, calc(100% - 2rem)); padding: 2rem; background: white; border-radius: 1rem; }
.stage { display: grid; gap: .75rem; padding: 1rem; background: #f1f0ff; border-radius: 1rem; }
.box { padding: 1rem; border-radius: .7rem; background: #635bdb; color: white; }
button { margin-top: 1rem; padding: .6rem 1rem; cursor: pointer; }
``

## Animation: src/main.js

``js
import "./style.css";
import { gsap } from "gsap";

const stage = document.querySelector("#stage");
const cleanupButton = document.querySelector("#cleanup");

const ctx = gsap.context(() => {
  gsap.from(".box", {
    y: 20,
    autoAlpha: 0,
    stagger: 0.12,
    duration: 0.55,
    ease: "power2.out",
  });
}, stage);

function cleanup() {
  ctx.revert();
  cleanupButton.removeEventListener("click", cleanup);
  window.removeEventListener("pagehide", cleanup);
}

cleanupButton.addEventListener("click", cleanup);
window.addEventListener("pagehide", cleanup);
``

## Expected result

The cards enter one after another. Clicking the cleanup button reverts their animation styles. The same cleanup also runs when the page is hidden, and the event listeners are removed.

## Practice variation

Add a second `.stage` and create a separate context scoped to it. Reuse the `.box` class and verify that neither context selects the other stage's boxes.

## Common mistakes

- Passing `document` as the scope when each component should be isolated.
- Calling `ctx.revert()` but leaving event listeners that can create new animations afterward.
- Expecting a reverted context to reset your JavaScript application state; it only cleans up collected animation work and styles.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous example</th><th>Chapter lesson</th><th>Chapter Q&amp;A</th><th>Next example</th></tr></thead>
  <tbody><tr><td><a href="016-utilities-and-reusable-effects.md">016 - Utilities and reusable effects example</a></td><td><a href="../lessons/017-context-cleanup-and-reversion.md">Lesson</a></td><td><a href="../qnas/017-context-cleanup-and-reversion.md">Q&amp;A</a></td><td><a href="018-responsive-motion-and-reduced-motion.md">018 - Responsive motion and reduced motion example</a></td></tr></tbody>
</table>
