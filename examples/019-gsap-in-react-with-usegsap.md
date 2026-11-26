# 019 - GSAP in React with useGSAP() Example

## Goal

Create a React component with a scoped entrance animation, a context-safe click animation, and automatic GSAP cleanup on unmount.

## Prerequisites and setup

Use Node.js and npm. Create a Vite React starter, install the dependencies, and start its development server:

```bash
npm create vite@latest gsap-react-demo -- --template react
cd gsap-react-demo
npm install
npm install gsap @gsap/react
npm run dev
```

The Vite React template already includes `index.html` with a `root` element and a `src/main.jsx` entry that renders `App`. Keep those files unless your template differs. Replace `src/App.jsx` and `src/style.css` with the code below.

## Component: `src/App.jsx`

```jsx
import { useRef } from "react";
import { gsap } from "gsap";
import { useGSAP } from "@gsap/react";
import "./style.css";

gsap.registerPlugin(useGSAP);

function App() {
  const container = useRef(null);

  const { contextSafe } = useGSAP(() => {
    gsap.from(".title", {
      y: 20,
      autoAlpha: 0,
      duration: 0.55,
      ease: "power2.out",
    });
  }, { scope: container });

  const rotateBox = contextSafe(() => {
    gsap.to(".box", {
      rotation: "+=180",
      duration: 0.7,
      transformOrigin: "center center",
      ease: "power2.inOut",
    });
  });

  return (
    <main ref={container} className="hero">
      <p className="eyebrow">React lifecycle</p>
      <h1 className="title">Scoped animation, safe cleanup</h1>
      <p>The component owns its GSAP work and reverts it when it unmounts.</p>
      <button className="hero__button" onClick={rotateBox}>
        Rotate the box
      </button>
      <div className="box" aria-hidden="true" />
    </main>
  );
}

export default App;
```

## Styles: `src/style.css`

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

.hero {
  width: min(42rem, calc(100% - 2rem));
  padding: 2rem;
  border-radius: 1rem;
  background: white;
}

.eyebrow { color: #635bdb; font-weight: 700; text-transform: uppercase; }
.hero__button { padding: .7rem 1rem; cursor: pointer; }
.box { width: 4rem; height: 4rem; margin-top: 1rem; border-radius: .8rem; background: #635bdb; }
```

## Expected result

The heading animates after the component mounts. Clicking the button rotates the box. The selector strings are scoped to `container`, and both the entrance and click-created animation belong to the hook's context. When the component unmounts, the hook reverts its recorded GSAP work.

## Practice variation

Add a prop called `distance` and pass it to the entrance tween. If the animation must be rebuilt whenever that prop changes, pass it in `dependencies` and configure `revertOnUpdate: true`. Try rendering two copies of the component and confirm each instance animates only its own children.

## Common mistakes

- Putting JSX in a `.js` file that is not processed as JSX; use the Vite React starter's `.jsx` file.
- Omitting `scope`, which can cause a selector to match elements outside this component.
- Creating the click tween without `contextSafe()`, so the hook does not collect it for cleanup.
- Calling `gsap.registerPlugin(useGSAP)` repeatedly inside the component instead of registering at module scope.
- Assuming the context removes event listeners added manually. This example uses React's `onClick`; manual listeners need their own cleanup.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous example</th><th>Chapter lesson</th><th>Chapter Q&amp;A</th><th>Next example</th></tr></thead>
  <tbody><tr><td><a href="018-responsive-motion-and-reduced-motion.md">018 - Responsive motion and reduced motion example</a></td><td><a href="../lessons/019-gsap-in-react-with-usegsap.md">Lesson</a></td><td><a href="../qnas/019-gsap-in-react-with-usegsap.md">Q&amp;A</a></td><td><a href="020-scrolltrigger-fundamentals.md">020 - ScrollTrigger fundamentals example</a></td></tr></tbody>
</table>
