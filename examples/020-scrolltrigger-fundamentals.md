# 020 - ScrollTrigger fundamentals Example

## Goal

Reveal one section when it approaches the viewport, with development markers to see the trigger boundary.

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
    <title>ScrollTrigger fundamentals demo</title>
  </head>
  <body>
    <main class="page">
      <section class="intro"><h1>Scroll to the feature</h1><p>Keep scrolling until the next section reaches the viewport.</p></section>
      <div class="spacer" aria-hidden="true"></div>
      <section class="feature"><p class="eyebrow">ScrollTrigger</p><h2>A section enters view</h2><p>The trigger starts when this section reaches the configured position.</p></section>
      <div class="spacer" aria-hidden="true"></div>
    </main>
    <script type="module" src="/src/main.js"></script>
  </body>
</html>
``

## Styles: src/style.css

``css
:root { font-family: system-ui, sans-serif; color: #172033; background: #eef2f8; }
body { margin: 0; }
.page { min-height: 100vh; }
.intro, .feature { width: min(44rem, calc(100% - 2rem)); margin: 0 auto; padding: 3rem 2rem; border-radius: 1rem; background: white; }
.intro { margin-top: 8vh; }
.feature { background: #e9e7ff; }
.eyebrow { color: #635bdb; font-weight: 700; text-transform: uppercase; }
.spacer { height: 60vh; }
``

## Animation: src/main.js

``js
import "./style.css";
import { gsap } from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";

gsap.registerPlugin(ScrollTrigger);

gsap.from(".feature", {
  y: 32,
  autoAlpha: 0,
  duration: 0.7,
  ease: "power2.out",
  scrollTrigger: {
    trigger: ".feature",
    start: "top 80%",
    markers: true,
  },
});
``

## Expected result

Scroll down until the feature section's top reaches about 80 percent down the viewport. The section animates into view, and colored markers show the calculated trigger positions.

## Practice variation

Change `start` to `"top center"` and compare. Remove `markers` after tuning. Add another section and create a second trigger using the same registration.

## Common mistakes

- Setting the page height too short to reach the trigger. The spacer elements provide a scroll range for this demo.
- Leaving markers enabled in a finished interface.
- Loading ScrollTrigger through both a CDN script and a package import.
- Forgetting to register the plugin, which can be hidden during development but fail after bundling.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous example</th><th>Chapter lesson</th><th>Chapter Q&amp;A</th><th>Next example</th></tr></thead>
  <tbody><tr><td><a href="019-gsap-in-react-with-usegsap.md">019 - GSAP in React with useGSAP() example</a></td><td><a href="../lessons/020-scrolltrigger-fundamentals.md">Lesson</a></td><td><a href="../qnas/020-scrolltrigger-fundamentals.md">Q&amp;A</a></td><td><a href="021-scrolltrigger-start-end-and-refresh.md">021 - ScrollTrigger start, end, and refresh example</a></td></tr></tbody>
</table>
