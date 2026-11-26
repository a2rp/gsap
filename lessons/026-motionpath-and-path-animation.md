# 026 - MotionPath and path animation

## Learning goals

- Animate an element along SVG path data or coordinate points.
- Use alignment, origin, auto-rotation, and path progress options.

## Core idea

MotionPathPlugin animates a target along an SVG path, raw SVG path data, or an array of coordinates. It can align the target to the path coordinate space and rotate it to follow the path's direction.

## How it works

Import and register MotionPathPlugin. Pass a path to `motionPath`, optionally using `align` and `alignOrigin` to map the path's coordinate system to the target. `autoRotate: true` turns the target along the tangent of the path. `start` and `end` select progress positions along the path. Path alignment calculations happen when the tween initializes.

``js
gsap.to(".ship", {
  duration: 3,
  ease: "power1.inOut",
  motionPath: {
    path: "#route",
    align: "#route",
    alignOrigin: [0.5, 0.5],
    autoRotate: true,
  },
});
``

Read the code from the target outward: identify the animated value, then the GSAP configuration that controls its start, destination, timing, or lifecycle. In DOM examples, make sure the selected elements exist before this module runs. In object examples, update the visible interface from the changing object value yourself.

## When to use it and its limits

Use MotionPath for a moving marker, decorative illustration, diagram flow, or other motion that must follow a designed curve. Keep the path and target coordinate systems understandable. A visual path in SVG can be adjusted by a designer while the animation configuration stays in JavaScript.

Alignment is calculated at the start of the animation and is not automatically recalculated when a responsive resize changes the path layout. If the geometry changes, rebuild the animation while preserving progress as needed. `autoRotate` depends on orientation; offset it when the artwork's forward direction is not aligned with the path tangent.

## Common mistakes

- Forgetting to register MotionPathPlugin.
- Aligning the target's top-left instead of its center when that causes a visible offset.
- Assuming `align` is responsive to viewport changes.
- Using `autoRotate` without checking the target artwork's default orientation.

## Recap and practice

Animate a small arrow along an SVG curve with `alignOrigin: [0.5, 0.5]` and `autoRotate: true`. Offset its rotation if the arrow points sideways by default. Resize the stage and decide whether to recreate the tween.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous lesson</th><th>Chapter Q&amp;A</th><th>Chapter example</th><th>Next lesson</th></tr></thead>
  <tbody><tr><td><a href="025-flip-and-layout-transitions.md">025 - Flip and layout transitions</a></td><td><a href="../qnas/026-motionpath-and-path-animation.md">Q&amp;A</a></td><td><a href="../examples/026-motionpath-and-path-animation.md">Example</a></td><td><a href="027-scrollto-and-programmatic-scrolling.md">027 - ScrollTo and programmatic scrolling</a></td></tr></tbody>
</table>
