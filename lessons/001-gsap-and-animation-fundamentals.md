# 001 - GSAP and Animation Fundamentals

## Learning goals

After this lesson, you should be able to explain what GSAP animates, distinguish a tween from a timeline, and describe how a browser animation progresses from a starting value to an ending value.

## What GSAP is

GSAP is a JavaScript animation platform. It updates values over time and can target DOM elements, SVG elements, and ordinary JavaScript objects. For DOM elements, its CSSPlugin handles common CSS properties and transforms. A tween describes a property change; a timeline sequences and controls multiple animations.

GSAP 3 is the modern API used throughout this course. The examples assume an ES module project and a GSAP version that supports the API shown. Always check the installed package when working with a different version.

## The animation model

A simple tween has four parts:

1. A target, such as a DOM element or object.
2. A starting value, read from the target unless specified explicitly.
3. A destination value.
4. A duration and optional timing configuration.

GSAP's animation engine advances a playhead and renders interpolated values in sync with browser animation frames. For example, if `x` starts at `0` and ends at `120`, the tween calculates intermediate values while it runs. An ease changes how progress is distributed across time; it does not change the destination.

```js
import { gsap } from "gsap";

const box = document.querySelector(".box");

gsap.to(box, {
  x: 120,
  rotation: 8,
  duration: 0.7,
  ease: "power2.out",
});
```

With a DOM target, `x` is a GSAP transform alias, so this animates translation without manually constructing a CSS `transform` string. The tween starts immediately by default and ends after 0.7 seconds, unless it is delayed, paused, or placed in a paused timeline.

A basic tween is not the same as a timeline. A tween describes one animation; a timeline is a container for ordering and controlling multiple tweens. Use a tween for a single independent change. Use a timeline when parts must overlap, wait, repeat together, or be controlled as one sequence.

## GSAP can animate ordinary objects

The animation engine is not restricted to HTML. This is useful for counters, game state, drawing libraries, and custom renderers:

```js
const state = { progress: 0 };

gsap.to(state, {
  progress: 1,
  duration: 1,
  onUpdate: () => {
    console.log(state.progress.toFixed(2));
  },
});
```

The object value changes over time. GSAP does not decide how that value is displayed; `onUpdate` or another rendering system must use it.

## Choosing animation intentionally

Animation should communicate a state change, hierarchy, or relationship. Small, purposeful movement is usually easier to follow than animating every element. Prefer animating `transform` and `opacity` for frequent motion, and profile the result instead of assuming every property has the same rendering cost.

The browser still performs layout, paint, and compositing work as needed. GSAP does not make an expensive visual effect free, nor does it automatically make a design accessible. Later lessons cover performance and reduced-motion handling.

## Common mistakes

- Passing a selector that matches no element. Check that the markup exists before creating the tween.
- Expecting a JavaScript object to update the page by itself. Connect object values to a render step.
- Using multiple delayed tweens for a sequence that would be clearer as a timeline.
- Assuming an ease changes the final value. It changes the path through time.
- Treating animation as essential content. A user should still understand the interface when motion is reduced or unavailable.

## Recap and practice

GSAP interpolates values over time. A tween animates a target; a timeline organizes multiple animations. Try animating one box's `x`, `rotation`, and `opacity`, then change only the duration and ease. Observe what changes and what stays the same.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous lesson</th><th>Chapter Q&amp;A</th><th>Chapter example</th><th>Next lesson</th></tr></thead>
  <tbody><tr><td>Start of course</td><td><a href="../qnas/001-gsap-and-animation-fundamentals.md">Q&amp;A</a></td><td><a href="../examples/001-gsap-and-animation-fundamentals.md">Example</a></td><td><a href="002-installation-and-project-setup.md">002 - Installation and project setup</a></td></tr></tbody>
</table>
