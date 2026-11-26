# 023 - ScrollTrigger callbacks, classes, and batch Example

## Goal

Reveal list items in batches as they enter and toggle a class on a related section label.

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
    <title>ScrollTrigger callbacks, classes, and batch demo</title>
  </head>
  <body>
    <main class="page">
      <section class="intro"><h1>Batching scroll callbacks</h1><p>Scroll down to reveal the list.</p></section>
      <section class="feature"><p class="feature__label">Active section</p><div class="items">
        <article class="item">Batch one</article><article class="item">Batch two</article><article class="item">Batch three</article><article class="item">Batch four</article>
      </div></section>
      <section class="outro"><h2>End of list</h2></section>
    </main>
    <script type="module" src="/src/main.js"></script>
  </body>
</html>
``

## Styles: src/style.css

``css
:root { font-family: system-ui, sans-serif; color: #172033; background: #eef2f8; }
body { margin: 0; }
.intro, .feature, .outro { width: min(42rem, calc(100% - 2rem)); margin: 12vh auto; padding: 2rem; background: white; border-radius: 1rem; }
.feature { min-height: 100vh; background: #f7f6ff; }
.feature__label { display: inline-block; padding: .5rem .8rem; border-radius: 999px; background: #e4e2f4; transition: background .2s, color .2s; }
.feature__label.is-active { color: white; background: #635bdb; }
.items { display: grid; gap: 1rem; margin-top: 2rem; }
.item { padding: 1.2rem; border-radius: .8rem; background: #e9e7ff; }
.outro { min-height: 60vh; }
``

## Animation: src/main.js

``js
import "./style.css";
import { gsap } from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";

gsap.registerPlugin(ScrollTrigger);

const items = gsap.utils.toArray(".item");
// The CSS baseline remains visible if JavaScript does not run.
gsap.set(items, { y: 18, autoAlpha: 0 });

ScrollTrigger.batch(items, {
  start: "top 85%",
  onEnter: (elements) => gsap.to(elements, {
    y: 0,
    autoAlpha: 1,
    duration: 0.5,
    stagger: 0.12,
    overwrite: true,
  }),
});

ScrollTrigger.create({
  trigger: ".feature",
  start: "top center",
  end: "bottom center",
  toggleClass: { targets: ".feature__label", className: "is-active" },
});
``

## Expected result

As list cards approach the viewport, nearby entries reveal together with a short stagger. The label receives `is-active` while the feature section is in its active scroll range. Reverse scrolling updates the class state.

## Practice variation

Use `onEnter` and `onEnterBack` callbacks to log the direction and progress for one trigger. Keep logs out of production and compare with the simpler `toggleClass` behavior.

## Common mistakes

- `gsap.set()` runs only after the module loads; keep a visible CSS baseline so content remains available without JavaScript.
- Batch callbacks receive an array. Do not assume `elements` is one element.
- Confirm the list is tall enough and spaced so entries enter at different times; otherwise a single batch may contain every item.
- Avoid heavy DOM reads or network work in scroll callbacks.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous example</th><th>Chapter lesson</th><th>Chapter Q&amp;A</th><th>Next example</th></tr></thead>
  <tbody><tr><td><a href="022-scrolltrigger-scrub-pin-and-snap.md">022 - ScrollTrigger scrub, pin, and snap example</a></td><td><a href="../lessons/023-scrolltrigger-callbacks-classes-and-batch.md">Lesson</a></td><td><a href="../qnas/023-scrolltrigger-callbacks-classes-and-batch.md">Q&amp;A</a></td><td><a href="024-observer-and-input-driven-motion.md">024 - Observer and input-driven motion example</a></td></tr></tbody>
</table>
