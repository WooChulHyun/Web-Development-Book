# JSX

JSX is an extension of JavaScript and looks very much like MXL. Code written in JSX is converted to plain JavaScript code by barbell when the code is been bundling before being executed in a browser.

```javascript
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

```javascript
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

```javascript
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

```javascript
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

```javascript
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

```javascript
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

```javascript
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

```javascript
import React from 'react';

function App() {
  const name = 'JavaScrip';
  
  return <>{name === 'React' ? <h1>This is React!</h1> : null}</>;
}

export default App;
```

If you render null \(falsy value\) like above code, it will show nothing. But you can do the same thing with shorter code than this.

```javascript
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

```javascript
const number = 0;
return number && <div>contents</div>
```

0 will be shown on the screen.



### Do not render undefined

In the react components, you should not create situations in which functions return only undefined.

```javascript
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

```javascript
import React from 'react';

function App() {
  const name = undefined;
  
  return name || 'Return value is undefined';
}

export default App;
```



It's ok to render undefined inside JSX.

```javascript
import React from 'react';

function App() {
  const name = undefined;
  
  return <div>{name}</div>;
}

export default App;
```



If there is a phrase that you want to show if the name value is undefined, you can write the following code.

```javascript
import React from 'react';

function App() {
  const name = undefined;
  
  return <div>{name || 'Name is Undefined'}</div>;
}

export default App;
```



### Inline Styling

When applying styles to DOM elements in React, you should put them in the form of objects, not in strings. Style names use camelCase syntax without hyphen. For example, write it as backgroundColor rather than background-color.

```javascript
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

```javascript
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



### className instead of class

When using CSS classes in regular HTML, use the class attribute, such as `<div class = "myclass> </ div>`, but in JSX you must write it as className, not class.

src/App.css

```css
.react {
  background: black;
  color: aqua;
  fontsize: 48px;
  fontweight: bold;
  padding: 16px;
}
```

src/App.js

```javascript
import React from 'react';
import './App.css';

function App() {
  const name = 'React';
  return <div className='react'>{name}</div>;
}

export default App;
```



### Closing Tag

When you write HTML code, you sometimes write code without closing the tag. For example, `<input>`, `<br>`. But in JSX, if you don't close tag, it occurs an error.

```javascript
import React from 'react';
import './App.css';

function App() {
  const name = 'React';
  return (
    <>
      <div className='react'>{name}</div>
      <input>
    </>
  );
}

export default App;
```

```text
./src/App.js
  Line 10:  Parsing error: Unterminated JSX contents

   8 |       <div className='react'>{name}</div>
   9 |       <input>
> 10 |     </>
     |        ^
  11 |   );
  12 | }
  13 | 
```



To resolve this error, you have to close the input tag.

```javascript
import React from 'react';
import './App.css';

function App() {
  const name = 'React';
  return (
    <>
      <div className='react'>{name}</div>
      <input></input>
    </>
  );
}

export default App;
```



If there is no additional content between the tags, you can also write: 

```javascript
import React from 'react';
import './App.css';

function App() {
  const name = 'React';
  return (
    <>
      <div className='react'>{name}</div>
      <input />
    </>
  );
}

export default App;
```

These tags are called self-closing tags.



### Annotation

Writing annotation in JSX is different from composing annotation in plain JavaScript.

```javascript
import React from 'react';
import './App.css';

function App() {
  const name = 'React';
  return (
    <>
    {/* This is how to write annotation in JSX */}
      <div 
        className='react' // You can write annotation with same way with JavaScript 
                          // if the tag has multiple lines
      >
        {name}
      </div>
      // This will be displayed in your screen
      /* This will be displayed in your screen */
      <input />
    </>
  );
}

export default App;
```



