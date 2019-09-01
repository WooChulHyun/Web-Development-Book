# Initial setting \(without create-react-app\)

## npm init - Start Node Project

* Use the terminal to navigate to the folder where you want to run your project.

![](https://i.postimg.cc/3R9XRcKv/initial-Setting1.png)



* Start the node project by entering the `npm init` command.

![](https://i.postimg.cc/K8yR65bS/initial-Setting2.png)

![](https://i.postimg.cc/vZdzHj90/initial-Setting3.png)



* The package.json file is created in the project folder.

![](https://i.postimg.cc/Jnt32WVz/initial-Setting4.png)



##  **npm i react react-dom -**React install



* Install React using the terminal. \(React installs react and react-dom.\)

React and react-dom are Initially one, but now separated into two.

If you do not set the version, the latest version is installed.

![](https://i.postimg.cc/0yTqQ9nL/initial-Setting5.png)

![](https://i.postimg.cc/FsYqJ2Ym/initial-Setting6.png)



##  **​npm i -D webpack webpack-cli**

\*\*\*\*

1. Install Webpack using the terminal.

"-D" means use only for development \(because we don't need Webpack to do real service\)

![](https://i.postimg.cc/jS0DVYNS/initial-Setting7.png)



## Babel



```bash
npm i -D @babel/core @babel/preset-env @babel/preset-react babel-loader @babel/plugin-proposal-class-properties
```



-@ babel / core: babel core library

-@ babel / preset-env: Library for browser backward compatibility

@ babel / preset-react:  React configuration library, allows to read the jsx.

@ babel / plugin-proposal-class-properties: required to write state = {} syntax

-babel-loader: Connect webpack and barbell.

![](https://i.postimg.cc/s2QkSxwV/initial-Setting8.png)



## Directory structure



![](https://i.postimg.cc/GpzCJtyV/initial-Setting9.png)



##  **src/index.jsx**

Using the extension as jsx not js, we can make it possible to implicitly define the use of jsx syntax inside the file. Use jsx if that file is only for react.

```jsx
const React = require('react');
const ReactDom = require('react-dom');
const App = require('./components/App');

ReactDom.render(<App />, document.getElementById('root'));
```

**import React from 'react':** Import React.

**import ReactDOM from 'react-dom':** Import a React dome.

**import App from './components/App':** Import the App component. \(You can set the path and omit .js.\)

**ReactDom.render \(\):** Renders the dom \(renders the app component to the element with the root id\)



##  **public/index.html**

```markup
<!DOCTYPE html>
<html>
   <head>
      <meta charset="UTF-8">
      <title>React TEST</title>
   </head> 
   <body>
      <div id="root"></div>
      <script src="../dist/bundle.js"></script>
   </body> 
</html>
```

 **&lt;div id="root"&gt;&lt;/ div&gt;:** the element where React will render

 **&lt;script src="./bundle.js"&gt;&lt;/ script&gt;:** Get the React dom.



##  **/src/conponents/app.js**

```javascript
const React = require('react');

class App extends React.Component {
    state = {
        text: 'Hello React',
    };
    render() {
        return (
            <h1>{this.state.text}</h1>
        );
    }
}

module.exports =  App;
```

**const React = require\('react'\) :** Call React.

**module.exports = App :** Make it available to use in other JavaScript file.



##  **webpack.config.js**

Set webpack.config.js in your root ****directory.

```javascript
const path = require('path');

module.exports = {
    name : 'test-setting', // Name of the webpack setting
    mode : 'development', // service: production
    devtool : 'eval', // service: hidden-source-map
    resolve : {
        extensions: ['.js','.jsx'] // List of extensions omitted from entry
    },
    entry: {
        app : ['./src/index'], // Elements to be merged (multiple)
    },

    module: {
        rules: [
          {
            test: /\.jsx?/,
            loader: 'babel-loader',
            options: {
                presets : ['@babel/preset-env','@babel/preset-react'],
                plugins : ['@babel/plugin-proposal-class-properties']
            },
        }
      ],
    },

    output: {
        path: path.join(__dirname, 'dist'), // (current dir/dist)
        filename: 'bundle.js'
    },
}
```



##  **npx webpack / npm run dev**

**npx webpack:** Creates the bundle.js file that you set in output.

```bash
npx webpack
```



**npm run dev:** 

edit package.json file:

![](https://i.postimg.cc/sD2zk16c/initial-Setting10.png)

```bash
npm run dev
```



![](https://i.postimg.cc/DfXp8hWT/initial-Setting11.png)



Open index.html in the browser

![](https://i.postimg.cc/Y90mPtWy/initial-Setting12.png)



## Detail Settings 



### @babel/preset-env

Determine which version of the Internet environment you are supporting.

```javascript
const path = require('path');

module.exports = {
  name: 'test-setting',
  mode: 'development',
  devtool: 'eval',
  resolve: {
    extensions: ['.js', '.jsx']
  },
  entry: {
    app: ['./src/index']
  },

  module: {
    rules: [
      {
        test: /\.jsx?/,
        loader: 'babel-loader',
        options: {
          presets: [
            [
              '@babel/preset-env',
              {
                targets: {
                  browsers: ['> 5% in KR', 'last 2 chrome version']
                },
                debug: true
              }
            ],
            '@babel/preset-react'
          ],
          plugins: ['@babel/plugin-proposal-class-properties']
        }
      }
    ]
  },

  output: {
    path: path.join(__dirname, 'dist'),
    filename: 'bundle.js'
  }
};
```



**Refer this site:** [https://github.com/browserslist/browserslist](https://github.com/browserslist/browserslist)

  


