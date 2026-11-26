# 025 - Flip and layout transitions Q&A

## What order should a Flip transition follow?

Capture the current layout with `Flip.getState()`, make the DOM or style change, and then call `Flip.from(state, options)` to animate from the captured state to the new one.

## Why must `getState()` run before the class change?

Flip needs the original geometry to compare with the new layout. If you capture after the change, it has no record of the prior positions and sizes.

## What does `absolute: true` do?

It temporarily positions affected targets absolutely during the flip. This can help with grid and flex layouts, but removes those elements from document flow during the transition.

## How can Flip transition between different DOM elements?

Use matching `data-flip-id` attributes so Flip can correlate the element in the old state with its replacement in the new state. `fade: true` can crossfade swapped elements.

## Can Flip animate CSS colors too?

It captures geometry and selected state by default. Use the `props` option in `Flip.getState()` to capture additional CSS properties, then let Flip animate those captured values.

## Does Flip support 3D transforms?

The documented Flip calculations do not accommodate 3D transforms such as `rotationX`, `rotationY`, or z. Keep the layout transition two-dimensional or use a different animation approach.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous Q&amp;A</th><th>Chapter lesson</th><th>Chapter example</th><th>Next Q&amp;A</th></tr></thead>
  <tbody><tr><td><a href="024-observer-and-input-driven-motion.md">024 - Observer and input-driven motion Q&amp;A</a></td><td><a href="../lessons/025-flip-and-layout-transitions.md">Lesson</a></td><td><a href="../examples/025-flip-and-layout-transitions.md">Example</a></td><td><a href="026-motionpath-and-path-animation.md">026 - MotionPath and path animation Q&amp;A</a></td></tr></tbody>
</table>
