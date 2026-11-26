# 012 - Setting values and quick methods

## Learning goals

- Use `gsap.set()` for immediate state and `gsap.delayedCall()` for a scheduled callback.
- Choose `quickTo()` or `quickSetter()` for repeated input updates.

## Core idea

`gsap.set()` applies values immediately. `gsap.delayedCall()` schedules a callback through the GSAP timing engine. `quickTo()` creates a reusable tweened setter, while `quickSetter()` creates a fast direct setter for a property.

## How it works

`gsap.set(target, vars)` is effectively a zero-duration tween with a clear API name. `gsap.delayedCall(delay, callback)` returns a tween-like animation that can be controlled or killed. `gsap.quickTo(target, property, vars)` returns a function; call it with new values to retarget the same tween. `gsap.quickSetter(target, property, unit)` returns a function that writes a value directly, with no smoothing tween.

``js
gsap.set(".dot", { x: 0, y: 0, scale: 0.8 });

const moveX = gsap.quickTo(".dot", "x", { duration: 0.25, ease: "power3.out" });
const moveY = gsap.quickTo(".dot", "y", { duration: 0.25, ease: "power3.out" });

gsap.delayedCall(1, () => console.log("One second elapsed"));
``

Read the code from the target outward: identify the animated value, then the GSAP configuration that controls its start, destination, timing, or lifecycle. In DOM examples, make sure the selected elements exist before this module runs. In object examples, update the visible interface from the changing object value yourself.

## When to use it and its limits

Use `set()` to prepare an initial pose or place a property at a known state. Use `delayedCall()` when animation timing should share GSAP's control methods. Choose `quickTo()` for smooth pointer-following or frequently changing destinations; choose `quickSetter()` when direct updates are needed and your code already handles smoothing.

A direct setter changes the property immediately and can look abrupt. A `quickTo()` duration determines how quickly it catches up, so repeated input can keep the target behind the pointer. Clean up event listeners that call these functions when their element or component is removed.

## Common mistakes

- Using `quickSetter()` when the effect needs smoothing and then wondering why movement is abrupt.
- Creating a fresh tween for every pointer event instead of retargeting one with `quickTo()`.
- Calling a delayed callback after its target UI has been removed.
- Forgetting that `gsap.set()` values remain as inline styles until overwritten or reverted.

## Recap and practice

Build a pointer follower using one `quickTo()` function for x and y. Compare with `quickSetter()` and add a small duration to the quickTo target. Remove the event listener when the demo component is disposed.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous lesson</th><th>Chapter Q&amp;A</th><th>Chapter example</th><th>Next lesson</th></tr></thead>
  <tbody><tr><td><a href="011-callbacks-and-animation-events.md">011 - Callbacks and animation events</a></td><td><a href="../qnas/012-setting-values-and-quick-methods.md">Q&amp;A</a></td><td><a href="../examples/012-setting-values-and-quick-methods.md">Example</a></td><td><a href="013-css-properties-and-transforms.md">013 - CSS properties and transforms</a></td></tr></tbody>
</table>
