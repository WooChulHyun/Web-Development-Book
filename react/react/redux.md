# Redux

## Installation

```bash
npm i redux react-redux
yarn add redux react-redux
```



## Preparing the UI

App.js

```javascript
import React from 'react';
import Counter from './components/counter/counter';
import Todos from './components/todo/Todo';

function App() {
  return (
    <div>
      <Counter number={0} />
      <hr />
      <Todos />
    </div>
  );
}

export default App;
```



Counter.js

```javascript
import React from 'react';

const counter = ({ number, onIncrease, onDecrease }) => {
  return (
    <div>
      <h1>{number}</h1>
      <div>
        <button onClick={onIncrease}>+1</button>
        <button onClick={onDecrease}>-1</button>
      </div>
    </div>
  );
};

export default counter;
```



Todos.js

```javascript
import React from 'react';

const TodoItem = ({ todo, onToggle, onRemove }) => {
  return (
    <div>
      <input type='checkbox' />
      <span>example text</span>
      <button>Delete</button>
    </div>
  );
};

const Todos = ({
  input,
  todos,
  onChangeInput,
  onInsert,
  onToggle,
  onRemove
}) => {
  const onSubmit = e => {
    e.preventDefault();
  };
  return (
    <div>
      <form onSubmit={onSubmit}>
        <input />
        <button type='submit'>Add</button>
      </form>
      <div>
        <TodoItem />
        <TodoItem />
        <TodoItem />
        <TodoItem />
        <TodoItem />
      </div>
    </div>
  );
};

export default Todos;
```

![](https://i.postimg.cc/GmWg3Cw1/Redux1.png)



## counter module

Code that writes action types, action generating functions, and reducers using the Ducks pattern is called a module.



### Defines action type

modules/counter.js

```javascript
const INCREASE = 'counter/INCREASE'
const DECREASE = 'counter/DECREASE'
```

The first thing we need to do is define the action type. Action type is defined in capital letters, and the string content is written in the form of 'module name / action name'.



### Create action generating functions

modules/counter.js

```javascript
const INCREASE = 'counter/INCREASE'
const DECREASE = 'counter/DECREASE'

export const increase = () => ({type: INCREASE})
export const decrease = () => ({type: DECREASE})
```



### Create initial state and reducer function

modules/counter.js

```javascript
const INCREASE = 'counter/INCREASE';
const DECREASE = 'counter/DECREASE';

export const increase = () => ({ type: INCREASE });
export const decrease = () => ({ type: DECREASE });

const initState = {
  number: 0
};

function counter(state = initState, action) {
  switch (action.type) {
    case INCREASE:
      return {
        number: state.number + 1
      };
    case DECREASE:
      return {
        number: state.number - 1
      };
    default:
      return state;
  }
}

export default counter;
```

