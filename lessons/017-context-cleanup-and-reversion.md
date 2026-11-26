# 017 - Context, cleanup, and reversion

## Learning goals

- Scope selector text and collect animations with `gsap.context()`.
- Revert animations when their owning interface is removed or reset.

## Core idea

A GSAP context groups animations and ScrollTriggers created while its callback runs. The optional scope limits selector text to descendants of a root element. Calling `revert()` kills collected animations and restores their recorded inline styles.

## How it works

Create a context around the animation setup and retain the returned context. When the component or interface is torn down, call `ctx.revert()`. A context also supports adding named functions that create animations later; those callbacks can be run through the context so their animations are collected. In React, `@gsap/react` provides `useGSAP()` and `contextSafe()` patterns, covered in the next React lesson.

``js
const ctx = gsap.context(() => {
  gsap.from(".box", {
    y: 20,
    autoAlpha: 0,
    stagger: 0.1,
    duration: 0.5,
  });
}, document.querySelector(".stage"));

// When the stage is removed or reset:
ctx.revert();
``

Read the code from the target outward: identify the animated value, then the GSAP configuration that controls its start, destination, timing, or lifecycle. In DOM examples, make sure the selected elements exist before this module runs. In object examples, update the visible interface from the changing object value yourself.

## When to use it and its limits

Use a context for component-owned or page-section-owned animation setup. It reduces selector collisions and gives cleanup one explicit owner. Reverting is useful when a modal closes, a route unmounts, a demo resets, or responsive conditions change.

A context does not remove DOM event listeners, timers, or arbitrary side effects created by your code. Clean those up separately. A context only records GSAP work created while the context is active or through its context-safe helpers.

## Common mistakes

- Creating animations in a later event callback without running that callback through the context.
- Assuming context cleanup removes listeners or application subscriptions.
- Using broad global selectors so one component animates another component's elements.
- Forgetting to call `revert()` during teardown.

## Recap and practice

Create two independent component roots that each contain an element named `.box`. Scope a context to each root and verify that each animation affects only its own box. Revert one context and leave the other running.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous lesson</th><th>Chapter Q&amp;A</th><th>Chapter example</th><th>Next lesson</th></tr></thead>
  <tbody><tr><td><a href="016-utilities-and-reusable-effects.md">016 - Utilities and reusable effects</a></td><td><a href="../qnas/017-context-cleanup-and-reversion.md">Q&amp;A</a></td><td><a href="../examples/017-context-cleanup-and-reversion.md">Example</a></td><td><a href="018-responsive-motion-and-reduced-motion.md">018 - Responsive motion and reduced motion</a></td></tr></tbody>
</table>
