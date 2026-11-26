# 012 - Setting values and quick methods Example

## Goal

Move a decorative dot toward the pointer with reusable quickTo tweens.

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
    <title>Setting values and quick methods demo</title>
  </head>
  <body>
    <main class="demo">
      <h1>Move the pointer inside this area</h1>
      <p>The dot eases toward each new pointer position.</p>
      <div class="stage" id="stage"><div class="dot" aria-hidden="true"></div></div>
    </main>
    <script type="module" src="/src/main.js"></script>
  </body>
</html>
```

## Styles: src/style.css

```css
:root { font-family: system-ui, sans-serif; color: #172033; background: #eef2f8; }
body { margin: 0; min-height: 100vh; display: grid; place-items: center; }
.demo { width: min(42rem, calc(100% - 2rem)); padding: 2rem; background: white; border-radius: 1rem; }
.stage { position: relative; height: 16rem; overflow: hidden; border: 2px dashed #aaa7d2; border-radius: 1rem; background: #f6f5ff; }
.dot { position: absolute; left: 0; top: 0; width: 2rem; height: 2rem; border-radius: 50%; background: #635bdb; pointer-events: none; }
```

## Animation: src/main.js

```js
import "./style.css";
import { gsap } from "gsap";

const stage = document.querySelector("#stage");
const dot = document.querySelector(".dot");

gsap.set(dot, { xPercent: -50, yPercent: -50 });
const setX = gsap.quickTo(dot, "x", { duration: 0.22, ease: "power3.out" });
const setY = gsap.quickTo(dot, "y", { duration: 0.22, ease: "power3.out" });

function moveDot(event) {
  const bounds = stage.getBoundingClientRect();
  setX(event.clientX - bounds.left);
  setY(event.clientY - bounds.top);
}

stage.addEventListener("pointermove", moveDot);
```

## Expected result

As the pointer moves inside the stage, the dot smoothly follows and catches up to the latest pointer position. The two `quickTo()` setters are created once and reused.

## Practice variation

Replace the quickTo functions with `gsap.quickSetter(dot, "x", "px")` and a matching y setter. Compare the direct motion, then implement smoothing yourself if needed.

## Common mistakes

- Forgetting the stage's bounding rectangle and using viewport coordinates as local coordinates.
- Recreating quickTo setters inside `pointermove`, which defeats the reusable-tween pattern.
- Using a dot that intercepts pointer events; `pointer-events: none` lets the stage keep receiving events.
- In a component, remove the listener during cleanup.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous example</th><th>Chapter lesson</th><th>Chapter Q&amp;A</th><th>Next example</th></tr></thead>
  <tbody><tr><td><a href="011-callbacks-and-animation-events.md">011 - Callbacks and animation events example</a></td><td><a href="../lessons/012-setting-values-and-quick-methods.md">Lesson</a></td><td><a href="../qnas/012-setting-values-and-quick-methods.md">Q&amp;A</a></td><td><a href="013-css-properties-and-transforms.md">013 - CSS properties and transforms example</a></td></tr></tbody>
</table>
