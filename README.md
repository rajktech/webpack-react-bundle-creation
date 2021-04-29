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
