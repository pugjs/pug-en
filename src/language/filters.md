---
title: Filters
template: language
id: language/filters
extraScripts:
  - /js/filters.js
---

# Filters

Filters let you use other languages in Pug templates.  They take a block of plain text as an input. 

To pass options to the filter, add them inside parentheses after the filter name (just as you would do with [tag attributes]): `:less(ieCompat=false)`.

All [JSTransformer modules] can be used as Pug filters. Popular filters include `:babel`, `:uglify-js`, `:scss`, and `:markdown-it`. Check out the documentation for the JSTransformer for the options supported for the specific filter. 

If you can't find an appropriate filter for your use case, you can write your own [custom filter].

For example, if you want to be able to use CoffeeScript and Markdown (using Markdown-it renderer) in your Pug template, you would first make sure that these features are installed:

```sh
$ npm install --save jstransformer-coffee-script
$ npm install --save jstransformer-markdown-it
```

Now, you should be able to render the following template:

~~~pug-preview
:markdown-it(linkify langPrefix='highlight-')
  # Markdown

  Markdown document with http://links.com and

  ```js
  var codeBlocks;
  ```
script
  :coffee-script
    console.log 'This is coffee script'
~~~

::: float warning Warning
**Filters are rendered at compile time.**  This makes them fast, but it also means that they cannot support dynamic content or options.

By default, compilation in the browser does not have access to JSTransformer-based filters, unless the JSTransformer modules are explicitly packed and made available through a CommonJS platform (such as Browserify or Webpack). In fact, the page you are reading right now uses Browserify to make the filters available in the browser.

Templates pre-compiled on the server do not have this limitation.
:::

## Inline Syntax

If the content of the filter is short, one can even use filters as if they are tags:

```pug-preview
p
  :markdown-it(inline) **BOLD TEXT**

p.
  In the midst of a large amount of plain
  text, suddenly a wild #[:markdown-it(inline) *Markdown*]
  appeared.
```

## Filtered Includes

You can also apply filters to external files, using the [include syntax](includes.html#including-filtered-text).

## Nested Filters

You can apply multiple filters on the same block of text. To do so, simply specify the filters on the same line. 

The filters are applied in reverse order. The text is first passed to the last filter; then, the result is passed to the second last filter, and so on.

In the following example, the script is first transformed by `babel`, and then by `cdata-js`.

```pug-preview
script
  :cdata-js:babel(presets=['es2015'])
    const myFunc = () => `This is ES2015 in a CD${'ATA'}`;
```

## Custom Filters

You can add your own filters to Pug via the [`filters` option][options].

```pug-preview-readonly demo
\\\\\\\\\\ options.js <
options.filters = {
  'my-own-filter': function (text, options) {
    if (options.addStart) text = 'Start\n' + text;
    if (options.addEnd)   text = text + '\nEnd';
    return text;
  }
};
\\\\\\\\\\ index.pug <
p
  :my-own-filter(addStart addEnd)
    Filter
    Body
\\\\\\\\\\ output.html >
<p>
  Start
  Filter
  Body
  End
</p>
```

[tag attributes]: attributes.html
[options]: ../api/reference.html#options
[JSTransformer modules]: https://www.npmjs.com/browse/keyword/jstransformer
[custom filter]: #custom-filters
