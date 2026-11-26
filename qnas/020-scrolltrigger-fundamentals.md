# 020 - ScrollTrigger fundamentals Q&A

## Is ScrollTrigger included in the GSAP core import?

It is a separate plugin import. Import it from the `gsap/ScrollTrigger` package path and register it with `gsap.registerPlugin(ScrollTrigger)`.

## Does a ScrollTrigger need a tween?

No. You can create a standalone ScrollTrigger for callbacks or state observation. The common pattern attaches it to a tween or timeline.

## What is `trigger`?

It identifies the element whose position in normal document flow is used to calculate the ScrollTrigger's start and end positions.

## Why do markers not appear?

Check that the plugin was imported and registered, the script ran without errors, and a ScrollTrigger instance was created for a matching trigger element.

## Does ScrollTrigger constantly inspect every element on scroll?

No. It calculates start/end positions up front and updates from scroll position, with refreshes when needed. This design avoids continuous per-element layout measurements.

## Does ScrollTrigger replace native scrolling?

No. It works with normal browser scrolling. Optional features like snapping can animate scroll position, but basic triggers, scrubbing, and pinning do not require custom scroll handling.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous Q&amp;A</th><th>Chapter lesson</th><th>Chapter example</th><th>Next Q&amp;A</th></tr></thead>
  <tbody><tr><td><a href="019-gsap-in-react-with-usegsap.md">019 - GSAP in React with useGSAP() Q&amp;A</a></td><td><a href="../lessons/020-scrolltrigger-fundamentals.md">Lesson</a></td><td><a href="../examples/020-scrolltrigger-fundamentals.md">Example</a></td><td><a href="021-scrolltrigger-start-end-and-refresh.md">021 - ScrollTrigger start, end, and refresh Q&amp;A</a></td></tr></tbody>
</table>
