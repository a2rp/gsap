# 015 - Keyframes, modifiers, and snapping

## Learning goals

- Represent several states in a keyframes tween.
- Use modifiers and snapping to constrain animated values.

## Core idea

Keyframes define multiple property states inside one tween. Modifiers transform values as they are applied, while snapping rounds or constrains values to a set of increments or points.

## How it works

A `keyframes` array contains successive sets of vars; each may define its own duration. The parent tween can supply common options. A `modifiers` function receives a value and returns the value GSAP should apply, which can wrap, clamp, or quantize it. `snap` is a convenient way to round selected properties or values to configured increments.

``js
gsap.to(".box", {
  keyframes: [
    { x: 100, duration: 0.6 },
    { x: 100, y: -36, duration: 0.4 },
    { x: 0, y: 0, duration: 0.6 },
  ],
  ease: "power1.inOut",
  modifiers: {
    x: gsap.utils.snap(10),
  },
});
``

Read the code from the target outward: identify the animated value, then the GSAP configuration that controls its start, destination, timing, or lifecycle. In DOM examples, make sure the selected elements exist before this module runs. In object examples, update the visible interface from the changing object value yourself.

## When to use it and its limits

Use keyframes for one target's multi-state motion when one playhead and one tween instance are convenient. Use a timeline when named beats, callbacks, labels, or complex overlaps need to remain explicit. Use a modifier when a value must obey a rule on every render; use snapping for grid-like or stepped values.

Keyframe durations and eases affect how segments join. A modifier changes rendered values and can create discontinuities if its rule is not smooth. Snapping can make a motion look jerky when the increment is too large or the duration is too short.

## Common mistakes

- Treating keyframes as a timeline with independently named children; a timeline may be clearer when the sequence needs labels or callbacks.
- Returning a string from a modifier for a property that expects a number or incompatible unit.
- Snapping a high-frequency motion too coarsely.
- Forgetting that a modifier can alter the visible output without changing the conceptual destination stored elsewhere.

## Recap and practice

Create a three-stage keyframe path for a box. Add a modifier that rounds x to 10-pixel increments, then change the increment to 2 and compare. Replace the keyframes with a timeline and decide which structure communicates the sequence better.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous lesson</th><th>Chapter Q&amp;A</th><th>Chapter example</th><th>Next lesson</th></tr></thead>
  <tbody><tr><td><a href="014-svg-and-attribute-animation.md">014 - SVG and attribute animation</a></td><td><a href="../qnas/015-keyframes-modifiers-and-snapping.md">Q&amp;A</a></td><td><a href="../examples/015-keyframes-modifiers-and-snapping.md">Example</a></td><td><a href="016-utilities-and-reusable-effects.md">016 - Utilities and reusable effects</a></td></tr></tbody>
</table>
