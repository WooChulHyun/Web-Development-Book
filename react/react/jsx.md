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



### Ternary operator

You cannot use if statements in JavaScript expressions inside JSX. You must use the if statement outside of JSX, or use ternary operateor within { }.

{% hint style="info" %}
In fact, you can use if and for statements through IIFE \(Immediately Invoked Function Expression\) inside JSX, but it is recommended to use them outside of JSX.
{% endhint %}

```jsx
import React from 'react';

function App() {
  const name = 'React';
  
  return (
    <>
      {name === 'React' ? <h1>This is React!</h1> : <h1>This is not React!</h1>}
    </>
  );
}

export default App;
```

If the `const name = 'React'` 

![](https://i.postimg.cc/1XkPpWLK/JSX2.png)



If the `const name = 'JavaScript'`

![](https://i.postimg.cc/yN1KX3r2/JSX3.png)



### Logical Operators \(&&\)

There may be situations where the content is shown when certain conditions are met, and when nothing is satisfied, nothing should be rendered at all. This can also be implemented using the Ternary operator.

```jsx
import React from 'react';

function App() {
  const name = 'JavaScrip';
  
  return <>{name === 'React' ? <h1>This is React!</h1> : null}</>;
}

export default App;
```

If you render null \(falsy value\) like above code, it will show nothing. But you can do the same thing with shorter code than this.

```jsx
import React from 'react';

function App() {
  const name = 'React';
  return <>{name === 'React' && <h1>This is React!</h1>}</>;
}

export default App;
```

{% hint style="warning" %}
Note that the falsy value of 0 is exceptively shown 0 to the screen.
{% endhint %}

```jsx
const number = 0;
return number && <div>contents</div>
```

0 will be shown on the screen.



### Do not render undefined

In the react components, you should not create situations in which functions return only undefined.

```jsx
import React from 'react';

function App() {
  const name = undefined;
  
  return name;
}

export default App;
```

This code occurs error as below.

App\(...\): Nothing was returned from render. This usually means a return statement is missing. Or, to render nothing, return null.

By using the logical Operators \(\|\|\), you can avoid errors above. You can specify the value to use when the return value is undefined.

```jsx
import React from 'react';

function App() {
  const name = undefined;
  
  return name || 'Return value is undefined';
}

export default App;
```



It's ok to render undefined inside JSX.

```jsx
import React from 'react';

function App() {
  const name = undefined;
  
  return <div>{name}</div>;
}

export default App;
```



If there is a phrase that you want to show if the name value is undefined, you can write the following code.

```jsx
import React from 'react';

function App() {
  const name = undefined;
  
  return <div>{name || 'Name is Undefined'}</div>;
}

export default App;
```



### Inline Styling

When applying styles to DOM elements in React, you should put them in the form of objects, not in strings. Style names use camelCase syntax without hyphen. For example, write it as backgroundColor rather than background-color.

```jsx
import React from 'react';

function App() {
  const name = 'React';
  const style = {
    backgroundColor: 'black',
    color: 'aqua',
    fontSize: '48px',
    fontWeight: 'bold',
    padding: '16px'
  };
  return <div style={style}>{name}</div>;
}

export default App;
```

Or, you can specify style values directly.

```jsx
import React from 'react';

function App() {
  const name = 'React';
  return (
    <div
      style={{
        backgroundColor: 'black',
        color: 'aqua',
        fontSize: '48px',
        fontWeight: 'bold',
        padding: '16px'
      }}
    >
      {name}
    </div>
  );
}

export default App;
```





