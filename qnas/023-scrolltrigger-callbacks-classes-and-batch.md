# 023 - ScrollTrigger callbacks, classes, and batch Q&A

## What does `onEnter` receive?

It receives the ScrollTrigger instance. You can inspect properties such as `trigger`, `progress`, `direction`, and `isActive`.

## How is `toggleClass` different from a callback?

`toggleClass` automatically adds/removes a class while the trigger is active. A callback lets you run custom logic at a boundary. Use the simplest option that expresses the behavior.

## What is the `targets` option in `toggleClass` for?

It lets you toggle a class on elements other than the trigger itself, for example highlighting a navigation label while a section is active.

## What does `ScrollTrigger.batch()` pass to `onEnter`?

It passes an array of the elements entering within the batch interval. Animate that array as a group or apply a stagger to its members.

## Does batch make every element share one ScrollTrigger?

No. It creates coordinated triggers for the targets and batches their callbacks. It is a convenience for grouping callbacks, not a single trigger for the entire list.

## Why are my items invisible when JavaScript fails?

They may have been hidden in CSS before the enhancement ran. Keep a visible baseline in CSS, then set the animation start state from JavaScript so unsupported or delayed scripts do not hide content.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous Q&amp;A</th><th>Chapter lesson</th><th>Chapter example</th><th>Next Q&amp;A</th></tr></thead>
  <tbody><tr><td><a href="022-scrolltrigger-scrub-pin-and-snap.md">022 - ScrollTrigger scrub, pin, and snap Q&amp;A</a></td><td><a href="../lessons/023-scrolltrigger-callbacks-classes-and-batch.md">Lesson</a></td><td><a href="../examples/023-scrolltrigger-callbacks-classes-and-batch.md">Example</a></td><td><a href="024-observer-and-input-driven-motion.md">024 - Observer and input-driven motion Q&amp;A</a></td></tr></tbody>
</table>
