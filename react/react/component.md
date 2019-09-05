# Component

## Class component and Functional component

There are functional components and class components in React.

Class Component:

```javascript
import React, { Component } from 'react';

class App extends Component {
  render() {
    const name = 'react';
    return <div className='react'>{name}</div>;
  }
}

export default App;
```



Functional Component:

```javascript
import React from 'react';

function App() {
  const name = 'React';
  return <div className='react'>{name}</div>;
}

export default App;
```



Before React v16.8, functional components couldn't use state and lifecycle, but since v16.8, the introduction of the Hooks feature allows us to do similar things in different ways. React official manuals also recommend using functional components and hooks when creating new components.



## Create component

src/App.js

```javascript
import React from 'react';
import MyComponent from './MyComponent';

function App() {
  return (
    <>
      <MyComponent />
    </>
  );
}

export default App;
```



src/MyComponent.js

```javascript
import React from 'react';

const MyComponent = () => {
  return <div>MyComponent</div>;
};

export default MyComponent;
```



## props

props is a short for properties that is used to set component properties. The props value can be set in the parent component where the component is called and used \(in this case, the App component is parent\).



### Setting props

src/App.js

```javascript
import React from 'react';
import MyComponent from './MyComponent';

function App() {
  return (
    <>
      <MyComponent name='react' />
    </>
  );
}

export default App;
```



### Using props

scr/MyComponent.js

```javascript
import React from 'react';

const MyComponent = props => {
  return <div>Hello {props.name}!</div>;
};

export default MyComponent;
```



## defaultProps

Setting default props that are shown by default when you do not specify props in parent component.

scr/MyComponent.js

```javascript
import React from 'react';

const MyComponent = props => {
  return <div>Hello {props.name}!</div>;
};

MyComponent.defaultProps = {
  name: 'Default Name'
};

export default MyComponent;
```



