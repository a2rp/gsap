# 030 - Performance and debugging Example

## Goal

Build a development-only diagnostic scene with ScrollTrigger markers, an explicit refresh after layout changes, and cleanup for the trigger and tween.

## Prerequisites and setup

Use Node.js, npm, and the project created in Chapter 002. If you need a fresh project, run:

```bash
npm create vite@latest gsap-demo -- --template vanilla
cd gsap-demo
npm install
npm install gsap
npm run dev
```

Keep the development server running. Put the markup in index.html, the styles in src/style.css, and the JavaScript in src/main.js. This example uses the local development server because the GSAP package is imported as an ES module.

## Markup: index.html

```html
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Performance and debugging demo</title>
  </head>
  <body>
<button type="button" data-add-content>Add content above scene</button>
<div class="spacer"></div>
<section class="scene" data-scene>
  <article class="card" data-card>Profile this animation</article>
</section>
<pre data-diagnostics aria-live="polite"></pre>
    <script type="module" src="/src/main.js"></script>
  </body>
</html>
```

## Styles: src/style.css

```css
.spacer { height: 20vh; }
.scene { min-height: 80vh; display: grid; place-items: center; }
.card { opacity: 0; transform: translateX(0); padding: 2rem; background: #24365b; border-radius: 1rem; }
```

## Animation: src/main.js

```js
import "./style.css";
import { gsap } from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";

gsap.registerPlugin(ScrollTrigger);

const scene = document.querySelector("[data-scene]");
const card = document.querySelector("[data-card]");
const addContent = document.querySelector("[data-add-content]");
const diagnostics = document.querySelector("[data-diagnostics]");

let tween;
if (scene && card) {
  tween = gsap.to(card, {
    x: 100,
    autoAlpha: 1,
    duration: 0.7,
    scrollTrigger: {
      trigger: scene,
      start: "top 80%",
      end: "bottom 20%",
      markers: true,
      onRefresh(self) {
        if (diagnostics) {
          diagnostics.textContent = `start: ${self.start}\nend: ${self.end}`;
        }
      }
    }
  });
}

addContent?.addEventListener("click", () => {
  const note = document.createElement("p");
  note.textContent = "New content changes the layout above the scene.";
  document.querySelector(".spacer")?.before(note);
  requestAnimationFrame(() => ScrollTrigger.refresh());
});

// Call from the view's teardown hook.
function cleanupDiagnostics() {
  tween?.scrollTrigger?.kill();
  tween?.kill();
}
```

## Expected result

Markers show the scene's current calculated start and end positions. Clicking the button changes document layout and then refreshes ScrollTrigger once. Diagnostics display the new positions. Cleanup kills the scene tween and its trigger when the view is removed.

## Practice variation

Add a targeted `gsap.getTweensOf(card)` readout to inspect the card's animation state. Remove the diagnostic panel and markers from the production build after correcting the scene.

## Common mistakes

Refreshing before the DOM insertion is committed; refreshing repeatedly during scroll; leaving markers in production; assuming transform-only animations make every scene fast; forgetting to clean up a custom event listener or ticker callback.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous example</th><th>Chapter lesson</th><th>Chapter Q&amp;A</th><th>Next example</th></tr></thead>
  <tbody><tr><td><a href="029-draggable-and-interaction.md">029 - Draggable and interaction example</a></td><td><a href="../lessons/030-performance-and-debugging.md">Lesson</a></td><td><a href="../qnas/030-performance-and-debugging.md">Q&amp;A</a></td><td><a href="031-accessibility-and-production-readiness.md">031 - Accessibility and production readiness example</a></td></tr></tbody>
</table>
