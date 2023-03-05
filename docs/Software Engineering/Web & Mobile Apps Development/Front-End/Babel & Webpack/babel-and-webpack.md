# Babel in Webpack

Does React use webpack?

React doesn't "need" babel or webpack but the library is built on the concept of using ES6 javascript syntax and JSX (essentially HTML in JS).03-Apr-2017

https://stackoverflow.com/questions/43175140/why-does-react-require-babel-and-webpack-to-work

Setup

https://medium.com/age-of-awareness/setup-react-with-webpack-and-babel-5114a14a47e9 (A must read article for all key concepts recomended)

what is webpack

At its core, webpack is a static module bundler for modern JavaScript applications.

https://webpack.js.org/concepts/

What is babel

Babel is responsible to converting new language features to old.

```jsx showLineNumbers
// Babel Input: ES2015 arrow function
[1, 2, 3].map((n) => n + 1);

// Babel Output: ES5 equivalent
[1, 2, 3].map(function (n) {
  return n + 1;
});
```

Webpack: When To Use And Why

(A must read article for all key concepts recomended)

https://blog.andrewray.me/webpack-when-to-use-and-why/

what is dependency graph

A dependency graph is a data structure formed by a directed graph that describes the dependency of an entity in the system on the other entities of the same system.

https://deepsource.io/glossary/dependency-graph/

graph vs tree

In computer science, a binary tree is a tree data structure in which each node has at most two children, which are referred to as the left child and the right child. ... It is also possible to interpret a binary tree as an undirected, rather than a directed graph, in which case a binary tree is an ordered, rooted tree.

https://en.wikipedia.org/wiki/Binary_tree

does create-react-app use webpack

Create React App comes configured with webpack and Babel so you don't have to set it all up.

https://scotch.io/starters/react/using-create-react-app-to-make-react-applications#:~:text=Create%20React%20App%20comes%20configured,to%20set%20it%20all%20up.

Where is create-react-app webpack config and files?

You will find that scripts object is using a library react-scripts

Now go to node_modules and look for react-scripts folder react-script-in-node-modules

This react-scripts/scripts and react-scripts/config folder contains all the webpack configurations.

https://stackoverflow.com/questions/48395804/where-is-create-react-app-webpack-config-and-files
https://github.com/facebook/create-react-app/blob/main/packages/react-scripts/scripts/build.js
https://i.stack.imgur.com/5Grrn.png

**npm install webpack webpack-cli webpack-dev-server --save-dev**

This install 3 packages main webpack package, webpack-cli to run webpack commands and webpack-dev-server to run react locally.

**An Introduction to Webpack Dev Server**

"dev": "webpack serve", how it works this works from input section in webpack-config.json

https://masteringjs.io/tutorials/webpack/dev-server

offline-plugin for webpack

This plugin is intended to provide an offline experience for webpack projects. It uses ServiceWorker, and AppCache as a fallback under the hood. Simply include this plugin in your webpack.config, and the accompanying runtime in your client script, and your project will become offline ready by caching all (or some) of the webpack output assets.

https://www.npmjs.com/package/offline-plugin

react webpack app complete creation with deployement

https://www.freecodecamp.org/news/how-to-set-up-deploy-your-react-app-from-scratch-using-webpack-and-babel-a669891033d4/

"npm install --save-dev @babel/core @babel/preset-env @babel/preset-react babel-loader
What we just installed:
@babel/core: Main dependency that includes the babel transform script.
@babel/preset-env: Transform ES6+ into valid ES5 code. Optionally configures browser polyfills automatically.
@babel/preset-react: extends Babel support to JSX.
babel-loader: Webpack loader that hooks Babel into webpack. We will run Babel from webpack with this package."

**webpack.config.js**

"module" is where we tell Webpack to use all of those loaders we installed before.

typescript with webpack

https://webpack.js.org/guides/typescript/

**source map for better error logs**

**Hot Module Reloading**

https://medium.com/@adityadixit06/how-to-write-a-webpack-configuration-for-react-with-babel-and-hot-module-reloading-c3025a063f5d

First, install ‘react-hot-loader’ with npm/yarn.

no need for react-hot-loader becuase webpack-dev-server doing out off the box automatically live reloading

[webpack-dev-server] Hot Module Replacement enabled.

index.js:519 [webpack-dev-server] Live Reloading enabled.

How do we run react js production code on local using webpack?

https://stackoverflow.com/questions/58747746/how-do-we-run-react-js-production-code-on-local-using-webpack?rq=1
