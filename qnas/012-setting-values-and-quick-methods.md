# 012 - Setting values and quick methods Q&A

## What is the difference between `gsap.set()` and `gsap.to()` with zero duration?

They can produce the same immediate property result. `gsap.set()` expresses the intent more clearly when you want to establish a state without describing an animated change.

## Does `gsap.delayedCall()` use milliseconds?

No. Its delay is in seconds, like GSAP's other timing values.

## When should I use `quickTo()`?

Use it when a property receives frequent new destinations but should ease toward them smoothly, such as a pointer follower. It reuses a tween instead of creating one per event.

## When should I use `quickSetter()`?

Use it when many direct writes to one property are required and you do not need tweened catch-up. It is useful for performance-sensitive updates when your own code handles smoothing.

## Can I cancel a delayed call?

Yes. Keep its returned animation reference and control or kill it as needed. Also remove the event or lifecycle source that would schedule it again.

## Does `quickTo()` immediately jump to the new destination?

No. It retargets a reusable tween and animates toward the new value according to its vars. Set `duration: 0` only if immediate changes are actually intended.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous Q&amp;A</th><th>Chapter lesson</th><th>Chapter example</th><th>Next Q&amp;A</th></tr></thead>
  <tbody><tr><td><a href="011-callbacks-and-animation-events.md">011 - Callbacks and animation events Q&amp;A</a></td><td><a href="../lessons/012-setting-values-and-quick-methods.md">Lesson</a></td><td><a href="../examples/012-setting-values-and-quick-methods.md">Example</a></td><td><a href="013-css-properties-and-transforms.md">013 - CSS properties and transforms Q&amp;A</a></td></tr></tbody>
</table>
