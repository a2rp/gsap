# 027 - ScrollTo and programmatic scrolling

## Learning goals

Animate the window or a scrollable element to a useful destination. Choose offsets and auto-kill behavior that cooperate with real user input. Keep programmatic navigation accessible and avoid fighting native scrolling.

## Core idea

ScrollToPlugin animates a target's scroll position. Use it for deliberate navigation to a section or coordinate. ScrollTrigger is for reacting to scroll positions and building scroll-linked scenes; ScrollTo is for moving the scroll position itself.

## How it works

Register ScrollToPlugin before using the scrollTo property. Target window for document scrolling or a specific overflow container for nested scrolling. A destination may be a number or an element selector/reference. Object form accepts x, y, offsetX, offsetY, and autoKill. Offset values account for fixed headers. Auto-kill lets the plugin stop controlling an axis when it detects that the user changed that scroll position externally. CSS scroll-behavior:smooth may conflict with a JavaScript scroll tween, so use one owner for the motion.

``js
import { gsap } from "gsap";
import { ScrollToPlugin } from "gsap/ScrollToPlugin";

gsap.registerPlugin(ScrollToPlugin);

const navigation = document.querySelector("[data-navigation]");
const button = document.querySelector("[data-scroll-to-contact]");
const contact = document.querySelector("#contact");

button?.addEventListener("click", () => {
  if (!contact) return;

  gsap.to(window, {
    duration: 0.8,
    ease: "power2.inOut",
    scrollTo: {
      y: contact,
      offsetY: navigation?.getBoundingClientRect().height ?? 0,
      autoKill: true
    }
  });
});
``

Read the code from the target outward: identify the animated value, then the GSAP configuration that controls its start, destination, timing, or lifecycle. In DOM examples, make sure the selected elements exist before this module runs. In object examples, update the visible interface from the changing object value yourself.

## When to use it and its limits

Use this for a table-of-contents control, a skip-to-section button, or moving an inner scroll panel to a selected item. Prefer a normal anchor link as the semantic foundation. Intercept it only when the animated transition improves the interaction, preserve keyboard activation, and ensure the destination can receive focus when appropriate. For reduced motion, use an immediate native scroll or a near-zero duration rather than forcing motion.

ScrollToPlugin does not create scroll-triggered animation scenes; use ScrollTrigger for that. Smooth document scrolling can conflict with CSS scroll-behavior:smooth or another script that writes scroll position. A section's final position depends on layout, sticky headers, and viewport size. Do not rely on a hard-coded pixel coordinate when the intended destination is a semantic element.

## Common mistakes

Animating a nested container when the window is the scroller; forgetting to register the plugin; using selector text for a missing element; measuring a fixed header only once even though its size changes; stacking CSS smooth scrolling and a GSAP tween; using ScrollTo to synchronize a scrubbed animation.

## Recap and practice

Add a page table of contents with three sections. Keep each link usable without JavaScript, animate the window to the target with an offset for a sticky header, and test a user interrupt during the tween. Then add a nested scroll panel and animate only that panel.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous lesson</th><th>Chapter Q&amp;A</th><th>Chapter example</th><th>Next lesson</th></tr></thead>
  <tbody><tr><td><a href="026-motionpath-and-path-animation.md">026 - MotionPath and path animation</a></td><td><a href="../qnas/027-scrollto-and-programmatic-scrolling.md">Q&amp;A</a></td><td><a href="../examples/027-scrollto-and-programmatic-scrolling.md">Example</a></td><td><a href="028-textplugin-and-splittext.md">028 - TextPlugin and SplitText</a></td></tr></tbody>
</table>
