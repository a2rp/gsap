# 006 - Targets and dynamic values

## Learning goals

- Select targets with selectors or element references.
- Use function-based, relative, and random values appropriately.

## Core idea

GSAP accepts selector text, a DOM element, arrays, NodeLists, and supported JavaScript objects as targets. A function-based value can compute a different property value for each target; GSAP calls it with the target index, the target, and the target collection.

## How it works

Selector strings are resolved to matching elements when the tween initializes. Function-based values are evaluated for each target on the first render, which lets a set of elements share one tween configuration while receiving different destinations. Relative strings such as `"+=24"` offset a current value. Random strings and `gsap.utils.random()` are useful for varied effects, but random output should not replace meaningful design.

```js
const items = gsap.utils.toArray(".item");

gsap.to(items, {
  x: (index, target, targets) => 40 + index * 24,
  rotation: (index) => (index % 2 === 0 ? 4 : -4),
  duration: 0.6,
  ease: "power2.out",
});
```

Read the code from the target outward: identify the animated value, then the GSAP configuration that controls its start, destination, timing, or lifecycle. In DOM examples, make sure the selected elements exist before this module runs. In object examples, update the visible interface from the changing object value yourself.

## When to use it and its limits

Use a selector for stable simple markup, an element reference when the caller already has a node, and an array when targets are assembled in application code. Use function-based values for index-based or target-specific calculations. Keep calculations deterministic when an animation must be reproducible.

A selector that matches nothing has no visible effect. Function-based values are not recalculated on every frame; they produce tween endpoints. For new values on repeated iterations, see `repeatRefresh`. Dynamically added DOM elements are not automatically added to an existing tween.

## Common mistakes

- Selecting a parent element when the animation should target its children.
- Assuming a function-based value receives only the target; it receives index, target, and target array.
- Expecting a new function result on every repeat without configuring recalculation.
- Passing a live application collection that changes unexpectedly while creating the tween.

## Recap and practice

Animate a list so each item travels a distance based on its index. Replace the selector with an array of element references. Then use `gsap.utils.random()` once to choose a destination and confirm it remains fixed for that tween.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous lesson</th><th>Chapter Q&amp;A</th><th>Chapter example</th><th>Next lesson</th></tr></thead>
  <tbody><tr><td><a href="005-timing-easing-and-repeats.md">005 - Timing, easing, and repeats</a></td><td><a href="../qnas/006-targets-and-dynamic-values.md">Q&amp;A</a></td><td><a href="../examples/006-targets-and-dynamic-values.md">Example</a></td><td><a href="007-staggers-and-distribution.md">007 - Staggers and distribution</a></td></tr></tbody>
</table>
