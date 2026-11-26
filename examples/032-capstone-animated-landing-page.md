# 032 - Capstone: animated landing page Example

## Goal

Assemble a complete small landing page with semantic in-page links, a reduced-motion-aware hero entrance, viewport reveals for feature cards, and correct cleanup.

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
    <title>Capstone: animated landing page demo</title>
  </head>
  <body>
<div class="page" data-page>
  <header class="site-header" data-header>
    <a href="#top" class="brand">Motion Studio</a>
    <nav aria-label="Main navigation">
      <a href="#features">Features</a>
      <a href="#approach">Approach</a>
      <a href="#contact">Contact</a>
    </nav>
  </header>
  <main id="top">
    <section class="hero" aria-labelledby="hero-title">
      <p data-hero-item>Thoughtful motion for the web</p>
      <h1 id="hero-title" data-hero-item>Make every interaction feel clear.</h1>
      <a class="button" href="#features" data-hero-item>Explore the work</a>
    </section>
    <section id="features" class="features" aria-labelledby="features-title" tabindex="-1">
      <h2 id="features-title">What we build</h2>
      <article class="feature-card" data-feature-card><h3>Purposeful</h3><p>Motion supports the task.</p></article>
      <article class="feature-card" data-feature-card><h3>Responsive</h3><p>Layouts adapt to the viewport.</p></article>
      <article class="feature-card" data-feature-card><h3>Accessible</h3><p>Content works with or without motion.</p></article>
    </section>
    <section id="approach" class="approach" aria-labelledby="approach-title" tabindex="-1">
      <h2 id="approach-title">Start with the experience</h2>
      <p>Build the semantic page first, then add motion where it helps.</p>
    </section>
    <section id="contact" class="contact" aria-labelledby="contact-title" tabindex="-1">
      <h2 id="contact-title">Ready to begin?</h2>
      <a href="mailto:hello@example.test">Get in touch</a>
    </section>
  </main>
</div>
    <script type="module" src="/src/main.js"></script>
  </body>
</html>
``

## Styles: src/style.css

``css
* { box-sizing: border-box; }
html { scroll-behavior: auto; }
body { margin: 0; font-family: system-ui, sans-serif; line-height: 1.5; }
.site-header { position: sticky; top: 0; z-index: 2; display: flex; justify-content: space-between; gap: 1rem; padding: 1rem 5vw; background: white; }
.site-header nav { display: flex; gap: 1rem; }
.hero, .features, .approach, .contact { padding: 5rem 8vw; }
.hero { min-height: 75vh; display: grid; align-content: center; gap: 1rem; background: #eef3ff; }
.hero h1 { max-width: 15ch; font-size: clamp(2.5rem, 8vw, 5rem); line-height: 1.05; }
.features { display: grid; gap: 1rem; }
.feature-card { padding: 1.5rem; border-radius: 1rem; background: #192d52; color: white; }
.button { justify-self: start; padding: 0.75rem 1rem; background: #315ee8; color: white; border-radius: 0.5rem; }
@media (prefers-reduced-motion: reduce) { *, *::before, *::after { scroll-behavior: auto !important; } }
@media (max-width: 38rem) { .site-header { align-items: flex-start; flex-direction: column; } .site-header nav { flex-wrap: wrap; } }
``

## Animation: src/main.js

``js
import "./style.css";
import { gsap } from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";
import { ScrollToPlugin } from "gsap/ScrollToPlugin";

gsap.registerPlugin(ScrollTrigger, ScrollToPlugin);

const page = document.querySelector("[data-page]");
const header = page?.querySelector("[data-header]");

if (page) {
  const motion = gsap.matchMedia(page);

  motion.add(
    {
      reduceMotion: "(prefers-reduced-motion: reduce)",
      fullMotion: "(prefers-reduced-motion: no-preference)"
    },
    ({ conditions }) => {
      if (conditions.fullMotion) {
        gsap.from(page.querySelectorAll("[data-hero-item]"), {
          y: 20,
          autoAlpha: 0,
          duration: 0.55,
          stagger: 0.1,
          ease: "power2.out"
        });

        gsap.utils.toArray("[data-feature-card]", page).forEach((card) => {
          gsap.from(card, {
            y: 26,
            autoAlpha: 0,
            duration: 0.5,
            ease: "power2.out",
            scrollTrigger: { trigger: card, start: "top 85%" }
          });
        });
      }

      const navigate = (event) => {
        const link = event.currentTarget;
        const href = link.getAttribute("href");
        const target = href ? page.querySelector(href) : null;
        if (!target || !conditions.fullMotion) return;

        event.preventDefault();
        gsap.to(window, {
          duration: 0.6,
          ease: "power2.inOut",
          scrollTo: {
            y: target,
            offsetY: header?.getBoundingClientRect().height ?? 0,
            autoKill: true
          },
          onComplete: () => target.focus({ preventScroll: true })
        });
        history.pushState(null, "", href);
      };

      const links = page.querySelectorAll('a[href^="#"]');
      links.forEach((link) => link.addEventListener("click", navigate));
      return () => links.forEach((link) => link.removeEventListener("click", navigate));
    }
  );

  // Call from a client-side view's teardown hook.
  function cleanupLandingPage() {
    motion.revert();
  }
}
``

## Expected result

Without JavaScript or when reduced motion is requested, every section, link, and action is still visible and usable. With full motion enabled, the hero items enter in a brief stagger, cards reveal as they approach the viewport, and in-page links scroll below the sticky header. Removing the page view reverts the context and its listener cleanup.

## Practice variation

Add a single timeline for the hero and label its beats. Keep the same static markup and reduced-motion behavior, and add only one new effect when it clarifies the content.

## Common mistakes

Hiding sections in CSS before GSAP runs; animating every section continuously; forgetting to register ScrollToPlugin or ScrollTrigger; using smooth scrolling when reduced motion is requested; retaining event listeners after route changes; failing to refresh triggers after asynchronously inserted content changes layout.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous example</th><th>Chapter lesson</th><th>Chapter Q&amp;A</th><th>Next example</th></tr></thead>
  <tbody><tr><td><a href="031-accessibility-and-production-readiness.md">031 - Accessibility and production readiness example</a></td><td><a href="../lessons/032-capstone-animated-landing-page.md">Lesson</a></td><td><a href="../qnas/032-capstone-animated-landing-page.md">Q&amp;A</a></td><td>End of course</td></tr></tbody>
</table>
