# 026 - MotionPath and path animation Q&A

## What can be used as a motion path?

MotionPathPlugin accepts an SVG path element, SVG path data string, or arrays of coordinate/property objects.

## What is the difference between `path` and `align`?

`path` defines the route. `align` maps the target to the path's coordinate space so it follows the path position correctly, even when the elements are nested or transformed.

## What does `alignOrigin` do?

It selects the point on the target that should align with the path, using normalized x/y values such as `[0.5, 0.5]` for the center.

## How does `autoRotate` work?

It rotates the target to follow the direction of the path. Use a numeric angle offset if the artwork's forward direction differs from the path tangent.

## Can MotionPath animate only x and y?

No. It can also animate arrays of other property values, such as scale and rotation. Use coordinates when the target must follow a two-dimensional route.

## Does path alignment update automatically on resize?

No. Alignment calculations occur when the animation starts. Rebuild or recalculate the animation if responsive layout changes the path geometry.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous Q&amp;A</th><th>Chapter lesson</th><th>Chapter example</th><th>Next Q&amp;A</th></tr></thead>
  <tbody><tr><td><a href="025-flip-and-layout-transitions.md">025 - Flip and layout transitions Q&amp;A</a></td><td><a href="../lessons/026-motionpath-and-path-animation.md">Lesson</a></td><td><a href="../examples/026-motionpath-and-path-animation.md">Example</a></td><td><a href="027-scrollto-and-programmatic-scrolling.md">027 - ScrollTo and programmatic scrolling Q&amp;A</a></td></tr></tbody>
</table>
