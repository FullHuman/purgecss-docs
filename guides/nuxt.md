# Nuxt

## Example

You can see an example [here](https://github.com/FullHuman/purgecss/tree/master/examples/with-nuxt/).

## Created with nuxtjs starter template

This example shows how to set up Purgecss with nuxtjs starter template.  
Once you initialzed your project with

```text
vue init nuxt-community/starter-template <project-name>
```

install the webpack plugin for purgecss:

```text
npm i --save-dev glob-all purgecss-webpack-plugin
```

You need to modify the file `nuxt.config.js` by adding he following code:

line 1

```javascript
const PurgecssPlugin = require('purgecss-webpack-plugin')
const glob = require('glob-all')
const path = require('path')
```

line 31

```javascript
extractCSS: true
```

line 44

```javascript
if (!isDev) {
  // Remove unused CSS using purgecss. See https://github.com/FullHuman/purgecss
  // for more information about purgecss.
  config.plugins.push(
    new PurgecssPlugin({
      paths: glob.sync([
        path.join(__dirname, './pages/**/*.vue'),
        path.join(__dirname, './layouts/**/*.vue'),
        path.join(__dirname, './components/**/*.vue')
      ]),
      whitelist: ['html', 'body']
    })
  )
}
```

## Results

This example is importing the tachyons css framework. Without purgecss, the base css file size is **88.2 kB**. Using purgecss, the base css file is **1.56 kB**

## Alternatives

Using the *extractCSS* option Nuxt will create CSS files that will be loaded separately by the browser.
When generating your application this might be a lot of small files.

To include the CSS into the header of the HTML file you'll need to run the following commands. 
Please note that using this configuration purgecss will be active in production and development mode.

```text
npm i --save-dev @fullhuman/postcss-purgecss
```

```javascript
import purgecss from '@fullhuman/postcss-purgecss'
```

```javascript
build: {
  postcss: {
    plugins: [
      purgecss({
        content: ['./pages/**/*.vue', './layouts/**/*.vue', './components/**/*.vue'],
        whitelist: ['html', 'body'],
      })
    ]
  }
}
```