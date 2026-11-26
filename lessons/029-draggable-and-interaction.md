# 029 - Draggable and interaction

## Learning goals

Create a bounded drag interaction with Draggable. Choose axis, snapping, and touch behavior for the task. Provide an equivalent keyboard-accessible way to operate the control.

## Core idea

Draggable turns an element into a pointer and touch interaction that can control x/y position, a single axis, or rotation. It provides drag lifecycle callbacks, bounds, snapping, and methods for enabling, disabling, and updating an instance.

## How it works

Register Draggable, then create an instance with Draggable.create(target, vars). Use type to constrain the affected transform, bounds to constrain movement, and snap or liveSnap for release-time or during-drag snapping. onPress, onDragStart, onDrag, and onDragEnd describe the interaction lifecycle. Use `allowNativeTouchScrolling` and CSS touch-action thoughtfully so a horizontal drag does not block vertical page scrolling. Inertia-based momentum needs InertiaPlugin. Keep a keyboard-operable native control or implement keyboard behavior that updates the same state.

``js
import { gsap } from "gsap";
import { Draggable } from "gsap/Draggable";

gsap.registerPlugin(Draggable);

const track = document.querySelector("[data-track]");
const thumb = document.querySelector("[data-thumb]");
const valueInput = document.querySelector("[data-value]");

if (track && thumb && valueInput) {
  const draggable = Draggable.create(thumb, {
    type: "x",
    bounds: track,
    edgeResistance: 1,
    onDrag() {
      const maxX = track.clientWidth - thumb.offsetWidth;
      const percent = maxX > 0 ? (this.x / maxX) * 100 : 0;
      valueInput.value = String(Math.round(percent));
    }
  })[0];

  valueInput.addEventListener("input", () => {
    const maxX = track.clientWidth - thumb.offsetWidth;
    const x = (Number(valueInput.value) / 100) * Math.max(0, maxX);
    gsap.set(thumb, { x });
    draggable.update();
  });
}
``

Read the code from the target outward: identify the animated value, then the GSAP configuration that controls its start, destination, timing, or lifecycle. In DOM examples, make sure the selected elements exist before this module runs. In object examples, update the visible interface from the changing object value yourself.

## When to use it and its limits

Use Draggable for direct-manipulation controls such as a scrubber, constrained card, or dial. State the interaction clearly, set useful bounds, and give the same action to keyboard and assistive-technology users. A native range input can supply an accessible keyboard control while its value is synchronized with a visual draggable thumb.

Draggable handles pointer/touch dragging, not the complete semantics or keyboard behavior of a custom control. InertiaPlugin is required for momentum. Transforms change visual position without changing normal document flow. Bounds and snap rules need re-evaluation if the container resizes.

## Common mistakes

Making an element drag without explaining how to operate it; omitting bounds; using `inertia: true` without InertiaPlugin; blocking all touch scrolling for a horizontal interaction; allowing an input or link inside the dragged surface to lose its normal behavior; forgetting to synchronize accessible values with pointer movement.

## Recap and practice

Build a horizontal value selector with a draggable thumb constrained to a track. Add a native range input that updates the same thumb and value, keep vertical page scrolling available on touch, and resize the track to confirm bounds remain sensible.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous lesson</th><th>Chapter Q&amp;A</th><th>Chapter example</th><th>Next lesson</th></tr></thead>
  <tbody><tr><td><a href="028-textplugin-and-splittext.md">028 - TextPlugin and SplitText</a></td><td><a href="../qnas/029-draggable-and-interaction.md">Q&amp;A</a></td><td><a href="../examples/029-draggable-and-interaction.md">Example</a></td><td><a href="030-performance-and-debugging.md">030 - Performance and debugging</a></td></tr></tbody>
</table>
