# React

## Example

You can see an example [here](https://github.com/FullHuman/purgecss/tree/master/examples/with-react/).

## Created with create-react-app

This example shows how to set up PurgeCSS with create-react-app template.  
Once you initialized your project with `npx create-react-app app`, install the webpack plugin for PurgeCSS:

```text
npm i --save-dev glob-all purgecss-webpack-plugin
```

## `eject` create-react-app 

You need to [eject](https://facebook.github.io/create-react-app/docs/available-scripts#npm-run-eject) in order to expose the webpack configuration offered by original create-react-app

Now, modify the file `config/webpack.prod.conf.js` by adding the following code with the rest of the imports:


```javascript
// import PurgeCSS webpack plugin and glob-all
const PurgecssPlugin = require('purgecss-webpack-plugin')
const glob = require('glob-all')
```

...and directly before `new ManifestPlugin(...)` in the plugins list, add this:

```javascript
    // Remove unused css with PurgeCSS. See https://github.com/FullHuman/purgecss
    // for more information about PurgeCSS.
    // Specify the path of the html files and source files
    new PurgecssPlugin({
      paths: [paths.appHtml, ...glob.sync(`${paths.appSrc}/*`)]
    }),
```

## Results

This example is importing the bootstrap css framework.  
Without PurgeCSS, the base css file size is **138 kB**.  
Using PurgeCSS, the base css file size is **4 kB**

