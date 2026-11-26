# 017 - Context, cleanup, and reversion Q&A

## What does `gsap.context()` collect?

GSAP animations and ScrollTriggers created while its callback executes, plus work created through context-safe callbacks. It can scope selector text to a supplied root.

## What does `ctx.revert()` do?

It kills collected animations and restores the inline styles that were present before those animations applied their changes. Use it when the context's owner is disposed or reset.

## Does a context remove event listeners?

No. Remove listeners, timers, observers, and application subscriptions in your own cleanup function. Context handles GSAP work.

## Why pass a scope element?

A scope makes selector text such as `".box"` resolve within the component or section rather than across the whole document. This avoids collisions when several instances use the same class names.

## What if an event handler creates an animation later?

Use a context-safe callback pattern so the new animation is associated with the correct context. In React, `@gsap/react` provides `contextSafe()` for this case.

## Can one context own infinite animations?

Yes, but they must be reverted or killed when their owner goes away. An infinite animation will not stop by completing on its own.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous Q&amp;A</th><th>Chapter lesson</th><th>Chapter example</th><th>Next Q&amp;A</th></tr></thead>
  <tbody><tr><td><a href="016-utilities-and-reusable-effects.md">016 - Utilities and reusable effects Q&amp;A</a></td><td><a href="../lessons/017-context-cleanup-and-reversion.md">Lesson</a></td><td><a href="../examples/017-context-cleanup-and-reversion.md">Example</a></td><td><a href="018-responsive-motion-and-reduced-motion.md">018 - Responsive motion and reduced motion Q&amp;A</a></td></tr></tbody>
</table>
