# 020 - ScrollTrigger fundamentals

## Learning goals

- Import and register ScrollTrigger.
- Attach a trigger to a tween and inspect its start/end with markers.

## Core idea

ScrollTrigger connects a tween or timeline to the browser's scroll position. It can start an animation when a region enters the scroller, link progress to scrolling, pin content, and call lifecycle callbacks.

## How it works

Import ScrollTrigger from the GSAP package and register it. Add a `scrollTrigger` configuration to a tween or timeline with a `trigger` element. At setup and refresh time, ScrollTrigger calculates start and end scroll positions based on normal document flow. It synchronizes updates with GSAP's rendering loop rather than continuously measuring every element.

```js
import { ScrollTrigger } from "gsap/ScrollTrigger";

gsap.registerPlugin(ScrollTrigger);

gsap.from(".feature", {
  y: 28,
  autoAlpha: 0,
  duration: 0.7,
  scrollTrigger: {
    trigger: ".feature",
    start: "top 80%",
    markers: true,
  },
});
```

Read the code from the target outward: identify the animated value, then the GSAP configuration that controls its start, destination, timing, or lifecycle. In DOM examples, make sure the selected elements exist before this module runs. In object examples, update the visible interface from the changing object value yourself.

## When to use it and its limits

Use ScrollTrigger when scroll position should control an animation or trigger a section interaction. Start with a single trigger and visible `markers: true` while tuning. Keep native scrolling available; ScrollTrigger does not require taking over scroll input.

A page needs enough scroll distance for the trigger to reach its start. If content or fonts change layout after measurements, positions may need refresh. Markers are a debugging aid, not final UI. A ScrollTrigger plugin must be loaded and registered.

## Common mistakes

- Forgetting to import or register ScrollTrigger, especially in a bundled production build.
- Using a selector for a trigger that does not exist or matches multiple unintended elements.
- Testing a scroll trigger on a page that has no vertical scroll range.
- Assuming start/end values update continuously while the DOM layout is being animated.

## Recap and practice

Attach a simple reveal tween to a section, enable markers, and scroll slowly through the page. Then resize the viewport and observe automatic recalculation. Add new content above the trigger and call `ScrollTrigger.refresh()` after the layout update.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous lesson</th><th>Chapter Q&amp;A</th><th>Chapter example</th><th>Next lesson</th></tr></thead>
  <tbody><tr><td><a href="019-gsap-in-react-with-usegsap.md">019 - GSAP in React with useGSAP()</a></td><td><a href="../qnas/020-scrolltrigger-fundamentals.md">Q&amp;A</a></td><td><a href="../examples/020-scrolltrigger-fundamentals.md">Example</a></td><td><a href="021-scrolltrigger-start-end-and-refresh.md">021 - ScrollTrigger start, end, and refresh</a></td></tr></tbody>
</table>
