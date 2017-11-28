# Javascript API

Start by installing Purgecss as a development dependency.

```
npm i -D purgecss
```

You can then use purgecss inside a javascript file.

## ES6 with import

```js
import Purgecss from 'purgecss'
const purgeCss = new Purgecss({
  content: ['**/*.html'],
  css: ['**/*.css']
})
const purgecssResult = purgecss.purge()
```

## ES5 with require

```js
var Purgecss = require('purgecss')
var purgecss = new Purgecss({
  content: ['**/*.html'],
  css: ['**/*.css']
})
var purgecssResult = purgecss.purge()
```

## Options

```
{
  content: Array<string | RawContent>,
  css: Array<string>,
  extractors?: Array<ExtractorsObj>,
  whitelist?: Array<string>,
  whitelistPatterns?: Array<RegExp>,
  stdin?: boolean,
}
```

* #### content

You can specified the content with an array of filename or glob \(see link\) that should be analyized by purgecss. The files can be html, pug, blade, ... files.

```js
new Purgecss({
    content: ['index.html', `**/*.js`, '**/*.html', '**/*.vue'],
    css: [`css/app.css`]
}
```

Purgecss works also with raw content, you need to pass an object with the `raw`and `extension` properties instead of the filename.

```js
new Purgecss({
    content: [
        {
            raw: '<html><body><div class="app"></div></body></html>',
            extension: 'html'
        },
        `**/*.js`, '**/*.html', '**/*.vue'],
    css: [`css/app.css`]
}
```

* #### extractors

Purgecss can be adapted to suit your need. If you notice a lot of unused css is not being removed, you might want to use a specific extractor.

