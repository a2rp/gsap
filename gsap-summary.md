# GSAP Summary

A topic-wide review of GSAP 3 concepts from this course. Use the [keywords index](gsap-keywords.md) to find API names and the [README roadmap](README.md) to open any chapter's lesson, Q&A, or example.

## What GSAP does

GSAP animates JavaScript values over time. It can update DOM CSS properties, SVG attributes, and ordinary object properties. A tween describes a change; a timeline sequences and controls multiple tweens. Plugins add capabilities such as scroll-triggered motion, layout transitions, path motion, and dragging.

The examples in this repository use GSAP 3 and ES modules. GSAP 3.15.1 was the latest release visible in the official project history when these notes were prepared. Match APIs to the version installed in your own project.

## Install and import

```bash
npm install gsap
```

```js
import { gsap } from "gsap";

const tween = gsap.to(".card", {
  x: 120,
  duration: 0.6,
  ease: "power2.out",
});
```

When importing a plugin, import and register it:

```js
import { gsap } from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";

gsap.registerPlugin(ScrollTrigger);
```

Registering makes plugin use explicit and avoids bundler tree-shaking problems. Read [installation and setup](lessons/002-installation-and-project-setup.md).

## Pick the right tween

```js
// Current values -> destination values
gsap.to(target, { x: 100 });

// Specified start values -> values captured from the target
gsap.from(target, { opacity: 0, y: 24 });

// Explicit start -> explicit destination
gsap.fromTo(target, { opacity: 0 }, { opacity: 1, duration: 0.4 });

// Apply state immediately
gsap.set(target, { autoAlpha: 1 });
```

Use `to()` when CSS or application state already defines the start. Use `from()` when the target should animate into its current state. Use `fromTo()` when both ends must be explicit. Keep initial CSS deliberate, especially for hidden elements and `from()` animations.

## Timing and motion

- `duration` and `delay` are in seconds.
- `ease` controls the velocity curve. Use `"none"` for linear motion and names such as `"power2.out"` for eased motion.
- `repeat` counts additional iterations; `-1` repeats indefinitely.
- `repeatDelay` inserts a pause between iterations.
- `yoyo: true` alternates direction when repeating.
- `stagger` offsets multiple targets; a configuration object can distribute motion across a grid or from a chosen origin.
- Function-based values receive the target index and element, enabling per-target distances.

See [timing and easing](lessons/005-timing-easing-and-repeats.md), [dynamic values](lessons/006-targets-and-dynamic-values.md), and [staggers](lessons/007-staggers-and-distribution.md).

## Sequence with a timeline

```js
const intro = gsap.timeline({ paused: true });

intro
  .from(".eyebrow", { y: 12, autoAlpha: 0, duration: 0.35 })
  .from(".title", { y: 28, autoAlpha: 0, duration: 0.55 }, "<0.1")
  .from(".button", { scale: 0.9, autoAlpha: 0, duration: 0.3 }, "-=0.15");

intro.play();
```

A timeline provides one playhead and one place to adjust order, overlap, repeat, and playback. The position parameter supports absolute seconds, labels, `"<"` for the previous animation's start, `">"` for its end, and relative offsets such as `"-=0.2"`. See [timeline fundamentals](lessons/008-timeline-fundamentals.md) and [position parameter](lessons/009-timeline-position-parameter.md).

## Animate DOM and SVG

For HTML, CSSPlugin is part of GSAP core. Prefer transform aliases such as `x`, `y`, `xPercent`, `rotation`, and `scale` instead of constructing transform strings. Use `autoAlpha` for opacity plus visibility when appropriate. For SVG, animate supported CSS properties or attributes through `attr`, and pay attention to SVG coordinate systems and transform origins.

Avoid animating layout-heavy properties such as `width`, `height`, `top`, and `left` continuously when a transform can accomplish the same visual result. When layout must change, measure and test the resulting document flow.

## Scope and cleanup

Use `gsap.context()` to collect animations and revert them together. In React, prefer `useGSAP()` from `@gsap/react`, which scopes selectors and handles cleanup for the component lifecycle. When creating animations from delayed callbacks or event handlers, use the hook's context-safe pattern so cleanup still captures them.

For responsive setup, `gsap.matchMedia()` runs separate animation setup for matching media queries and reverts it when the query changes. It also supports `prefers-reduced-motion`, which should be used to reduce or remove nonessential motion.

See [context and cleanup](lessons/017-context-cleanup-and-reversion.md), [responsive motion](lessons/018-responsive-motion-and-reduced-motion.md), and [React](lessons/019-gsap-in-react-with-usegsap.md).

## ScrollTrigger model

ScrollTrigger measures start/end positions up front, then synchronizes updates with scrolling and animation frames. It does not continuously inspect every element's position. A basic setup:

```js
import { gsap } from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";

gsap.registerPlugin(ScrollTrigger);

gsap.from(".feature", {
  y: 32,
  autoAlpha: 0,
  duration: 0.7,
  scrollTrigger: {
    trigger: ".feature",
    start: "top 80%",
    markers: true,
  },
});
```

- `trigger` selects the element used for position calculations.
- `start` and `end` describe where trigger and scroller positions meet.
- `scrub` links playhead progress to scroll position.
- `pin` holds an element for a scroll range and may add spacing.
- `toggleActions` chooses actions at enter/leave boundaries.
- `markers` are for development and should be removed when not needed.
- Call `ScrollTrigger.refresh()` after application layout changes that invalidate measured positions.

See [ScrollTrigger fundamentals](lessons/020-scrolltrigger-fundamentals.md), [start/end/refresh](lessons/021-scrolltrigger-start-end-and-refresh.md), and [scrub/pin/snap](lessons/022-scrolltrigger-scrub-pin-and-snap.md).

## Common plugin choices

| Need | Tool |
| --- | --- |
| Scroll position controls an animation | ScrollTrigger |
| Observe wheel, touch, pointer, or drag-like gestures | Observer |
| Animate between changed DOM layouts | Flip |
| Follow an SVG or motion path | MotionPathPlugin |
| Animate the browser or element scroll position | ScrollToPlugin |
| Interpolate text content or split text for visual animation | TextPlugin or SplitText |
| Pointer-driven dragging | Draggable |

Import and register only the plugins a project uses. Check browser support, accessibility behavior, and version requirements for the exact feature. Use SplitText with care: the text must remain readable and understandable without animation.

## Performance and accessibility checklist

- Animate `transform` and `opacity` where possible, then profile real devices.
- Avoid creating duplicate tweens on every event; use `quickTo()` or a reusable timeline when it fits.
- Revert animations and remove event listeners when a component or page section is removed.
- Keep content visible and usable when JavaScript is delayed, disabled, or motion is reduced.
- Respect `prefers-reduced-motion`; avoid essential information being conveyed only through movement.
- Keep scroll interactions tied to native scrolling and avoid trapping keyboard or touch users.
- Use markers to diagnose ScrollTrigger positions, then remove development-only diagnostics.
- Recheck after fonts, images, route transitions, or dynamic content change layout.

## Troubleshooting checklist

1. Confirm the package and plugin import paths match the installed GSAP version.
2. Register each imported plugin.
3. Confirm the target exists when the tween is created and is scoped to the right component.
4. Inspect computed styles and ensure the animated property has a valid start value.
5. Check `from()` immediate rendering and timeline overlap if content flashes.
6. For scroll issues, enable markers and review `trigger`, `start`, `end`, pin spacing, and refresh timing.
7. In component frameworks, verify context cleanup and route unmount behavior.
8. Test reduced-motion preferences, keyboard operation, mobile layout, and production bundling.

## Course path

Start with [the README roadmap](README.md), then work through the chapters from foundations to the [capstone](lessons/032-capstone-animated-landing-page.md). Each chapter has its own lesson, Q&A, and example.
