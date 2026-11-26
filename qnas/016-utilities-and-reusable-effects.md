# 016 - Utilities and reusable effects Q&A

## Do utilities return values or functions?

It depends on the call. Some methods accept a value immediately, while others return a reusable function when the final value argument is omitted. Read the method signature and store the returned function if it will be used repeatedly.

## What does `gsap.utils.pipe()` do?

It passes a value through a sequence of functions in order. For example, clamp first, then map to a new range, then snap the mapped result.

## What is the difference between `wrap()` and `wrapYoyo()`?

`wrap()` cycles back to the start after reaching the end. `wrapYoyo()` alternates direction at the boundaries.

## When is `registerEffect()` useful?

Use it for a repeated animation pattern with a meaningful name and configurable defaults. A small one-off tween does not need an effect wrapper.

## What does `extendTimeline: true` enable?

It adds the effect as a method on timelines, so you can insert that reusable effect into a timeline sequence.

## Where should I register an effect?

Register it once in a shared animation setup module, not repeatedly during component rendering. Keep its name unique and ensure the setup module runs before the effect is used.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous Q&amp;A</th><th>Chapter lesson</th><th>Chapter example</th><th>Next Q&amp;A</th></tr></thead>
  <tbody><tr><td><a href="015-keyframes-modifiers-and-snapping.md">015 - Keyframes, modifiers, and snapping Q&amp;A</a></td><td><a href="../lessons/016-utilities-and-reusable-effects.md">Lesson</a></td><td><a href="../examples/016-utilities-and-reusable-effects.md">Example</a></td><td><a href="017-context-cleanup-and-reversion.md">017 - Context, cleanup, and reversion Q&amp;A</a></td></tr></tbody>
</table>
