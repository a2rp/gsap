# 004 - gsap.from() and gsap.fromTo()

## Learning goals

- Explain how `from()` uses supplied values as the start and reads the end from the target.
- Use `fromTo()` when both ends need explicit values and understand `immediateRender`.

## Core idea

`gsap.from()` starts at values provided in its vars object and animates toward the target's current values. `gsap.fromTo()` receives separate start and destination objects, so it makes both sides explicit.

## How it works

A `from()` tween is conceptually a `to()` tween with the playhead moving from an explicitly supplied state toward the state GSAP reads from the target. This makes it convenient for entrances. `from()` and `fromTo()` commonly render their starting values immediately. In timelines, that can make an element appear hidden before its scheduled position; `immediateRender: false` can defer that initial write when appropriate.

```js
gsap.from(".card", {
  y: 24,
  autoAlpha: 0,
  duration: 0.6,
  stagger: 0.15,
});

gsap.fromTo(".notice",
  { scale: 0.9, autoAlpha: 0 },
  { scale: 1, autoAlpha: 1, duration: 0.35, ease: "back.out(1.4)" }
);
```

Read the code from the target outward: identify the animated value, then the GSAP configuration that controls its start, destination, timing, or lifecycle. In DOM examples, make sure the selected elements exist before this module runs. In object examples, update the visible interface from the changing object value yourself.

## When to use it and its limits

Use `from()` for a brief entrance when the final appearance is already defined by CSS. Use `fromTo()` when a deterministic start and end are both required, such as repeated UI states or when multiple sources can affect initial styles.

A `from()` tween can overwrite a visible state as soon as it is created. This can cause flashes, especially if the page first paints before JavaScript runs. Explicit endpoints still need valid CSS properties and should not conflict with other animations.

## Common mistakes

- Assuming `from()` waits until its timeline position before applying the start values.
- Creating a `from()` tween before checking the element's intended final style.
- Using `fromTo()` everywhere even when the current style is the correct destination.
- Forgetting that `fromTo()` places special options such as `duration` and `ease` in the destination vars object.

## Recap and practice

Create two cards with their final styles in CSS. Animate one with `from()` and one with `fromTo()`. Put each in a timeline after a delay and compare the initial render. Then test `immediateRender: false` on the delayed entrance.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous lesson</th><th>Chapter Q&amp;A</th><th>Chapter example</th><th>Next lesson</th></tr></thead>
  <tbody><tr><td><a href="003-tweens-with-gsap-to.md">003 - Tweens with gsap.to()</a></td><td><a href="../qnas/004-gsap-from-and-fromto.md">Q&amp;A</a></td><td><a href="../examples/004-gsap-from-and-fromto.md">Example</a></td><td><a href="005-timing-easing-and-repeats.md">005 - Timing, easing, and repeats</a></td></tr></tbody>
</table>
