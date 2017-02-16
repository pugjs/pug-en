---
title: Plain Text
template: language
id: language/plain-text
---

# Plain Text

Pug provides four ways of getting *plain text* --- that is, any code or text content that should go, mostly unprocessed, directly into the rendered HTML. They are useful in different situations. Plain text does still use tag and string [interpolation](interpolation.html), but the first word on the line is not a Pug tag. And because plain text is not escaped, you can also include literal HTML.

One common pitfall here is managing whitespace in the rendered HTML. We will talk about that at the end of this page.

## Inline in a Tag

The easiest way to add plain text is *inline*. The first term on the line is the tag itself. Everything after the tag and one space will be the text contents of that tag. This is most useful when the plain text content is short (or if you don't mind lines running long).

```pug-preview
p This is plain old <em>text</em> content.
```

## Literal HTML

Whole lines are also treated as plain text when they begin with a left angle bracket (`<`), which may occasionally be useful for writing literal HTML tags in places that could otherwise be inconvenient. For example, one use case is [conditional comments](comments.html#conditional-comments). Since literal HTML tags do not get processed, they do not self-close, unlike Pug tags.

```pug-preview
<html>

body
  p Indenting the body tag here would make no difference.
  p HTML itself isn't whitespace-sensitive.

</html>
```

## Piped Text

Another way to add plain text to templates is to prefix a line with a pipe character (`|`). This method is useful for mixing plain text with inline tags, as we discuss later in the Whitespace Control section.

```pug-preview
p
  | The pipe always goes at the beginning of its own line,
  | not counting indentation.
```

## Block in a Tag

Often you might want large blocks of text within a tag.  A good example is writing JavaScript and CSS code in the `script` and `style` tags.  To do this, just add a `.` right after the tag name, or after the closing parenthesis, if the tag has [attributes](attributes.html). There should be no space between the tag and the dot. Plain text contents of the tag must be indented one level:

```pug-preview
script.
  if (usingPug)
    console.log('you are awesome')
  else
    console.log('use pug')
```

You can also create a dot block of plain text *after* other tags within the parent tag.

```pug-preview
div
  p This text belongs to the paragraph tag.
  br
  .
    This text belongs to the div tag.
```

## Whitespace Control

Managing the whitespace of the rendered HTML is the trickiest part about learning Pug. By default, Pug removes spaces from the beginning and end of the lines for both inline-level tags and plain text lines and blocks. The value here is that it gives you full control over whether inline tags and/or plain text should touch. It even lets you place tags in the middle of words.

```pug-preview
| You put the em
em pha
| sis on the wrong syl
em la
| ble.
```

The trade-off is that it *requires* you to think about and take control over whether tags and text touch. Don't worry, though, you'll get the hang of it soon enough.

If you need the text and/or inline-level tags to touch --- perhaps you need a period to appear outside the hyperlink at the end of a sentence --- this is easy, as it's basically what happens unless you tell Pug otherwise.

```pug-preview
a ...sentence ending with a link
| .
```

If you need to *add* space, you have a few options:

Depending on where you need the whitespace, you could add an extra space at the beginning of the plain text line (after the pipe for piped text). Or you could add a trailing space at the *end* of the plain text line. Less often, you might need extra space *inside the tag*, but it's the same idea --- extra spaces at the beginning of the text (after the tag), or at the end of the line. This may require configuring your code editor *not* to strip trailing spaces when you save, and you will need to make sure all contributors to your project do the same.

**NOTE** the trailing and leading spaces here:

```pug-preview
| Hey, check out 
a(href="http://example.biz/kitteh.png") this picture
|  of my cat!
```

You could add one or more "empty" piped line --- a pipe with either spaces or nothing after it. This will insert whitespace in the rendered HTML.

```pug-preview
| Don't
|
em touch
|
| me!
```

Another trick is to use string [interpolation](interpolation.html): `=` can be used to add a literal space or newline character to the rendered HTML.

```pug-preview
p
  | space
  = " "
  | space
p
  | line
  = "\n"
  | line
```

Especially if your inline tags don't require many attributes, you may find it easiest to use tag interpolation, or literal HTML, within a plain text *block*.

```pug-preview
p.
  Using regular tags helps keep your lines short,
  but interpolated tags may be easier to #[em visualize]
  whether the tags and text are whitespace-separated.
```
