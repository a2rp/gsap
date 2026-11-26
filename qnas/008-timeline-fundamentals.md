# 008 - Timeline fundamentals Q&A

## When should I use a timeline instead of several tweens?

Use a timeline when the animations form one ordered or overlapping sequence, need one playback control, or will be retimed together. Use separate tweens for independent reactions.

## Do timeline children start simultaneously by default?

No. Without an explicit position, each child is appended after the timeline's current end, so the default behavior is sequential.

## Does a timeline play automatically?

Yes, a new timeline plays immediately unless configured with `paused: true` or controlled by a parent animation.

## What does `defaults` do?

It supplies default tween vars for children added to the timeline. A child's own value takes precedence for the property it explicitly sets.

## What does chaining return?

Timeline methods such as `.to()` and `.from()` return the timeline, allowing additional child animations to be chained. The variable created by `gsap.timeline()` is the controllable timeline instance.

## How do I reverse a sequence?

Keep a reference to the timeline and call `reverse()`. It moves the same playhead backward, so the children play in reverse timing order.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous Q&amp;A</th><th>Chapter lesson</th><th>Chapter example</th><th>Next Q&amp;A</th></tr></thead>
  <tbody><tr><td><a href="007-staggers-and-distribution.md">007 - Staggers and distribution Q&amp;A</a></td><td><a href="../lessons/008-timeline-fundamentals.md">Lesson</a></td><td><a href="../examples/008-timeline-fundamentals.md">Example</a></td><td><a href="009-timeline-position-parameter.md">009 - Timeline position parameter Q&amp;A</a></td></tr></tbody>
</table>
