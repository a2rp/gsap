# 024 - Observer and input-driven motion Example

## Goal

Observe direction changes inside a panel, animate a small indicator, and provide keyboard-accessible buttons for the same action.

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
    <title>Observer and input-driven motion demo</title>
  </head>
  <body>
    <main class="demo">
      <h1>Observe directional input</h1>
      <div class="gesture-area" id="gestureArea" tabindex="0" aria-describedby="help">
        <div class="arrow" aria-hidden="true">↑</div>
        <p id="status" aria-live="polite">Use wheel, swipe, or the buttons.</p>
      </div>
      <p id="help">Focus this panel, then use a wheel or swipe gesture.</p>
      <div class="controls"><button id="up">Previous</button><button id="down">Next</button></div>
    </main>
    <script type="module" src="/src/main.js"></script>
  </body>
</html>
```

## Styles: src/style.css

```css
:root { font-family: system-ui, sans-serif; color: #172033; background: #eef2f8; }
body { margin: 0; min-height: 100vh; display: grid; place-items: center; }
.demo { width: min(40rem, calc(100% - 2rem)); padding: 2rem; background: white; border-radius: 1rem; }
.gesture-area { min-height: 12rem; display: grid; place-items: center; align-content: center; gap: 1rem; border: 2px dashed #aaa7d2; border-radius: 1rem; background: #f6f5ff; outline-offset: 4px; }
.arrow { font-size: 3rem; color: #635bdb; }
.controls { display: flex; gap: .5rem; margin-top: 1rem; }
button { padding: .6rem .9rem; cursor: pointer; }
```

## Animation: src/main.js

```js
import "./style.css";
import { gsap } from "gsap";
import { Observer } from "gsap/Observer";

gsap.registerPlugin(Observer);

const area = document.querySelector("#gestureArea");
const arrow = document.querySelector(".arrow");
const status = document.querySelector("#status");

function showDirection(direction) {
  status.textContent = direction === "up" ? "Upward input" : "Downward input";
  gsap.to(arrow, { y: direction === "up" ? -12 : 12, duration: 0.15, yoyo: true, repeat: 1 });
}

const observer = Observer.create({
  target: area,
  type: "wheel,touch,pointer",
  tolerance: 24,
  onUp: () => showDirection("up"),
  onDown: () => showDirection("down"),
});

document.querySelector("#up").addEventListener("click", () => showDirection("up"));
document.querySelector("#down").addEventListener("click", () => showDirection("down"));
window.addEventListener("pagehide", () => observer.kill(), { once: true });
```

## Expected result

Wheel or swipe movement over the panel updates the status and briefly nudges the arrow. The Previous and Next buttons trigger the same response without requiring a gesture. Page scrolling remains native outside the panel.

## Practice variation

Change `tolerance` and compare how small movements are filtered. If you already registered ScrollTrigger, replace the standalone Observer import with `ScrollTrigger.observe()` and keep the same callback configuration.

## Common mistakes

- Adding `preventDefault` without checking whether the panel needs native page scrolling.
- Expecting `onUp` and `onDown` deltas to have the same physical scale across devices.
- Omitting keyboard-accessible controls for actions otherwise available only through swipe or wheel gestures.
- Forgetting to kill the observer when its element is removed.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous example</th><th>Chapter lesson</th><th>Chapter Q&amp;A</th><th>Next example</th></tr></thead>
  <tbody><tr><td><a href="023-scrolltrigger-callbacks-classes-and-batch.md">023 - ScrollTrigger callbacks, classes, and batch example</a></td><td><a href="../lessons/024-observer-and-input-driven-motion.md">Lesson</a></td><td><a href="../qnas/024-observer-and-input-driven-motion.md">Q&amp;A</a></td><td><a href="025-flip-and-layout-transitions.md">025 - Flip and layout transitions example</a></td></tr></tbody>
</table>
