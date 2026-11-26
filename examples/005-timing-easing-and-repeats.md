# 005 - Timing, easing, and repeats Example

## Goal

Compare repeat timing, yoyo direction, and easing with one visible dot and a replay button.

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
    <title>Timing, easing, and repeats demo</title>
  </head>
  <body>
    <main class="demo">
      <h1>Timing controls the feel</h1>
      <div class="track"><div class="dot"></div></div>
      <p>Three iterations, with a short gap between each repeat.</p>
      <button id="replay">Replay</button>
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
.track { height: 4rem; padding: .5rem; background: #e7e9f2; border-radius: 999px; }
.dot { width: 3rem; height: 3rem; border-radius: 50%; background: #635bdb; }
button { margin-top: 1rem; padding: .6rem 1rem; cursor: pointer; }
```

## Animation: src/main.js

```js
import "./style.css";
import { gsap } from "gsap";

const tween = gsap.to(".dot", {
  x: 280,
  duration: 0.7,
  ease: "power2.inOut",
  repeat: 2,
  repeatDelay: 0.25,
  yoyo: true,
  paused: true,
});

document.querySelector("#replay").addEventListener("click", () => tween.restart());
```

## Expected result

Clicking Replay moves the dot forward, waits briefly, then moves it backward. It repeats this forward-and-back pattern three times in total because there are three iterations and yoyo reverses alternate iterations.

## Practice variation

Set `yoyo` to false and compare the endpoint after each repeat. Then set `ease` to `"none"` and notice the velocity becomes linear within each iteration.

## Common mistakes

- Making the horizontal track shorter than the `x` destination. Reduce the destination or widen the track.
- Starting the tween immediately and clicking Replay only after it has completed; the example pauses it until requested.
- Expecting the repeat pause to occur after the final iteration.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous example</th><th>Chapter lesson</th><th>Chapter Q&amp;A</th><th>Next example</th></tr></thead>
  <tbody><tr><td><a href="004-gsap-from-and-fromto.md">004 - gsap.from() and gsap.fromTo() example</a></td><td><a href="../lessons/005-timing-easing-and-repeats.md">Lesson</a></td><td><a href="../qnas/005-timing-easing-and-repeats.md">Q&amp;A</a></td><td><a href="006-targets-and-dynamic-values.md">006 - Targets and dynamic values example</a></td></tr></tbody>
</table>
