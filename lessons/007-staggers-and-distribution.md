# 007 - Staggers and distribution

## Learning goals

- Offset the start times of a tween across multiple targets.
- Use stagger configuration to control order and distribution.

## Core idea

A stagger adds a start-time offset between targets in a single tween. A numeric stagger is the gap in seconds between adjacent target starts. An object provides richer patterns such as a start point, grid, axis, amount, each, and a distribution ease.

## How it works

GSAP resolves the target collection, assigns each target a position in the stagger sequence, and schedules the same tween configuration at different offsets. `each` specifies the interval per target; `amount` spreads the sequence across an overall duration. `from` changes the origin of the distribution, and `grid` allows a two-dimensional layout to be treated as a grid.

```js
gsap.from(".tile", {
  y: 24,
  autoAlpha: 0,
  duration: 0.45,
  ease: "power2.out",
  stagger: {
    each: 0.08,
    from: "center",
    grid: "auto",
    axis: "x",
  },
});
```

Read the code from the target outward: identify the animated value, then the GSAP configuration that controls its start, destination, timing, or lifecycle. In DOM examples, make sure the selected elements exist before this module runs. In object examples, update the visible interface from the changing object value yourself.

## When to use it and its limits

Use a stagger for coordinated lists, galleries, menus, and repeated interface elements. A short stagger can make a group feel sequential while keeping its shared motion consistent. For individually different animations, use function-based values in addition to or instead of stagger.

A stagger does not create separate reusable tweens for application logic; it coordinates a multi-target tween. The order depends on the target list and, for grid patterns, the configured grid shape. Too much stagger can make a UI feel slow.

## Common mistakes

- Confusing `each` with `amount`: `each` is a gap per target; `amount` is the total span of the distribution.
- Using `grid: "auto"` on a layout whose positions are changing while the tween is initialized.
- Assuming the stagger changes property values; it primarily changes start times and can combine with function-based values.
- Applying a very long stagger to large collections without considering user wait time.

## Recap and practice

Animate a row of cards with a short numeric stagger. Change it to an object with `from: "center"`, then use a CSS grid and `grid: "auto"`. Compare the visual order and total sequence length.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous lesson</th><th>Chapter Q&amp;A</th><th>Chapter example</th><th>Next lesson</th></tr></thead>
  <tbody><tr><td><a href="006-targets-and-dynamic-values.md">006 - Targets and dynamic values</a></td><td><a href="../qnas/007-staggers-and-distribution.md">Q&amp;A</a></td><td><a href="../examples/007-staggers-and-distribution.md">Example</a></td><td><a href="008-timeline-fundamentals.md">008 - Timeline fundamentals</a></td></tr></tbody>
</table>
