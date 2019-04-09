## How to set up new React project with Webpack and Hotloader


##### Run `npm init`
Input your details as required

#### Create dist folder in root with an index.html containing:
```
<!DOCTYPE html>
<html>
  <head>
    <title>The Minimal React Webpack Babel Setup</title>
  </head>
  <body>
    <div id="app"></div>
    <script src="./bundle.js"></script>
  </body>
</html>
```


#### Install webpack:
`npm install --save-dev webpack webpack-dev-server webpack-cli`


#### Edit Package.json scripts object to add:
`"start": "webpack-dev-server --config ./webpack.config.js --mode development",`


#### Create webpack.config.js in root folder with the following:
```
module.exports = {
  entry: './src/index.js',
  output: {
    path: __dirname + '/dist',
    publicPath: '/',
    filename: 'bundle.js'
  },
  devServer: {
    contentBase: './dist'
  }
};
```


#### Create src folder in root with index.js containing:
`console.log('My Minimal React Webpack Babel Setup');`
Should log "My Minimal React Webpack Babel Setup" to console


#### `npm start` to test working status


#### Install babel from root folder
`npm install --save-dev @babel/core @babel/preset-env`

`npm install --save-dev babel-loader`

`npm install --save-dev @babel/preset-react`


#### Edit package.json under licence with:
```
"babel": {
  "presets": [
    "@babel/preset-env",
    "@babel/preset-react"
  ]
},
```
<span style="color:red">if react error on next test says something about repeat/duplicate babel setting, delete this.</span>


#### Update webpack.config.js to:
```
module.exports = {
  entry: './src/index.js',
  module: {
    rules: [
      {
        test: /\.(js|jsx)$/,
        exclude: /node_modules/,
        use: ['babel-loader']
      }
    ]
  },
  resolve: {
    extensions: ['*', '.js', '.jsx']
  },
  output: {
    path: __dirname + '/dist',
    publicPath: '/',
    filename: 'bundle.js'
  },
  devServer: {
    contentBase: './dist'
  }
};
```


#### Create .babelrc in root folder with:
```
{
  "presets": [
    "@babel/preset-env",
    "@babel/preset-react"
  ]
}
```


#### Install React
`npm install --save react react-dom`


#### Update src/index.js to:
```
import React from 'react';
import ReactDOM from 'react-dom';

const title = 'My Minimal React Webpack Babel Setup';

ReactDOM.render(
  <div>{title}</div>,
  document.getElementById('app')
);
```


#### Install React Hot Loader
`npm install --save-dev react-hot-loader`


#### Update webpack.config.js to:
```
const webpack = require('webpack');

module.exports = {
  entry: './src/index.js',
  module: {
    rules: [
      {
        test: /\.(js|jsx)$/,
        exclude: /node_modules/,
        use: ['babel-loader']
      }
    ]
  },
  resolve: {
    extensions: ['*', '.js', '.jsx']
  },
  output: {
    path: __dirname + '/dist',
    publicPath: '/',
    filename: 'bundle.js'
  },
  plugins: [
    new webpack.HotModuleReplacementPlugin()
  ],
  devServer: {
    contentBase: './dist',
    hot: true
  }
};
```


#### Update src/index.js with:
`module.hot.accept();` at bottom of file


#### `npm start` to test


Instructions taken from:<br />
https://www.robinwieruch.de/minimal-react-webpack-babel-setup/
