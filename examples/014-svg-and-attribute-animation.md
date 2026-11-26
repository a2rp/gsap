# 014 - SVG and attribute animation Example

## Goal

Animate the center and radius of an SVG circle while preserving the difference between attributes and transforms.

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
    <title>SVG and attribute animation demo</title>
  </head>
  <body>
    <main class="demo">
      <h1>SVG coordinates and attributes</h1>
      <svg class="scene" viewBox="0 0 320 120" role="img" aria-labelledby="svgTitle">
        <title id="svgTitle">A circle moves along a guide</title>
        <line x1="30" y1="60" x2="290" y2="60" class="guide" />
        <circle id="orb" cx="30" cy="60" r="24" class="orb" />
      </svg>
      <button id="animate">Animate</button>
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
.scene { display: block; width: 100%; height: auto; background: #f6f5ff; border-radius: 1rem; }
.guide { stroke: #c8c5e8; stroke-width: 4; stroke-linecap: round; }
.orb { fill: #635bdb; }
button { margin-top: 1rem; padding: .6rem 1rem; cursor: pointer; }
``

## Animation: src/main.js

``js
import "./style.css";
import { gsap } from "gsap";

const orb = document.querySelector("#orb");
const animateButton = document.querySelector("#animate");

animateButton.addEventListener("click", () => {
  gsap.fromTo(orb,
    { attr: { cx: 30, r: 24 } },
    { attr: { cx: 290, r: 32 }, duration: 1, ease: "power2.inOut", yoyo: true, repeat: 1 }
  );
});
``

## Expected result

Clicking Animate moves the circle's center through the SVG viewBox and grows its radius slightly. It returns to its original attribute values on the yoyo iteration.

## Practice variation

Replace the `attr` destination for `cx` with a GSAP `x` transform. The element will be translated relative to its original geometry instead of changing the circle's center attribute.

## Common mistakes

- Using `r: 32` outside the `attr` object; that is not the SVG circle's radius attribute.
- Expecting `cx` units to equal CSS pixels on a scaled SVG.
- Giving the SVG no accessible name or surrounding explanation when the illustration communicates information.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous example</th><th>Chapter lesson</th><th>Chapter Q&amp;A</th><th>Next example</th></tr></thead>
  <tbody><tr><td><a href="013-css-properties-and-transforms.md">013 - CSS properties and transforms example</a></td><td><a href="../lessons/014-svg-and-attribute-animation.md">Lesson</a></td><td><a href="../qnas/014-svg-and-attribute-animation.md">Q&amp;A</a></td><td><a href="015-keyframes-modifiers-and-snapping.md">015 - Keyframes, modifiers, and snapping example</a></td></tr></tbody>
</table>
