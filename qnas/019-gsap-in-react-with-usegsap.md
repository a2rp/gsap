# 019 - GSAP in React with useGSAP() Q&A

## Why use `@gsap/react` instead of a plain `useEffect()`?

`useGSAP()` is a React-aware hook that scopes GSAP work with context and automatically reverts collected animations when its lifecycle ends. It also provides an SSR-safe effect strategy.

## What does the `scope` ref do?

It limits selector text used inside the hook to descendants of that component root. This prevents a `.title` selector from matching a different component elsewhere on the page.

## Does `useGSAP()` run on every render?

No. Its default behavior is similar to an effect with an empty dependency array. Pass `dependencies` when the animation should react to changing values.

## When should I set `revertOnUpdate: true`?

Use it when animations should be reverted and rebuilt whenever a listed dependency changes. Without it, GSAP context cleanup normally occurs when the hook is torn down.

## What is `contextSafe()` for?

It wraps a function that creates GSAP animations after the main hook callback has run, such as a click handler. Animations created by that function are recorded by the context and cleaned up with it.

## Does context cleanup remove my event listener?

No. Remove event listeners, timers, and subscriptions yourself in a cleanup function. The context handles associated GSAP animations and ScrollTriggers.

## Can I run GSAP during server rendering?

Do not access browser DOM or create DOM animations during server rendering. `useGSAP()` uses an isomorphic lifecycle approach so its animation setup runs on the client.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous Q&amp;A</th><th>Chapter lesson</th><th>Chapter example</th><th>Next Q&amp;A</th></tr></thead>
  <tbody><tr><td><a href="018-responsive-motion-and-reduced-motion.md">018 - Responsive motion and reduced motion Q&amp;A</a></td><td><a href="../lessons/019-gsap-in-react-with-usegsap.md">Lesson</a></td><td><a href="../examples/019-gsap-in-react-with-usegsap.md">Example</a></td><td><a href="020-scrolltrigger-fundamentals.md">020 - ScrollTrigger fundamentals Q&amp;A</a></td></tr></tbody>
</table>
