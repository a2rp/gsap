# 030 - Performance and debugging Q&A

## What should I check first when an animation stutters?

Reproduce and profile the page. Find whether scripting, layout, paint, assets, or too many simultaneous effects consume the frame budget before changing animation code.

## Why are transforms and opacity common animation choices?

They often avoid layout recalculation and can be composited efficiently. They are a useful starting point, not a guarantee that the full page will be fast.

## What do ScrollTrigger markers help diagnose?

They show the calculated start and end positions so you can compare the trigger geometry with the page and find configuration mistakes.

## What is the difference between ScrollTrigger.update() and refresh()?

Update checks the current scroll position and updates linked animations and callbacks. Refresh recalculates start and end positions from current layout.

## How can I inspect active tweens and triggers?

Use `gsap.getTweensOf(target)` for tweens of a target and `ScrollTrigger.getAll()` for existing ScrollTrigger instances.

## Should I add will-change to every animated element?

No. It can use additional memory and create too many layers. Add it only after profiling shows a benefit for a specific element.

## When should a custom ticker listener be removed?

Remove it when its owning component or scene is disposed. Otherwise custom frame work can continue after the UI is gone.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous Q&amp;A</th><th>Chapter lesson</th><th>Chapter example</th><th>Next Q&amp;A</th></tr></thead>
  <tbody><tr><td><a href="029-draggable-and-interaction.md">029 - Draggable and interaction Q&amp;A</a></td><td><a href="../lessons/030-performance-and-debugging.md">Lesson</a></td><td><a href="../examples/030-performance-and-debugging.md">Example</a></td><td><a href="031-accessibility-and-production-readiness.md">031 - Accessibility and production readiness Q&amp;A</a></td></tr></tbody>
</table>
