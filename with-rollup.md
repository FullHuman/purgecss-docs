# Rollup

Start by installing the Rollup plugin as a dev dependency.

```
npm i -D rollup-plugin-purgecss
```

```js
import { rollup } from 'rollup'
import purgecss from 'rollup-plugin-purgecss'

rollup({
  entry: 'main.js',
  plugins: [
    purgecss({
      content: ['index.html']
    })
  ]
})
```



