# 018 - Responsive motion and reduced motion Q&A

## What happens when a media query stops matching?

GSAP reverts the animations and ScrollTriggers collected by that matchMedia callback, then can run the setup again if the condition later matches.

## How do I read multiple conditions?

Pass an object whose property names map to media-query strings. The callback receives a `conditions` object with booleans for those names.

## Should reduced motion remove every animation?

Not necessarily, but it should remove or reduce nonessential movement. Preserve content, state changes, and usability. A short opacity transition may be acceptable in some interfaces, while others should use a direct state change.

## Does matchMedia replace responsive CSS?

No. Use CSS for layout and presentation. Use `gsap.matchMedia()` when the animation setup itself needs different behavior at breakpoints or for user preferences.

## How do I clean up the matchMedia instance?

Call its `revert()` method when the owning page or component is disposed, and remove any event listeners your own code added.

## What if the user changes their motion preference while the page is open?

A media-query-based setup can respond to the condition change and revert/rebuild the animation setup, so avoid caching a one-time preference check outside that lifecycle.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous Q&amp;A</th><th>Chapter lesson</th><th>Chapter example</th><th>Next Q&amp;A</th></tr></thead>
  <tbody><tr><td><a href="017-context-cleanup-and-reversion.md">017 - Context, cleanup, and reversion Q&amp;A</a></td><td><a href="../lessons/018-responsive-motion-and-reduced-motion.md">Lesson</a></td><td><a href="../examples/018-responsive-motion-and-reduced-motion.md">Example</a></td><td><a href="019-gsap-in-react-with-usegsap.md">019 - GSAP in React with useGSAP() Q&amp;A</a></td></tr></tbody>
</table>
