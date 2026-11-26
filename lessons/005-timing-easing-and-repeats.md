# 005 - Timing, easing, and repeats

## Learning goals

- Configure duration, delay, ease, repeat, repeatDelay, and yoyo.
- Calculate how repeat settings affect total playback.

## Core idea

Tween timing options control when a tween starts, how long one iteration lasts, how values change during that iteration, and whether it repeats. Duration is per iteration; repeat counts additional iterations.

## How it works

`repeat: 2` produces three iterations total. `repeatDelay` adds a pause between iterations but not after the final iteration. With `yoyo: true`, each repeated iteration reverses direction. An ease maps normalized progress onto a curve; it does not change the tween's endpoint. An infinite repeat (`-1`) has no natural completion and therefore does not reach `onComplete` unless stopped or altered.

``js
gsap.to(".dot", {
  x: 220,
  duration: 0.8,
  delay: 0.2,
  ease: "power2.inOut",
  repeat: 2,
  repeatDelay: 0.25,
  yoyo: true,
});
``

Read the code from the target outward: identify the animated value, then the GSAP configuration that controls its start, destination, timing, or lifecycle. In DOM examples, make sure the selected elements exist before this module runs. In object examples, update the visible interface from the changing object value yourself.

## When to use it and its limits

Use easing to make motion feel intentional, repeats for ambient loops or repeated feedback, and yoyo for a clear return path. For a multi-element sequence with separate pauses or directions, a timeline is usually easier to reason about than multiple independently repeating tweens.

Long or infinite motion can distract and may need a pause control or a reduced-motion alternative. Repeating values that depend on random or function-based inputs may need `repeatRefresh` to recalculate them on each iteration.

## Common mistakes

- Reading `repeat: 2` as two total plays instead of one initial play plus two repeats.
- Expecting `repeatDelay` to happen after the final iteration.
- Adding `yoyo` without a repeat and expecting it to reverse.
- Using an ease name that is not available or omitting the correct in/out suffix for the intended motion.

## Recap and practice

Calculate the duration of a tween with `duration: 0.5`, `repeat: 3`, and `repeatDelay: 0.2`. Then toggle yoyo and compare its ending position. Try a linear ease and an eased curve with the same duration.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous lesson</th><th>Chapter Q&amp;A</th><th>Chapter example</th><th>Next lesson</th></tr></thead>
  <tbody><tr><td><a href="004-gsap-from-and-fromto.md">004 - gsap.from() and gsap.fromTo()</a></td><td><a href="../qnas/005-timing-easing-and-repeats.md">Q&amp;A</a></td><td><a href="../examples/005-timing-easing-and-repeats.md">Example</a></td><td><a href="006-targets-and-dynamic-values.md">006 - Targets and dynamic values</a></td></tr></tbody>
</table>
