---
layout: learn
title: using vue js to make a music player
date: 2018-01-19 16:43:39 +0800
categories: learning
tags: jnj,homework
keywords: vuejs
---

Using vue js to build a music player

## stage one: build a simple vue js app

###  step one: Creating a basic structure

1. create a <mark>package.json</mark> file in root folder 
 	- Could use cmd <mark> Npm init </mark> and fill the content as required

```javascript
{
  "name": "learn",
  "version": "1.0.0",
  "description": "to learn how to write vue js",
  "main": "index.html",
  "dependencies": {
    "webpack": "^3.10.0"
  },
  "devDependencies": {
  },
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "build": "webpack"
  },
  "author": "lyra",
  "license": "MIT"
}
```
Things to be noted here：
	- please note the scripts in the js code
	in order to use npm run build to compile the whole files

2. create an <mark>index.html</mark> in root folder
3. create a folder <mark>src</mark> and add a file <mark>src/main.js</mark>

### step two: Basic webpack build

1. create a file called <mark>webpack.config.js</mark>

An example could be: 

```javascript

const path = require('path');


module.exports = {
    entry: './src/main.js',
    output: {
        path: path.resolve(__dirname, 'build'),//__dirname + '/build'
        filename:'build.js'
    },
    module:{
        loaders: [
            {
                test:/\.js$/,
                loader: 'babel-loader',
                exclude: /node_modules/
            },
            {
                test: /\.vue$/,
                loader: 'vue-loader'
            },

        ]
    }
}

```

Things to be noted here：
 	- path should be absolute path

2. create a file called <mark>.babelrc</mark>
install webpack using cmd <mark>npm install --save-dev webpack</mark>
3. and install other local libraries.

An example could be:

```

   "babel-core": "^6.26.0",
    "babel-loader": "^7.1.2",
    "babel-plugin-transform-runtime": "^6.23.0",
    "babel-preset-es2015": "^6.24.1",
    "babel-preset-stage-0": "^6.24.1",
    "babel-runtime": "^6.26.0",
    "css-loader": "^0.28.9",
    "vue": "^2.5.13",
    "vue-loader": "^13.7.0",
    "vue-template-compiler": "^2.5.13"

```




