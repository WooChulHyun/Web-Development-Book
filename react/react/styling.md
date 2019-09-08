# Styling

## CSS

Common CSS is used the same way as we normally do. However, we have to care about in naming to avoid duplicate names. CSS created through create-react-app include the component name in the CSS class name like App-header.Or use a CSS Selector to format it as .App .loge {}.



## Sass, Scss

In create-react-app v1, additional work was required to use Sass, but from v2 it can be used without any additional configuration.

First we need to install a library called node-sass. This library converts Sass to CSS.

```bash
npm install node-sass
yarn add node-sass
```



### utiles.scss

Sass variables and @mixin, which can be used in multiple files, can be created separately from other files and easily loaded and used where they are needed.

Create a directory called styles in the src directory and create a utils.scss file in it.



## CSS Module

The CSS Module automatically creates a class name in the form of a unique value: \[file name\]-\[class name\]\_\_\[hash value\] to prevent component style class names duplication. In create-react-app v1, css-loader had to be set. However, since v2 or later, the CSS module is applied when the file is saved with the .module.css extension.

With the CSS Module, the class will only work inside the component. If you want to make a class is used globally in a web page, you can enter: global first.

```css
:global .something {
  font-weight: 800;
}
```



