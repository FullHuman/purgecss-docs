# Nuxt

## Module

There is a community module called [nuxt-purgecss](https://github.com/Developmint/nuxt-purgecss) to make the usage of purgecss with Nuxt as easy as possible. With it's fitting defaults, you only need to make a few changes (or none at all)
to the configuration.

### Example

You can see an example using the `nuxt-purgecss` module [here](https://github.com/FullHuman/purgecss/tree/master/examples/with-nuxt-module/).

## Manual configurtion

### Example

You can see an example [here](https://github.com/FullHuman/purgecss/tree/master/examples/with-nuxt-manual/).

### create-nuxt-app and webpack plugin

This example shows how to set up Purgecss with `create-nuxt-app` 
Once you initialized your project with

```text
npx create-nuxt-app <project-name>
```

and selected the options that fit your needs,
install the webpack plugin for purgecss together with `glob-all`:

```text
npm i --save-dev glob-all purgecss-webpack-plugin
```

You need to modify the file `nuxt.config.js` by adding he following code:

line 1

```javascript
import PurgecssPlugin from 'purgecss-webpack-plugin'
import glob from 'glob-all'
import path from 'path'
```

In your `build` segment

```javascript
extractCSS: true
```

in your `build.extend` function.

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

### Results

This example is importing the tachyons css framework. Without purgecss, the base css file size is **88.2 kB**. Using purgecss, the base css file is **1.56 kB**

### PostCSS plugin

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
