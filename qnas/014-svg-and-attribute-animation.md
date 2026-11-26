# 014 - SVG and attribute animation Q&A

## Does the `attr` object need a plugin registration?

No. AttrPlugin is an internal plugin included in GSAP core. Numeric DOM/SVG attributes can be animated with `attr: { ... }` without separately importing or registering it.

## What is the difference between `attr: { x: 100 }` and `x: 100`?

Inside `attr`, `x` changes the element's SVG attribute where applicable. Outside `attr`, `x` is GSAP's CSS transform alias and visually translates the element.

## Can I animate every SVG property with `attr`?

You can animate DOM attributes supported as interpolable values, especially numeric geometry attributes. CSS-related presentation belongs in normal vars, and some attributes have formats or unit changes that cannot interpolate cleanly.

## Why does changing `cx` look different from using `x`?

`cx` changes a circle's geometry center in the SVG coordinate system. `x` applies a transform to the rendered element, leaving the original geometry values unchanged.

## What does `viewBox` change?

It defines the SVG's internal coordinate rectangle and how that rectangle maps to the rendered viewport. A coordinate such as `cx: 100` is in the SVG's user space, not necessarily 100 CSS pixels.

## How should I set an SVG transform origin?

Use GSAP's SVG-aware transform support and test the chosen origin against the artwork. `transformOrigin` works with SVG elements; `svgOrigin` can define a point in the SVG canvas coordinate system when that behavior is needed.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous Q&amp;A</th><th>Chapter lesson</th><th>Chapter example</th><th>Next Q&amp;A</th></tr></thead>
  <tbody><tr><td><a href="013-css-properties-and-transforms.md">013 - CSS properties and transforms Q&amp;A</a></td><td><a href="../lessons/014-svg-and-attribute-animation.md">Lesson</a></td><td><a href="../examples/014-svg-and-attribute-animation.md">Example</a></td><td><a href="015-keyframes-modifiers-and-snapping.md">015 - Keyframes, modifiers, and snapping Q&amp;A</a></td></tr></tbody>
</table>
