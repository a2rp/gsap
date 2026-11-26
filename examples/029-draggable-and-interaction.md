# 029 - Draggable and interaction Example

## Goal

Create a horizontal percentage control whose draggable visual thumb is synchronized with a native keyboard-operable range input.

## Prerequisites and setup

Use Node.js, npm, and the project created in Chapter 002. If you need a fresh project, run:

```bash
npm create vite@latest gsap-demo -- --template vanilla
cd gsap-demo
npm install
npm install gsap
npm run dev
```

Keep the development server running. Put the markup in index.html, the styles in src/style.css, and the JavaScript in src/main.js. This example uses the local development server because the GSAP package is imported as an ES module.

## Markup: index.html

```html
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Draggable and interaction demo</title>
  </head>
  <body>
<label for="progress-value">Progress</label>
<input id="progress-value" type="range" min="0" max="100" value="35" data-value>
<div class="track" data-track aria-hidden="true">
  <div class="thumb" data-thumb></div>
</div>
<output data-output for="progress-value">35%</output>
    <script type="module" src="/src/main.js"></script>
  </body>
</html>
```

## Styles: src/style.css

```css
.track { position: relative; height: 2rem; border-radius: 1rem; background: #d9e2f2; touch-action: pan-y; }
.thumb { position: absolute; top: 0; left: 0; width: 2rem; height: 2rem; border-radius: 50%; background: #315ee8; cursor: grab; }
.thumb:active { cursor: grabbing; }
input[type="range"] { width: 100%; }
```

## Animation: src/main.js

```js
import "./style.css";
import { gsap } from "gsap";
import { Draggable } from "gsap/Draggable";

gsap.registerPlugin(Draggable);

const track = document.querySelector("[data-track]");
const thumb = document.querySelector("[data-thumb]");
const input = document.querySelector("[data-value]");
const output = document.querySelector("[data-output]");

if (track && thumb && input && output) {
  const maxX = () => Math.max(0, track.clientWidth - thumb.offsetWidth);
  const setFromInput = () => {
    const percent = Number(input.value);
    gsap.set(thumb, { x: (percent / 100) * maxX() });
    output.value = `${percent}%`;
  };

  const draggable = Draggable.create(thumb, {
    type: "x",
    bounds: track,
    edgeResistance: 1,
    onDrag() {
      const percent = maxX() ? Math.round((this.x / maxX()) * 100) : 0;
      input.value = String(percent);
      output.value = `${percent}%`;
    }
  })[0];

  input.addEventListener("input", () => {
    setFromInput();
    draggable.update();
  });

  const resizeObserver = new ResizeObserver(() => {
    setFromInput();
    draggable.applyBounds(track);
  });
  resizeObserver.observe(track);
  setFromInput();

  // Call from the view's teardown hook.
  function cleanupDragger() {
    resizeObserver.disconnect();
    input.removeEventListener("input", setFromInput);
    draggable.kill();
  }
}
```

## Expected result

Dragging the thumb updates the range value and percentage output. Operating the native range by keyboard or pointer moves the visual thumb to the matching position. The range remains the semantic control, and touch users can still scroll vertically.

## Practice variation

Add a `liveSnap` rule that snaps the drag to 10 percent increments. Update the native range to the snapped value during drag so the visual and accessible state always agree.

## Common mistakes

Treating the decorative thumb as the only control; forgetting that drag changes need to update the native range; recalculating track width only at startup; using an inertial option without its plugin; setting touch-action to disable vertical page scrolling.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous example</th><th>Chapter lesson</th><th>Chapter Q&amp;A</th><th>Next example</th></tr></thead>
  <tbody><tr><td><a href="028-textplugin-and-splittext.md">028 - TextPlugin and SplitText example</a></td><td><a href="../lessons/029-draggable-and-interaction.md">Lesson</a></td><td><a href="../qnas/029-draggable-and-interaction.md">Q&amp;A</a></td><td><a href="030-performance-and-debugging.md">030 - Performance and debugging example</a></td></tr></tbody>
</table>
