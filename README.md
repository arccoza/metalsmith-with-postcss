# Metalsmith with PostCSS

A Metalsmith plugin for [PostCSS](https://github.com/postcss/postcss/).

## Explanation
Use PostCSS and PostCSS plugins with Metalsmith.

## Install

`npm install metalsmith-with-postcss --save`

## Example

metalsmith.json config example:
```js
{
  "plugins": {
    "metalsmith-with-postcss": {
      pattern: ['**/*.css', '!**/_*/*', '!**/_*'], //This is the default.
      plugins: {
        'postcss-import': {},
        'postcss-if-media': {},
        'postcss-custom-media': {},
        'postcss-media-minmax': {},
        'postcss-layout': {},
        'postcss-aspect-ratio': {},
        'autoprefixer': {}
      }
    }
  }
}
```

Build script example:
```js
var metalsmith = require('metalsmith');
var markdown = require('metalsmith-markdown');
var postcss = require('metalsmith-with-postcss');


metalsmith(__dirname)
  .source('src')
  .destination('pub')
  .use(postcss({
    pattern: ['**/*.css', '!**/_*/*', '!**/_*'], //This is the default.
    plugins: {
      'postcss-import': {},
      'postcss-if-media': {},
      'postcss-custom-media': {},
      'postcss-media-minmax': {},
      'postcss-layout': {},
      'postcss-aspect-ratio': {},
      'autoprefixer': {}
    }
  }))
  .use(markdown({
    gfm: true,
    tables: true
  }))
  .build(function (err) {
    if (err) {
      throw err;
    }
  });
  
```

## Options

  - `pattern`
    - __Default value:__ `['**/*.css', '!**/_*/*', '!**/_*']`
    - __Description:__ Only process files that match this pattern, can be an array of multiple patterns, following [multimatch](https://github.com/sindresorhus/multimatch) rules. The default patterns exclude any files or folders prefixed with an underscore.
  - `plugins`
    - __Default value:__ {}
    - __Description:__ A collection of plugin module names as keys and any options for them as values.
  - `map`
    - __Default value:__ {inline: true}
    - __Description:__ Source mapping options passed directly to PostCSS.
