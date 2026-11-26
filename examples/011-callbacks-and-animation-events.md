# 011 - Callbacks and animation events Example

## Goal

Use callbacks to report progress for a plain object tween and keep the page display in sync.

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
    <title>Callbacks and animation events demo</title>
  </head>
  <body>
    <main class="demo">
      <h1>Animation lifecycle</h1>
      <output id="value">0</output>
      <p id="status" aria-live="polite">Ready</p>
      <button id="start">Start</button>
    </main>
    <script type="module" src="/src/main.js"></script>
  </body>
</html>
```

## Styles: src/style.css

```css
:root { font-family: system-ui, sans-serif; color: #172033; background: #eef2f8; }
body { margin: 0; min-height: 100vh; display: grid; place-items: center; }
.demo { width: min(34rem, calc(100% - 2rem)); padding: 2rem; background: white; border-radius: 1rem; }
output { display: block; margin: 1rem 0; font-size: 3rem; font-variant-numeric: tabular-nums; }
button { padding: .6rem 1rem; cursor: pointer; }
```

## Animation: src/main.js

```js
import "./style.css";
import { gsap } from "gsap";

const display = document.querySelector("#value");
const status = document.querySelector("#status");
const state = { value: 0 };

function startCount() {
  state.value = 0;
  const tween = gsap.to(state, {
    value: 100,
    duration: 1.4,
    ease: "none",
    onStart: () => { status.textContent = "Running"; },
    onUpdate: () => { display.value = String(Math.round(state.value)); display.textContent = display.value; },
    onComplete: () => { status.textContent = "Complete"; },
  });
  return tween;
}

document.querySelector("#start").addEventListener("click", startCount);
```

## Expected result

The number counts from zero to one hundred. The status changes to Running when playback begins and Complete when the finite tween reaches its end.

## Practice variation

Keep the returned tween, add a button that reverses it, and update the status with `onReverseComplete`. Then interrupt it with `kill()` and observe that normal completion is not reported.

## Common mistakes

- Updating `textContent` in `onUpdate` is suitable for this small demo, but frequent DOM writes can be costly in a large interface.
- Repeated clicks create multiple counters; disable the button or define how a new tween should replace the old one.
- The status callback should not be the only record of whether an application operation succeeded.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous example</th><th>Chapter lesson</th><th>Chapter Q&amp;A</th><th>Next example</th></tr></thead>
  <tbody><tr><td><a href="010-labels-nested-timelines-and-controls.md">010 - Labels, nested timelines, and controls example</a></td><td><a href="../lessons/011-callbacks-and-animation-events.md">Lesson</a></td><td><a href="../qnas/011-callbacks-and-animation-events.md">Q&amp;A</a></td><td><a href="012-setting-values-and-quick-methods.md">012 - Setting values and quick methods example</a></td></tr></tbody>
</table>
