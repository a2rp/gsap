# 010 - Labels, nested timelines, and controls Example

## Goal

Create a labeled parent sequence with a nested details timeline and expose playback controls.

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
    <title>Labels, nested timelines, and controls demo</title>
  </head>
  <body>
    <main class="demo">
      <p class="eyebrow">GSAP sequence</p>
      <h1 class="title">Named animation beats</h1>
      <ul class="details"><li class="detail">First detail</li><li class="detail">Second detail</li></ul>
      <div class="controls"><button id="play">Play</button><button id="reverse">Reverse</button><button id="seek">Seek to details</button></div>
    </main>
    <script type="module" src="/src/main.js"></script>
  </body>
</html>
``

## Styles: src/style.css

``css
:root { font-family: system-ui, sans-serif; color: #172033; background: #eef2f8; }
body { margin: 0; min-height: 100vh; display: grid; place-items: center; }
.demo { width: min(40rem, calc(100% - 2rem)); padding: 2rem; background: white; border-radius: 1rem; }
.eyebrow { color: #635bdb; text-transform: uppercase; font-weight: 700; }
.details { display: grid; gap: .5rem; padding-left: 1.25rem; }
.controls { display: flex; flex-wrap: wrap; gap: .5rem; }
button { padding: .6rem .9rem; cursor: pointer; }
``

## Animation: src/main.js

``js
import "./style.css";
import { gsap } from "gsap";

const details = gsap.timeline();
details.from(".detail", { y: 14, autoAlpha: 0, stagger: 0.12, duration: 0.35 });

const page = gsap.timeline({ paused: true });
page.addLabel("intro")
  .from(".eyebrow", { y: 10, autoAlpha: 0, duration: 0.3 }, "intro")
  .from(".title", { y: 22, autoAlpha: 0, duration: 0.5 }, "intro+=0.1")
  .addLabel("details", "+=0.15")
  .add(details, "details")
  .addLabel("complete");

document.querySelector("#play").addEventListener("click", () => page.play());
document.querySelector("#reverse").addEventListener("click", () => page.reverse());
document.querySelector("#seek").addEventListener("click", () => page.pause().seek("details"));
``

## Expected result

Play reveals the eyebrow and title, then plays the nested list sequence. Reverse moves backward through both. Seek to details pauses at the named beat so you can inspect the child sequence's start.

## Practice variation

Change the title tween position to `"intro+=0.3"`. Add another named label after the nested sequence and seek to it from a button.

## Common mistakes

- If the details appear immediately, remember that a child timeline plays on its own until it is placed under the paused parent. Create it paused or pause it before adding, if that is needed for the desired initial state.
- Seeking after play without pausing leaves the parent moving.
- Using duplicate selectors in multiple component instances can animate unrelated details.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous example</th><th>Chapter lesson</th><th>Chapter Q&amp;A</th><th>Next example</th></tr></thead>
  <tbody><tr><td><a href="009-timeline-position-parameter.md">009 - Timeline position parameter example</a></td><td><a href="../lessons/010-labels-nested-timelines-and-controls.md">Lesson</a></td><td><a href="../qnas/010-labels-nested-timelines-and-controls.md">Q&amp;A</a></td><td><a href="011-callbacks-and-animation-events.md">011 - Callbacks and animation events example</a></td></tr></tbody>
</table>
