# 028 - TextPlugin and SplitText Q&A

## How do TextPlugin and SplitText differ?

TextPlugin changes an element's text content over time. SplitText divides existing text into lines, words, or characters that can be targeted as separate animation units.

## Does TextPlugin animate HTML markup?

No. It replaces text content, so treat its value as text rather than interpolated rich markup.

## What is the TextPlugin delimiter used for?

It controls how the replacement text is divided during the tween. The default is character-based; a space delimiter can progress word by word.

## What does SplitText.create() provide?

It creates wrappers for requested text units and returns an instance with arrays such as words, chars, and lines that can be used as tween targets.

## Why can line splitting change after resize?

Lines are determined by browser layout. A different container width, font, or font load can change where the lines wrap.

## How should a SplitText instance be cleaned up?

Call its revert() method when the view is disposed so the original text structure is restored and generated wrappers are removed.

## How can text animation remain accessible?

Keep the complete meaningful text available in the reading order. Use splitting as a visual treatment and prevent assistive technology from receiving a confusing series of decorative character fragments.

## Chapter navigation

<table width="100%">
  <thead><tr><th>Previous Q&amp;A</th><th>Chapter lesson</th><th>Chapter example</th><th>Next Q&amp;A</th></tr></thead>
  <tbody><tr><td><a href="027-scrollto-and-programmatic-scrolling.md">027 - ScrollTo and programmatic scrolling Q&amp;A</a></td><td><a href="../lessons/028-textplugin-and-splittext.md">Lesson</a></td><td><a href="../examples/028-textplugin-and-splittext.md">Example</a></td><td><a href="029-draggable-and-interaction.md">029 - Draggable and interaction Q&amp;A</a></td></tr></tbody>
</table>
