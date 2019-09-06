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



## children

children is props that is used to show the contents between the tags.

src/App.js

```javascript
import React from 'react';
import MyComponent from './MyComponent';

function App() {
  return (
    <>
      <MyComponent>Children</MyComponent>
    </>
  );
}

export default App;
```



src/MyComponent.js

```javascript
import React from 'react';

const MyComponent = props => {
  return (
    <div>
      Hello {props.name}!<br />
      Children value is {props.children}
    </div>
  );
};

MyComponent.defaultProps = {
  name: 'Default Name'
};

export default MyComponent;
```



## Using destructuring assignment

Whenever you use props value from MyComponent, props keyword is prefixed like props.name, props.children. To make this task easier, we use ES6's destructuring assignment syntax.



src/MyComponent.js

```javascript
import React from 'react';

const MyComponent = props => {
  const { name, children } = props;
  return (
    <div>
      Hello {name}!<br />
      Children value is {children}
    </div>
  );
};

MyComponent.defaultProps = {
  name: 'Default Name'
};

export default MyComponent;
```

Or

```javascript
import React from 'react';

const MyComponent = ({ name, children }) => {
  return (
    <div>
      Hello {name}!<br />
      Children value is {children}
    </div>
  );
};

MyComponent.defaultProps = {
  name: 'Default Name'
};

export default MyComponent;
```



## propTypes

### propTypes

Use propTypes to specify the required props for a component or to specify the type of props. First of all, to use propTypes, you have to use the import statement at the top of your code.

```javascript
import React from 'react';
import PropTypes from 'prop-types';

const MyComponent = ({ name, children }) => {
  return (
    <div>
      Hello {name}!<br />
      Children value is {children}
    </div>
  );
};

MyComponent.defaultProps = {
  name: 'Default Name'
};

MyComponent.propTypes = {
  name: PropTypes.string
};

export default MyComponent;
```



### isRequired

To occur a warning when no propTypes are specified, add isRequired  after specifying propTypes.

```javascript
import React from 'react';
import PropTypes from 'prop-types';

const MyComponent = ({ name, children }) => {
  return (
    <div>
      Hello {name}!<br />
      Children value is {children}
    </div>
  );
};

MyComponent.defaultProps = {
  name: 'Default Name'
};

MyComponent.propTypes = {
  name: PropTypes.string.isRequired
};

export default MyComponent;
```



### Kind of PropTypes

* array
* arrayOf\(other PropType\): Refers to an array of specific PropType. For example, arrayOf\(PropTypes.number\) is an array consist of numbers.
* bool: true or false value
* func: function
* number
* object
* string
* symbol: ES6's Symbol
* node: Everything you can be rendered\(number, string, JSX code, children\)
* instanceOf\(class\): An instance of a particular class \(ex. instanceof\(MyClass\)\)
* oneOf\(\['dog', 'cat'\]\): One of the given array elements
* oneOfType\(\[React.PropTypes.string, PropTypes.number\]\): One of the given array kind
* objectOf\(React.PropTypes.number\): PropType object which all key values are given as arguments
* shape\({ name: PropTypes.string, num: PropTypes.number }\): The object with the given schema
* any



## Class component with props

```javascript
import React, { Component } from 'react';
import PropTypes from 'prop-types';

class MyComponent extends Component {
  render() {
    const { name, children } = this.props;
    return (
      <div>
        Hello {name}! <br />
        Children value is {children}
      </div>
    );
  }
}

MyComponent.defaultProps = {
  name: 'Default Name'
};

MyComponent.propTypes = {
  name: PropTypes.string.isRequired
};

export default MyComponent;
```

Or

```javascript
import React, { Component } from 'react';
import PropTypes from 'prop-types';

class MyComponent extends Component {
  static defaultProps = {
    name: 'Default Name'
  };

  static propTypes = {
    name: PropTypes.string.isRequired
  };

  render() {
    const { name, children } = this.props;
    return (
      <div>
        Hello {name}! <br />
        Children value is {children}
      </div>
    );
  }
}

export default MyComponent;
```



## state

In React, state is a value that can change inside a component. props is the value set by the parent component, and the component itself can only use those props for read-only.

Currently, when you use MyComponent in App component, you have to change props in App component which is parents component to change the value. In MyComponent,  you cannot directly change the name value. \(You can change props value by taking them in the state.\)

There are currently two kinds of state in React. One is the state that a class component has, and the other is the state used by a function called useState in a functional component.

