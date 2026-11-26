# 021 - ScrollTrigger start, end, and refresh Example

## Goal

Tie a scrubbed box movement to the measured height of its section and inspect start/end positions after resizing.

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
    <title>ScrollTrigger start, end, and refresh demo</title>
  </head>
  <body>
    <main class="page">
      <section class="intro"><h1>Measured scroll range</h1><p>Scroll through the feature section.</p></section>
      <section class="feature"><div class="feature__box">Scrub range</div><p>The end distance follows this section's height.</p></section>
      <section class="outro"><h2>After the trigger</h2></section>
    </main>
    <script type="module" src="/src/main.js"></script>
  </body>
</html>
```

## Styles: src/style.css

```css
:root { font-family: system-ui, sans-serif; color: #172033; background: #eef2f8; }
body { margin: 0; }
.page { min-height: 100vh; }
.intro, .feature, .outro { width: min(44rem, calc(100% - 2rem)); margin: 0 auto 25vh; padding: 2rem; border-radius: 1rem; background: white; }
.feature { min-height: 65vh; background: #e9e7ff; }
.feature__box { width: 8rem; padding: 1rem; border-radius: .8rem; color: white; background: #635bdb; }
.outro { margin-bottom: 0; }
```

## Animation: src/main.js

```js
import "./style.css";
import { gsap } from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";

gsap.registerPlugin(ScrollTrigger);

const feature = document.querySelector(".feature");

gsap.to(".feature__box", {
  x: 240,
  scrollTrigger: {
    trigger: feature,
    start: "top 75%",
    end: () => `+=${feature.offsetHeight}`,
    scrub: true,
    invalidateOnRefresh: true,
    markers: true,
  },
});
```

## Expected result

The box's horizontal progress follows the scroll position from the section start to an end distance based on the section's measured height. Resizing changes the measured distance after ScrollTrigger refreshes.

## Practice variation

Change `end` to `"clamp(bottom top)"` in GSAP 3.12 or newer and observe how a trigger near the page end is constrained. Add content above the section and call `ScrollTrigger.refresh()` after the new content is rendered.

## Common mistakes

- Testing only at one viewport size while relying on a measured height.
- Calling `refresh()` before the layout change has been applied.
- Forgetting to register ScrollTrigger.
- Leaving markers enabled after checking the start and end.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous example</th><th>Chapter lesson</th><th>Chapter Q&amp;A</th><th>Next example</th></tr></thead>
  <tbody><tr><td><a href="020-scrolltrigger-fundamentals.md">020 - ScrollTrigger fundamentals example</a></td><td><a href="../lessons/021-scrolltrigger-start-end-and-refresh.md">Lesson</a></td><td><a href="../qnas/021-scrolltrigger-start-end-and-refresh.md">Q&amp;A</a></td><td><a href="022-scrolltrigger-scrub-pin-and-snap.md">022 - ScrollTrigger scrub, pin, and snap example</a></td></tr></tbody>
</table>
