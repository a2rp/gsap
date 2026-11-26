# 004 - gsap.from() and gsap.fromTo() Q&A

## What is the final state for `gsap.from()`?

Unless explicitly configured otherwise, GSAP reads the target's current value as the destination. The values in the vars object are the starting values.

## Why does a `from()` tween hide my element before it starts?

`from()` commonly uses immediate rendering to apply its starting values as soon as it is created. In a timeline, set `immediateRender: false` when the start state should wait until the tween begins, and confirm that the CSS baseline is intentional.

## When is `fromTo()` preferable?

Use it when the starting and ending values both need to be explicit and deterministic. For example, use it when a component may be in different CSS states before the animation.

## Where do `duration` and `ease` go in `fromTo()`?

They belong in the third argument, the destination vars object, along with the ending property values and callback options.

## Can `from()` animate multiple elements?

Yes. It applies the starting values to each matched target and reads each target's own current values for its destination. Add `stagger` to offset their start times.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous Q&amp;A</th><th>Chapter lesson</th><th>Chapter example</th><th>Next Q&amp;A</th></tr></thead>
  <tbody><tr><td><a href="003-tweens-with-gsap-to.md">003 - Tweens with gsap.to() Q&amp;A</a></td><td><a href="../lessons/004-gsap-from-and-fromto.md">Lesson</a></td><td><a href="../examples/004-gsap-from-and-fromto.md">Example</a></td><td><a href="005-timing-easing-and-repeats.md">005 - Timing, easing, and repeats Q&amp;A</a></td></tr></tbody>
</table>
