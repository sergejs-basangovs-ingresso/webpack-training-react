### Branches:

1. master branch - beginning, no webpack is set.
   Only react and react-dom packages are installed
2. setup the webpack

    - npm i --save-dev webpack webpack-cli
    - add new file: webpack.config.js
    - in config.json add new script:
      "build": "webpack --mode production"
    - in webpack.config.js, we shall import/export the modules using the commonJS/es5 syntax, because the webpack doesn't know yet the ex6, that is provided by babel.

    module.exports = {
    module: { // there are multiple modules that can be run within webpack
    rules: [ // rules - first module
    {

     }
    ]
    }
    }
