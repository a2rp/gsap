# GSAP Keywords and Concepts

A searchable index of GSAP 3 APIs and animation concepts used in this course. These are JavaScript library APIs and browser concepts, not JavaScript reserved words. For full explanations, follow the linked lesson.

## Core animation terms

| Term | Meaning |
| --- | --- |
| Animation | Base type behind tweens and timelines. It exposes playback state and methods such as `play()`, `pause()`, `reverse()`, `progress()`, and `timeScale()`. See [timeline fundamentals](lessons/008-timeline-fundamentals.md). |
| Tween | Animation from one set of property values to another over time. |
| Target | DOM element, selector string, array, NodeList, or JavaScript object whose properties are animated. See [targets and dynamic values](lessons/006-targets-and-dynamic-values.md). |
| Vars | Configuration object passed to a tween or timeline. It contains animated properties and special options such as `duration`, `ease`, and callbacks. |
| `gsap.to()` | Animates from the target's current values to destination values. See [tweens with gsap.to()](lessons/003-tweens-with-gsap-to.md). |
| `gsap.from()` | Animates from specified values toward the target's current values. Its immediate render behavior can affect initial styles. See [from() and fromTo()](lessons/004-gsap-from-and-fromto.md). |
| `gsap.fromTo()` | Defines both explicit start values and destination values. |
| `gsap.set()` | Applies values immediately using a zero-duration tween. See [setting values](lessons/012-setting-values-and-quick-methods.md). |
| `duration` | Time in seconds for a tween's active iteration. A timeline's total duration also depends on positions, repeats, and repeat delays. |
| `delay` | Wait before an animation starts. For multi-step sequences, a timeline is usually easier to revise than many delays. |
| `ease` | Function or named curve that maps linear progress to perceived motion. Common names include `none`, `power1.out`, `power2.inOut`, `back.out`, `bounce.out`, and `elastic.out`. |
| `repeat` | Number of additional iterations. `repeat: 1` means two total iterations; `repeat: -1` loops indefinitely. |
| `repeatDelay` | Pause in seconds between repeat iterations. |
| `yoyo` | Reverses direction on alternating repeat iterations. It has no effect without repeats. |
| `yoyoEase` | Controls easing on alternating yoyo iterations. |
| `easeReverse` | GSAP 3.15 feature for choosing easing when an animation playhead reverses direction. Check version before using it in older projects. |
| `stagger` | Delays the start for each target in a multi-target tween. It can be a number or a configuration object. See [staggers](lessons/007-staggers-and-distribution.md). |
| `immediateRender` | Controls whether a tween renders its starting state immediately. It is especially relevant to `from()` tweens and timeline insertion. |
| `overwrite` | Controls how a new tween interacts with other tweens affecting the same target and properties. |
| `invalidate()` | Clears recorded start/end values so they can be recalculated on a later render. Useful with dynamic values and refresh-driven animations. |

## Timeline terms

| Term | Meaning |
| --- | --- |
| Timeline | Container that sequences, overlaps, nests, and controls tweens as one animation. See [timeline fundamentals](lessons/008-timeline-fundamentals.md). |
| `gsap.timeline()` | Creates a timeline, optionally with defaults, repeat settings, callbacks, and paused state. |
| Position parameter | Optional final argument on timeline methods that places an item at a time, label, or relative offset. See [position parameter](lessons/009-timeline-position-parameter.md). |
| `"<"` | Position shorthand for the start of the previous child animation. |
| `">"` | Position shorthand for the end of the previous child animation. |
| `"+=1"` | One second after the current end of the timeline. `"-=0.25"` overlaps the end by a quarter second. |
| Label | Named timeline position added with `addLabel()` and used for placement, seeking, or snapping. |
| Nested timeline | Timeline added as a child of another timeline, allowing a reusable sequence to be controlled as a unit. |
| `play()` / `pause()` | Start or stop playhead movement. |
| `resume()` / `reverse()` | Continue in the current direction or move the playhead backward. |
| `restart()` / `seek()` | Start over or jump to a time/label. |
| `progress()` / `totalProgress()` | Read or set normalized progress from 0 to 1, with or without repeats included. |
| `timeScale()` | Read or set playback speed. `2` is twice normal speed; `0.5` is half speed. |
| `addPause()` | Inserts a pause at a timeline position, optionally invoking a callback. |
| `then()` | Returns a promise that resolves when the animation completes. Repeating animations need special consideration because they may not complete. |

## Tween values and browser properties

| Term | Meaning |
| --- | --- |
| Function-based value | Function evaluated for a target to compute a property value. It receives the target index, target, and target collection. |
| Relative value | String such as `"+=20"` or `"-=20"` that offsets the current value. |
| Random value | String syntax such as `"random(0, 100)"` or `"random([red, blue])"`, or the `gsap.utils.random()` helper. |
| CSSPlugin | Core plugin that handles CSS properties and transforms for DOM elements. It is included with GSAP. |
| Transform aliases | GSAP properties such as `x`, `y`, `xPercent`, `rotation`, `scale`, `scaleX`, and `transformOrigin`. |
| `autoAlpha` | Convenience property that combines opacity and visibility, useful for showing/hiding elements. |
| `clearProps` | Special CSSPlugin property used to remove inline styles when a tween completes or reaches its configured clear point. |
| Attribute animation | Use `attr: { ... }` to animate SVG or DOM attributes such as `cx`, `r`, or `viewBox` values. |
| SVG origin | SVG transforms have coordinate-system details. GSAP provides SVG-aware transform handling; choose and verify the correct transform origin. See [SVG animation](lessons/014-svg-and-attribute-animation.md). |
| Keyframes | Multiple property states expressed in one tween's `keyframes` configuration. |
| Modifier | A function applied to a value on each render, useful for wrapping, quantizing, or constraining values. |
| Snap | Rounds values to a step or selected values using the tween's `snap` option or a utility helper. |
| `quickSetter()` | Optimized setter for repeatedly writing one property to one or more targets. |
| `quickTo()` | Reusable tween-based setter that smoothly retargets a property, useful for pointer-following motion. |
| Ticker | GSAP's requestAnimationFrame-based update loop for callbacks that must stay synchronized with animation rendering. |

## Utilities and reusable animation

| Term | Meaning |
| --- | --- |
| `gsap.utils.clamp()` | Constrains a value to a minimum and maximum. |
| `gsap.utils.mapRange()` | Maps a value from one numeric range to another. |
| `gsap.utils.normalize()` | Converts a value in a range into normalized progress from 0 to 1. |
| `gsap.utils.interpolate()` | Interpolates between values, arrays, or supported color/string values. |
| `gsap.utils.wrap()` / `wrapYoyo()` | Maps values into a repeating range, with or without alternating direction. |
| `gsap.utils.snap()` | Returns a function that snaps values to a numeric increment or configured points. |
| `gsap.utils.distribute()` | Produces values distributed across a set of targets. Commonly used for stagger patterns. |
| `gsap.registerEffect()` | Defines a named reusable animation effect that can be invoked through `gsap.effects`. |

## Lifecycle and responsive setup

| Term | Meaning |
| --- | --- |
| `gsap.context()` | Collects GSAP animations created in a scope and can revert them together. It can also scope selector text to a root element. See [context and cleanup](lessons/017-context-cleanup-and-reversion.md). |
| `revert()` | Restores animation-related inline styles and kills collected animations in a context or media-query setup. |
| `contextSafe()` | Marks delayed/event-handler animation creation as belonging to a context when using `@gsap/react`. |
| `gsap.matchMedia()` | Runs animation setup for matching media queries and reverts it when conditions stop matching. It can read `prefers-reduced-motion`. |
| `prefers-reduced-motion` | Operating-system/browser preference exposed as a CSS/JS media query. Use it to reduce or remove nonessential motion. |
| `useGSAP()` | React hook from `@gsap/react` for scoped animation setup and automatic cleanup. See [GSAP in React](lessons/019-gsap-in-react-with-usegsap.md). |
| Plugin registration | `gsap.registerPlugin(Plugin)` makes a plugin available and protects it from bundler tree-shaking. |

## Scroll and interaction plugins

| Term | Meaning |
| --- | --- |
| ScrollTrigger | Plugin for activating, scrubbing, pinning, snapping, or observing animations according to scroll positions. See [fundamentals](lessons/020-scrolltrigger-fundamentals.md). |
| `trigger` | Element whose document-flow position is used to calculate a ScrollTrigger's start and end. |
| `start` / `end` | Positions that define when a ScrollTrigger becomes active and when it finishes. |
| `scrub` | Links animation progress to scroll progress. A number adds catch-up smoothing. |
| `pin` | Holds an element in place while the configured scroll range passes. |
| `toggleActions` | Four actions for enter, leave, enter-back, and leave-back boundaries. |
| `markers` | Development visuals for inspecting calculated trigger boundaries. |
| `refresh()` | Recalculates trigger positions after layout changes. |
| `Observer` | Plugin for unified pointer, touch, wheel, and scroll gesture callbacks. |
| `Flip` | Plugin that records layout state, applies a DOM/style change, then animates between the two states. |
| `MotionPathPlugin` | Plugin that animates a target along a path and can align its rotation to that path. |
| `ScrollToPlugin` | Plugin for animating a window or element scroll position. |
| `TextPlugin` | Plugin that interpolates text content in a target. It is not a substitute for accessible semantic content. |
| `SplitText` | Plugin that splits text into lines, words, or characters for animation and can re-split on responsive changes. Preserve a usable text experience when animation is unavailable. |
| `Draggable` | Plugin for making elements respond to pointer/touch dragging with configurable bounds and callbacks. |

## Troubleshooting vocabulary

| Term | Meaning |
| --- | --- |
| Flash of hidden content | Visible initial state appears before a `from()` tween initializes. Set intentional CSS baseline styles and review `immediateRender`. |
| Layout shift | Document geometry changes unexpectedly, often because animated layout properties or pin spacing affect normal flow. |
| Transform cache | GSAP caches transform components for efficient updates. Prefer GSAP transform properties consistently instead of mixing direct style writes mid-animation. |
| Tree-shaking | Bundler removes code it thinks is unused. Explicitly import and register GSAP plugins. |
| Stale start values | A tween retains values captured earlier. Use function-based values, invalidate when appropriate, or recreate the animation after layout changes. |
| Cleanup leak | Event handlers, timelines, or ScrollTriggers continue after a component is removed. Scope and revert animations during lifecycle cleanup. |
| Scrub duration | With numeric `scrub`, the animation playhead catches up over that many seconds; it is not the scroll range length. |
| Reduced motion | A request to remove/reduce motion. Preserve meaning and interaction if an animation is skipped. |

## Lesson index

- [Core, tweens, and timelines](lessons/001-gsap-and-animation-fundamentals.md)
- [Responsive, cleanup, and React](lessons/017-context-cleanup-and-reversion.md)
- [ScrollTrigger and plugins](lessons/020-scrolltrigger-fundamentals.md)
- [Performance and production](lessons/030-performance-and-debugging.md)
