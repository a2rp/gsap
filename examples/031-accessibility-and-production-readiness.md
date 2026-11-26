# 031 - Accessibility and production readiness Example

## Goal

Enhance a semantic card and button with motion only when the user has not requested reduced motion, and clean up the media context and button listener.

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
    <title>Accessibility and production readiness demo</title>
  </head>
  <body>
<section data-feature aria-labelledby="feature-title">
  <h2 id="feature-title">Featured lesson</h2>
  <article class="feature-card" data-panel>
    <p>Read the lesson and try the example.</p>
    <a href="#lesson-content">Open lesson</a>
  </article>
  <button type="button" data-play>Replay entrance</button>
  <div id="lesson-content" tabindex="-1"><h3>Lesson content</h3></div>
</section>
    <script type="module" src="/src/main.js"></script>
  </body>
</html>
``

## Styles: src/style.css

``css
.feature-card { opacity: 1; transform: none; }
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after { scroll-behavior: auto !important; }
}
``

## Animation: src/main.js

``js
import "./style.css";
import { gsap } from "gsap";

const root = document.querySelector("[data-feature]");
const panel = root?.querySelector("[data-panel]");
const replay = root?.querySelector("[data-play]");
const reduceMotion = window.matchMedia("(prefers-reduced-motion: reduce)");

if (root && panel && replay) {
  const motion = gsap.matchMedia(root);

  motion.add(
    {
      reduceMotion: "(prefers-reduced-motion: reduce)",
      fullMotion: "(prefers-reduced-motion: no-preference)"
    },
    ({ conditions }) => {
      gsap.set(panel, { autoAlpha: 1, x: 0 });
      if (conditions.fullMotion) {
        gsap.from(panel, { autoAlpha: 0, x: 20, duration: 0.4, ease: "power2.out" });
      }

      const replayEntrance = () => {
        gsap.killTweensOf(panel);
        if (reduceMotion.matches) {
          gsap.set(panel, { autoAlpha: 1, x: 0 });
          return;
        }
        gsap.fromTo(panel,
          { autoAlpha: 0, x: 20 },
          { autoAlpha: 1, x: 0, duration: 0.4, ease: "power2.out" }
        );
      };

      replay.addEventListener("click", replayEntrance);
      return () => replay.removeEventListener("click", replayEntrance);
    }
  );

  // Call from the view's teardown hook.
  function cleanupFeature() {
    motion.revert();
  }
}
``

## Expected result

The article and link are available without waiting for an entrance animation. With reduced motion requested, the card remains in place and replay exposes it immediately. Otherwise, the entrance uses a short transform and opacity transition. Removing the view reverts the media context and removes its listener.

## Practice variation

Use a short opacity-only transition for the non-reduced path and keep the reduced path immediate. Confirm both paths retain the same content and actions.

## Common mistakes

Starting the card hidden in CSS so it stays invisible if JavaScript fails; skipping the reduced-motion branch; attaching the replay listener outside the cleanup scope; using the visual entrance as the only indication that the content exists; leaving development markers enabled.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous example</th><th>Chapter lesson</th><th>Chapter Q&amp;A</th><th>Next example</th></tr></thead>
  <tbody><tr><td><a href="030-performance-and-debugging.md">030 - Performance and debugging example</a></td><td><a href="../lessons/031-accessibility-and-production-readiness.md">Lesson</a></td><td><a href="../qnas/031-accessibility-and-production-readiness.md">Q&amp;A</a></td><td><a href="032-capstone-animated-landing-page.md">032 - Capstone: animated landing page example</a></td></tr></tbody>
</table>
