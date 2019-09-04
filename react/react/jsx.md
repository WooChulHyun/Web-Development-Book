# JSX

JSX is an extension of JavaScript and looks very much like MXL. Code written in JSX is converted to plain JavaScript code by barbell when the code is been bundling before being executed in a browser.

```jsx
function App() {
  return (
    <div>
      Hello <b>react</b>
    </div>
  );
}
```

This JSX Code will be converted to

```javascript
function App() {
  return React.createElement(
    'div',
    null,
    'Hello',
    React.createElement('b', null, 'react')
  );
}

```



## JSX Grammar

### Wrapped Element

If a component has multiple elements, it must be wrapped in a single parent element.

```jsx
import React from 'react'

function App() {
  return (
    <h1>Hello React!</h1>
    <h2>How are you?</h2>
  )
}

export default App;
```

If you run this code with `npm start` or `yarn start`, you can see this error,

```text
./src/App.js
  Line 6:  Parsing error: Adjacent JSX elements must be wrapped in an enclosing tag. 
  Did you want a JSX fragment <>...</>?

  4 |   return (
  5 |     <h1>Hello React!</h1>
> 6 |     <h2>How are you?</h2>
    |     ^
  7 |   )
  8 | }
  9 | 
```



The error occurs because multiple elements are not wrapped by a single parent element. This error can be fixed by:

```jsx
import React from 'react';

function App() {
  return (
    <div>
      <h1>Hello React!</h1>
      <h2>How are you?</h2>
    </div>
  );
}

export default App;
```

Or you can use Fragments introduced with React v16 and above.

```jsx
import React, { Fragment } from 'react';

function App() {
  return (
    <Fragment>
      <h1>Hello React!</h1>
      <h2>How are you?</h2>
    </Fragment>
  );
}

export default App;
```

Or

```jsx
import React from 'react';

function App() {
  return (
    <>
      <h1>Hello React!</h1>
      <h2>How are you?</h2>
    </>
  );
}

export default App;
```



![](https://i.postimg.cc/j5dvqt3p/JSX1.png)



### JavaScript Expression

You can write JavaScript expressions in JSX. To write a JavaScript expression, you can wrap the code within { } inside the JSX.

```jsx
import React from 'react';

function App() {
  const name = 'React';
  return (
    <>
      <h1>Hello {name}!</h1>
      <h2>How are you?</h2>
    </>
  );
}

export default App;
```



![](https://i.postimg.cc/j5dvqt3p/JSX1.png)



### 

