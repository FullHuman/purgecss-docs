# JavaScript API

Start by installing PurgeCSS as a dev dependency.

```text
npm i -D purgecss
```

You can now use PurgeCSS inside a JavaScript file.

In the following examples, the options passed to PurgeCSS are the same as the ones [here](configuration.md). The result `purgecssResult` is an array of an object containing the name of the files with the purged CSS.

## ES6 with import

```javascript
import Purgecss from 'purgecss'
const purgeCss = new Purgecss({
  content: ['**/*.html'],
  css: ['**/*.css']
})
const purgecssResult = purgecss.purge()
```

The format of purgecssResult is

```javascript
[
    {
        file: 'main.css',
        css: '/* purged css for main.css */'
    },
    {
        file: 'animate.css',
        css: '/* purged css for animate.css */'
    }
]
```

## ES5 with require

```javascript
var Purgecss = require('purgecss')
var purgecss = new Purgecss({
  content: ['**/*.html'],
  css: ['**/*.css']
})
var purgecssResult = purgecss.purge()
```

