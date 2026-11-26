# 009 - Timeline position parameter

## Learning goals

- Place timeline children at absolute times, labels, and relative positions.
- Read the difference between `"<"`, `">"`, and relative offsets.

## Core idea

The optional final position argument on timeline methods decides where a child is placed. Without it, the child is appended at the timeline's end. With it, sequences can overlap precisely without hard-coding every child's delay.

## How it works

A number is an absolute time from the start of the timeline. A label names a time. `"<"` points to the start of the previous child animation and `">"` to its end. A string such as `"-=0.2"` or `"+=0.4"` offsets from the current end of the timeline. Label-relative positions such as `"intro+=0.2"` place a child relative to a named point.

```js
const tl = gsap.timeline({ paused: true });

tl.to(".one", { x: 120, duration: 1 }, 0)
  .to(".two", { x: 120, duration: 0.7 }, "<")
  .to(".three", { x: 120, duration: 0.5 }, "-=0.2");
```

Read the code from the target outward: identify the animated value, then the GSAP configuration that controls its start, destination, timing, or lifecycle. In DOM examples, make sure the selected elements exist before this module runs. In object examples, update the visible interface from the changing object value yourself.

## When to use it and its limits

Use positions to make small, intentional overlaps and gaps. Prefer labels for meaningful beats such as `"headline"` or `"details"`, especially when more than a few children are involved. Keep a timeline readable by using consistent formatting and avoiding unexplained negative offsets.

The previous-child shorthands refer to the most recently added animation, not necessarily the timeline's current end. Relative offsets can be confusing if durations change. A position string referencing a label can create that label if it does not already exist, so spelling mistakes may silently create a new position.

## Common mistakes

- Treating `"<"` as the beginning of the timeline rather than the start of the prior child.
- Using `"-=0.2"` and assuming it overlaps with a particular tween when intervening children changed the current end.
- Using bare numeric positions as if they were relative offsets; `2` is an absolute time in seconds.
- Misspelling labels and creating an unintended new label position.

## Recap and practice

Create a three-tween timeline where the second begins at the first tween's start, and the third overlaps the current end by 0.2 seconds. Replace the numeric overlap with a label-relative position and compare how easy each version is to edit.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous lesson</th><th>Chapter Q&amp;A</th><th>Chapter example</th><th>Next lesson</th></tr></thead>
  <tbody><tr><td><a href="008-timeline-fundamentals.md">008 - Timeline fundamentals</a></td><td><a href="../qnas/009-timeline-position-parameter.md">Q&amp;A</a></td><td><a href="../examples/009-timeline-position-parameter.md">Example</a></td><td><a href="010-labels-nested-timelines-and-controls.md">010 - Labels, nested timelines, and controls</a></td></tr></tbody>
</table>
