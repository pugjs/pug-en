---
title: Tags
template: language
id: language/tags
---

# Tags

By default, text at the start of a line (or after only white space) represents an html tag.  Indented tags are nested, creating the tree like structure of html.

```pug-preview
ul
  li Item A
  li Item B
  li Item C
```

Pug also knows which elements are self closing:

```pug-preview
img
```

## Block Expansion

To save space, Pug provides an inline syntax for nested tags.

```pug-preview
a: img
```

## Self Closing Tags

Tags such as `img`, `meta`, and `link` are automatically self-closing (unless you use the XML doctype).  You can also explicitly self close a tag by simply appending the `/` character.  Only do this if you know what you're doing.

```pug-preview
foo/
foo(bar='baz')/
```

## Rendered Whitespace For Inline Elements

Inline (as opposed to block-level) HTML elements --- that is, elements that only contain ["phrasing content"](https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/Content_categories#Phrasing_content) --- behave like [plain text](plain-text.html#whitespace-control) in Pug: By default, whitespace is removed at the beginning and end of the line.
