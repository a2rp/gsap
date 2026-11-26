# 016 - Utilities and reusable effects Example

## Goal

Register a configurable fade-rise effect and reuse it for a list inside a parent timeline.

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
    <title>Utilities and reusable effects demo</title>
  </head>
  <body>
    <main class="demo">
      <h1>Reusable animation effects</h1>
      <ul class="items"><li class="item">Clamp and map values</li><li class="item">Register a named effect</li><li class="item">Reuse it in a timeline</li></ul>
      <button id="play">Play</button>
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
.items { display: grid; gap: .65rem; padding: 0; list-style: none; }
.item { padding: 1rem; border-radius: .7rem; background: #e9e7ff; }
button { padding: .6rem 1rem; cursor: pointer; }
```

## Animation: src/main.js

```js
import "./style.css";
import { gsap } from "gsap";

gsap.registerEffect({
  name: "fadeRise",
  defaults: { distance: 18, duration: 0.45 },
  extendTimeline: true,
  effect: (targets, config) => gsap.from(targets, {
    y: config.distance,
    autoAlpha: 0,
    duration: config.duration,
    stagger: config.stagger,
    ease: "power2.out",
  }),
});

const sequence = gsap.timeline({ paused: true });
sequence.fadeRise(".item", { distance: 24, stagger: 0.12 });

document.querySelector("#play").addEventListener("click", () => sequence.restart());
```

## Expected result

Clicking Play runs one shared fade-and-rise pattern across the list. The effect's default values can be overridden at the call site.

## Practice variation

Call `gsap.effects.fadeRise(".item", { distance: 10 })` outside a timeline. Add a second utility that maps a slider's 0 to 100 value into the list's animation distance.

## Common mistakes

- Registering the same named effect each time the Play button is clicked.
- Passing a selector that does not match the list items.
- Extending a timeline with effects that have no clear naming or ownership convention.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous example</th><th>Chapter lesson</th><th>Chapter Q&amp;A</th><th>Next example</th></tr></thead>
  <tbody><tr><td><a href="015-keyframes-modifiers-and-snapping.md">015 - Keyframes, modifiers, and snapping example</a></td><td><a href="../lessons/016-utilities-and-reusable-effects.md">Lesson</a></td><td><a href="../qnas/016-utilities-and-reusable-effects.md">Q&amp;A</a></td><td><a href="017-context-cleanup-and-reversion.md">017 - Context, cleanup, and reversion example</a></td></tr></tbody>
</table>
