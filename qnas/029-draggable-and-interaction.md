# 029 - Draggable and interaction Q&A

## What does Draggable do?

It attaches pointer and touch dragging behavior to an element and can update transform position or rotation while exposing bounds, callbacks, snapping, and instance controls.

## How do I limit movement to one axis?

Set the `type` option to `x` or `y` for transform movement on that axis, or use the corresponding positional property option when appropriate.

## What is the difference between snap and liveSnap?

`liveSnap` constrains values while dragging. `snap` adjusts the destination after release.

## How can I keep a drag within a container?

Pass the container as `bounds` so Draggable calculates the allowed movement region.

## Does Draggable automatically make a custom widget keyboard accessible?

No. Add keyboard behavior and semantics or provide an equivalent native control, such as a range input for a slider-like interaction.

## What is required for inertia after release?

InertiaPlugin must be loaded and registered along with Draggable, and the Draggable configuration must enable inertia.

## How can a horizontal drag preserve vertical touch scrolling?

Configure the interaction and CSS so horizontal gestures are handled by the drag while vertical gestures remain available to native page scrolling.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous Q&amp;A</th><th>Chapter lesson</th><th>Chapter example</th><th>Next Q&amp;A</th></tr></thead>
  <tbody><tr><td><a href="028-textplugin-and-splittext.md">028 - TextPlugin and SplitText Q&amp;A</a></td><td><a href="../lessons/029-draggable-and-interaction.md">Lesson</a></td><td><a href="../examples/029-draggable-and-interaction.md">Example</a></td><td><a href="030-performance-and-debugging.md">030 - Performance and debugging Q&amp;A</a></td></tr></tbody>
</table>
