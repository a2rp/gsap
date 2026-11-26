# 008 - Timeline fundamentals Example

## Goal

Create a small hero sequence whose child tweens can be played and reversed together.

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
    <title>Timeline fundamentals demo</title>
  </head>
  <body>
    <main class="demo">
      <p class="eyebrow">A timeline sequence</p>
      <h1 class="title">Bring the pieces in order</h1>
      <p class="copy">One parent playhead controls the whole introduction.</p>
      <button class="action" id="play">Play</button>
      <button id="reverse">Reverse</button>
    </main>
    <script type="module" src="/src/main.js"></script>
  </body>
</html>
```

## Styles: src/style.css

```css
:root { font-family: system-ui, sans-serif; color: #172033; background: #eef2f8; }
body { margin: 0; min-height: 100vh; display: grid; place-items: center; }
.demo { width: min(40rem, calc(100% - 2rem)); padding: 2.5rem; background: white; border-radius: 1rem; }
.eyebrow { color: #635bdb; font-weight: 700; text-transform: uppercase; letter-spacing: .08em; }
.title { max-width: 14ch; font-size: clamp(2rem, 7vw, 3.5rem); line-height: 1.05; }
button { margin-right: .5rem; padding: .65rem 1rem; cursor: pointer; }
```

## Animation: src/main.js

```js
import "./style.css";
import { gsap } from "gsap";

const intro = gsap.timeline({
  defaults: { duration: 0.5, ease: "power2.out" },
  paused: true,
});

intro
  .from(".eyebrow", { y: 12, autoAlpha: 0 })
  .from(".title", { y: 24, autoAlpha: 0 })
  .from(".copy", { y: 16, autoAlpha: 0 }, "-=0.2")
  .from(".action", { scale: 0.92, autoAlpha: 0 });

document.querySelector("#play").addEventListener("click", () => intro.play());
document.querySelector("#reverse").addEventListener("click", () => intro.reverse());
```

## Expected result

Click Play and the eyebrow, title, copy, and button appear in sequence, with the copy overlapping the title slightly. Reverse plays the existing sequence backward.

## Practice variation

Set `paused: false` or remove it and compare the initial render. Give `.title` a different duration to override the timeline default.

## Common mistakes

- Forgetting `paused: true` while expecting to start the sequence from a button.
- Recreating a new timeline every time a button is clicked without deciding what to do with the previous one.
- Assuming the overlapping `"-=0.2"` position will be explained automatically; annotate timeline positions when the sequence becomes complex.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous example</th><th>Chapter lesson</th><th>Chapter Q&amp;A</th><th>Next example</th></tr></thead>
  <tbody><tr><td><a href="007-staggers-and-distribution.md">007 - Staggers and distribution example</a></td><td><a href="../lessons/008-timeline-fundamentals.md">Lesson</a></td><td><a href="../qnas/008-timeline-fundamentals.md">Q&amp;A</a></td><td><a href="009-timeline-position-parameter.md">009 - Timeline position parameter example</a></td></tr></tbody>
</table>
