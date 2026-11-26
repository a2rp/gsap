# 001 - GSAP and Animation Fundamentals Example

## Goal

Animate a card and a plain JavaScript object so you can see that GSAP works with both browser elements and application data.

## Prerequisites

Use a local JavaScript project with Node.js and npm installed. If you do not have one, create a vanilla Vite starter and install GSAP:

```bash
npm create vite@latest gsap-fundamentals -- --template vanilla
cd gsap-fundamentals
npm install
npm install gsap
npm run dev
```

Keep the Vite server running and open its local address in your browser. This example uses ES module imports, so opening the HTML file directly with `file://` is not the intended setup.

## Files

Use the starter's `index.html`, `src/style.css`, and `src/main.js` files. Replace the starter content with the snippets below.

### `index.html`

```html
<div class="card" aria-live="polite">
  <p class="label">GSAP target</p>
  <h1>One tween, two kinds of values</h1>
  <p>Watch the card move while the numeric value changes.</p>
  <output class="progress">0.00</output>
</div>
<script type="module" src="/src/main.js"></script>
```

### `src/style.css`

```css
:root {
  font-family: system-ui, sans-serif;
  color: #172033;
  background: #eef2f8;
}

body {
  margin: 0;
  min-height: 100vh;
  display: grid;
  place-items: center;
}

.card {
  width: min(32rem, calc(100% - 2rem));
  padding: 2rem;
  border-radius: 1rem;
  background: white;
  box-shadow: 0 1rem 3rem #18233a22;
}

.label { color: #5b4bdb; font-weight: 700; }
.progress { display: inline-block; font-variant-numeric: tabular-nums; }
```

### `src/main.js`

```js
import { gsap } from "gsap";
import "./style.css";

const card = document.querySelector(".card");
const output = document.querySelector(".progress");
const state = { progress: 0 };

gsap.to(card, {
  y: -12,
  rotation: 1,
  duration: 0.8,
  ease: "power2.out",
});

gsap.to(state, {
  progress: 1,
  duration: 1.2,
  ease: "none",
  onUpdate: () => {
    output.value = state.progress.toFixed(2);
    output.textContent = state.progress.toFixed(2);
  },
});
```

## Expected result

The card rises slightly and tilts. The output counts smoothly from `0.00` to `1.00`. The first tween targets an element; the second changes a plain object and uses `onUpdate` to display the changing value.

## Variations

- Change `y` to `-32` and compare the distance.
- Change the card's ease to `"none"` and compare its motion.
- Remove the object tween's `onUpdate` callback. The underlying number still changes, but the page no longer displays it.
- Add `opacity: 0.8` to the card tween and observe that all configured properties animate in the same tween.

## Common mistakes

- If the page is blank, check the terminal and browser console for an import error.
- If the card does not move, verify the Vite entry file still imports `src/main.js` and the selector matches the markup.
- Do not add the same GSAP setup in both the HTML and JavaScript entry files.
- The object example uses `output.value` and `textContent` so it works with an `<output>` element; changing only the JavaScript object would not update the DOM.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous example</th><th>Chapter lesson</th><th>Chapter Q&amp;A</th><th>Next example</th></tr></thead>
  <tbody><tr><td>Start of course</td><td><a href="../lessons/001-gsap-and-animation-fundamentals.md">Lesson</a></td><td><a href="../qnas/001-gsap-and-animation-fundamentals.md">Q&amp;A</a></td><td><a href="002-installation-and-project-setup.md">002 - Installation and project setup example</a></td></tr></tbody>
</table>
