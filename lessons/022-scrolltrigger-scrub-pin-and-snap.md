# 022 - ScrollTrigger scrub, pin, and snap

## Learning goals

- Link a timeline to scroll progress with `scrub`.
- Use pinning and snapping deliberately and understand their layout effects.

## Core idea

`scrub` links an animation's progress to scroll progress. `pin` holds a trigger element in place over a configured range. `snap` can settle the scroll position at selected progress values after scrolling stops.

## How it works

With `scrub: true`, the animation playhead follows the scrollbar directly. A numeric scrub adds catch-up smoothing in seconds. Pinning temporarily holds an element and normally adds spacing so later content does not collapse under it. Snap can target increments, arrays, functions, or timeline labels. When snapping to labels, the timeline needs meaningful labels.

```js
const story = gsap.timeline({
  scrollTrigger: {
    trigger: ".story",
    start: "top top",
    end: () => `+=${window.innerHeight * 2}`,
    scrub: 0.4,
    pin: true,
    snap: "labelsDirectional",
    markers: true,
  },
});

story.addLabel("start")
  .to(".story__card", { x: 180, duration: 1 })
  .addLabel("middle")
  .to(".story__card", { rotation: 180, duration: 1 })
  .addLabel("end");
```

Read the code from the target outward: identify the animated value, then the GSAP configuration that controls its start, destination, timing, or lifecycle. In DOM examples, make sure the selected elements exist before this module runs. In object examples, update the visible interface from the changing object value yourself.

## When to use it and its limits

Use scrub for animations that should visually track reading progress, pin for a section that should remain visible during a defined sequence, and snap only when landing on discrete positions improves the interaction. Preserve user control and test touch, keyboard, and reduced-motion behavior.

Pinning affects layout and can interact with ancestors that use transforms, overflow, or complex positioning. A very long pinned range can trap attention. Numeric scrub delays catch-up; it is not the scroll distance. Snapping animates scroll position after the user stops and should never make content inaccessible.

## Common mistakes

- Assuming `scrub: 0.5` means half a viewport; it means the playhead catches up over about half a second.
- Forgetting to define a usable `end`, which controls the scroll distance for scrub and pin.
- Snapping to labels that were never created.
- Pinning nested elements without checking the resulting pin spacing and document flow.

## Recap and practice

Create a pinned section with a three-step timeline and `snap: "labelsDirectional"`. Add labels for each step. Then remove snap and compare the level of user control. Reduce the pin duration and observe how later content flows.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous lesson</th><th>Chapter Q&amp;A</th><th>Chapter example</th><th>Next lesson</th></tr></thead>
  <tbody><tr><td><a href="021-scrolltrigger-start-end-and-refresh.md">021 - ScrollTrigger start, end, and refresh</a></td><td><a href="../qnas/022-scrolltrigger-scrub-pin-and-snap.md">Q&amp;A</a></td><td><a href="../examples/022-scrolltrigger-scrub-pin-and-snap.md">Example</a></td><td><a href="023-scrolltrigger-callbacks-classes-and-batch.md">023 - ScrollTrigger callbacks, classes, and batch</a></td></tr></tbody>
</table>
