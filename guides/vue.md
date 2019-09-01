# Vue

## Example

You can see an example [here](https://github.com/FullHuman/purgecss/tree/master/examples/with-vue/).

## Created with vue-cli

This example shows how to set up PurgeCSS with vue-webpack template.  
Once you initialized your project with `vue init webpack`, install the webpack plugin for PurgeCSS:

```text
npm i --save-dev glob-all purgecss-webpack-plugin
```

You need to modify the file `webpack.prod.conf.js` by adding the following code:

line 13

```javascript
// import PurgeCSS webpack plugin and glob-all
const PurgecssPlugin = require('purgecss-webpack-plugin')
const glob = require('glob-all')
```

line 58

```javascript
    // Remove unused CSS using PurgeCSS. See https://github.com/FullHuman/purgecss
    // for more information about PurgeCSS.
    new PurgecssPlugin({
      paths: glob.sync([
        path.join(__dirname, './../src/index.html'),
        path.join(__dirname, './../**/*.vue'),
        path.join(__dirname, './../src/**/*.js')
      ])
    }),
```

## Results

This example is importing the bootstrap css framework.  
Without PurgeCSS, the css file size is **117 kB**.  
Using PurgeCSS, the css file size is **2.98 kB**

