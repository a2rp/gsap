# 021 - ScrollTrigger start, end, and refresh

## Learning goals

- Read start/end expressions as matching positions between the trigger and scroller.
- Recalculate measured positions after layout changes.

## Core idea

A ScrollTrigger's `start` and `end` define the scroll positions where it becomes active and completes. String values describe a point on the trigger meeting a point on the scroller, such as `"top 80%"` or `"bottom center"`.

## How it works

Start and end are measured when a trigger is created and when ScrollTrigger refreshes. They are not continuously remeasured while scrolling. A number specifies an absolute scroll value; a function can return a value at refresh time. `ScrollTrigger.refresh()` forces recalculation after a layout change. `update()` checks the current scroll position against the existing measurements but does not recalculate those positions. `clamp()` wrapping is available in GSAP 3.12 and newer to keep calculated positions within scroll bounds.

```js
const section = document.querySelector(".feature");

gsap.to(".feature__box", {
  x: 240,
  scrollTrigger: {
    trigger: section,
    start: "top 75%",
    end: () => `+=${section.offsetHeight}`,
    scrub: true,
    invalidateOnRefresh: true,
    markers: true,
  },
});
```

Read the code from the target outward: identify the animated value, then the GSAP configuration that controls its start, destination, timing, or lifecycle. In DOM examples, make sure the selected elements exist before this module runs. In object examples, update the visible interface from the changing object value yourself.

## When to use it and its limits

Choose start and end based on a visible design event and confirm them with markers. Use functions when section height or another measured value determines the scroll distance. Refresh after images, fonts, accordions, or application content change the layout above triggers.

Repeated refreshes are expensive; call them after a meaningful layout update, not on every scroll or animation frame. A function value runs at creation/refresh time, not continuously. If an animation's start values also depend on changed layout, `invalidateOnRefresh` may be needed in addition to recalculating trigger positions.

## Common mistakes

- Reading `"top 80%"` as a fixed scroll coordinate rather than two points that meet.
- Calling `ScrollTrigger.update()` when the actual problem is stale measurements that require `refresh()`.
- Refreshing before the DOM has completed the layout change.
- Assuming a functional `end` value is updated on every scroll event.

## Recap and practice

Set a section's end to its measured height with a function. Resize the viewport and compare markers. Add content above the section after a button click, then call refresh after the DOM update and observe the corrected positions.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous lesson</th><th>Chapter Q&amp;A</th><th>Chapter example</th><th>Next lesson</th></tr></thead>
  <tbody><tr><td><a href="020-scrolltrigger-fundamentals.md">020 - ScrollTrigger fundamentals</a></td><td><a href="../qnas/021-scrolltrigger-start-end-and-refresh.md">Q&amp;A</a></td><td><a href="../examples/021-scrolltrigger-start-end-and-refresh.md">Example</a></td><td><a href="022-scrolltrigger-scrub-pin-and-snap.md">022 - ScrollTrigger scrub, pin, and snap</a></td></tr></tbody>
</table>
