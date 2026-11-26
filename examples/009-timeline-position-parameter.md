# 009 - Timeline position parameter Example

## Goal

Arrange three colored bars with absolute, previous-child, and relative-end positions.

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
    <title>Timeline position parameter demo</title>
  </head>
  <body>
    <main class="demo">
      <h1>Timeline positions</h1>
      <div class="row"><span class="bar one">one</span></div>
      <div class="row"><span class="bar two">two</span></div>
      <div class="row"><span class="bar three">three</span></div>
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
.demo { width: min(42rem, calc(100% - 2rem)); padding: 2rem; background: white; border-radius: 1rem; }
.row { height: 3.5rem; margin: .5rem 0; padding: .35rem; background: #e7e9f2; border-radius: .75rem; }
.bar { display: block; width: 6rem; height: 2.8rem; padding: .5rem; color: white; border-radius: .5rem; }
.one { background: #635bdb; } .two { background: #139b7a; } .three { background: #d06a2d; }
button { padding: .6rem 1rem; cursor: pointer; }
```

## Animation: src/main.js

```js
import "./style.css";
import { gsap } from "gsap";

const tl = gsap.timeline({ paused: true });

tl.to(".one", { x: 260, duration: 1, ease: "none" }, 0)
  .to(".two", { x: 260, duration: 0.7, ease: "none" }, "<")
  .to(".three", { x: 260, duration: 0.5, ease: "none" }, "-=0.2");

document.querySelector("#play").addEventListener("click", () => tl.restart());
```

## Expected result

The first and second bars begin together because the second uses `"<"`. The third begins 0.2 seconds before the then-current end of the timeline, so it overlaps the existing sequence.

## Practice variation

Add a label at 0.4 seconds and place one tween at that label. Then change the first tween's duration and compare the label's fixed position with the end-relative position.

## Common mistakes

- Setting the destination beyond the row's width; lower `x` if a bar clips.
- Replaying before the prior timeline ends, which can make positions appear to jump.
- Forgetting that the three rows have independent coordinate spaces but share one timeline playhead.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous example</th><th>Chapter lesson</th><th>Chapter Q&amp;A</th><th>Next example</th></tr></thead>
  <tbody><tr><td><a href="008-timeline-fundamentals.md">008 - Timeline fundamentals example</a></td><td><a href="../lessons/009-timeline-position-parameter.md">Lesson</a></td><td><a href="../qnas/009-timeline-position-parameter.md">Q&amp;A</a></td><td><a href="010-labels-nested-timelines-and-controls.md">010 - Labels, nested timelines, and controls example</a></td></tr></tbody>
</table>
