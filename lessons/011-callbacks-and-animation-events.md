# 011 - Callbacks and animation events

## Learning goals

- Respond to tween and timeline lifecycle events.
- Distinguish per-frame updates from start, repeat, completion, and interruption callbacks.

## Core idea

Callbacks let application code respond to animation lifecycle events. Common callbacks include `onStart`, `onUpdate`, `onRepeat`, `onComplete`, `onReverseComplete`, and `onInterrupt`.

## How it works

Pass a function in the vars object. `onStart` runs when playback begins, `onUpdate` runs on render updates, and completion callbacks run at their respective endpoints. A repeating tween can call `onRepeat`; an infinite tween will not naturally call `onComplete`. `onInterrupt` can be useful when a tween is killed or overwritten before completion. Keep callbacks small because they may run during animation rendering.

```js
const state = { value: 0 };

gsap.to(state, {
  value: 100,
  duration: 1,
  onStart: () => console.log("started"),
  onUpdate: () => renderValue(state.value),
  onComplete: () => console.log("completed"),
});
```

Read the code from the target outward: identify the animated value, then the GSAP configuration that controls its start, destination, timing, or lifecycle. In DOM examples, make sure the selected elements exist before this module runs. In object examples, update the visible interface from the changing object value yourself.

## When to use it and its limits

Use callbacks to synchronize a small UI state with animation completion, update a display based on an object tween, or coordinate an action with a timeline. For business logic that must happen independently of motion, do not make the animation the only source of truth.

`onUpdate` may fire often and should not perform expensive DOM reads, network calls, or repeated layout work. Callback order can be affected by repeats, reversals, pauses, and interruptions. A tween can be overwritten or killed before its completion callback.

## Common mistakes

- Putting expensive calculations in `onUpdate`.
- Expecting `onComplete` to run on an infinite repeat.
- Changing application state only after an animation when that state must be available immediately.
- Calling callbacks that refer to detached DOM nodes after a component has unmounted.

## Recap and practice

Animate a numeric object and display its rounded value in `onUpdate`. Add `onStart` and `onComplete` messages, then pause, reverse, and kill the tween to observe which lifecycle events occur.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous lesson</th><th>Chapter Q&amp;A</th><th>Chapter example</th><th>Next lesson</th></tr></thead>
  <tbody><tr><td><a href="010-labels-nested-timelines-and-controls.md">010 - Labels, nested timelines, and controls</a></td><td><a href="../qnas/011-callbacks-and-animation-events.md">Q&amp;A</a></td><td><a href="../examples/011-callbacks-and-animation-events.md">Example</a></td><td><a href="012-setting-values-and-quick-methods.md">012 - Setting values and quick methods</a></td></tr></tbody>
</table>
