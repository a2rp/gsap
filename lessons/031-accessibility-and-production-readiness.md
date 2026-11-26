# 031 - Accessibility and production readiness

## Learning goals

Respect reduced-motion preferences and preserve usable content when animation is absent. Keep animated interactions semantic, keyboard-operable, and under user control. Prepare animation code for cleanup, responsive layouts, and production review.

## Core idea

Animation is part of an interface, so it must not hide essential information or block interaction. Accessible motion keeps the content understandable without animation, offers equivalent interaction paths, and respects user preferences such as prefers-reduced-motion.

## How it works

Use gsap.matchMedia() to create separate motion behavior for reduced and non-reduced preferences. Animations created inside a matching handler are recorded and reverted when the condition changes or the match media context is reverted. Keep controls as native links and buttons where possible. Avoid autoplaying essential announcements, provide pause/stop controls for persistent motion, preserve focus and reading order, and ensure animation does not create keyboard traps. Clean up event listeners, custom ticker callbacks, Draggable instances, split text, and context-owned animations when a view is removed. Remove markers and diagnostics before production.

```js
import { gsap } from "gsap";

const root = document.querySelector("[data-feature]");
const playButton = root?.querySelector("[data-play]");
const panel = root?.querySelector("[data-panel]");

const motion = gsap.matchMedia(root);
motion.add(
  {
    reduceMotion: "(prefers-reduced-motion: reduce)",
    fullMotion: "(prefers-reduced-motion: no-preference)"
  },
  ({ conditions }) => {
    if (!panel) return;

    gsap.set(panel, { autoAlpha: 1, x: 0 });
    if (conditions.fullMotion) {
      gsap.from(panel, { autoAlpha: 0, x: 24, duration: 0.45, ease: "power2.out" });
    }
  }
);

// When the owning view is disposed:
// playButton?.removeEventListener("click", onPlay);
// motion.revert();
```

Read the code from the target outward: identify the animated value, then the GSAP configuration that controls its start, destination, timing, or lifecycle. In DOM examples, make sure the selected elements exist before this module runs. In object examples, update the visible interface from the changing object value yourself.

## When to use it and its limits

Begin with the static, semantic interface and add motion as enhancement. Test with the operating system's reduced-motion setting, keyboard only, screen-reader reading order, narrow viewports, and interrupted transitions. For a meaningful animated state change, expose the state through text or semantics rather than relying only on movement or color.

A reduced-motion preference does not prescribe one universal animation policy; choose behavior appropriate to the experience, often removing large or continuous movement while preserving essential state changes. gsap.matchMedia() reverts animations and ScrollTriggers created in its handler, but external listeners or unrelated resources still need explicit cleanup.

## Common mistakes

Hiding all content until an animation runs; ignoring reduced motion; using a clickable div without keyboard semantics; making an essential action depend on a hover or timed sequence; allowing motion to steal focus; forgetting to remove listeners; leaving development markers or console diagnostics enabled in a release.

## Recap and practice

Take an animated card reveal and create a reduced-motion path that exposes the card immediately. Verify the button is keyboard-operable, content order remains meaningful, focus is not moved by decoration, and teardown removes all listeners and animation contexts.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous lesson</th><th>Chapter Q&amp;A</th><th>Chapter example</th><th>Next lesson</th></tr></thead>
  <tbody><tr><td><a href="030-performance-and-debugging.md">030 - Performance and debugging</a></td><td><a href="../qnas/031-accessibility-and-production-readiness.md">Q&amp;A</a></td><td><a href="../examples/031-accessibility-and-production-readiness.md">Example</a></td><td><a href="032-capstone-animated-landing-page.md">032 - Capstone: animated landing page</a></td></tr></tbody>
</table>
