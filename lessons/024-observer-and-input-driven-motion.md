# 024 - Observer and input-driven motion

## Learning goals

- Create an Observer for wheel, touch, pointer, and scroll-like input.
- Configure callbacks and thresholds without unnecessarily disabling native interaction.

## Core idea

Observer normalizes input events into callbacks such as `onUp`, `onDown`, `onDrag`, and `onChange`. It can combine wheel, touch, pointer, and scroll inputs so an interaction does not need separate low-level handlers for each device.

## How it works

Import and register `Observer`, then call `Observer.create()` with a target, event `type`, and callbacks. Observer accumulates movement deltas and debounces them by default for frame-synchronized processing. `tolerance` sets a minimum movement threshold, while `dragMinimum` filters tiny initial pointer/touch movement before treating it as a drag. The Observer instance can be disabled, enabled, or killed.

``js
const observer = Observer.create({
  target: ".gesture-area",
  type: "wheel,touch,pointer",
  tolerance: 18,
  onUp: () => showDirection("up"),
  onDown: () => showDirection("down"),
});

// When the owning area is removed:
observer.kill();
``

Read the code from the target outward: identify the animated value, then the GSAP configuration that controls its start, destination, timing, or lifecycle. In DOM examples, make sure the selected elements exist before this module runs. In object examples, update the visible interface from the changing object value yourself.

## When to use it and its limits

Use Observer for gesture-driven controls, directional navigation, or custom input logic that genuinely needs normalized deltas. If ScrollTrigger is already loaded, its `ScrollTrigger.observe()` method exposes the same Observer capability. Keep ordinary page scrolling native unless the interaction has a strong reason to intercept it.

Observer reports input; it does not create a complete accessible interaction model. A swipe-only control needs keyboard and visible button alternatives. Preventing default events can interfere with browser scrolling and touch behavior.

## Common mistakes

- Setting `preventDefault: true` globally and unintentionally blocking native scrolling.
- Treating wheel and touch deltas as identical magnitudes.
- Failing to kill the Observer when its target section is disposed.
- Building a full-page interaction that works only with gestures and has no keyboard controls.

## Recap and practice

Observe wheel and touch movement over a bounded interaction panel. Update a status label for up/down callbacks. Add equivalent Previous and Next buttons so the same action is available without a gesture.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous lesson</th><th>Chapter Q&amp;A</th><th>Chapter example</th><th>Next lesson</th></tr></thead>
  <tbody><tr><td><a href="023-scrolltrigger-callbacks-classes-and-batch.md">023 - ScrollTrigger callbacks, classes, and batch</a></td><td><a href="../qnas/024-observer-and-input-driven-motion.md">Q&amp;A</a></td><td><a href="../examples/024-observer-and-input-driven-motion.md">Example</a></td><td><a href="025-flip-and-layout-transitions.md">025 - Flip and layout transitions</a></td></tr></tbody>
</table>
