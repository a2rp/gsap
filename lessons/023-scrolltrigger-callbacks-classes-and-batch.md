# 023 - ScrollTrigger callbacks, classes, and batch

## Learning goals

- Use ScrollTrigger callbacks for enter/leave events.
- Toggle a class or batch multiple elements that enter near one another.

## Core idea

ScrollTrigger callbacks report when the scroll position crosses trigger boundaries. `toggleClass` manages an active class during the active range. `ScrollTrigger.batch()` coordinates callbacks for multiple targets that enter within a short interval.

## How it works

Callbacks such as `onEnter`, `onLeave`, `onEnterBack`, `onLeaveBack`, `onToggle`, and `onUpdate` receive the ScrollTrigger instance. Use its `trigger`, `progress`, `direction`, and other properties. `toggleClass` can apply a class to the trigger or to other targets. `batch()` groups nearby enter/leave callbacks and passes an array of elements to the callback, which can then be animated together with a stagger.

```js
ScrollTrigger.batch(".item", {
  start: "top 85%",
  onEnter: (elements) => gsap.to(elements, {
    y: 0,
    autoAlpha: 1,
    duration: 0.5,
    stagger: 0.12,
    overwrite: true,
  }),
});

ScrollTrigger.create({
  trigger: ".feature",
  start: "top center",
  end: "bottom center",
  toggleClass: { targets: ".feature__label", className: "is-active" },
});
```

Read the code from the target outward: identify the animated value, then the GSAP configuration that controls its start, destination, timing, or lifecycle. In DOM examples, make sure the selected elements exist before this module runs. In object examples, update the visible interface from the changing object value yourself.

## When to use it and its limits

Use callbacks for small actions synchronized with scroll boundaries, such as updating a progress display or starting a reveal. Use `toggleClass` when active state should be expressed in CSS. Use `batch()` for repeated cards or list items to coordinate a group entering the viewport.

`onUpdate` can run frequently and should stay lightweight. A callback's visual changes need cleanup or reset behavior for reverse scrolling. Batch callbacks group events based on their timing window; they do not make all targets one permanent animation.

## Common mistakes

- Doing expensive application work in `onUpdate`.
- Forgetting to restore a class or style when scrolling backward.
- Passing a single element assumption to a batch callback that receives an array.
- Hiding all content in CSS before the JavaScript has a chance to initialize.

## Recap and practice

Create a list that starts in its normal visible state. During script setup, set its items to an animated start pose, then use `ScrollTrigger.batch()` to reveal nearby items. Add a class toggle to a section and verify it changes in both scroll directions.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous lesson</th><th>Chapter Q&amp;A</th><th>Chapter example</th><th>Next lesson</th></tr></thead>
  <tbody><tr><td><a href="022-scrolltrigger-scrub-pin-and-snap.md">022 - ScrollTrigger scrub, pin, and snap</a></td><td><a href="../qnas/023-scrolltrigger-callbacks-classes-and-batch.md">Q&amp;A</a></td><td><a href="../examples/023-scrolltrigger-callbacks-classes-and-batch.md">Example</a></td><td><a href="024-observer-and-input-driven-motion.md">024 - Observer and input-driven motion</a></td></tr></tbody>
</table>
