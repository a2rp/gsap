# 008 - Timeline fundamentals

## Learning goals

- Create a timeline and add tweens in sequence.
- Use timeline defaults and control a group with one playhead.

## Core idea

A timeline is a sequencing container for tweens, callbacks, and nested timelines. By default, each child is added at the end of the existing timeline, so chained calls play one after another.

## How it works

`gsap.timeline()` returns a Timeline instance. Its `.to()`, `.from()`, and `.fromTo()` methods add child tweens and return the timeline, which enables chaining. Timeline `defaults` are inherited by child tweens unless a child overrides them. A parent playhead controls the position of its children, so the whole sequence can be paused, reversed, repeated, or scrubbed as one unit.

``js
const intro = gsap.timeline({
  defaults: { duration: 0.45, ease: "power2.out" },
  paused: true,
});

intro
  .from(".eyebrow", { y: 12, autoAlpha: 0 })
  .from(".title", { y: 24, autoAlpha: 0 })
  .from(".action", { scale: 0.9, autoAlpha: 0 });

intro.play();
``

Read the code from the target outward: identify the animated value, then the GSAP configuration that controls its start, destination, timing, or lifecycle. In DOM examples, make sure the selected elements exist before this module runs. In object examples, update the visible interface from the changing object value yourself.

## When to use it and its limits

Use a timeline for a coordinated entrance, a multi-step interaction, or any group of animations whose order may change during design. Keep independent reactions separate if they do not share timing or lifecycle.

A timeline does not automatically make every animation inside it semantically related. Overusing one giant timeline can make event-driven interface code difficult to maintain. Child durations and positions determine the total timeline duration.

## Common mistakes

- Creating separate tweens with delays when one timeline would make sequence edits safer.
- Forgetting that a timeline plays immediately unless it is created paused.
- Expecting a timeline's `defaults` to override a child's explicit setting.
- Adding a child to a timeline after the timeline has already completed without resetting or replaying it.

## Recap and practice

Build a three-step heading entrance with `.from()` calls. Pause the timeline, add a Play button, and then reverse it. Change one child's `duration` to see how local overrides interact with timeline defaults.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous lesson</th><th>Chapter Q&amp;A</th><th>Chapter example</th><th>Next lesson</th></tr></thead>
  <tbody><tr><td><a href="007-staggers-and-distribution.md">007 - Staggers and distribution</a></td><td><a href="../qnas/008-timeline-fundamentals.md">Q&amp;A</a></td><td><a href="../examples/008-timeline-fundamentals.md">Example</a></td><td><a href="009-timeline-position-parameter.md">009 - Timeline position parameter</a></td></tr></tbody>
</table>
