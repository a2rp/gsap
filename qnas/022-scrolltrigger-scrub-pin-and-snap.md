# 022 - ScrollTrigger scrub, pin, and snap Q&A

## What does `scrub: true` do?

It directly links the animation playhead to scroll progress between the trigger's start and end. Scrolling backward moves the animation backward.

## What does a numeric scrub value mean?

It is the approximate number of seconds for the playhead to catch up to the scrollbar position. It is a smoothing time, not a pixel distance.

## What does pinning do to the page layout?

ScrollTrigger holds the pin element during its active range and, by default, adds spacing so following content can continue below it. This layout effect should be tested in context.

## How does `snap: "labelsDirectional"` work?

It snaps the scroll progress to timeline labels and favors the direction the user last scrolled. The timeline must contain meaningful labels.

## Can `toggleActions` be combined with scrub?

Scrub controls progress by scroll position, while toggleActions control playback at boundary crossings. For a directly scroll-linked animation, scrub is usually the central control; avoid combining settings that fight over playback.

## Why does pinned content jump?

Check the trigger order, pin spacing, ancestor transforms/overflow, and whether the element's dimensions change. Enable markers and keep triggers created in document order where possible.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous Q&amp;A</th><th>Chapter lesson</th><th>Chapter example</th><th>Next Q&amp;A</th></tr></thead>
  <tbody><tr><td><a href="021-scrolltrigger-start-end-and-refresh.md">021 - ScrollTrigger start, end, and refresh Q&amp;A</a></td><td><a href="../lessons/022-scrolltrigger-scrub-pin-and-snap.md">Lesson</a></td><td><a href="../examples/022-scrolltrigger-scrub-pin-and-snap.md">Example</a></td><td><a href="023-scrolltrigger-callbacks-classes-and-batch.md">023 - ScrollTrigger callbacks, classes, and batch Q&amp;A</a></td></tr></tbody>
</table>
