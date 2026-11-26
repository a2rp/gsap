# 015 - Keyframes, modifiers, and snapping Q&A

## When should I use keyframes instead of a timeline?

Use keyframes when one target moves through a compact sequence of property states and you want one tween. Use a timeline when you need labels, callbacks, multiple targets with different schedules, or clear child control.

## Can each keyframe have its own duration?

Yes. Keyframe objects can specify durations, allowing the stages to take different amounts of time. Check the chosen keyframe syntax and easing options against the installed GSAP version.

## What is a modifier?

A modifier is a function that transforms an animated property value before it is applied. It can constrain or map rendered values, for example snapping x values to a grid.

## How is `snap` different from a modifier?

`snap` is a convenient configuration for rounding values to increments or configured points. A modifier is more general and can implement arbitrary value rules.

## Does snapping change the tween's final destination?

It changes the value rendered through the configured snapping behavior. The underlying tween configuration still describes the original destination, so inspect the visual result rather than assuming internal values are identical to display values.

## Why does my modifier produce unexpected output?

Check that the function receives the type and unit you expect, and return a compatible value. Keep modifiers deterministic and avoid expensive calculations because they can run on animation renders.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous Q&amp;A</th><th>Chapter lesson</th><th>Chapter example</th><th>Next Q&amp;A</th></tr></thead>
  <tbody><tr><td><a href="014-svg-and-attribute-animation.md">014 - SVG and attribute animation Q&amp;A</a></td><td><a href="../lessons/015-keyframes-modifiers-and-snapping.md">Lesson</a></td><td><a href="../examples/015-keyframes-modifiers-and-snapping.md">Example</a></td><td><a href="016-utilities-and-reusable-effects.md">016 - Utilities and reusable effects Q&amp;A</a></td></tr></tbody>
</table>
