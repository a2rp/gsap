# 027 - ScrollTo and programmatic scrolling Q&A

## What problem does ScrollToPlugin solve?

It animates the scroll position of the window or a scrollable element toward a coordinate or element. It moves the scroller; it does not create scroll-triggered animation scenes.

## How do I account for a fixed header?

Use an offsetY that represents the header's current height so the destination is not hidden underneath it. Re-measure if the header can resize.

## What does autoKill do?

It allows ScrollToPlugin to stop controlling an axis after it detects that the user changed that scroll position outside the tween, such as by taking over the scrollbar.

## Can I use ScrollToPlugin on an overflow panel?

Yes. Target the scrollable element instead of window, and make sure that element actually owns the relevant scrolling.

## Why can CSS scroll-behavior cause a conflict?

Both CSS and GSAP may try to smooth the same scroll change. Choose one mechanism for a given interaction to avoid competing motion.

## When should I use ScrollTrigger instead?

Use ScrollTrigger when animation should respond to scroll position. Use ScrollToPlugin when an interaction should move the scroller to a destination.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous Q&amp;A</th><th>Chapter lesson</th><th>Chapter example</th><th>Next Q&amp;A</th></tr></thead>
  <tbody><tr><td><a href="026-motionpath-and-path-animation.md">026 - MotionPath and path animation Q&amp;A</a></td><td><a href="../lessons/027-scrollto-and-programmatic-scrolling.md">Lesson</a></td><td><a href="../examples/027-scrollto-and-programmatic-scrolling.md">Example</a></td><td><a href="028-textplugin-and-splittext.md">028 - TextPlugin and SplitText Q&amp;A</a></td></tr></tbody>
</table>
