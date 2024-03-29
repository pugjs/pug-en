---
title: Interpolation
template: language
id: language/interpolation
---

<!--
.panel-heading Hey!
.panel-body
  p.
    The Pug source code displayed in this, and many of the other pages
    in these docs, is interactive. Edit it and see what happens!
-->

# Interpolation

Pug provides operators for a variety of your different interpolative needs.

## String Interpolation, Escaped

Consider the placement of the following template's locals: `title`, `author`, and `theGreat`.

```pug-preview
- var title = "On Dogs: Man's Best Friend";
- var author = "enlore";
- var theGreat = "<span>escape!</span>";

h1= title
p Written with love by #{author}
p This will be safe: #{theGreat}
```

`title` follows the basic pattern for evaluating a template local, but the code in between `#{` and `}` is evaluated, escaped, and the result buffered into the output of the template being rendered.

This can be any valid Javascript expression, so you can do whatever feels good.

```pug-preview
- var msg = "not my inside voice";
p This is #{msg.toUpperCase()}
```

Pug is smart enough to figure out where the expression ends, so you can even include `}` without escaping.

```pug-preview
p No escaping for #{'}'}!
```

If you need to include a verbatim `#{`, you can either escape it, or use interpolation. (So meta!)

```pug-preview
p Escaping works with \#{interpolation}
p Interpolation works with #{'#{interpolation}'} too!
```

## String Interpolation, Unescaped

You don't *have* to play it safe. You can buffer unescaped values into your templates, too.

```pug-preview
- var riskyBusiness = "<em>Some of the girls are wearing my mother's clothing.</em>";
.quote
  p Joel: !{riskyBusiness}
```

::: float danger Caution
**Keep in mind that buffering unescaped content into your templates can be mighty risky if that content comes fresh from your users.**  Never trust user input!
:::

## Tag Interpolation

Interpolation works not only on JavaScript values, but on Pug as well. Just use the tag interpolation syntax, like so:

```pug-preview
p.
  This is a very long and boring paragraph that spans multiple lines.
  Suddenly there is a #[strong strongly worded phrase] that cannot be
  #[em ignored].
p.
  And here's an example of an interpolated tag with an attribute:
  #[q(lang="es") ¡Hola Mundo!]
```

You could accomplish the same thing by writing an HTML tag inline with your Pug...but then, what's the point of writing the Pug? Wrap an inline Pug tag declaration in `#[` and `]`, and it'll be evaluated and buffered into the content of its containing tag.

### Whitespace Control

The tag interpolation syntax is especially useful for inline tags, where whitespace before and after the tag is significant. 

By default, however, Pug removes all spaces before and after tags. Check out the following example:

```pug-preview
p
  | If I don't write the paragraph with tag interpolation, tags like
  strong strong
  | and
  em em
  | might produce unexpected results.
p.
  If I do, whitespace is #[strong respected] and #[em everybody] is happy.
```

See the whitespace section in the [Plain Text](plain-text.html#whitespace-control) page for more discussion on this topic.

## Attribute Interpolation

::: float danger Caution
Previous versions of Pug/Jade supported an interpolation syntax such as:

```pug
a(href="/#{url}") Link
```

This syntax is **no longer supported.** Alternatives are found below. (Check our [migration guide] for more information on other incompatibilities between Pug v2 and previous versions.)
:::

Here are some alternatives you can use to include variables in your attribute:

1. Simply write the attribute in JavaScript:

   ```pug-preview
   - var url = 'pug-test.html';
   a(href='/' + url) Link
   |
   |
   - url = 'https://example.com/'
   a(href=url) Another link
   ```

2. If your JavaScript runtime supports ES2015 [template strings] (including Node.js/io.js 1.0.0 and later), you can also use its syntax to simplify your attributes:

   ```pug-preview (features=['templatestrings'])
   - var btnType = 'info'
   - var btnSize = 'lg'
   button(type='button' class='btn btn-' + btnType + ' btn-' + btnSize)
   |
   |
   button(type='button' class=`btn btn-${btnType} btn-${btnSize}`)
   ```
