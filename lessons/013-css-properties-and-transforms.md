# 013 - CSS properties and transforms

## Learning goals

- Animate common CSS properties and GSAP transform aliases.
- Use `autoAlpha`, `transformOrigin`, and `clearProps` with an understanding of inline styles.

## Core idea

For DOM targets, GSAP's CSSPlugin animates supported CSS properties. Transform aliases such as `x`, `y`, `xPercent`, `scale`, `rotation`, and `rotationX` make transforms easier to compose than manually editing a CSS transform string.

## How it works

GSAP parses and caches transform components so independent transform values can be composed efficiently. CSS values may include numbers, units, colors, and supported strings. `autoAlpha` combines opacity with visibility for show/hide transitions. `transformOrigin` defines the point around which rotation and scale occur. `clearProps` can remove inline properties when a tween completes.

``js
gsap.to(".card", {
  x: 40,
  y: -12,
  rotation: 2,
  scale: 1.03,
  transformOrigin: "center center",
  duration: 0.5,
  ease: "power2.out",
});
``

Read the code from the target outward: identify the animated value, then the GSAP configuration that controls its start, destination, timing, or lifecycle. In DOM examples, make sure the selected elements exist before this module runs. In object examples, update the visible interface from the changing object value yourself.

## When to use it and its limits

Prefer transform aliases for movement, rotation, and scale. Use `autoAlpha` for elements that should not remain focusable/visible at opacity zero, while ensuring hidden interactive content is also managed semantically. Use `clearProps` when inline styles should be removed after an animation and normal CSS should regain control.

Animating layout properties such as width or position can cause layout work; choose a transform only when it preserves the intended layout. Removing inline styles with `clearProps` can expose different CSS values, so check the resulting state. CSS property support and behavior can vary by element and browser.

## Common mistakes

- Setting `transform` directly in CSS after GSAP has cached transform components and expecting the values to combine as intended.
- Assuming `autoAlpha: 0` removes an element from the accessibility tree in every scenario; manage focus and interaction state too.
- Clearing all props when only one inline property should be removed.
- Animating width/height where a scale transform would provide the same visual effect with less layout work.

## Recap and practice

Animate a card's x, y, rotation, and scale using separate GSAP properties. Change `transformOrigin` and compare. Add `clearProps: "transform"` on completion and inspect computed styles and the visible result.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous lesson</th><th>Chapter Q&amp;A</th><th>Chapter example</th><th>Next lesson</th></tr></thead>
  <tbody><tr><td><a href="012-setting-values-and-quick-methods.md">012 - Setting values and quick methods</a></td><td><a href="../qnas/013-css-properties-and-transforms.md">Q&amp;A</a></td><td><a href="../examples/013-css-properties-and-transforms.md">Example</a></td><td><a href="014-svg-and-attribute-animation.md">014 - SVG and attribute animation</a></td></tr></tbody>
</table>
