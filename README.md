# GSAP Learning Notes

A structured, hands-on guide to GSAP (GreenSock Animation Platform), from the first tween through timelines, responsive animation, framework cleanup, and scroll-driven interfaces. The notes are written as a progressive course: each chapter has a lesson, practical Q&A, and a focused example.

GSAP is a JavaScript animation library for animating DOM elements, SVG, and ordinary JavaScript objects. The course uses the GSAP 3 API. At the time these notes were prepared, the official project history showed GSAP 3.15.1 as the latest release. Check your installed package version when working on a project because releases can change.

## Learning outcomes

By following the chapters in order, you will learn to:

- Install GSAP in a modern JavaScript project and register plugins correctly.
- Build and control tweens and timelines with predictable timing.
- Animate CSS properties, transforms, SVG attributes, and JavaScript object values.
- Create staggered, responsive, and accessible motion.
- Scope and clean up animations in component-based applications, including React.
- Build scroll-triggered interactions while preserving normal browser scrolling.
- Choose and use common GSAP plugins for state transitions, paths, scrolling, and interaction.
- Debug layout, timing, performance, and lifecycle problems.

## Prerequisites and setup

You should know basic JavaScript, DOM selection, CSS, and how to run a local development server. React chapters also assume familiarity with React components and effects.

For a project using npm and a JavaScript bundler:

```bash
npm install gsap
```

Import GSAP in a JavaScript module:

```js
import { gsap } from "gsap";

gsap.to(".box", { x: 120, duration: 0.6 });
```

Plugins must be imported and registered when the project setup requires it. Each plugin lesson includes its import pattern. The official GSAP installation guidance says the plugins are available from npm in GSAP 3.13 and later. This repository's MIT license applies to these notes; it does not replace the license terms for GSAP or any dependency.

## How to use these notes

1. Read the lesson in order and run its example in a browser-based JavaScript project.
2. Change one value at a time and observe how the animation behaves.
3. Use the matching Q&A to resolve common errors and compare related APIs.
4. Revisit the summary and keywords index when using the notes as a reference.
5. Keep examples isolated from production code until you understand their cleanup and accessibility behavior.

## Quick guides

- [GSAP summary](gsap-summary.md)
- [GSAP keywords and concepts](gsap-keywords.md)

## Chapter roadmap

<table width="100%">
  <thead>
    <tr><th width="48">No.</th><th>Lesson</th><th width="72">Q&amp;A</th><th width="88">Example</th></tr>
  </thead>
  <tbody>
    <tr><td>001</td><td><a href="lessons/001-gsap-and-animation-fundamentals.md">GSAP and animation fundamentals</a></td><td><a href="qnas/001-gsap-and-animation-fundamentals.md">Open Q&amp;A</a></td><td><a href="examples/001-gsap-and-animation-fundamentals.md">Open example</a></td></tr>
    <tr><td>002</td><td><a href="lessons/002-installation-and-project-setup.md">Installation and project setup</a></td><td><a href="qnas/002-installation-and-project-setup.md">Open Q&amp;A</a></td><td><a href="examples/002-installation-and-project-setup.md">Open example</a></td></tr>
    <tr><td>003</td><td><a href="lessons/003-tweens-with-gsap-to.md">Tweens with gsap.to()</a></td><td><a href="qnas/003-tweens-with-gsap-to.md">Open Q&amp;A</a></td><td><a href="examples/003-tweens-with-gsap-to.md">Open example</a></td></tr>
    <tr><td>004</td><td><a href="lessons/004-gsap-from-and-fromto.md">gsap.from() and gsap.fromTo()</a></td><td><a href="qnas/004-gsap-from-and-fromto.md">Open Q&amp;A</a></td><td><a href="examples/004-gsap-from-and-fromto.md">Open example</a></td></tr>
    <tr><td>005</td><td><a href="lessons/005-timing-easing-and-repeats.md">Timing, easing, and repeats</a></td><td><a href="qnas/005-timing-easing-and-repeats.md">Open Q&amp;A</a></td><td><a href="examples/005-timing-easing-and-repeats.md">Open example</a></td></tr>
    <tr><td>006</td><td><a href="lessons/006-targets-and-dynamic-values.md">Targets and dynamic values</a></td><td><a href="qnas/006-targets-and-dynamic-values.md">Open Q&amp;A</a></td><td><a href="examples/006-targets-and-dynamic-values.md">Open example</a></td></tr>
    <tr><td>007</td><td><a href="lessons/007-staggers-and-distribution.md">Staggers and distribution</a></td><td><a href="qnas/007-staggers-and-distribution.md">Open Q&amp;A</a></td><td><a href="examples/007-staggers-and-distribution.md">Open example</a></td></tr>
    <tr><td>008</td><td><a href="lessons/008-timeline-fundamentals.md">Timeline fundamentals</a></td><td><a href="qnas/008-timeline-fundamentals.md">Open Q&amp;A</a></td><td><a href="examples/008-timeline-fundamentals.md">Open example</a></td></tr>
    <tr><td>009</td><td><a href="lessons/009-timeline-position-parameter.md">Timeline position parameter</a></td><td><a href="qnas/009-timeline-position-parameter.md">Open Q&amp;A</a></td><td><a href="examples/009-timeline-position-parameter.md">Open example</a></td></tr>
    <tr><td>010</td><td><a href="lessons/010-labels-nested-timelines-and-controls.md">Labels, nested timelines, and controls</a></td><td><a href="qnas/010-labels-nested-timelines-and-controls.md">Open Q&amp;A</a></td><td><a href="examples/010-labels-nested-timelines-and-controls.md">Open example</a></td></tr>
    <tr><td>011</td><td><a href="lessons/011-callbacks-and-animation-events.md">Callbacks and animation events</a></td><td><a href="qnas/011-callbacks-and-animation-events.md">Open Q&amp;A</a></td><td><a href="examples/011-callbacks-and-animation-events.md">Open example</a></td></tr>
    <tr><td>012</td><td><a href="lessons/012-setting-values-and-quick-methods.md">Setting values and quick methods</a></td><td><a href="qnas/012-setting-values-and-quick-methods.md">Open Q&amp;A</a></td><td><a href="examples/012-setting-values-and-quick-methods.md">Open example</a></td></tr>
    <tr><td>013</td><td><a href="lessons/013-css-properties-and-transforms.md">CSS properties and transforms</a></td><td><a href="qnas/013-css-properties-and-transforms.md">Open Q&amp;A</a></td><td><a href="examples/013-css-properties-and-transforms.md">Open example</a></td></tr>
    <tr><td>014</td><td><a href="lessons/014-svg-and-attribute-animation.md">SVG and attribute animation</a></td><td><a href="qnas/014-svg-and-attribute-animation.md">Open Q&amp;A</a></td><td><a href="examples/014-svg-and-attribute-animation.md">Open example</a></td></tr>
    <tr><td>015</td><td><a href="lessons/015-keyframes-modifiers-and-snapping.md">Keyframes, modifiers, and snapping</a></td><td><a href="qnas/015-keyframes-modifiers-and-snapping.md">Open Q&amp;A</a></td><td><a href="examples/015-keyframes-modifiers-and-snapping.md">Open example</a></td></tr>
    <tr><td>016</td><td><a href="lessons/016-utilities-and-reusable-effects.md">Utilities and reusable effects</a></td><td><a href="qnas/016-utilities-and-reusable-effects.md">Open Q&amp;A</a></td><td><a href="examples/016-utilities-and-reusable-effects.md">Open example</a></td></tr>
    <tr><td>017</td><td><a href="lessons/017-context-cleanup-and-reversion.md">Context, cleanup, and reversion</a></td><td><a href="qnas/017-context-cleanup-and-reversion.md">Open Q&amp;A</a></td><td><a href="examples/017-context-cleanup-and-reversion.md">Open example</a></td></tr>
    <tr><td>018</td><td><a href="lessons/018-responsive-motion-and-reduced-motion.md">Responsive motion and reduced motion</a></td><td><a href="qnas/018-responsive-motion-and-reduced-motion.md">Open Q&amp;A</a></td><td><a href="examples/018-responsive-motion-and-reduced-motion.md">Open example</a></td></tr>
    <tr><td>019</td><td><a href="lessons/019-gsap-in-react-with-usegsap.md">GSAP in React with useGSAP()</a></td><td><a href="qnas/019-gsap-in-react-with-usegsap.md">Open Q&amp;A</a></td><td><a href="examples/019-gsap-in-react-with-usegsap.md">Open example</a></td></tr>
    <tr><td>020</td><td><a href="lessons/020-scrolltrigger-fundamentals.md">ScrollTrigger fundamentals</a></td><td><a href="qnas/020-scrolltrigger-fundamentals.md">Open Q&amp;A</a></td><td><a href="examples/020-scrolltrigger-fundamentals.md">Open example</a></td></tr>
    <tr><td>021</td><td><a href="lessons/021-scrolltrigger-start-end-and-refresh.md">ScrollTrigger start, end, and refresh</a></td><td><a href="qnas/021-scrolltrigger-start-end-and-refresh.md">Open Q&amp;A</a></td><td><a href="examples/021-scrolltrigger-start-end-and-refresh.md">Open example</a></td></tr>
    <tr><td>022</td><td><a href="lessons/022-scrolltrigger-scrub-pin-and-snap.md">ScrollTrigger scrub, pin, and snap</a></td><td><a href="qnas/022-scrolltrigger-scrub-pin-and-snap.md">Open Q&amp;A</a></td><td><a href="examples/022-scrolltrigger-scrub-pin-and-snap.md">Open example</a></td></tr>
    <tr><td>023</td><td><a href="lessons/023-scrolltrigger-callbacks-classes-and-batch.md">ScrollTrigger callbacks, classes, and batch</a></td><td><a href="qnas/023-scrolltrigger-callbacks-classes-and-batch.md">Open Q&amp;A</a></td><td><a href="examples/023-scrolltrigger-callbacks-classes-and-batch.md">Open example</a></td></tr>
    <tr><td>024</td><td><a href="lessons/024-observer-and-input-driven-motion.md">Observer and input-driven motion</a></td><td><a href="qnas/024-observer-and-input-driven-motion.md">Open Q&amp;A</a></td><td><a href="examples/024-observer-and-input-driven-motion.md">Open example</a></td></tr>
    <tr><td>025</td><td><a href="lessons/025-flip-and-layout-transitions.md">Flip and layout transitions</a></td><td><a href="qnas/025-flip-and-layout-transitions.md">Open Q&amp;A</a></td><td><a href="examples/025-flip-and-layout-transitions.md">Open example</a></td></tr>
    <tr><td>026</td><td><a href="lessons/026-motionpath-and-path-animation.md">MotionPath and path animation</a></td><td><a href="qnas/026-motionpath-and-path-animation.md">Open Q&amp;A</a></td><td><a href="examples/026-motionpath-and-path-animation.md">Open example</a></td></tr>
    <tr><td>027</td><td><a href="lessons/027-scrollto-and-programmatic-scrolling.md">ScrollTo and programmatic scrolling</a></td><td><a href="qnas/027-scrollto-and-programmatic-scrolling.md">Open Q&amp;A</a></td><td><a href="examples/027-scrollto-and-programmatic-scrolling.md">Open example</a></td></tr>
    <tr><td>028</td><td><a href="lessons/028-textplugin-and-splittext.md">TextPlugin and SplitText</a></td><td><a href="qnas/028-textplugin-and-splittext.md">Open Q&amp;A</a></td><td><a href="examples/028-textplugin-and-splittext.md">Open example</a></td></tr>
    <tr><td>029</td><td><a href="lessons/029-draggable-and-interaction.md">Draggable and interaction</a></td><td><a href="qnas/029-draggable-and-interaction.md">Open Q&amp;A</a></td><td><a href="examples/029-draggable-and-interaction.md">Open example</a></td></tr>
    <tr><td>030</td><td><a href="lessons/030-performance-and-debugging.md">Performance and debugging</a></td><td><a href="qnas/030-performance-and-debugging.md">Open Q&amp;A</a></td><td><a href="examples/030-performance-and-debugging.md">Open example</a></td></tr>
    <tr><td>031</td><td><a href="lessons/031-accessibility-and-production-readiness.md">Accessibility and production readiness</a></td><td><a href="qnas/031-accessibility-and-production-readiness.md">Open Q&amp;A</a></td><td><a href="examples/031-accessibility-and-production-readiness.md">Open example</a></td></tr>
    <tr><td>032</td><td><a href="lessons/032-capstone-animated-landing-page.md">Capstone: animated landing page</a></td><td><a href="qnas/032-capstone-animated-landing-page.md">Open Q&amp;A</a></td><td><a href="examples/032-capstone-animated-landing-page.md">Open example</a></td></tr>
  </tbody>
</table>

## Version and scope

The notes focus on the modern GSAP 3 API and browser-based JavaScript. Package examples use ES modules and current npm installation patterns. Plugin APIs and browser behavior can change, so compare your installed version with the official package metadata when applying a lesson to a production project. The lessons avoid assuming that every animation is automatically accessible: motion should respect user preferences and retain usable content when animation is disabled.
