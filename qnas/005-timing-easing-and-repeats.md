# 005 - Timing, easing, and repeats Q&A

## How many iterations does `repeat: 1` play?

Two: the initial iteration plus one repeat. A `repeat` value counts additional iterations.

## Is `repeatDelay` included after the last play?

No. It is the gap between iterations, so three iterations have two repeat-delay gaps.

## Does `yoyo: true` reverse a tween on its own?

No. Yoyo reverses alternating repeat iterations, so set a positive repeat count or `repeat: -1` as well.

## How do I estimate total time for a finite tween?

For a tween with `n` total iterations and repeat delay `d`, a basic estimate is `duration * n + d * (n - 1)`, plus any initial delay. This excludes effects from nesting, parent timelines, and time scaling.

## What is the difference between `power2.in` and `power2.out`?

They use the same general power curve with different directions. `in` starts more gradually and accelerates; `out` starts quickly and settles. `inOut` eases at both ends.

## Why does `onComplete` never run on my loop?

An infinite repeat has no completion point. Use `onRepeat` for iteration notifications, or stop/reconfigure the tween when the loop should end.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous Q&amp;A</th><th>Chapter lesson</th><th>Chapter example</th><th>Next Q&amp;A</th></tr></thead>
  <tbody><tr><td><a href="004-gsap-from-and-fromto.md">004 - gsap.from() and gsap.fromTo() Q&amp;A</a></td><td><a href="../lessons/005-timing-easing-and-repeats.md">Lesson</a></td><td><a href="../examples/005-timing-easing-and-repeats.md">Example</a></td><td><a href="006-targets-and-dynamic-values.md">006 - Targets and dynamic values Q&amp;A</a></td></tr></tbody>
</table>
