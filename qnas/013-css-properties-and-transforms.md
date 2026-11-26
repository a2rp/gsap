# 013 - CSS properties and transforms Q&A

## Why use `x` instead of `transform: "translateX(...)"`?

GSAP transform aliases let you animate individual transform components and combine them consistently. They also work with GSAP's transform parsing and caching.

## What does `autoAlpha` do?

It combines opacity with visibility so an element can become invisible at zero opacity and visible again when opacity increases. It is useful for presentation, but interactive content may also need focus and pointer state management.

## Can GSAP animate color values?

Yes, CSSPlugin supports common color formats and interpolates between them. Use consistent, valid color values and avoid expecting arbitrary CSS tokens to interpolate unless they resolve to supported values.

## What does `clearProps` remove?

It removes specified inline style properties when configured on a tween. Use a targeted list such as `"transform,opacity"` when only those properties should be cleared.

## Why does CSS `transform` conflict with GSAP `x`?

Both affect the same transform declaration. If direct CSS writes change transforms while GSAP holds cached components, the values can conflict. Prefer GSAP transform aliases for animated transforms and use `clearProps` or context reversion when restoring CSS.

## Should every animation use transforms?

No. Use transforms when they preserve the design and avoid unnecessary layout. A real layout change may require animating layout properties or using a FLIP-style transition, which is covered later.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous Q&amp;A</th><th>Chapter lesson</th><th>Chapter example</th><th>Next Q&amp;A</th></tr></thead>
  <tbody><tr><td><a href="012-setting-values-and-quick-methods.md">012 - Setting values and quick methods Q&amp;A</a></td><td><a href="../lessons/013-css-properties-and-transforms.md">Lesson</a></td><td><a href="../examples/013-css-properties-and-transforms.md">Example</a></td><td><a href="014-svg-and-attribute-animation.md">014 - SVG and attribute animation Q&amp;A</a></td></tr></tbody>
</table>
