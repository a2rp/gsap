# 001 - GSAP and Animation Fundamentals Q&A

## 1. What does GSAP animate?

GSAP can animate DOM elements, SVG elements, and ordinary JavaScript objects. With DOM elements, its CSSPlugin handles CSS properties and transforms. With a plain object, GSAP changes its properties; your code must use those values to update a canvas, chart, or other renderer.

## 2. What is the difference between a tween and a timeline?

A tween describes a change in one or more properties of a target over time. A timeline is a container that orders tweens and other timelines, including overlaps and gaps. A single independent change usually needs only a tween; a sequence is easier to maintain as a timeline.

## 3. How does GSAP know the starting value?

A `gsap.to()` tween reads the target's current value when it initializes, unless you use an explicit-start API or other configuration. For CSS properties, that value comes from the element's styles. For a plain object, it comes from the object's property. If the current value is not what you expect, inspect the computed style or object state before creating the tween.

## 4. Does `duration: 1` mean one second?

Yes. GSAP durations and delays are expressed in seconds. A `duration` of `1` means one second for a normal iteration. Repeats and repeat delays affect total elapsed time.

## 5. Does an ease change the final value?

No. An ease changes how the playhead progresses between the start and end values. The destination remains the destination value. `"none"` gives linear progress; `"power2.out"` starts more quickly and settles toward the end.

## 6. Can GSAP animate values that are not CSS properties?

Yes. Any numeric or otherwise supported object property can be animated. For custom rendering, use callbacks such as `onUpdate` to redraw using the current values. Do not expect GSAP to know how your application should display an arbitrary object.

## 7. Why is my element not moving?

Check these points in order:

1. Confirm the selector matches an element and the script runs after the markup is available.
2. Check the browser console for an import or JavaScript error.
3. Confirm the animated property is appropriate for the target. For DOM transforms, try a supported alias such as `x` or `y`.
4. Check whether another animation or CSS rule is replacing the result.
5. Temporarily increase the duration and inspect the target during playback.

## 8. Does GSAP automatically make animation smooth or accessible?

GSAP synchronizes its rendering with browser animation frames, but the visual result still depends on the property, device, layout, and workload. Profile expensive effects. Accessibility also requires design decisions: keep content understandable without motion and respect reduced-motion preferences, covered later in the course.

## 9. When should I create a timeline?

Create one when several changes form a single sequence, should overlap, need to be replayed together, or need one playback control. Independent one-off reactions can remain separate tweens. Avoid turning every isolated property change into a global timeline without a reason.

## 10. What does GSAP do with a completed tween?

A normal completed tween stops updating its target. You can keep a reference to control it while it exists, but finished one-off animations generally do not need manual cleanup. Long-lived timelines, event listeners, ScrollTriggers, and framework-created animations still need appropriate lifecycle management.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous Q&amp;A</th><th>Chapter lesson</th><th>Chapter example</th><th>Next Q&amp;A</th></tr></thead>
  <tbody><tr><td>Start of course</td><td><a href="../lessons/001-gsap-and-animation-fundamentals.md">Lesson</a></td><td><a href="../examples/001-gsap-and-animation-fundamentals.md">Example</a></td><td><a href="002-installation-and-project-setup.md">002 - Installation and project setup Q&amp;A</a></td></tr></tbody>
</table>
