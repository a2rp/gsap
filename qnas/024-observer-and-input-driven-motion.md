# 024 - Observer and input-driven motion Q&A

## What input types can Observer monitor?

Its `type` option can include `wheel`, `touch`, `pointer`, and `scroll`. The event types can be combined in a comma-delimited string.

## What does `tolerance` do?

It sets the minimum accumulated delta required before movement callbacks fire. This filters tiny changes and can reduce accidental responses.

## What is `dragMinimum` for?

It sets the minimum initial pointer/touch movement needed to count as a drag. It helps avoid classifying small touch jitter as intentional dragging.

## Does Observer automatically stop native scrolling?

No. It observes input. Use event prevention only when the interaction deliberately requires it, and provide accessible alternatives if native behavior is interrupted.

## Do I need the standalone Observer import when ScrollTrigger is loaded?

No. ScrollTrigger includes Observer functionality and exposes it through `ScrollTrigger.observe()`. If you are already loading ScrollTrigger, that can avoid a separate Observer import.

## How do I clean up an Observer?

Keep the instance returned by `Observer.create()` and call `kill()` when its owner is removed. `disable()` is temporary if the instance may be reused later.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous Q&amp;A</th><th>Chapter lesson</th><th>Chapter example</th><th>Next Q&amp;A</th></tr></thead>
  <tbody><tr><td><a href="023-scrolltrigger-callbacks-classes-and-batch.md">023 - ScrollTrigger callbacks, classes, and batch Q&amp;A</a></td><td><a href="../lessons/024-observer-and-input-driven-motion.md">Lesson</a></td><td><a href="../examples/024-observer-and-input-driven-motion.md">Example</a></td><td><a href="025-flip-and-layout-transitions.md">025 - Flip and layout transitions Q&amp;A</a></td></tr></tbody>
</table>
