# 031 - Accessibility and production readiness Q&A

## What should remain true when animation is disabled?

All essential content and actions should still be visible, understandable, and usable. Motion should enhance the interface rather than gate access to it.

## How can GSAP respond to prefers-reduced-motion?

Use `gsap.matchMedia()` with a reduced-motion media condition and provide a simpler or immediate behavior for that condition.

## What does gsap.matchMedia() clean up automatically?

Animations and ScrollTriggers created while its matching handler runs are recorded and reverted when the conditions stop matching or the object is reverted.

## Does that remove every event listener in the component?

No. Remove event listeners and other external resources explicitly as part of the owning view's cleanup.

## Why prefer native buttons and links for animated controls?

They already provide expected keyboard behavior, focusability, and semantics. Custom elements require those behaviors to be implemented and maintained.

## What should be checked before production?

Check reduced motion, keyboard operation, reading order, focus behavior, responsive layout, cleanup, and removal of development-only markers and diagnostics.

## Should reduced motion always remove every transition?

Not necessarily. Choose a suitable reduced-motion experience, typically removing large or continuous movement while retaining clear, brief state feedback where helpful.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous Q&amp;A</th><th>Chapter lesson</th><th>Chapter example</th><th>Next Q&amp;A</th></tr></thead>
  <tbody><tr><td><a href="030-performance-and-debugging.md">030 - Performance and debugging Q&amp;A</a></td><td><a href="../lessons/031-accessibility-and-production-readiness.md">Lesson</a></td><td><a href="../examples/031-accessibility-and-production-readiness.md">Example</a></td><td><a href="032-capstone-animated-landing-page.md">032 - Capstone: animated landing page Q&amp;A</a></td></tr></tbody>
</table>
