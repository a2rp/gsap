# 028 - TextPlugin and SplitText Example

## Goal

Replace a short status label word by word and animate a heading by word while preserving a readable text source and restoring the original DOM on cleanup.

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
    <title>TextPlugin and SplitText demo</title>
  </head>
  <body>
<p class="status" data-status aria-live="polite">Loading</p>
<h1 class="headline" data-heading>Motion with meaning</h1>
<button type="button" data-replay>Replay heading</button>
    <script type="module" src="/src/main.js"></script>
  </body>
</html>
``

## Styles: src/style.css

``css
.headline { overflow: hidden; }
.headline .word { display: inline-block; }
.status { min-height: 1.5em; }
@media (prefers-reduced-motion: reduce) {
  .headline, .status { scroll-behavior: auto; }
}
``

## Animation: src/main.js

``js
import "./style.css";
import { gsap } from "gsap";
import { TextPlugin } from "gsap/TextPlugin";
import { SplitText } from "gsap/SplitText";

gsap.registerPlugin(TextPlugin, SplitText);

const status = document.querySelector("[data-status]");
const heading = document.querySelector("[data-heading]");
const replay = document.querySelector("[data-replay]");
const reduceMotion = window.matchMedia("(prefers-reduced-motion: reduce)");

if (status) {
  gsap.to(status, {
    duration: reduceMotion.matches ? 0 : 0.8,
    ease: "none",
    text: { value: "Ready to begin", delimiter: " " }
  });
}

let split;
let reveal;

function playHeading() {
  if (!heading) return;
  reveal?.kill();
  split?.revert();
  split = SplitText.create(heading, { type: "words" });
  reveal = gsap.from(split.words, {
    duration: reduceMotion.matches ? 0 : 0.5,
    y: 14,
    autoAlpha: 0,
    stagger: reduceMotion.matches ? 0 : 0.07,
    ease: "power2.out"
  });
}

replay?.addEventListener("click", playHeading);
playHeading();

// Call this from the view's teardown hook.
function cleanupTextMotion() {
  replay?.removeEventListener("click", playHeading);
  reveal?.kill();
  split?.revert();
}
``

## Expected result

The status text changes word by word. The heading words appear in a short stagger, and Replay restarts the effect without stacking wrappers. Calling cleanupTextMotion restores the original heading markup and removes the event listener.

## Practice variation

Use TextPlugin with a character delimiter for a short non-live decorative phrase, or split a headline into lines after its font is ready. Keep a complete static text alternative when the visual animation is hidden from assistive technology.

## Common mistakes

Splitting the text repeatedly without reverting the prior instance; using TextPlugin to inject markup; announcing each animation fragment; leaving the replay listener attached after teardown; assuming line splits remain unchanged across responsive widths.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous example</th><th>Chapter lesson</th><th>Chapter Q&amp;A</th><th>Next example</th></tr></thead>
  <tbody><tr><td><a href="027-scrollto-and-programmatic-scrolling.md">027 - ScrollTo and programmatic scrolling example</a></td><td><a href="../lessons/028-textplugin-and-splittext.md">Lesson</a></td><td><a href="../qnas/028-textplugin-and-splittext.md">Q&amp;A</a></td><td><a href="029-draggable-and-interaction.md">029 - Draggable and interaction example</a></td></tr></tbody>
</table>
