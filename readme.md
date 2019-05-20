## SETUP

1. Initiate a new project with `yarn init`
2. Replicate the file structure above
3. Ensure that the following are installed globally 
	- **babel-cli@6.24.1** `yarn global add babel-cli@6.24.1` test with `babel --help`
	- **live-server** `yarn global add live-server` test with `live-server --version`
4. No add dependencies:
	-`yarn add babel-preset-react@6.24.1 babel-preset-env@1.5.2`
5. Command to set up babel to watch for file changes and to build to `public/scripts/app.js`
	- `babel src/app.js --out-file=public/scripts/app.js --presets=env,react --watch`
6. Now run command to launch live-server `live-server public`

If install dependencies locally then use this script:

```
  "scripts":{
    "serve": "live-server public/",
    "build": "babel src/app.js --out-file=public/scripts/app.js --presets=env,react --watch"
  }
```



## Webpack

BASIC SETUP
```
  const path = require('path');
  module.exports = {
    entry: './src/app.js',   //the main file we want to start converting
    output: {
      path: path.join(__dirname, 'public'),  //dirname gives us the directory of any machine and then join adds the path we want to connect to
      filename: 'bundle.js'  //this can be named anything as long as it matches the script in public/index.html 
    }
  };
```

ADDING BABEL TO WEBPACK

To enable babel webpack we need to add dependencies
    "babel-core": "6.25.0",
    "babel-loader": "7.1.1"

Also need to add a new file: `.babelrc` to state the presets to use

```
{
  "presets":[
    "env",
    "react"
  ]
}
```

This is the main webpack config file now with webpack-loader

```
const path = require('path');
module.exports = {
  entry: './src/app.js',
  output: {
    path: path.join(__dirname, 'public'),
    filename: 'bundle.js'
  },
  module:{
    rules:[{
      loader: 'babel-loader',
      test: /\.js$/,    //tell webpack to look for anything that ends with .js (using regex)
      exclude: /node_modules/ //exclude anything in node_modules
    }]
  }
};
```


## Dev Tools in Webpack
To make it easy to track the source of errors and logs, add this line:
`devtool:'cheap-module-eval-source-map'`


