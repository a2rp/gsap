# 019 - GSAP in React with useGSAP()

## Learning goals

- Scope component animations with `useGSAP()` from `@gsap/react`.
- Use the hook's cleanup, dependency, and context-safe patterns correctly.

## Core idea

GSAP works in React without a wrapper, but component lifecycles require scoped selectors and cleanup. The official `@gsap/react` package provides `useGSAP()`, which integrates GSAP context with React effects and reverts collected animations when the component is cleaned up.

## How it works

Install both `gsap` and `@gsap/react`, import the hook, and register it with `gsap.registerPlugin(useGSAP)`. Pass a ref as `scope` so selector text only targets descendants of that component. `useGSAP()` defaults to running once, similar to an effect with an empty dependency array. For values that change, pass `dependencies`; use `revertOnUpdate: true` if animations should be reverted and rebuilt whenever those dependencies change. Wrap event handlers that create animations later with `contextSafe()` and remove their listeners during cleanup.

```js
import { useRef } from "react";
import { gsap } from "gsap";
import { useGSAP } from "@gsap/react";

gsap.registerPlugin(useGSAP);

function Hero() {
  const container = useRef(null);

  useGSAP(() => {
    gsap.from(".title", { y: 24, autoAlpha: 0, duration: 0.6 });
  }, { scope: container });

  return <section ref={container}><h1 className="title">Welcome</h1></section>;
}
```

Read the code from the target outward: identify the animated value, then the GSAP configuration that controls its start, destination, timing, or lifecycle. In DOM examples, make sure the selected elements exist before this module runs. In object examples, update the visible interface from the changing object value yourself.

## When to use it and its limits

Use `useGSAP()` for component-owned animations, especially when targeting repeated class names or creating timelines and ScrollTriggers. Use actual element refs when a direct node target is clearer. Keep animation setup out of render and avoid triggering state updates on every animation frame unless the UI truly requires them.

The hook does not make arbitrary timers, event listeners, or subscriptions disappear; clean those up yourself. In server-rendered applications, animation work must run on the client. A `contextSafe()` wrapper scopes GSAP work but does not replace normal React event cleanup.

## Common mistakes

- Calling GSAP during render rather than inside `useGSAP()` or a user event.
- Omitting `scope` while using broad selector strings in a component with repeated class names.
- Recreating animations on every render by using a raw effect without correct dependencies.
- Creating an animation inside a click handler without `contextSafe()`.
- Forgetting to remove manually registered event listeners.

## Recap and practice

Build a `Hero` component with one container ref and a scoped `.title` entrance. Add a button whose handler creates a second animation through `contextSafe()`. Unmount the component and confirm both animations are reverted and no listener remains.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous lesson</th><th>Chapter Q&amp;A</th><th>Chapter example</th><th>Next lesson</th></tr></thead>
  <tbody><tr><td><a href="018-responsive-motion-and-reduced-motion.md">018 - Responsive motion and reduced motion</a></td><td><a href="../qnas/019-gsap-in-react-with-usegsap.md">Q&amp;A</a></td><td><a href="../examples/019-gsap-in-react-with-usegsap.md">Example</a></td><td><a href="020-scrolltrigger-fundamentals.md">020 - ScrollTrigger fundamentals</a></td></tr></tbody>
</table>
