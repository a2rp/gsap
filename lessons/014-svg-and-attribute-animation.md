# 014 - SVG and attribute animation

## Learning goals

- Animate SVG presentation with GSAP CSS transforms and numeric SVG attributes.
- Distinguish an SVG geometry attribute from a CSS transform property.

## Core idea

GSAP can animate SVG through CSSPlugin and the internal AttrPlugin. Attributes such as `cx`, `cy`, `r`, and `stroke-dashoffset` describe SVG geometry or presentation. CSS transform aliases such as `x`, `y`, and `rotation` transform the rendered SVG element.

## How it works

Put SVG attributes inside `attr: { ... }` when you want to change the actual attribute value. Numeric attributes interpolate between their current and destination numbers. CSS-related properties belong outside `attr`; for example, `x` outside `attr` applies a transform, while `x` inside `attr` changes an SVG geometry coordinate where supported. AttrPlugin is included in GSAP core and does not need separate registration.

```js
const circle = document.querySelector("#orb");

gsap.to(circle, {
  attr: { cx: 260, r: 38 },
  duration: 0.9,
  ease: "power2.inOut",
});

gsap.to(circle, { rotation: 180, transformOrigin: "center center", duration: 1 });
```

Read the code from the target outward: identify the animated value, then the GSAP configuration that controls its start, destination, timing, or lifecycle. In DOM examples, make sure the selected elements exist before this module runs. In object examples, update the visible interface from the changing object value yourself.

## When to use it and its limits

Use attributes when the drawing geometry itself should change, such as moving a circle's center or changing a rectangle's width. Use transforms for moving, rotating, or scaling an element as a visual object. Keep the SVG `viewBox` coordinate system in mind because its units scale independently of CSS pixel dimensions.

Attribute animation does not automatically convert between incompatible units such as pixels and percentages. SVG transform origins have browser-specific details; GSAP's CSSPlugin provides SVG-aware transform handling. Do not animate an attribute and a CSS property with the same visual meaning unintentionally.

## Common mistakes

- Putting CSS `opacity`, `fill`, or transform-related styles into `attr` when they should be CSS properties.
- Confusing `attr: { x: 100 }` with GSAP's `x: 100` transform alias.
- Treating `viewBox` units as CSS pixels.
- Changing the SVG origin without checking how the artwork's coordinate system is authored.

## Recap and practice

Move a circle by changing its `cx` attribute, then separately move it with the GSAP `x` transform property. Compare how the geometry and transform differ. Try rotating a grouped shape around a configured `transformOrigin`.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous lesson</th><th>Chapter Q&amp;A</th><th>Chapter example</th><th>Next lesson</th></tr></thead>
  <tbody><tr><td><a href="013-css-properties-and-transforms.md">013 - CSS properties and transforms</a></td><td><a href="../qnas/014-svg-and-attribute-animation.md">Q&amp;A</a></td><td><a href="../examples/014-svg-and-attribute-animation.md">Example</a></td><td><a href="015-keyframes-modifiers-and-snapping.md">015 - Keyframes, modifiers, and snapping</a></td></tr></tbody>
</table>
