# 013 - CSS properties and transforms Example

## Goal

Create a hover-like card motion with movement, rotation, scale, and opacity while keeping styles understandable.

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
    <title>CSS properties and transforms demo</title>
  </head>
  <body>
    <main class="demo">
      <h1>Animate transform components</h1>
      <article class="card"><p>GSAP CSSPlugin</p><h2>Move, rotate, scale</h2><p>Use separate properties to compose the transform.</p></article>
      <button id="animate">Animate card</button>
    </main>
    <script type="module" src="/src/main.js"></script>
  </body>
</html>
```

## Styles: src/style.css

```css
:root { font-family: system-ui, sans-serif; color: #172033; background: #eef2f8; }
body { margin: 0; min-height: 100vh; display: grid; place-items: center; }
.demo { width: min(38rem, calc(100% - 2rem)); padding: 2rem; background: white; border-radius: 1rem; }
.card { padding: 1.5rem; border-radius: 1rem; background: #e9e7ff; transform-origin: center; }
.card p:first-child { color: #635bdb; font-weight: 700; }
button { margin-top: 1rem; padding: .6rem 1rem; cursor: pointer; }
```

## Animation: src/main.js

```js
import "./style.css";
import { gsap } from "gsap";

const card = document.querySelector(".card");
const animateButton = document.querySelector("#animate");

animateButton.addEventListener("click", () => {
  gsap.to(card, {
    x: 12,
    y: -8,
    rotation: 1.5,
    scale: 1.02,
    transformOrigin: "center center",
    duration: 0.45,
    ease: "power2.out",
    overwrite: "auto",
  });
});
```

## Expected result

Clicking the button moves, lifts, slightly rotates, and scales the card. GSAP composes those transform components in one tween.

## Practice variation

Change the transform origin to `"left center"` and compare the rotation. Try animating `autoAlpha` on a separate decorative element and check its visibility behavior.

## Common mistakes

- Repeated button clicks may create competing transitions; `overwrite: "auto"` helps resolve overlapping active properties, but a production interaction should still define its intended interruption behavior.
- Using `clearProps` without checking which CSS values become active afterward.
- Animating a focusable card to opacity zero without removing it from interaction or moving focus appropriately.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous example</th><th>Chapter lesson</th><th>Chapter Q&amp;A</th><th>Next example</th></tr></thead>
  <tbody><tr><td><a href="012-setting-values-and-quick-methods.md">012 - Setting values and quick methods example</a></td><td><a href="../lessons/013-css-properties-and-transforms.md">Lesson</a></td><td><a href="../qnas/013-css-properties-and-transforms.md">Q&amp;A</a></td><td><a href="014-svg-and-attribute-animation.md">014 - SVG and attribute animation example</a></td></tr></tbody>
</table>
