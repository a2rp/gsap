# 003 - Tweens with gsap.to() Q&A

## Does `gsap.to()` always start from zero?

No. It reads the target's current value when the tween initializes. If the target is already translated, scaled, or partly transparent, the animation starts from that state.

## What does `gsap.to()` return?

It returns a Tween instance. Store it when you need to control, inspect, reverse, or kill the animation later. If the tween is a simple fire-and-forget effect, you do not need a variable.

## Can one `gsap.to()` target several elements?

Yes. A selector that matches several elements or an array of element references animates each target. Use `stagger` when their starts should be offset rather than simultaneous.

## Why does the tween jump when it starts?

A jump often means the rendered starting value differs from the value you expected, or a competing style/tween writes to the same property. Inspect computed styles and simplify to one tween while debugging.

## When should I use `fromTo()` instead?

Use `fromTo()` when both the initial and final values must be explicit. Use `to()` when the current rendered state should determine the start.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous Q&amp;A</th><th>Chapter lesson</th><th>Chapter example</th><th>Next Q&amp;A</th></tr></thead>
  <tbody><tr><td><a href="002-installation-and-project-setup.md">002 - Installation and project setup Q&amp;A</a></td><td><a href="../lessons/003-tweens-with-gsap-to.md">Lesson</a></td><td><a href="../examples/003-tweens-with-gsap-to.md">Example</a></td><td><a href="004-gsap-from-and-fromto.md">004 - gsap.from() and gsap.fromTo() Q&amp;A</a></td></tr></tbody>
</table>
