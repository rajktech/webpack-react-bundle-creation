# webpack-react-bundle-creation
This repo has sample code of creating bundle of react app created without CRA method

Reference: https://medium.com/swlh/a-complete-webpack-setup-for-react-e56a2edf78ae

<h3>Steps:</h3>
<h4>Create a folder</h4>
<pre>mkdir webpack-react-bundle-creation
cd webpack-react-bundle-creation</pre>

<h4>Init your project. -y will skip the questions</h4>
<pre>npm init -y</pre>

<h4>Install webpack, CLI and the development server for testing</h4>
<pre>npm install --save-dev webpack webpack-cli webpack-dev-server</pre>

<h4>Install React and React DOM as dependencies</h4>
<pre>npm install react react-dom</pre>

<h4>Install Core and JavasScipt Loaders</h4>
<pre>npm install --save-dev @babel/core babel-loader @babel/preset-env @babel/preset-react</pre>

<h4>Install CSS Loaders</h4>
<pre>npm install --save-dev css-loader style-loader postcss-loader postcss --save-dev</pre>

<h4>Install Image Loaders</h4>
<pre>npm install --save-dev file-loader url-loader</pre>

<h4>Install Plugins</h4>
<pre>npm install --save-dev autoprefixer
npm install --save-dev html-webpack-plugin</pre>

<h4>Create Files</h4>
<pre>mkdir -p src
touch src/index.html src/index.js src/index.css</pre>

<h4>Edit your index.html</h4>
<pre>
&lt;!DOCTYPE html&gt;
&lt;html lang="en"&gt;
&lt;head&gt;
    &lt;meta charset="UTF-8"&gt;
    &lt;meta name="viewport" content="width=device-width, initial-scale=1.0"&gt;
    &lt;meta http-equiv="X-UA-Compatible" content="ie=edge"&gt;
    &lt;title&gt;My React App&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
    &lt;div id="root"&gt;&lt;/div&gt;
&lt;/body&gt;
&lt;/html&gt;
</pre>

<h4>Edit your index.js</h4>
<pre>
import React from "react";
import ReactDOM from "react-dom";

import MyImage from './assets/dog.jpg';
import './index.css';

const App = () =&gt; {
  return (
    &lt;div&gt;
        &lt;div&gt;Welcome to my-webpack-react-starter&lt;/div&gt;
        &lt;img src={MyImage} /&gt;
    &lt;/div&gt;
  );
};

ReactDOM.render(&lt;App /&gt;, document.querySelector("#root"));
</pre>

<h4>Edit your index.css</h4>
<pre>
body {
    margin: 50;
    padding: 50;
}

div {
    background-color: teal;
}

img {
    width: 640px;
    height: 426px;
}
</pre>

<h4>Build Configuration for Webpack and Babel</h4>
<p>Create a .babelrc file inside the root of your project folder and insert the below lines to it.</p>
<pre>touch .babelrc</pre>
<p>In this file, you specify all the presets to apply in your code</p>
<pre>{ "presets": ["@babel/preset-env", "@babel/preset-react"] }</pre>

<p>In your package.json file include your start script for dev, your build script for the production build.
This is the complete file:</p>
<pre>
{
  "name": "webpack-react-starter",
  "version": "1.0.0",
  "description": "A Webpack + Babel + React Starter bolerplate ",
  "repository": {
    "type": "git"
  },
  "keywords": [
    "Autoprefixer",
    "PostCSS",
    "Webpack",
    "React",
    "Babel"
  ],
  "author": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "start": "webpack-dev-server --open --hot --mode development",
    "build": "webpack --mode production"
  },
  "license": "MIT",
  "browserslist": "> 1%,last 2 versions",
  "devDependencies": {
    "@babel/core": "^7.7.5",
    "@babel/preset-env": "^7.7.6",
    "@babel/preset-react": "^7.7.4",
    "autoprefixer": "^9.7.3",
    "babel-loader": "^8.0.6",
    "css-loader": "^3.3.2",
    "file-loader": "^5.0.2",
    "html-webpack-plugin": "^3.2.0",
    "postcss": "^8.1.0",
    "postcss-loader": "^4.0.2",
    "style-loader": "^1.0.1",
    "url-loader": "^3.0.0",
    "webpack": "^4.41.3",
    "webpack-cli": "^3.3.10",
    "webpack-dev-server": "^3.9.0"
  },
  "dependencies": {
    "react": "^16.12.0",
    "react-dom": "^16.12.0"
  }
}
</pre>

<p>Create a webpack.config.js in the root folder</p>
<pre>
const path = require('path');
const autoprefixer = require('autoprefixer');
const HtmlWebpackPlugin = require('html-webpack-plugin');

module.exports = {
    entry: './src/index.js',
    output: {
        path: path.resolve(_\_dirname, 'dist'),
        filename: 'bundle.js',
        chunkFilename: '[id].js',
        publicPath: ''
    },
    resolve: {
        extensions: ['.js', '.jsx']
    },
    module: {
        rules: [
            {
                test: /\.js$/,
                loader: 'babel-loader',
                exclude: /node_modules/
            },
            {
                test: /\.css$/,
                exclude: /node_modules/,
                use: [
                    { loader: 'style-loader' },
                    { 
                        loader: 'css-loader',
                        options: {
                            modules: {
                                localIdentName: "[name]_\_[local]_\__[hash:base64:5]",
                            },														
                            sourceMap: true
                        }
                     },
                     { 
                         loader: 'postcss-loader',
                        options: {
                            postcssOptions: {
                                plugins: [
                                    [ 'autoprefixer', {}, ],
                                ],
                            },
                        }
                      }
                ]
            },
            {
                test: /\.(png|jpe?g|gif)$/,
                loader: 'url-loader?limit=10000&name=img/[name].[ext]'
            }
        ]
    },
    plugins: [
        new HtmlWebpackPlugin({
            template: _\_dirname + '/src/index.html',
            filename: 'index.html',
            inject: 'body'
        })
    ]
};
</pre>

<p>Let’s run our example project in development first:</p>
<pre>npm run start</pre>

<p>To build your production release:</p>
<pre>npm run build</pre>

