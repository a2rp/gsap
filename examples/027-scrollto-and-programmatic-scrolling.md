# 027 - ScrollTo and programmatic scrolling Example

## Goal

Build a small in-page contents list that smoothly moves to a target section while leaving ordinary anchor navigation available.

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
    <title>ScrollTo and programmatic scrolling demo</title>
  </head>
  <body>
<nav class="contents" aria-label="On this page">
  <a href="#overview" data-scroll-link>Overview</a>
  <a href="#details" data-scroll-link>Details</a>
  <a href="#contact" data-scroll-link>Contact</a>
</nav>

<header class="site-header" data-site-header>Article guide</header>
<main>
  <section id="overview" tabindex="-1"><h2>Overview</h2></section>
  <section id="details" tabindex="-1"><h2>Details</h2></section>
  <section id="contact" tabindex="-1"><h2>Contact</h2></section>
</main>
    <script type="module" src="/src/main.js"></script>
  </body>
</html>
``

## Styles: src/style.css

``css
html { scroll-behavior: auto; }
.site-header { position: sticky; top: 0; }
section { min-height: 70vh; scroll-margin-top: 1rem; }
.contents { display: flex; gap: 1rem; }
``

## Animation: src/main.js

``js
import "./style.css";
import { gsap } from "gsap";
import { ScrollToPlugin } from "gsap/ScrollToPlugin";

gsap.registerPlugin(ScrollToPlugin);

const header = document.querySelector("[data-site-header]");
const reduceMotion = window.matchMedia("(prefers-reduced-motion: reduce)");

document.querySelectorAll("[data-scroll-link]").forEach((link) => {
  link.addEventListener("click", (event) => {
    const href = link.getAttribute("href");
    const destination = href ? document.querySelector(href) : null;
    if (!destination) return;

    event.preventDefault();
    const offset = header?.getBoundingClientRect().height ?? 0;

    gsap.to(window, {
      duration: reduceMotion.matches ? 0 : 0.7,
      ease: "power2.out",
      scrollTo: { y: destination, offsetY: offset, autoKill: true },
      onComplete: () => destination.focus({ preventScroll: true })
    });

    history.replaceState(null, "", href);
  });
});
``

## Expected result

Activating a contents link moves the document to the selected section, leaving its heading clear of the sticky header. If the user takes over scrolling, the tween can stop. Keyboard users can activate the same links and focus moves to the destination section. With reduced motion enabled, the position changes without a prolonged tween.

## Practice variation

Replace window with a scrollable article container and animate that container. Keep each section link's href pointed at a real id, and calculate the destination relative to the chosen scroller.

## Common mistakes

Removing href values and making the controls inaccessible; animating window when a nested element owns scrolling; hard-coding the header offset; using a nonzero duration for reduced motion; allowing CSS smooth behavior and ScrollToPlugin to compete.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous example</th><th>Chapter lesson</th><th>Chapter Q&amp;A</th><th>Next example</th></tr></thead>
  <tbody><tr><td><a href="026-motionpath-and-path-animation.md">026 - MotionPath and path animation example</a></td><td><a href="../lessons/027-scrollto-and-programmatic-scrolling.md">Lesson</a></td><td><a href="../qnas/027-scrollto-and-programmatic-scrolling.md">Q&amp;A</a></td><td><a href="028-textplugin-and-splittext.md">028 - TextPlugin and SplitText example</a></td></tr></tbody>
</table>
