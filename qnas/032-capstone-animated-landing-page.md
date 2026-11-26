# 032 - Capstone: animated landing page Q&A

## What does this capstone combine?

It combines a short timeline-like hero entrance, per-card ScrollTrigger reveals, optional ScrollTo navigation, and a reduced-motion path managed by gsap.matchMedia().

## Why keep semantic anchors if navigation is animated?

Anchors provide a real destination and native keyboard and browser behavior. The GSAP interaction enhances navigation when motion is allowed.

## How does the example honor reduced motion?

It skips the entrance and scroll tween when the reduced-motion condition is active, while keeping all page content and links available.

## Why scope selectors to the page root?

Scoping keeps the animation setup limited to the current view and avoids accidentally selecting similarly named elements elsewhere in a larger application.

## Why does each feature card get its own ScrollTrigger?

Each trigger is tied to the card whose visibility matters, which makes the start condition direct and easier to tune.

## What must be cleaned up when a client-side view is removed?

Revert the match-media context and remove event listeners or other resources owned by the view.

## What should be tested before calling the page production-ready?

Check content without JavaScript, reduced motion, keyboard navigation, focus and reading order, narrow viewports, layout changes, and cleanup during navigation.

## When should ScrollTrigger.refresh() be considered?

After a meaningful layout change that alters trigger positions, such as inserting content above a scene. Call it after the DOM update rather than on every scroll event.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous Q&amp;A</th><th>Chapter lesson</th><th>Chapter example</th><th>Next Q&amp;A</th></tr></thead>
  <tbody><tr><td><a href="031-accessibility-and-production-readiness.md">031 - Accessibility and production readiness Q&amp;A</a></td><td><a href="../lessons/032-capstone-animated-landing-page.md">Lesson</a></td><td><a href="../examples/032-capstone-animated-landing-page.md">Example</a></td><td>End of course</td></tr></tbody>
</table>
