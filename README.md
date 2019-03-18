# Introduction

[Purgecss](https://github.com/FullHuman/purgecss) is a tool to remove unused CSS. It can be used as part of your development workflow. Purgecss comes with a JavaScript API, a CLI, and plugins for popular build tools.

Here are a couple of ways to use Purgecss:

* [CLI](./#cli)
* [JavaScript API](./#javascript-api)
* [Webpack](./#webpack)
* [Gulp](./#gulp)
* [Rollup](./#rollup)

## CLI

You can install the CLI in two ways. By installing Purgecss globally or using npx.

### Install globally

```text
npm i -g purgecss
```

You can then use it with

```text
purgecss --css <css> --content <content> [option]
```

### Using npx

[npx](https://www.npmjs.com/package/npx) allows you to run the CLI locally without installing the package globally.

You can install Purgecss as a dev dependency

```text
npm i -D purgecss
```

You can then use it with

```text
npx purgecss --css <css> --content <content> [option]
```

## JavaScript API

Start by installing Purgecss as a dev dependency.

```text
npm i -D purgecss
```

You can then use Purgecss inside a JavaScript file.

### ES6 with import

```javascript
import Purgecss from 'purgecss'
const purgecss = new Purgecss({
  content: ['**/*.html'],
  css: ['**/*.css']
})
const purgecssResult = purgecss.purge()
```

### ES5 with require

```javascript
var Purgecss = require('purgecss')
var purgecss = new Purgecss({
  content: ['**/*.html'],
  css: ['**/*.css']
})
var purgecssResult = purgecss.purge()
```

## Webpack

Start by installing the plugin as a dev dependency:

```text
npm i -D purgecss-webpack-plugin
```

```javascript
const path = require('path')
const glob = require('glob')
const ExtractTextPlugin = require('extract-text-webpack-plugin')
const PurgecssPlugin = require('purgecss-webpack-plugin')

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
      paths: glob.sync(`${PATHS.src}/*`)
    })
  ]
}
```

## PostCSS

Start by installing the PostCSS plugin as a dev dependency:

```text
npm i -D @fullhuman/postcss-purgecss
```

In `postcss.config.js`:

```javascript
module.exports = {
  plugins: [
    purgecss({
      content: ['./**/*.html']
    })
  ]
}
```

## Gulp

Start by installing the Gulp plugin as a dev dependency:

```text
npm i -D gulp-purgecss
```

```javascript
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

## Grunt

Start by installing the Grunt plugin as a dev dependency:

```text
npm i -D grunt-purgecss
```

```javascript
module.exports = grunt => {

  grunt.initConfig({
    purgecss: {
      options: {
        content: ['./src/**/*.html']
      },
      my_target: {
        files: {
          './dist/app.purged.css': './src/app.css'
        }
      }
    }
  })

  grunt.loadNpmTasks('grunt-purgecss')
  grunt.registerTask('default', ['purgecss'])
}
```

## Rollup

Start by installing the Rollup plugin as a dev dependency:

```text
npm i -D rollup-plugin-purgecss
```

```javascript
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

