---
layout: post
title:      "Building a Creatively Styled Quiz App"
date:       2021-03-01 17:34:40 +0000
permalink:  building_a_creatively_styled_quiz_app
---

*Using some css styling that I haven't used before.*

Using :root { 

The :root CSS pseudo-class matches the root element of a tree representing the document. In HTML, :root represents the <html> element and is identical to the selector html, except that its specificity is higher.

*, *::before, *::after {

The ::before and ::after pseudo-elements in CSS allows you to insert content onto a page without it needing to be in the HTML. While the end result is not actually in the DOM, it appears on the page as if it is, and would essentially be like this:

```
div::before {
  content: "before";
}
div::after {
  content: "after";
}
<div>
  before
  <!-- Rest of stuff inside the div -->
  after
</div>
```

Using --hue-neutral, --hue-wrong, and --hue-correct and The hue-rotate() CSS function rotates the hue of an element and its contents. Its result is a <filter-function>.




