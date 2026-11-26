# 010 - Labels, nested timelines, and controls

## Learning goals

- Name meaningful moments with timeline labels.
- Nest a reusable timeline and control the parent playhead.

## Core idea

Labels give names to positions in a timeline. Nested timelines let you package a sequence and add it to a parent timeline as one child. Both help keep animation logic readable as an interface grows.

## How it works

Use `addLabel(name, position)` to create a named point. Pass the label to a timeline method or use `seek(label)` to move to it. A child timeline can be built independently, then added with `parent.add(child, position)`. The parent controls the child playhead. Methods such as `play()`, `pause()`, `reverse()`, `restart()`, `seek()`, `progress()`, and `timeScale()` control playback.

```js
const detailSequence = gsap.timeline();
detailSequence
  .from(".detail", { y: 16, autoAlpha: 0, stagger: 0.1 });

const page = gsap.timeline({ paused: true });
page.addLabel("intro")
  .from(".title", { y: 24, autoAlpha: 0 }, "intro")
  .addLabel("details", "+=0.2")
  .add(detailSequence, "details")
  .addLabel("complete");
```

Read the code from the target outward: identify the animated value, then the GSAP configuration that controls its start, destination, timing, or lifecycle. In DOM examples, make sure the selected elements exist before this module runs. In object examples, update the visible interface from the changing object value yourself.

## When to use it and its limits

Use labels for scene beats such as `"intro"`, `"details"`, or `"complete"`. Nest timelines when a card, menu, or hero sequence should be reusable. Keep control logic near the code that owns the timeline.

Labels name positions, not events. Seeking to a label does not change the timeline's paused or playing state. A nested timeline's duration contributes to its parent's total duration; changing child content can affect parent timing.

## Common mistakes

- Using unclear label names such as `"a"` and `"b"` in a timeline maintained by a team.
- Creating a new child timeline each time a control is clicked without killing or reusing the previous one.
- Expecting `seek()` to start playback after jumping to a label.
- Changing a nested sequence's duration and forgetting that the parent's later positions may shift.

## Recap and practice

Build a child timeline for a badge reveal, add it to a labeled parent timeline, and add buttons for play, reverse, and `seek("details")`. Verify whether each control should resume or remain paused after seeking.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous lesson</th><th>Chapter Q&amp;A</th><th>Chapter example</th><th>Next lesson</th></tr></thead>
  <tbody><tr><td><a href="009-timeline-position-parameter.md">009 - Timeline position parameter</a></td><td><a href="../qnas/010-labels-nested-timelines-and-controls.md">Q&amp;A</a></td><td><a href="../examples/010-labels-nested-timelines-and-controls.md">Example</a></td><td><a href="011-callbacks-and-animation-events.md">011 - Callbacks and animation events</a></td></tr></tbody>
</table>
