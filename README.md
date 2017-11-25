# Purgecss

Purgecss is a tool to remove unused css. It can be used as part of your development workflow. Purgecss comes with a Javascript API, a CLI and plugins for popular build tools.

Here are a couple of ways to use Purgecss:

* CLI
* Javascript API
* Webpack
* Gulp
* Rollup

## CLI

You can install the CLI in two ways. By installing purgecss globaly or using npx.

### Install globally

```
npm i -g purgecss
```

You can then use it with

```
purgecss --css <css> --content <content> [option]
```

### Using npx

[npx](https://www.npmjs.com/package/npx)[^1] allows you to run cli locally without installing the package globally.

You can install purgecss as a dev dependency

```
npm i -D purgecss
```

You can then use it with

```
npx purgecss --css <css> --content <content> [option]
```

## Javascript API

 Start by installing Purgecss as a development dependency.

```
npm i -D purgecss
```

You can then use purgecss inside a javascript file.

### ES6 with import

```js
import Purgecss from 'purgecss'
const purgeCss = new Purgecss({
  content: ['**/*.html'],
  css: ['**/*.css']
})
const purgecssResult = purgecss.purge()
```

### ES5 with require

```js
var Purgecss = require('purgecss')
var purgecss = new Purgecss({
  content: ['**/*.html'],
  css: ['**/*.css']
})
var purgecssResult = purgecss.purge()
```

## Webpack

```js
const path = require('path')
const glob = require('glob')
const ExtractTextPlugin = require('extract-text-webpack-plugin')
const PurgecssPlugin = require('../../')

const PATHS = {
  src: path.join(__dirname, 'src')
}

module.exports = {
  entry: './src/index.js',
  output: {
    filename: 'bundle.js',
    path: path.join(__dirname, 'dist')
  },
  module: {
    rules: [
      {
        test: /\.css$/,
        use: ExtractTextPlugin.extract({
          fallback: 'style-loader',
          use: 'css-loader?sourceMap'
        })
      }
    ]
  },
  plugins: [
    new ExtractTextPlugin('[name].css?[hash]'),
    new PurgecssPlugin({
      paths: glob.sync(`${PATHS.src}/*`),
      styleExtensions: ['.css']
    })
  ]
}
```

## Gulp

```js
const gulp = require('gulp')
const purgecss = require('gulp-purgecss')

gulp.task('purgecss', () => {
  return gulp
    .src('src/**/*.css')
    .pipe(
      purgecss({
        content: ['src/**/*.html']
      })
    )
    .pipe(gulp.dest('build/css'))
})
```

## Rollup

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



[^1]: If you want to use npx, npm 5.2.0+ must be installed.

