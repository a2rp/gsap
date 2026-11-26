# 025 - Flip and layout transitions

## Learning goals

- Capture a layout before a DOM or class change and animate to the new layout.
- Use `Flip.getState()` and `Flip.from()` safely.

## Core idea

Flip animates visual transitions between two layout states. It follows the First, Last, Invert, Play pattern: capture the current state, make the DOM or style change, then animate the recorded elements into their new positions.

## How it works

Import and register `Flip`. Call `Flip.getState(targets)` before changing classes, DOM structure, or layout. Apply the state change synchronously, then pass the captured state to `Flip.from(state, vars)`. `Flip.from()` compares the recorded geometry with the current layout, temporarily applies inverse transforms, and animates those offsets away. It returns a timeline that can be controlled or extended.

```js
const state = Flip.getState(".tile");
grid.classList.toggle("is-expanded");

Flip.from(state, {
  duration: 0.6,
  ease: "power1.inOut",
  absolute: true,
  stagger: 0.04,
});
```

Read the code from the target outward: identify the animated value, then the GSAP configuration that controls its start, destination, timing, or lifecycle. In DOM examples, make sure the selected elements exist before this module runs. In object examples, update the visible interface from the changing object value yourself.

## When to use it and its limits

Use Flip for grid reordering, expanding cards, shared-element transitions, or layout changes where elements should appear to move smoothly between their old and new positions. Keep stable targets or matching `data-flip-id` values when elements are replaced.

Flip captures geometry and selected properties, not arbitrary application state. It does not accommodate 3D transforms such as `rotationX` or `rotationY`. `absolute: true` removes affected elements from document flow during the flip, so account for layout space. In-progress transitions can be affected by viewport changes.

## Common mistakes

- Applying the class or DOM change before calling `Flip.getState()`.
- Capturing too broad a set of elements, including containers whose movement compounds with child movement.
- Using `absolute: true` without checking what happens to the surrounding layout.
- Expecting Flip to animate arbitrary properties without capturing them through its `props` option.

## Recap and practice

Build a grid where the first card expands when a button is pressed. Capture state before toggling the class, then call `Flip.from()`. Add `data-flip-id` values to replace one card element with another while preserving the visual transition.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous lesson</th><th>Chapter Q&amp;A</th><th>Chapter example</th><th>Next lesson</th></tr></thead>
  <tbody><tr><td><a href="024-observer-and-input-driven-motion.md">024 - Observer and input-driven motion</a></td><td><a href="../qnas/025-flip-and-layout-transitions.md">Q&amp;A</a></td><td><a href="../examples/025-flip-and-layout-transitions.md">Example</a></td><td><a href="026-motionpath-and-path-animation.md">026 - MotionPath and path animation</a></td></tr></tbody>
</table>
