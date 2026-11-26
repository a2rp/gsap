# 003 - Tweens with gsap.to() Example

## Goal

Move a card to a destination, fade it slightly, and control playback with buttons.

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
    <title>Tweens with gsap.to() demo</title>
  </head>
  <body>
    <main class="demo">
      <h1>Control one tween</h1>
      <div class="track"><div class="box" aria-label="Moving box"></div></div>
      <div class="controls"><button id="play">Play</button><button id="reverse">Reverse</button><button id="restart">Restart</button></div>
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
.track { height: 6rem; padding: .5rem; background: #e7e9f2; border-radius: 1rem; }
.box { width: 5rem; height: 5rem; border-radius: .8rem; background: #635bdb; }
.controls { display: flex; gap: .75rem; margin-top: 1rem; }
button { padding: .6rem 1rem; cursor: pointer; }
```

## Animation: src/main.js

```js
import "./style.css";
import { gsap } from "gsap";

const tween = gsap.to(".box", {
  x: 300,
  opacity: 0.55,
  duration: 1.2,
  ease: "power2.inOut",
  paused: true,
});

document.querySelector("#play").addEventListener("click", () => tween.play());
document.querySelector("#reverse").addEventListener("click", () => tween.reverse());
document.querySelector("#restart").addEventListener("click", () => tween.restart());
```

## Expected result

The box begins at its CSS position. Play moves and fades it toward the end of the track, Reverse runs the playhead toward the start, and Restart begins the tween again.

## Practice variation

Change the CSS starting position to `transform: translateX(20px)` and observe the destination relative to that rendered state. Then change the ease but leave all other values constant.

## Common mistakes

- Making the track too short for the destination; lower `x` or widen `.track`.
- Omitting `paused: true`, causing the tween to finish before you click a control.
- Looking for a CSS `transform` string in the vars object; GSAP uses transform aliases such as `x`.
- Binding event handlers before the markup exists in the page.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous example</th><th>Chapter lesson</th><th>Chapter Q&amp;A</th><th>Next example</th></tr></thead>
  <tbody><tr><td><a href="002-installation-and-project-setup.md">002 - Installation and project setup example</a></td><td><a href="../lessons/003-tweens-with-gsap-to.md">Lesson</a></td><td><a href="../qnas/003-tweens-with-gsap-to.md">Q&amp;A</a></td><td><a href="004-gsap-from-and-fromto.md">004 - gsap.from() and gsap.fromTo() example</a></td></tr></tbody>
</table>
