# 016 - Utilities and reusable effects

## Learning goals

- Use common `gsap.utils` methods as values or reusable functions.
- Register a named effect to reuse a tween pattern consistently.

## Core idea

GSAP utilities perform common value transformations such as clamping, mapping, snapping, wrapping, interpolation, and selecting elements. Many utilities can return a reusable function. `gsap.registerEffect()` packages an animation pattern behind a named function and optional defaults.

## How it works

For example, `gsap.utils.clamp(0, 100)` returns a function that constrains later inputs, and `gsap.utils.mapRange(0, 100, 0, 500)` returns a range mapper. `gsap.utils.pipe()` composes functions from left to right. A registered effect receives targets and a configuration object and should return a tween or timeline. With `extendTimeline: true`, the named effect can be added through a timeline method.

```js
const pointerToX = gsap.utils.pipe(
  gsap.utils.clamp(0, 100),
  gsap.utils.mapRange(0, 100, 0, 320),
  gsap.utils.snap(8)
);

console.log(pointerToX(37));

gsap.registerEffect({
  name: "fadeRise",
  defaults: { distance: 20, duration: 0.5 },
  extendTimeline: true,
  effect: (targets, config) => gsap.from(targets, {
    y: config.distance,
    autoAlpha: 0,
    duration: config.duration,
    stagger: config.stagger,
  }),
});
```

Read the code from the target outward: identify the animated value, then the GSAP configuration that controls its start, destination, timing, or lifecycle. In DOM examples, make sure the selected elements exist before this module runs. In object examples, update the visible interface from the changing object value yourself.

## When to use it and its limits

Use utilities to keep range math and reusable value rules small and testable. Register an effect when a pattern is reused across a project and its configuration deserves a stable API. Keep the effect's defaults conservative and document its accepted options.

Utilities operate on values; they do not decide application state or rendering. Effects are global to the GSAP instance and names can collide, so choose distinct names and register them once. Do not build a named effect for a one-off tween.

## Common mistakes

- Calling a utility factory repeatedly instead of reusing the returned mapper or clamper.
- Reversing the order of functions in `pipe()` and producing unexpected values.
- Registering an effect repeatedly during component rendering.
- Designing effect options with names that conflict with GSAP's standard tween vars or silently ignoring configuration.

## Recap and practice

Create a reusable pointer-range mapper with `pipe()`, `clamp()`, `mapRange()`, and `snap()`. Then register a `fadeRise` effect and use it directly and inside a timeline.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous lesson</th><th>Chapter Q&amp;A</th><th>Chapter example</th><th>Next lesson</th></tr></thead>
  <tbody><tr><td><a href="015-keyframes-modifiers-and-snapping.md">015 - Keyframes, modifiers, and snapping</a></td><td><a href="../qnas/016-utilities-and-reusable-effects.md">Q&amp;A</a></td><td><a href="../examples/016-utilities-and-reusable-effects.md">Example</a></td><td><a href="017-context-cleanup-and-reversion.md">017 - Context, cleanup, and reversion</a></td></tr></tbody>
</table>
