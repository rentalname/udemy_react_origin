勉強会 進行資料 1
==

# agenda
+ 環境構築
+ webpack-dev-server
+ eslint
+ scss
+ react
+ react componentの作成
+ component props
+ component state

## 環境構築
### エディタ
+ atom
+ or すきなの

### yarn
+ `brew install yarn`
+ `yarn init`
+ `yarn add webpack webpack-dev-server babel-core babel-loader babel-preset-react babel-preset-react babel-preset-es2015`

### .gitignoreの設定
+ `echo 'node_modules' > .gitignore`

### `webpack.config.js`の作成

```javascript
const publicDir = path.join(__dirname, '/public');
module.exports = [
  {
    entry: [
      './src/index.jsx',
    ],
    output: {
      path: publicDir,
      publicPath: '/',
      filename: 'bundle.js',
    },
    module: {
      loaders: [{
        exclude: /node_modules/,
        loader: 'babel-loader',
        query: {
          presets: ['react', 'es2015'],
        },
      }],
    },
    resolve: {
      extensions: ['.js', '.jsx'],
    },
    devServer: {
      historyApiFallback: true,
      contentBase: publicDir,
    },
  },
];

```

## webpack-dev-server
+ `yarn add webpack webpack-dev-server babel-core babel-loader babel-preset-react babel-preset-react babel-preset-es2015`
+ `mkdir public`
+ `mkdir src`
+ webpack-dev-serverの起動
  + `./node_modules/.bin/webpack-dev-server`

### package.jsonにサーバーの起動コマンドを登録
```
{
  "scripts": {
    "start": "./node_modules/.bin/webpack-dev-server"
  }
}
```

+ yarn run start

## eslintの導入
+ `yarn add eslint eslint-plugin-react`
+ `./node_modules/.bin/eslint --init`
  + airbnb
  + javascript
+ `yarn install`

### eslintとeditorの連携
+ `apm install es6-javascript intentions busy-signal linter-ui-default linter linter-eslint`


## scss
### webpack.config.jsの編集
```javascript
const path = require('path');
const ExtractTextPlugin = require('extract-text-webpack-plugin');

const publicDir = path.join(__dirname, '/public');
module.exports = [
  {
    entry: [
      './src/index.jsx',
    ],
    output: {
      path: publicDir,
      publicPath: '/',
      filename: 'bundle.js',
    },
    module: {
      loaders: [{
        exclude: /node_modules/,
        loader: 'babel-loader',
        query: {
          presets: ['react', 'es2015'],
        },
      }],
    },
    resolve: {
      extensions: ['.js', '.jsx'],
    },
    devServer: {
      historyApiFallback: true,
      contentBase: publicDir,
    },
  },
  {
    entry: {
      style: './stylesheets/index.scss',
    },
    output: {
      path: publicDir,
      publicPath: '/',
      filename: 'bundle.css',
    },
    module: {
      loaders: [
        {
          test: /\.css$/,
          loader: ExtractTextPlugin.extract({ fallback: 'style-loader', use: 'css-loader' }),
        },
        {
          test: /\.scss$/,
          loader: ExtractTextPlugin.extract({ fallback: 'style-loader', use: 'css-loader!sass-loader' }),
        },
      ],
    },
    plugins: [
      new ExtractTextPlugin('bundle.css'),
    ],
  },
];

```

### パッケージの追加
+ `yarn add node-sass style-loader css-loader sass-loader import-glob-loader extract-text-webpack-plugin`

### stylesheetsディレクトリの追加
+ `mkdir stylesheets`

## react
+ `yarn add react@15.6.1 react-dom@15.6.1`

## react component
### componentディレクトリの作成
+ `mkdir src/components`

### appコンポーネントの作成

#### app.js
```javascript
import React from 'react'
import ReactDOM from 'react-dom'

function App(props) {
  return (<div>Hello from functional App</div>)
}

export default App
```

```javascript
import React, {Component} from 'react'
import ReactDOM from 'react-dom'

class App extends Component {
  render() {
    return (<div>Hello from class App</div>)
  }
}

export default App
```

### atomへのjsxプラグインの導入
` apm install language-javascript-jsx`

## component props
## component state
