# 028 - TextPlugin and SplitText

## Learning goals

Choose TextPlugin for text replacement and SplitText for per-unit animation. Register text plugins and configure their options deliberately. Preserve readable text, responsive layout, and cleanup when splitting animated text.

## Core idea

TextPlugin tween-replaces an element's text content over time. SplitText divides existing text into lines, words, or characters so GSAP can target those elements. They solve different problems: replacement versus animated pieces.

## How it works

Register each plugin used by the page. TextPlugin accepts a string or an object with value and options such as delimiter; the default progression is character-based and a space delimiter can reveal words. SplitText.create() returns a SplitText instance with arrays such as chars, words, and lines. Create the split after the intended font is available, animate only the needed units, and call revert() during teardown. Text layout can change with width and font loading, so responsive splitting must be rebuilt or use supported autoSplit behavior. Keep the original full text in the DOM's accessible reading flow and avoid exposing a confusing sequence of decorative character nodes to assistive technology.

``js
import { gsap } from "gsap";
import { TextPlugin } from "gsap/TextPlugin";
import { SplitText } from "gsap/SplitText";

gsap.registerPlugin(TextPlugin, SplitText);

const status = document.querySelector("[data-status]");
const heading = document.querySelector("[data-heading]");

if (status) {
  gsap.to(status, {
    duration: 1.2,
    ease: "none",
    text: { value: "Ready to explore", delimiter: " " }
  });
}

if (heading) {
  const split = SplitText.create(heading, { type: "words" });
  gsap.from(split.words, {
    duration: 0.45,
    y: 18,
    autoAlpha: 0,
    stagger: 0.08,
    ease: "power2.out"
  });

  // When this view is removed, revert the split and its generated wrappers.
  // split.revert();
``

Read the code from the target outward: identify the animated value, then the GSAP configuration that controls its start, destination, timing, or lifecycle. In DOM examples, make sure the selected elements exist before this module runs. In object examples, update the visible interface from the changing object value yourself.

## When to use it and its limits

Use TextPlugin for a short status or label that changes from one string to another. Use SplitText when the design needs separate word or line targets for a stagger. Prefer splitting words or lines over individual characters when that achieves the design. If the animation is decorative, give assistive technology a stable full-text equivalent and avoid announcing every animated unit.

TextPlugin replaces text content; it is not a rich text or HTML interpolation tool. SplitText creates DOM wrappers and its line grouping depends on rendered layout. Font loading, responsive width, and localization can change line breaks. Generated wrappers need to be reverted when their view is disposed. Do not assume text rendered as many visual nodes has the same accessibility or selection behavior as the original single text node.

## Common mistakes

Using TextPlugin as if it interpolates HTML; splitting before the final font loads; keeping split wrappers after component teardown; animating every character when a word stagger would work; treating generated visual spans as the accessible source of truth; registering no plugin imports in a bundler setup.

## Recap and practice

Animate a loading label with TextPlugin, then reveal a short headline by word with SplitText. Resize the page, change the font loading order, and navigate away and back. Confirm that the complete text remains understandable and that generated wrappers are cleaned up.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous lesson</th><th>Chapter Q&amp;A</th><th>Chapter example</th><th>Next lesson</th></tr></thead>
  <tbody><tr><td><a href="027-scrollto-and-programmatic-scrolling.md">027 - ScrollTo and programmatic scrolling</a></td><td><a href="../qnas/028-textplugin-and-splittext.md">Q&amp;A</a></td><td><a href="../examples/028-textplugin-and-splittext.md">Example</a></td><td><a href="029-draggable-and-interaction.md">029 - Draggable and interaction</a></td></tr></tbody>
</table>
