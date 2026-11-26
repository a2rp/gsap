# 018 - Responsive motion and reduced motion

## Learning goals

- Use `gsap.matchMedia()` to create animation setups for matching conditions.
- Respect the `prefers-reduced-motion` user preference.

## Core idea

`gsap.matchMedia()` connects GSAP setup to CSS media queries. It runs a callback when a query matches and reverts animations created by that callback when the query stops matching. It can also provide named boolean conditions for responsive layouts and motion preferences.

## How it works

Create a matchMedia instance and call `.add()` with a query or conditions object. The callback receives a context with the matching conditions. Use those booleans to choose an appropriate animation setup. A `prefers-reduced-motion: reduce` condition should skip or substantially reduce nonessential motion while keeping the interface's content and state understandable.

```js
const mm = gsap.matchMedia();

mm.add({
  desktop: "(min-width: 48rem)",
  reduceMotion: "(prefers-reduced-motion: reduce)",
}, ({ conditions }) => {
  if (conditions.reduceMotion) {
    gsap.set(".card", { y: 0, autoAlpha: 1 });
    return;
  }

  gsap.from(".card", {
    y: conditions.desktop ? 28 : 10,
    autoAlpha: 0,
    duration: conditions.desktop ? 0.65 : 0.35,
    stagger: 0.1,
  });
});
```

Read the code from the target outward: identify the animated value, then the GSAP configuration that controls its start, destination, timing, or lifecycle. In DOM examples, make sure the selected elements exist before this module runs. In object examples, update the visible interface from the changing object value yourself.

## When to use it and its limits

Use matchMedia when the animation itself should differ by breakpoint or user preference. For example, use a short fade on small screens and no movement for reduced motion. Keep layout responsive in CSS and use GSAP conditions for animation behavior.

A media query callback can run again when conditions change, so its collected GSAP work must be reversible and its setup should be safe to recreate. `matchMedia()` does not replace responsive CSS or a broader accessibility review. Reduced motion does not mean hiding essential information.

## Common mistakes

- Creating animations outside the `.add()` callback and expecting them to revert when the query changes.
- Checking reduced motion once at page load and failing to respond if the preference changes.
- Replacing motion with `autoAlpha: 0` and leaving content hidden.
- Making a no-motion state unusable because the animation was responsible for revealing content.

## Recap and practice

Create named desktop and reduced-motion conditions. Use movement for the desktop condition, a minimal opacity change on smaller screens, and a direct visible state when reduced motion is requested. Resize and change the OS/browser preference to observe reversion.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous lesson</th><th>Chapter Q&amp;A</th><th>Chapter example</th><th>Next lesson</th></tr></thead>
  <tbody><tr><td><a href="017-context-cleanup-and-reversion.md">017 - Context, cleanup, and reversion</a></td><td><a href="../qnas/018-responsive-motion-and-reduced-motion.md">Q&amp;A</a></td><td><a href="../examples/018-responsive-motion-and-reduced-motion.md">Example</a></td><td><a href="019-gsap-in-react-with-usegsap.md">019 - GSAP in React with useGSAP()</a></td></tr></tbody>
</table>
