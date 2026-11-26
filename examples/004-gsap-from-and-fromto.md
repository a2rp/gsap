# 004 - gsap.from() and gsap.fromTo() Example

## Goal

Compare a `from()` entrance with an explicit `fromTo()` transition and inspect their initial styles.

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
    <title>gsap.from() and gsap.fromTo() demo</title>
  </head>
  <body>
    <main class="demo">
      <h1>Start state choices</h1>
      <section class="cards">
        <article class="card"><h2>from()</h2><p>End comes from CSS.</p></article>
        <article class="notice"><h2>fromTo()</h2><p>Both ends are explicit.</p></article>
      </section>
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
.cards { display: grid; grid-template-columns: repeat(2, 1fr); gap: 1rem; }
.card, .notice { min-height: 9rem; padding: 1rem; border-radius: .75rem; background: #e9e7ff; }
.notice { background: #dff5ed; }
@media (max-width: 34rem) { .cards { grid-template-columns: 1fr; } }
```

## Animation: src/main.js

```js
import "./style.css";
import { gsap } from "gsap";

gsap.from(".card", {
  y: 28,
  autoAlpha: 0,
  duration: 0.7,
  ease: "power2.out",
});

gsap.fromTo(".notice",
  { scale: 0.92, autoAlpha: 0 },
  { scale: 1, autoAlpha: 1, duration: 0.7, ease: "power2.out", delay: 0.2 }
);
```

## Expected result

The first card rises from below and fades to the CSS-defined visible state. The notice animates from an explicit scale and opacity to explicit final values.

## Practice variation

Place each animation in a timeline with a delay. Observe the page immediately after load, then try `immediateRender: false` and explain when its initial state changes.

## Common mistakes

- Defining `.card` or `.notice` with `display: none`; `autoAlpha` cannot make a `display: none` element visible.
- Expecting the timeline position to prevent `from()` from rendering its start state immediately.
- Setting only opacity in CSS and leaving other visible styles undefined when the animation needs a clear final state.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous example</th><th>Chapter lesson</th><th>Chapter Q&amp;A</th><th>Next example</th></tr></thead>
  <tbody><tr><td><a href="003-tweens-with-gsap-to.md">003 - Tweens with gsap.to() example</a></td><td><a href="../lessons/004-gsap-from-and-fromto.md">Lesson</a></td><td><a href="../qnas/004-gsap-from-and-fromto.md">Q&amp;A</a></td><td><a href="005-timing-easing-and-repeats.md">005 - Timing, easing, and repeats example</a></td></tr></tbody>
</table>
