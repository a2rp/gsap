# 009 - Timeline position parameter Q&A

## Is a number such as `2` relative to the last tween?

No. A numeric position is an absolute time in seconds from the start of the timeline. Use a relative string such as `"+=2"` or `"-=2"` for an offset from the end.

## What does `"<"` refer to?

It refers to the start time of the previously added child animation. It does not mean the start of the whole timeline.

## What does `">"` refer to?

It refers to the end time of the previously added child. To add a gap, combine it with an offset such as `">+=0.2"`.

## How is `"-=0.3"` different from `"<-=0.3"`?

`"-=0.3"` places the child 0.3 seconds before the current end of the timeline. `"<-=0.3"` places it 0.3 seconds before the start of the previous child.

## Why use labels instead of numeric positions?

Labels name meaningful timeline beats. They make placement easier to understand and adjust when earlier durations change.

## Can a position reference a label that does not exist?

Yes. GSAP can create a label at the timeline's end as part of processing a position string. A misspelled label may therefore produce a valid but unintended placement, so keep label names consistent.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous Q&amp;A</th><th>Chapter lesson</th><th>Chapter example</th><th>Next Q&amp;A</th></tr></thead>
  <tbody><tr><td><a href="008-timeline-fundamentals.md">008 - Timeline fundamentals Q&amp;A</a></td><td><a href="../lessons/009-timeline-position-parameter.md">Lesson</a></td><td><a href="../examples/009-timeline-position-parameter.md">Example</a></td><td><a href="010-labels-nested-timelines-and-controls.md">010 - Labels, nested timelines, and controls Q&amp;A</a></td></tr></tbody>
</table>
