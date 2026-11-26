# 003 - Tweens with gsap.to()

## Learning goals

- Create a tween from current values to destination values.
- Choose useful duration, ease, and control settings for a one-off animation.

## Core idea

`gsap.to(targets, vars)` reads the start state when the tween initializes and animates toward the values in `vars`. Its return value is a Tween instance that can be paused, reversed, or inspected.

## How it works

The target can be a selector, element, array of elements, or supported JavaScript object. The vars object combines destination properties with special settings such as `duration`, `ease`, `delay`, `onComplete`, and `paused`. For DOM targets, GSAP normalizes CSS transforms such as `x` and `rotation`. When you need to replay or reverse the tween later, keep its return value.

```js
const tween = gsap.to(".box", {
  x: 160,
  opacity: 0.5,
  duration: 0.8,
  ease: "power2.out",
  paused: true,
});

tween.play();
```

Read the code from the target outward: identify the animated value, then the GSAP configuration that controls its start, destination, timing, or lifecycle. In DOM examples, make sure the selected elements exist before this module runs. In object examples, update the visible interface from the changing object value yourself.

## When to use it and its limits

Use `to()` when CSS or application state already gives the element a meaningful start and you want to move it to a new state. It is well suited to independent interface reactions and simple property transitions. Use a timeline for a sequence with timing relationships.

The computed start value depends on when the tween initializes. If another style or animation changes the target first, the result may differ from what you expected. A `to()` tween does not define an explicit starting state, and multiple simultaneous tweens of the same properties need an intentional overwrite strategy.

## Common mistakes

- Forgetting that the destination is relative to the current value, not a hard-coded start.
- Setting a transform in CSS and then overriding it elsewhere without checking the computed result.
- Creating a new tween on every pointer event instead of reusing or retargeting one.
- Keeping a reference but never using it, which makes the code harder to read.

## Recap and practice

Animate a box to `x: 160` and `opacity: 0.5`. Change its initial CSS transform and rerun the page to see how `to()` uses the current state. Then store the tween and add a button that pauses and resumes it.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous lesson</th><th>Chapter Q&amp;A</th><th>Chapter example</th><th>Next lesson</th></tr></thead>
  <tbody><tr><td><a href="002-installation-and-project-setup.md">002 - Installation and project setup</a></td><td><a href="../qnas/003-tweens-with-gsap-to.md">Q&amp;A</a></td><td><a href="../examples/003-tweens-with-gsap-to.md">Example</a></td><td><a href="004-gsap-from-and-fromto.md">004 - gsap.from() and gsap.fromTo()</a></td></tr></tbody>
</table>
