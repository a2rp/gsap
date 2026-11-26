# 006 - Targets and dynamic values Q&A

## Which target forms does GSAP accept?

Common choices are selector strings, a single element, arrays of targets, NodeLists, and supported objects. Use `gsap.utils.toArray()` when you want a predictable array from DOM selectors.

## What arguments does a function-based value receive?

It receives the target's index, the target itself, and the collection of targets. You can ignore unused arguments, as in `(index) => index * 20`.

## Does a function-based value run every frame?

No. GSAP evaluates it to determine a tween value when the tween first renders. It is not an `onUpdate` callback. Use `onUpdate` when you need per-frame work.

## How do I reselect elements added after the tween starts?

Create a new tween or update the target collection after those elements exist. An already-created tween does not automatically watch the DOM for new matching elements.

## How do relative values work?

A value such as `"+=20"` adds 20 to the starting value, while `"-=20"` subtracts 20. The meaning of the number and unit depends on the animated property.

## How can random values change on each repeat?

Use a random or function-based value with `repeatRefresh: true` when appropriate. This causes GSAP to invalidate and recalculate recorded values on full repeat iterations. Verify the exact behavior for the tween configuration you use.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous Q&amp;A</th><th>Chapter lesson</th><th>Chapter example</th><th>Next Q&amp;A</th></tr></thead>
  <tbody><tr><td><a href="005-timing-easing-and-repeats.md">005 - Timing, easing, and repeats Q&amp;A</a></td><td><a href="../lessons/006-targets-and-dynamic-values.md">Lesson</a></td><td><a href="../examples/006-targets-and-dynamic-values.md">Example</a></td><td><a href="007-staggers-and-distribution.md">007 - Staggers and distribution Q&amp;A</a></td></tr></tbody>
</table>
