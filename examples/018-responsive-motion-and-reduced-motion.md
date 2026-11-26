# 018 - Responsive motion and reduced motion Example

## Goal

Animate a card differently on wide and narrow screens, and leave it immediately visible for reduced motion.

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
    <title>Responsive motion and reduced motion demo</title>
  </head>
  <body>
    <main class="demo">
      <h1>Responsive animation choices</h1>
      <article class="card"><h2>Always readable</h2><p>The card remains available if its entrance animation is skipped.</p></article>
      <article class="card"><h2>Preference aware</h2><p>Motion is selected from the current media conditions.</p></article>
    </main>
    <script type="module" src="/src/main.js"></script>
  </body>
</html>
```

## Styles: src/style.css

```css
:root { font-family: system-ui, sans-serif; color: #172033; background: #eef2f8; }
body { margin: 0; min-height: 100vh; display: grid; place-items: center; }
.demo { width: min(44rem, calc(100% - 2rem)); padding: 2rem; background: white; border-radius: 1rem; }
.card { margin-top: 1rem; padding: 1rem; border-radius: .8rem; background: #e9e7ff; }
.card h2 { margin-top: 0; }
```

## Animation: src/main.js

```js
import "./style.css";
import { gsap } from "gsap";

const mm = gsap.matchMedia();

mm.add({
  wide: "(min-width: 48rem)",
  reduceMotion: "(prefers-reduced-motion: reduce)",
}, ({ conditions }) => {
  if (conditions.reduceMotion) {
    gsap.set(".card", { y: 0, autoAlpha: 1 });
    return;
  }

  gsap.from(".card", {
    y: conditions.wide ? 28 : 8,
    autoAlpha: 0,
    duration: conditions.wide ? 0.6 : 0.3,
    stagger: 0.12,
    ease: "power2.out",
  });
});

window.addEventListener("pagehide", () => mm.revert(), { once: true });
```

## Expected result

On wide screens, the cards rise a small distance as they appear. On narrow screens the movement is shorter and quicker. With reduced motion enabled, the cards appear directly in their visible state.

## Practice variation

Change the reduced-motion branch to use a brief opacity-only transition if that fits the interface. Ensure no content begins hidden in CSS so the page remains usable before JavaScript initializes.

## Common mistakes

- Starting `.card` elements with CSS opacity zero and relying only on the animation to reveal them.
- Forgetting the matchMedia context is tied to the conditions, so recreating unrelated global state inside it may duplicate work.
- Failing to revert the matchMedia instance when its owning page section is disposed.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous example</th><th>Chapter lesson</th><th>Chapter Q&amp;A</th><th>Next example</th></tr></thead>
  <tbody><tr><td><a href="017-context-cleanup-and-reversion.md">017 - Context, cleanup, and reversion example</a></td><td><a href="../lessons/018-responsive-motion-and-reduced-motion.md">Lesson</a></td><td><a href="../qnas/018-responsive-motion-and-reduced-motion.md">Q&amp;A</a></td><td><a href="019-gsap-in-react-with-usegsap.md">019 - GSAP in React with useGSAP() example</a></td></tr></tbody>
</table>
