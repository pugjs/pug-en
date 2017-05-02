---
title: Code
template: language
id: language/code
---

# Code

Pug allows you to write inline JavaScript code in your templates. There are three types of code: Unbuffered, Buffered, and Unescaped Buffered.

## Unbuffered Code

Unbuffered code starts with `-`. It does not directly add anything to the output.

```pug-preview
- for (var x = 0; x < 3; x++)
  li item
```

Pug also supports block unbuffered code:

```pug-preview
-
  var list = ["Uno", "Dos", "Tres",
          "Cuatro", "Cinco", "Seis"]
each item in list
  li= item
```

## Buffered Code

Buffered code starts with `=`. It evaluates the JavaScript expression and outputs the result. For security, buffered code is first HTML escaped.

```pug-preview
p
  = 'This code is <escaped>!'
```

It can also be written inline with attributes, and supports the full range of JavaScript expressions:

```pug-preview
p= 'This code is' + ' <escaped>!'
```

## Unescaped Buffered Code

Unescaped buffered code starts with `!=`. It evaluates the JavaScript expression and outputs the result. Unescaped buffered code does not perform any escaping, so is unsafe for user input:

```pug-preview
p
  != 'This code is <strong>not</strong> escaped!'
```

Unescaped buffered code can also be written inline with attributes, and supports the full range of JavaScript expressions:

```pug-preview
p!= 'This code is' + ' <strong>not</strong> escaped!'
```

::: float danger Caution
**Unescaped buffered code can be dangerous.** You must be sure to sanitize any user
inputs to avoid [cross-site scripting] (XSS).
:::

[cross-site scripting]: https://en.wikipedia.org/wiki/Cross-site_scripting
