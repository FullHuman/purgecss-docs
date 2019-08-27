# React

## Example

You can see an example [here](https://github.com/FullHuman/purgecss/tree/master/examples/with-react/).

## Created with create-react-app

This example shows how to set up Purgecss with create-react-app template.  
Once you initialized your project with `npx create-react-app app`, install the webpack plugin for purgecss:

```text
npm i --save-dev glob-all purgecss-webpack-plugin
```

### Method 1 - Run Purgecss CLI in `postbuild`

Add the following code in **package.json**

```json
"scripts": {
  "postbuild": "purgecss --css build/static/css/*.css --content build/static/index.html build/static/js/*.js --out build/static/css"
},
```

### Method 2 - `eject` create-react-app 

You need to [eject](https://facebook.github.io/create-react-app/docs/available-scripts#npm-run-eject) in order to expose the webpack configuration offered by original create-react-app

Now, modify the file `config/webpack.prod.conf.js` by adding the following code with the rest of the imports:


```javascript
// import Purgecss webpack plugin and glob-all
const PurgecssPlugin = require('purgecss-webpack-plugin')
const glob = require('glob-all')
```

...and directly before `new ManifestPlugin(...)` in the plugins list, add this:

```javascript
    // Remove unused css with Purgecss. See https://github.com/FullHuman/purgecss
    // for more information about purgecss.
    // Specify the path of the html files and source files
    new PurgecssPlugin({
      paths: [paths.appHtml, ...glob.sync(`${paths.appSrc}/*`)]
    }),
```

## Results

This example is importing the bootstrap css framework.  
Without purgecss, the base css file size is **138 kB**.  
Using purgecss, the base css file size is **4 kB**

