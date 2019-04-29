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

```bash
npm i -g purgecss
```

Run Purgecss from the terminal:

```bash
purgecss --css <css> --content <content> [option]
```

### Use npx

[npx](https://www.npmjs.com/package/npx) allows you to run the CLI locally without installing the package globally.

Install Purgecss as a dev dependency:

```bash
npm i -D purgecss
```

Run Purgecss from the terminal:

```bash
npx purgecss --css <css> --content <content> [option]
```

## JavaScript API

Install Purgecss as a dev dependency:

```bash
npm i -D purgecss
```

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

Install the Webpack plugin as a dev dependency:

```bash
npm i -D purgecss-webpack-plugin
```

Use the plugin in your Webpack config:

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

Install the PostCSS plugin as a dev dependency:

```bash
npm i -D @fullhuman/postcss-purgecss
```

Use the plugin in your PostCSS config:

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

Install the Gulp plugin as a dev dependency:

```bash
npm i -D gulp-purgecss
```

Use the plugin in your Gulpfile:

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

Install the Grunt plugin as a dev dependency:

```bash
npm i -D grunt-purgecss
```

Use the plugin in your Gruntfile:

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

Install the Rollup plugin as a dev dependency:

```bash
npm i -D rollup-plugin-purgecss
```

Use the plugin in your Rollup config:

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

