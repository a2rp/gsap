# 011 - Callbacks and animation events Q&A

## How often can `onUpdate` run?

It runs when the animation renders, typically once per animation frame while the tween is active. Do not assume a fixed number of calls or use it for expensive work.

## When does `onComplete` run for a repeating tween?

After the final iteration of a finite repeat. A tween with `repeat: -1` has no natural final iteration, so it does not complete on its own.

## What is `onInterrupt` for?

It notifies you when a tween is interrupted before normal completion, such as when it is killed or overwritten. Use it for cleanup or diagnostics, not as a substitute for normal state management.

## Does reversing trigger `onComplete` again?

Reverse playback has its own endpoint behavior, including `onReverseComplete` when the playhead reaches the beginning. The callback sequence depends on the current direction and the animation state.

## Can I pass arguments to a callback?

Yes. Callback parameter options exist, but closures are often clearer for simple cases. Be careful not to call the function while configuring it; pass a function reference or arrow function.

## Should callbacks update application state?

They can synchronize presentation with a completed transition, but core state should not depend solely on an animation finishing. The animation can be interrupted, skipped for reduced motion, or removed with its component.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous Q&amp;A</th><th>Chapter lesson</th><th>Chapter example</th><th>Next Q&amp;A</th></tr></thead>
  <tbody><tr><td><a href="010-labels-nested-timelines-and-controls.md">010 - Labels, nested timelines, and controls Q&amp;A</a></td><td><a href="../lessons/011-callbacks-and-animation-events.md">Lesson</a></td><td><a href="../examples/011-callbacks-and-animation-events.md">Example</a></td><td><a href="012-setting-values-and-quick-methods.md">012 - Setting values and quick methods Q&amp;A</a></td></tr></tbody>
</table>
