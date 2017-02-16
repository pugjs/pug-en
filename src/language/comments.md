---
title: Comments
template: language
id: language/comments
---

# Comments

Buffered comments look the same as single-line JavaScript comments. They act sort of like markup tags, producing *HTML* comments in the rendered page. Like tags, buffered comments must appear on their own line.

```pug-preview
// just some paragraphs
p foo
p bar
```

Pug also supports unbuffered comments, by simply adding a hyphen. These are only for commenting on the Pug code itself, and *do not* appear in the rendered HTML.

```pug-preview
//- will not output within markup
p foo
p bar
```

## Block Comments

A block comment is legal as well:

```pug-preview
body
  //-
    Comments for your template writers.
    Use as much text as you want.
  //
    Comments for your HTML readers.
    Use as much text as you want.
```

## Conditional Comments

Pug does not have any special syntax for conditional comments, the peculiar method of adding fallback markup for old versions of Internet Explorer. But since all lines beginning with `<` are treated as [plain text](plain-text.html), normal HTML-style conditional comments will do fine.

```pug-preview
doctype html

<!--[if IE 8]>
<html lang="en" class="lt-ie9">
<![endif]-->
<!--[if gt IE 8]><!-->
<html lang="en">
<!--<![endif]-->

body
  p Supporting old web browsers is a pain.

</html>
```
