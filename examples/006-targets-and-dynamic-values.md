# 006 - Targets and dynamic values Example

## Goal

Use one tween for three cards while calculating a distinct travel distance and rotation for each.

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
    <title>Targets and dynamic values demo</title>
  </head>
  <body>
    <main class="demo">
      <h1>Values can depend on the target</h1>
      <div class="item-list">
        <div class="item">Target zero</div>
        <div class="item">Target one</div>
        <div class="item">Target two</div>
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
.demo { width: min(36rem, calc(100% - 2rem)); padding: 2rem; background: white; border-radius: 1rem; }
.item-list { display: grid; gap: .7rem; }
.item { width: 12rem; padding: .9rem; color: white; background: #635bdb; border-radius: .7rem; }
button { margin-top: 1rem; padding: .6rem 1rem; cursor: pointer; }
``

## Animation: src/main.js

``js
import "./style.css";
import { gsap } from "gsap";

const items = gsap.utils.toArray(".item");

const tween = gsap.to(items, {
  x: (index) => 24 + index * 34,
  rotation: (index) => index % 2 === 0 ? 3 : -3,
  duration: 0.7,
  ease: "power2.out",
  paused: true,
});

document.querySelector("#replay").addEventListener("click", () => tween.restart());
``

## Expected result

Each card moves a different distance and receives a small rotation based on its index. The values stay fixed during that playback.

## Practice variation

Replace the value functions with a small calculation based on the target's `data-distance` attribute. Convert the attribute to a number before returning it, because DOM attributes are strings.

## Common mistakes

- Calling `Number()` on a missing or nonnumeric data attribute without checking its value.
- Assuming the function is repeatedly invoked on every animation frame.
- Creating the tween before the `.item` elements have been inserted into the document.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous example</th><th>Chapter lesson</th><th>Chapter Q&amp;A</th><th>Next example</th></tr></thead>
  <tbody><tr><td><a href="005-timing-easing-and-repeats.md">005 - Timing, easing, and repeats example</a></td><td><a href="../lessons/006-targets-and-dynamic-values.md">Lesson</a></td><td><a href="../qnas/006-targets-and-dynamic-values.md">Q&amp;A</a></td><td><a href="007-staggers-and-distribution.md">007 - Staggers and distribution example</a></td></tr></tbody>
</table>
