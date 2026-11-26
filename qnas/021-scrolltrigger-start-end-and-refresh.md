# 021 - ScrollTrigger start, end, and refresh Q&A

## What does `start: "top 80%"` mean?

The trigger's top meets a point 80 percent down the scroller's viewport. The two positions define a scroll coordinate when the trigger is measured.

## What does `end: "+=500"` mean?

It sets the end 500 pixels after the calculated start position. Relative end values are useful when the scroll distance should be fixed.

## When should I use a function for `end`?

Use a function when the end depends on current layout measurements. ScrollTrigger calls it when calculating positions, such as during creation and refresh.

## What is the difference between `refresh()` and `update()`?

`refresh()` recalculates start and end positions. `update()` evaluates current scroll position against existing measurements and updates progress/callbacks.

## When is `invalidateOnRefresh` useful?

It invalidates the linked animation's recorded values on refresh, which can be useful when those values depend on dimensions that changed. It is separate from recalculating the trigger's start and end.

## When can I use `clamp()` in a start/end expression?

The `clamp()` syntax is supported in GSAP 3.12 and newer. It constrains a calculated position to the maximum scroll bounds, which can prevent triggers near the page edge from falling outside the scroll range.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous Q&amp;A</th><th>Chapter lesson</th><th>Chapter example</th><th>Next Q&amp;A</th></tr></thead>
  <tbody><tr><td><a href="020-scrolltrigger-fundamentals.md">020 - ScrollTrigger fundamentals Q&amp;A</a></td><td><a href="../lessons/021-scrolltrigger-start-end-and-refresh.md">Lesson</a></td><td><a href="../examples/021-scrolltrigger-start-end-and-refresh.md">Example</a></td><td><a href="022-scrolltrigger-scrub-pin-and-snap.md">022 - ScrollTrigger scrub, pin, and snap Q&amp;A</a></td></tr></tbody>
</table>
