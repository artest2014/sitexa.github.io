---
layout: post
title: NodeJS & npm & nvm
category: 'technology'
---

Today it’s hard to imagine any serious Web development without NodeJS. Even though Gradle plugins performing frontend related tasks exist, they usually lag behind the original libraries written for Node. Besides, we are going to use NodeJS only during development and installing it on production servers is completely unnecessary.

When people talk about NodeJS in the context of Web development, they usually mean two things:
-   1. node - the Node JavaScript interpreter based on V8 engine
-   2. npm - the Node Package Manager, which comes with Node and helps with downloading and installing node-packages, running JS scripts

Fortunately, nvm manages the versions of both tools.

##  Setting up nvm
-   Go to https://github.com/creationix/nvm33 and scroll down to the Install script section 
-   Copy the wget or curl script and run it in the terminal
-   After installation is complete, restart the terminal


##  Choosing the version

To see the list of available NodeJS versions type:

```$ nvm ls-remote``` 

to see local list use: 

```$ nvm ls```

Install certain version:

```$ nvm install v6.9.1 ```

Switch to certainly version:

```$ nvm use v6.9.1```

Check node & npm version:

``` 
$ node --version
v7.10.0
$ npm --version
4.2.0
```

##  package.json

The main file for npm is package.json. It contains information about the project such as project name, version, description, author etc. Since we’re not going to publish our project, most of these fields are not important.

### create package.json

``` npm init ```

There are 3 sections within it:
-   dependencies
-   devDependecies
-   scripts

### add package as an application dependency

```$ npm i react -S```

### add package as development dependency

```$ npm i webpack -D```

### downloads all these dependencies to a directory called node_modules

```$ npm i ```

### install package globally:

```$ npm i http-server -G```

### command in scripts

``` 
{
    //...
    "scripts": {
        "watch": "webpack --watch"
    }
    //... 
}
```

run scripts:

```$ npm run watch```

##  Module bundlers

### CommonJS 

``` 
var React = require('react');
var _ = require('lodash');
var HelloWorld = require('./helloworld.jsx');
```

### EcmaScript 6

``` 
import React from 'react';
import _ from 'lodash';
import HelloWorld from './helloworld.jsx';
```

### browserify - 13.0.1

Browserify lets you require('modules') in the browser by bundling up all of your dependencies.

### webpack - v2.6.0

webpack is a module bundler. Its main purpose is to bundle JavaScript files for usage in a browser, yet it is also capable of transforming, bundling, or packaging just about any resource or asset.

### Babel - v6.24.1

Babel is a JavaScript compiler.

It takes your source code written using EcmaScript 6 (or EcmaScript 7) syntax and turns it into JS code that modern browsers understand.

##  React

React37 is a JavaScript library developed by Facebook and open-sourced in 2013. It combines several unconventional approaches to typical frontend problems, which appeals to many developers. In particular, React promotes the idea of writing HTML-tags alongside JavaScript code. It may look crazy at first, but many agree that this approach gives a lot of flexibility. 

Unlike more feature-rich solutions like AngularJS, React is only concerned with the View in MVC (Model-View-Controller), which can be both a good thing or bad thing. On the bright side, it means that React is very unopinionated about the technology stack you are going to use and thus compatible with almost everything. The bad news is that many familiar components of a typical JavaScript framework are not provided out of the box.

### Axios - v0.16.1

Axios is promise based HTTP client for the browser and node.js .

-   Make XMLHttpRequests from the browser
-   Make http requests from node.js
-   Supports the Promise API
-   Intercept request and response
-   Transform request and response data
-   Cancel requests
-   Automatic transforms for JSON data
-   Client side support for protecting against XSRF

Get request:

``` 
// Make a request for a user with a given ID
axios.get('/user?ID=12345')
  .then(function (response) {
    console.log(response);
  })
  .catch(function (error) {
    console.log(error);
  });

// Optionally the request above could also be done as
axios.get('/user', {
    params: {
      ID: 12345
    }
  })
  .then(function (response) {
    console.log(response);
  })
  .catch(function (error) {
    console.log(error);
  });
```

POST request:

``` 
axios.post('/user', {
    firstName: 'Fred',
    lastName: 'Flintstone'
  })
  .then(function (response) {
    console.log(response);
  })
  .catch(function (error) {
    console.log(error);
  });
```

**axios API**

``` 
// Send a POST request
axios({
  method: 'post',
  url: '/user/12345',
  data: {
    firstName: 'Fred',
    lastName: 'Flintstone'
  }
});

// GET request for remote image
axios({
  method:'get',
  url:'http://bit.ly/2mTM3nY',
  responseType:'stream'
})
  .then(function(response) {
  response.data.pipe(fs.createWriteStream('ada_lovelace.jpg'))
});

// Send a GET request (default method)
axios('/user/12345');
```