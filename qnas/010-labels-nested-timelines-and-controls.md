# 010 - Labels, nested timelines, and controls Q&A

## What is a timeline label?

A name assigned to a time on a timeline. Labels make placement and navigation more readable than unexplained numeric seconds.

## How do I add a nested timeline?

Build the child timeline, then add that instance to a parent with `parent.add(child, position)`. The parent timeline can control the child as part of its sequence.

## Does `seek("details")` play the timeline?

No. `seek()` moves the playhead to the label but preserves whether the animation was paused or playing. Call `play()` separately when playback should continue.

## How do I make a reusable animation sequence?

Create a function that builds and returns a timeline for a specific component, then add the returned timeline to its owner. Make the function's target scope explicit so repeated components do not animate one another.

## What does `timeScale(2)` do?

It doubles the animation playback speed. A value of `0.5` plays at half speed. It scales the parent timeline and therefore affects its child sequence too.

## Can I use the same child timeline in two parents?

An animation instance has one parent at a time. For two independent sequences, create separate child timeline instances from a factory function rather than trying to parent one instance twice.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous Q&amp;A</th><th>Chapter lesson</th><th>Chapter example</th><th>Next Q&amp;A</th></tr></thead>
  <tbody><tr><td><a href="009-timeline-position-parameter.md">009 - Timeline position parameter Q&amp;A</a></td><td><a href="../lessons/010-labels-nested-timelines-and-controls.md">Lesson</a></td><td><a href="../examples/010-labels-nested-timelines-and-controls.md">Example</a></td><td><a href="011-callbacks-and-animation-events.md">011 - Callbacks and animation events Q&amp;A</a></td></tr></tbody>
</table>
