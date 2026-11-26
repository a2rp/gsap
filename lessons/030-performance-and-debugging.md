# 030 - Performance and debugging

## Learning goals

Find whether slow animation comes from rendering, layout, excessive work, or incorrect trigger positions. Use GSAP inspection and ScrollTrigger diagnostics deliberately. Prefer simple, measurable optimizations over blanket performance flags.

## Core idea

Smooth animation depends on the browser doing little work per frame. Start by identifying what is slow and which properties change. Transform and opacity often avoid layout work, but profiling and the actual page determine the right fix. GSAP keeps its animation updates synchronized with the browser rendering cycle.

## How it works

Use ScrollTrigger markers during development to see calculated start and end positions. Call refresh after a layout change that affects trigger geometry; refresh recalculates positions, while update checks the current scroll position. Inspect active tweens with gsap.getTweensOf() and triggers with ScrollTrigger.getAll(). Avoid repeated DOM measurements or layout writes inside frame callbacks. If you add a custom gsap.ticker listener, remove it when no longer needed. Measure with browser performance tools before adding will-change or forcing layers.

```js
import { gsap } from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";

gsap.registerPlugin(ScrollTrigger);

const card = document.querySelector("[data-card]");
if (card) {
  gsap.to(card, {
    x: 120,
    autoAlpha: 1,
    duration: 0.7,
    scrollTrigger: {
      trigger: card,
      start: "top 85%",
      markers: import.meta.env?.DEV ?? false
    }
  });

  console.log("card tweens", gsap.getTweensOf(card));
  console.log("all triggers", ScrollTrigger.getAll());
}

// After inserting content above existing triggers:
requestAnimationFrame(() => ScrollTrigger.refresh());
```

Read the code from the target outward: identify the animated value, then the GSAP configuration that controls its start, destination, timing, or lifecycle. In DOM examples, make sure the selected elements exist before this module runs. In object examples, update the visible interface from the changing object value yourself.

## When to use it and its limits

When an animation stutters, reproduce the issue and profile the page first. Check for layout shifts, large images, expensive filters, excessive simultaneous animations, repeated event listeners, and stale ScrollTrigger measurements. Use markers to diagnose geometry, then remove them from production. Optimize the cause rather than adding CSS hints everywhere.

Animating transform and opacity is often efficient, but it does not guarantee a fast page when the scene contains many large layers or expensive effects. A refresh can be costly if called too often. Diagnostic markers and console inspection are development tools. `will-change` and forced GPU layers consume memory and can make performance worse.

## Common mistakes

Adding will-change to every animated element; disabling lag smoothing to hide frame drops; calling refresh on every scroll event; measuring layout repeatedly inside onUpdate; leaving ticker listeners or markers enabled in production; using gsap.killTweensOf broadly and stopping unrelated motion.

## Recap and practice

Create a ScrollTrigger scene with markers. Record its start/end values and inspect it while resizing. Insert content above it, call refresh once after the DOM update, and compare. Use browser profiling to identify whether layout, paint, or scripting is the actual bottleneck.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous lesson</th><th>Chapter Q&amp;A</th><th>Chapter example</th><th>Next lesson</th></tr></thead>
  <tbody><tr><td><a href="029-draggable-and-interaction.md">029 - Draggable and interaction</a></td><td><a href="../qnas/030-performance-and-debugging.md">Q&amp;A</a></td><td><a href="../examples/030-performance-and-debugging.md">Example</a></td><td><a href="031-accessibility-and-production-readiness.md">031 - Accessibility and production readiness</a></td></tr></tbody>
</table>
