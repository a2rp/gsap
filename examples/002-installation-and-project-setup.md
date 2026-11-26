# 002 - Installation and project setup Example

## Goal

Create a minimal Vite page, install GSAP, and animate one box from the module entry file.

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
    <title>Installation and project setup demo</title>
  </head>
  <body>
    <main class="demo">
      <h1>GSAP is installed</h1>
      <div class="box" aria-label="Animated box"></div>
    </main>
    <script type="module" src="/src/main.js"></script>
  </body>
</html>
```

## Styles: src/style.css

```css
:root { font-family: system-ui, sans-serif; color: #172033; background: #eef2f8; }
body { margin: 0; min-height: 100vh; display: grid; place-items: center; }
.demo { width: min(34rem, calc(100% - 2rem)); padding: 2rem; background: white; border-radius: 1rem; }
.box { width: 5rem; height: 5rem; border-radius: 1rem; background: #635bdb; }
```

## Animation: src/main.js

```js
import "./style.css";
import { gsap } from "gsap";

const box = document.querySelector(".box");

if (!box) {
  throw new Error("Expected .box in index.html");
}

gsap.to(box, {
  x: 180,
  rotation: 12,
  duration: 0.8,
  ease: "power2.out",
});
```

## Expected result

The local Vite page loads without a module-resolution error. The box moves to the right and rotates slightly once the page starts.

## Practice variation

Install a plugin from the `gsap` package in the same project, import it from its package path, register it, and use it in a small demo. Keep the plugin import and its registration together in the same entry module while learning.

## Common mistakes

- Running the install command outside the Vite project folder.
- Opening `index.html` directly instead of using Vite's development server.
- Removing the Vite entry script from `index.html`.
- Importing a plugin but forgetting `gsap.registerPlugin()`.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous example</th><th>Chapter lesson</th><th>Chapter Q&amp;A</th><th>Next example</th></tr></thead>
  <tbody><tr><td><a href="001-gsap-and-animation-fundamentals.md">001 - GSAP and animation fundamentals example</a></td><td><a href="../lessons/002-installation-and-project-setup.md">Lesson</a></td><td><a href="../qnas/002-installation-and-project-setup.md">Q&amp;A</a></td><td><a href="003-tweens-with-gsap-to.md">003 - Tweens with gsap.to() example</a></td></tr></tbody>
</table>
