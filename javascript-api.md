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



