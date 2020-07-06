### Branches:

1.  master branch - beginning, no webpack is set.
    Only react and react-dom packages are installed
2.  installing-the-webpack branch

        - npm i --save-dev webpack webpack-cli
        - add new file: webpack.config.js
        - in config.json add new script:
          "build": "webpack --mode production"
        - in webpack.config.js, we shall import/export the modules using the commonJS/es5 syntax, because the webpack doesn't know yet the es6, that is provided by babel.

        module.exports = {
          module: { // there are multiple modules that can be run within webpack
            rules: [ // rules - first module
              {
                test: /\.(js|jsx)$/, // this is the regex for what type of files to pick
                exclude: /node_modules/,  // this is the regex for which directory to exclude
              }
            ]
          }
        }

        - install babel packages:
          npm i @babel/core @babel/preset-env @babel/preset-react babel-loader --save-dev

        - webpack.config.js;
          module.exports = {
            module: {
              rules: [
                {
                  test: /\.(js|jsx)$/,
                  exclude: /node_modules/,
                  use: {
                    loader: "babel-loader"
                  },
                },
              ],
            },
          };
          "babel-loader" - is the module that will look for a file .babelrc
        - create  .babelrc - file that tells babel library what does it need to transpile down to .

        - .babelrc :
            {
              "presets": ["@babel/preset-env, @babel/preset-react"]
            }

3.  2-config-webpack branch:

        -   now we need to bring another loader, so webpack knows what to do with .css files
            style-loader, css-loader, sass-loader (if want to use sass).
            style-loader: loader that allows to convert different types of style files
            css-loader: loader that allows our css files to be read by javascript files.

            npm i style-loader css-loader --save-dev

        - webpack.config.js:

          module.exports = {
            module: {
              rules: [
                {
                  test: /\.(js|jsx)$/,
                  exclude: /node_modules/,
                  use: {
                    loader: "babel-loader",
                  },
                },
                {
                  test: /\.css$/,
                  use: ["style-loader", "css-loader"],
                },
              ],
            },
          };

        - now , we need a loader that we can output and build the html file:

        npm i html-loader html-webpack-plugin --save-dev

        - then, webpack.config.js:
          const HtmlWebpackPlugin = require("html-webpack-plugin");
          module.exports = {
            module: {
              rules: [
                 ...
                {
                  test: /\.html$/,
                  use: {
                    loader: "html-loader",
                  },
                },
              ],
            },
            plugins: [
              new HtmlWebpackPlugin({
                template: "./index.html", //<= the path to where is our index.html located
              }),
            ]
          };
        - then in src/ files just make sure when importing files, write their .js/.jsx/.css extensions
          (eg. import App from "./App.jsx"; )

        - then run : npm run build
          OR
          can run : webpack --mode production

          the build will be in dist/ folder
