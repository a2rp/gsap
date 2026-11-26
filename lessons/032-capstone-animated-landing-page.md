# 032 - Capstone: animated landing page

## Learning goals

Combine GSAP fundamentals, timelines, ScrollTrigger, ScrollTo, and reduced-motion handling in one page. Keep semantic content visible without JavaScript and preserve native navigation behavior. Organize animation setup and cleanup so the page remains maintainable.

## Core idea

A polished animated page is a collection of small, purposeful motion decisions. Start with complete semantic content and clear layout. Add a controlled hero entrance, reveal feature cards when they approach the viewport, and provide optional smooth in-page navigation. Respect reduced motion and remove listeners and match-media work when the page is disposed.

## How it works

Use an ES module and register every imported plugin once. Build a short hero timeline for related elements. Give each feature card its own ScrollTrigger so its geometry remains local and understandable. Use ScrollToPlugin only for animated navigation, leaving native anchors available when reduced motion is requested. Scope selectors to the page root. Use gsap.matchMedia() to create the motion path and return cleanup for native event listeners. Keep visible CSS defaults so content is readable before JavaScript runs.

``js
import { gsap } from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";
import { ScrollToPlugin } from "gsap/ScrollToPlugin";

gsap.registerPlugin(ScrollTrigger, ScrollToPlugin);

const page = document.querySelector("[data-page]");
const header = page?.querySelector("[data-header]");
const motion = page ? gsap.matchMedia(page) : null;

motion?.add(
  {
    reduceMotion: "(prefers-reduced-motion: reduce)",
    fullMotion: "(prefers-reduced-motion: no-preference)"
  },
  ({ conditions }) => {
    if (!page) return;

    if (conditions.fullMotion) {
      gsap.from(page.querySelectorAll("[data-hero-item]"), {
        y: 22,
        autoAlpha: 0,
        duration: 0.55,
        stagger: 0.1,
        ease: "power2.out"
      });

      gsap.utils.toArray("[data-feature-card]", page).forEach((card) => {
        gsap.from(card, {
          y: 28,
          autoAlpha: 0,
          duration: 0.55,
          ease: "power2.out",
          scrollTrigger: { trigger: card, start: "top 85%" }
        });
      });
    }

    const onNavigate = (event) => {
      const link = event.currentTarget;
      const href = link.getAttribute("href");
      const destination = href ? page.querySelector(href) : null;
      if (!destination || !conditions.fullMotion) return;

      event.preventDefault();
      gsap.to(window, {
        duration: 0.65,
        ease: "power2.inOut",
        scrollTo: {
          y: destination,
          offsetY: header?.getBoundingClientRect().height ?? 0,
          autoKill: true
        },
        onComplete: () => destination.focus({ preventScroll: true })
      });
      history.pushState(null, "", href);
    };

    const links = page.querySelectorAll('a[href^="#"]');
    links.forEach((link) => link.addEventListener("click", onNavigate));
    return () => links.forEach((link) => link.removeEventListener("click", onNavigate));
  }
);

// Call when this page view is disposed:
// motion?.revert();
``

Read the code from the target outward: identify the animated value, then the GSAP configuration that controls its start, destination, timing, or lifecycle. In DOM examples, make sure the selected elements exist before this module runs. In object examples, update the visible interface from the changing object value yourself.

## When to use it and its limits

Use this capstone as a starting point, not as a motion checklist. Each animation should clarify hierarchy or response. Keep native links as the navigation contract, use motion as an enhancement, and test the page with reduced motion, keyboard input, narrow screens, slow rendering, and JavaScript disabled.

The example assumes a browser page with a single document scroller and a stable header. A router, nested scroller, changing header height, content loaded after initialization, or client-side view transition may need a different lifecycle and a deliberate ScrollTrigger refresh. The sample is a foundation and still needs project-specific content, visual design, and browser testing.

## Common mistakes

Animating every element because the library is available; hiding content in CSS before JavaScript runs; replacing anchor links with click-only controls; forgetting to revert the match-media context; using the same motion for reduced-motion and full-motion preferences; leaving markers or test diagnostics in the release.

## Recap and practice

Build a landing page with a hero, three feature cards, and a contact section. Add a short hero entrance, card reveals, and header-aware in-page navigation. Then validate the same content with reduced motion, JavaScript disabled, keyboard navigation, and a narrow viewport.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous lesson</th><th>Chapter Q&amp;A</th><th>Chapter example</th><th>Next lesson</th></tr></thead>
  <tbody><tr><td><a href="031-accessibility-and-production-readiness.md">031 - Accessibility and production readiness</a></td><td><a href="../qnas/032-capstone-animated-landing-page.md">Q&amp;A</a></td><td><a href="../examples/032-capstone-animated-landing-page.md">Example</a></td><td>End of course</td></tr></tbody>
</table>
