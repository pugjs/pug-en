---
title: Includes
template: language
id: language/includes
---

# Includes

Includes allow you to insert the contents of one Pug file into another.

```pug-preview
\\\\\\\\\\ index.pug
//- index.pug
doctype html
html
  include includes/head.pug
  body
    h1 My Site
    p Welcome to my super lame site.
    include includes/foot.pug
\\\\\\\\\\ includes/head.pug
//- includes/head.pug
head
  title My Site
  script(src='/javascripts/jquery.js')
  script(src='/javascripts/app.js')
\\\\\\\\\\ includes/foot.pug
//- includes/foot.pug
footer#footer
  p Copyright (c) foobar
```

If the path is absolute (e.g., `include /root.pug`), it is resolved by prepending `options.basedir` (e.g., `pug.compileFile(path, {basedir: __basedir})`). Otherwise, paths are resolved relative to the current file being compiled.

If no file extension is given, `.pug` is automatically appended to the file name.

## Including Plain Text

Including non-Pug files simply includes their raw text.

```pug-preview
\\\\\\\\\\ index.pug
//- index.pug
doctype html
html
  head
    style
      include style.css
  body
    h1 My Site
    p Welcome to my super lame site.
    script
      include script.js
\\\\\\\\\\ style.css
/* style.css */
h1 {
  color: red;
}
\\\\\\\\\\ script.js
// script.js
console.log('You are awesome');
```

## Including Filtered Text

You can combine filters with includes, allowing you to filter things as you include them.

```pug-preview-readonly
\\\\\\\\\\ index.pug <
//- index.pug
doctype html
html
  head
    title An Article
  body
    include:markdown-it article.md
\\\\\\\\\\ article.md <
# article.md

This is an article written in markdown.
\\\\\\\\\\ output.html >
<!DOCTYPE html>
<html>
  <head>
    <title>An Article</title>
  </head>
  <body>
    <h1>article.md</h1>
    <p>This is an article written in markdown.</p>
  </body>
</html>
```
