# 007 - Staggers and distribution Q&A

## What does `stagger: 0.1` mean?

It starts adjacent targets 0.1 seconds apart. The complete group animation therefore lasts longer than one target's duration.

## What is the difference between `each` and `amount`?

`each` defines the time offset between successive targets. `amount` defines the overall time span across the staggered group, which GSAP distributes among the targets.

## What values can `from` use?

Common origins include `"start"`, `"center"`, `"end"`, an index, or a target reference. Choose an origin that matches the intended reading order and layout.

## When should I use a grid stagger?

Use a grid pattern when targets are arranged in rows and columns and the visual sequence should radiate from a point or follow an axis. The target list still needs to correspond to the rendered layout.

## Can each element also have a different value?

Yes. Use function-based property values alongside a stagger. The stagger determines when each target begins; the value function determines that target's property value.

## Why do grid stagger results look wrong after resizing?

A grid distribution is based on target positions when the tween is created. If the responsive layout changes, recreate or invalidate the animation in a resize-aware setup rather than assuming the old target arrangement is still correct.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous Q&amp;A</th><th>Chapter lesson</th><th>Chapter example</th><th>Next Q&amp;A</th></tr></thead>
  <tbody><tr><td><a href="006-targets-and-dynamic-values.md">006 - Targets and dynamic values Q&amp;A</a></td><td><a href="../lessons/007-staggers-and-distribution.md">Lesson</a></td><td><a href="../examples/007-staggers-and-distribution.md">Example</a></td><td><a href="008-timeline-fundamentals.md">008 - Timeline fundamentals Q&amp;A</a></td></tr></tbody>
</table>
