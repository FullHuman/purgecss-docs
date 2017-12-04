# Configuration

Purgecss has  a list of options that allow you to customize its behavior. Customization can improve the performance or efficiency of Purgecss. You can create a configuration file with the options and use it with Purgecss.

## Configuration file

The configuration file is a simple js file. By default, the javascript api will look for `purgecss.config.js`.

```js
module.exports = {
    content: ['index.html'],
    css: ['style.css']
}
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

```js
new Purgecss({
    content: ['index.html', `**/*.js`, '**/*.html', '**/*.vue'],
    css: [`css/app.css`],
    extractors: {
        extractor: class {
            static extract(content) {
                content.match(/a-Z/) || []
            }
        },
        extension: ['html', 'blade']
    }
}
```

More information about extractors [here](/extractors.md).







