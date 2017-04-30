---
title: Tags
template: language
id: language/tags
---

# Tags

By default, text at the start of a line (or after only white space) represents an HTML tag.  Indented tags are nested, creating the tree structure of HTML.

```pug-preview
ul
  li Item A
  li Item B
  li Item C
```

Pug also knows which elements are self-closing:

```pug-preview
img
```

## Block Expansion

To save space, Pug provides an inline syntax for nested tags.

```pug-preview
a: img
```

## Self-Closing Tags

Tags such as `img`, `meta`, and `link` are automatically self-closing (unless you use the XML doctype).  

You can also explicitly self close a tag by appending the `/` character. Only do this if you know what you're doing.

```pug-preview
foo/
foo(bar='baz')/
```

## Rendered Whitespace

Whitespace is removed from the beginning and end of tags, so that you have control over whether the rendered HTML elements touch or not. Whitespace control is generally handled via [plain text](plain-text.html#whitespace-control).
