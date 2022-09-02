---
title: Migrating to Pug 3 (from Pug 2)
template: generic
id: api/migration-v3
---

# Migrating to Pug 3 (from Pug 2)

If you are migrating from Jade, please follow the [Migrating to Pug 2](migration-v2.html) article first. This article covers how to upgrade from Pug 2 to Pug 3.

For a complete list of new features, please refer to [the release notes](https://github.com/pugjs/pug/releases/tag/pug%403.0.0). What follows are instructions for dealing with breaking changes only.

## filters with `minify`

::: float warning Note
If you are not using filters with the "minify" option, you can ignore this change.
:::

If you were using filters that output JavaScript or CSS, along with the `minify` option, you now need to include an extra dependency. If you want to support minifying JavaScript, you must install `jstransformer-uglify-js` and if you want to support minifying CSS, you must install `jstransformer-clean-css`.

## `read` plugins should now return `Buffer`

::: float warning Note
If you are not using plugins, you can ignore this change. 
:::

If you are using a `read` plugin to override the way that pug reads files, and you want to support the new `renderBuffer` filters, you will need to return `Buffer`.

e.g.

```pug-preview-readonly
\\\\\\\\\\ old.js <
//- old

pug.renderFile(filename, {
  plugins: [
    {
      read: (filename) => {
        // this returns a "string"
        return fs.readFileSync(filename, 'utf8');
      },
    }
  ]
})
\\\\\\\\\\ new.js >
//- new

pug.renderFile(filename, {
  plugins: [
    {
      read: (filename) => {
        // this returns a "Buffer"
        return fs.readFileSync(filename);
      },
    }
  ]
})
```

## Node.js Support

We dropped support for node versions prior to 10.0.0. We recommend upgrading all projects using pug to node.js 12, but we will support 10 until April 2021.

In future we may drop support for node versions [when they reach end of life](https://github.com/nodejs/Release) without a major version bump.
