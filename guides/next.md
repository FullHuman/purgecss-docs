# Next

## Module

To simply configure purgecss with next.js, you can use [next-purgecss](https://github.com/lucleray/next-purgecss).

## Installation

### 1. Install the packages

`next-purgecss` requires one of the following **css next plugins** :

- [next-css](https://github.com/zeit/next-plugins/tree/master/packages/next-css)
- [next-less](https://github.com/zeit/next-plugins/tree/master/packages/next-less)
- [next-sass](https://github.com/zeit/next-plugins/tree/master/packages/next-sass)

Just pick the one that fits your needs. In the following steps, I will use `next-css` but it works the same for the other **css next plugins**.

For example, install `next-css` and `next-purgecss` :

```
yarn add @zeit/next-css next-purgecss --dev
```

or with npm :

```
npm install @zeit/next-css next-purgecss --save-dev
```

### 2. Edit `next.config.js`.

```js
// next.config.js
const withCss = require('@zeit/next-css')
const withPurgeCss = require('next-purgecss')

module.exports = withCss(withPurgeCss())
```

## Options

By default, this plugin will scan `components` and `pages` directories for classnames.

Under the hood, `next-purgecss` uses the Purgecss Webpack Plugin. You can pass custom options to the plugin 
by defining `purgeCss` object in your `next.config.js` :

```js
// next.config.js
module.exports = withCss(
  withPurgeCss({
    purgeCss: {
      whitelist: () => ['my-custom-class']
    }
  })
)
```

See the page dedicated to the [Purgecss Webpack Plugin](https://www.purgecss.com/with-webpack) for more information.
