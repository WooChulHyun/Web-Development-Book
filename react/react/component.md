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



