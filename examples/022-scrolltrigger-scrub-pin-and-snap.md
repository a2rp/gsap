# 022 - ScrollTrigger scrub, pin, and snap Example

## Goal

Pin a visual story panel while a two-step animation follows the scrollbar and snaps to named timeline beats.

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
    <title>ScrollTrigger scrub, pin, and snap demo</title>
  </head>
  <body>
    <main class="page">
      <section class="intro"><h1>A pinned scroll story</h1><p>Scroll to the panel and continue through its animation.</p></section>
      <section class="story">
        <div class="story__card"><p>Story card</p><h2>Follow the scroll</h2></div>
        <p class="story__hint">The card moves, turns, and settles at labeled beats.</p>
      </section>
      <section class="outro"><h2>Story complete</h2></section>
    </main>
    <script type="module" src="/src/main.js"></script>
  </body>
</html>
``

## Styles: src/style.css

``css
:root { font-family: system-ui, sans-serif; color: #172033; background: #eef2f8; }
body { margin: 0; }
.intro, .outro { min-height: 55vh; display: grid; align-content: center; width: min(44rem, calc(100% - 2rem)); margin: auto; }
.story { min-height: 70vh; display: grid; align-content: center; gap: 1rem; padding: 2rem max(1rem, calc((100vw - 44rem) / 2)); background: #dedbff; overflow: hidden; }
.story__card { width: min(20rem, 70vw); padding: 1.5rem; border-radius: 1rem; color: white; background: #635bdb; }
.story__hint { max-width: 30rem; }
.outro { min-height: 70vh; }
``

## Animation: src/main.js

``js
import "./style.css";
import { gsap } from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";

gsap.registerPlugin(ScrollTrigger);

const timeline = gsap.timeline({
  scrollTrigger: {
    trigger: ".story",
    start: "top top",
    end: () => `+=${window.innerHeight * 1.6}`,
    scrub: 0.35,
    pin: true,
    snap: "labelsDirectional",
    markers: true,
  },
});

timeline.addLabel("start")
  .to(".story__card", { x: 160, duration: 1, ease: "none" })
  .addLabel("turn")
  .to(".story__card", { rotation: 12, duration: 1, ease: "none" })
  .addLabel("end");
``

## Expected result

When the story reaches the top of the viewport, the panel pins. Scrolling through the range moves and rotates the card; after scrolling stops, the scroll position can settle on a labeled beat. Markers show the active range.

## Practice variation

Set `scrub: true` and compare direct tracking with the smoothed numeric scrub. Remove `pin` and check how the story section and following content flow.

## Common mistakes

- Leaving markers on in the final interface.
- Testing only with a mouse wheel; check touch scrolling and keyboard users.
- Pinning a section without enough content after it to make the end of the range reachable.
- Using `snap` without labels or a clear reason for discrete scroll stopping.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous example</th><th>Chapter lesson</th><th>Chapter Q&amp;A</th><th>Next example</th></tr></thead>
  <tbody><tr><td><a href="021-scrolltrigger-start-end-and-refresh.md">021 - ScrollTrigger start, end, and refresh example</a></td><td><a href="../lessons/022-scrolltrigger-scrub-pin-and-snap.md">Lesson</a></td><td><a href="../qnas/022-scrolltrigger-scrub-pin-and-snap.md">Q&amp;A</a></td><td><a href="023-scrolltrigger-callbacks-classes-and-batch.md">023 - ScrollTrigger callbacks, classes, and batch example</a></td></tr></tbody>
</table>
