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



