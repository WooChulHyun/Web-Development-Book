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

The state type of the component must be an object.

### state for class component

src/Counter.js

```javascript
import React, { Component } from 'react';

class Counter extends Component {
  constructor(props) {
    super(props);
    this.state = {
      number: 0
    };
  }
  render() {
    const { number } = this.state;
    return (
      <div>
        <h1>{number}</h1>
        <button
          onClick={() => {
            this.setState({ number: number + 1 });
          }}
        >
          +1
        </button>
      </div>
    );
  }
}

export default Counter;
```

Or

```javascript
import React, { Component } from 'react';

class Counter extends Component {
  constructor(props) {
    super(props);
    this.state = {
      number: 0
    };
  }

  increaseNum = () => {
    const { number } = this.state;
    this.setState({ number: number + 1 });
  };

  render() {
    const { number } = this.state;
    return (
      <div>
        <h1>{number}</h1>
        <button onClick={this.increaseNum}>+1</button>
      </div>
    );
  }
}

export default Counter;
```



Take out state from constructor

```javascript
import React, { Component } from 'react';

class Counter extends Component {
  state = {
    number: 0
  };

  increaseNum = () => {
    const { number } = this.state;
    this.setState({ number: number + 1 });
  };

  render() {
    const { number } = this.state;
    return (
      <div>
        <h1>{number}</h1>
        <button onClick={this.increaseNum}>+1</button>
      </div>
    );
  }
}

export default Counter;
```



### prevState

When you update the state value using this.setState, the state is updated asynchronously. What if you call this.setState twice inside a function set in onClick like this:

```javascript
import React, { Component } from 'react';

class Counter extends Component {
  state = {
    number: 0
  };

  increaseNum = () => {
    this.setState({ number: number + 1 });
    console.log(this.state.number);
    
    this.setState({ number: number + 1 });
    console.log(this.state.number);
  };

  render() {
    const { number } = this.state;
    return (
      <div>
        <h1>{number}</h1>
        <button onClick={this.increaseNum}>+1</button>
      </div>
    );
  }
}

export default Counter;
```

![](https://i.postimg.cc/rp3M6sQC/Component1.png)

Because this.setState works asynchronously, you can see that console.log\(\) works first, so console.log\(\) displays the previous state number. And we wrote the code that adds 1 to the number twice , but only incremented by one.

To solve this problem we have to put the function as an argument to this.setState.

For example,

```javascript
this.setState((prevState, props) => {
  return {
    //undate contents
  }
})
```

If you do not need props, you can skip props.

```javascript
import React, { Component } from 'react';

class Counter extends Component {
  state = {
    number: 0
  };

  increaseNum = () => {
    this.setState(prevState => {
      return { number: prevState.number + 1 };
    });
    console.log(this.state.number);
    
    this.setState(prevState => {
      return { number: prevState.number + 1 };
    });
    console.log(this.state.number);
  };

  render() {
    const { number } = this.state;
    return (
      <div>
        <h1>{number}</h1>
        <button onClick={this.increaseNum}>+1</button>
      </div>
    );
  }
}

export default Counter;

```

![](https://i.postimg.cc/x1JSvHvG/Component2.png)

But still console.log\(this.state.number\) display previous number.



### this.setState callback

If you want to update a value using setState and want to do some particular task after, you can do by registering the callback function as the second parameter of setState.

```javascript
import React, { Component } from 'react';

class Counter extends Component {
  state = {
    number: 0
  };

  increaseNum = () => {
    this.setState(
      prevState => {
        return { number: prevState.number + 1 };
      },
      () => console.log(this.state.number)
    );
    
    this.setState(
      prevState => {
        return { number: prevState.number + 1 };
      },
      () => console.log(this.state.number)
    );
  };

  render() {
    const { number } = this.state;
    return (
      <div>
        <h1>{number}</h1>
        <button onClick={this.increaseNum}>+1</button>
      </div>
    );
  }
}

export default Counter;
```

![](https://i.postimg.cc/BnTkJg4v/Component3.png)



### useState

Before React v16.8, state was not available to functional components. Since v16.8, you can use state in functional components using a function called useState. Hooks are also used in this process.

The state type of a class component must be an object, but the state type of a functional component is free\(number, string, object, array, etc.\).

```javascript
import React, { useState } from 'react';

const Counter2 = () => {
  const [number, setNumber] = useState(0);

  const increaseNum = () => {
    setNumber(number + 1);
    console.log(number);
    setNumber(number + 1);
    console.log(number);
  };

  return (
    <div>
      <h1>{number}</h1>
      <button onClick={increaseNum}>+1</button>
    </div>
  );
};

export default Counter2;
```

This code has the same problem as the code above.

![](https://i.postimg.cc/rp3M6sQC/Component1.png)

You can solve this problem in a similar way that class component used to solve this problem.

```javascript
import React, { useState } from 'react';

const Counter2 = () => {
  const [number, setNumber] = useState(0);

  const increaseNum = () => {
    setNumber(prevState => {
      return prevState + 1;
    });
    console.log(number);
    setNumber(prevState => {
      return prevState + 1;
    });
    console.log(number);
  };

  return (
    <div>
      <h1>{number}</h1>
      <button onClick={increaseNum}>+1</button>
    </div>
  );
};

export default Counter2;
```

![](https://i.postimg.cc/x1JSvHvG/Component2.png)

But useState does not have a callback function. This can be solved using useEffect in Hooks.

