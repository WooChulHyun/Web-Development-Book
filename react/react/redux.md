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



### Creates action generating functions

modules/counter.js

```javascript
const INCREASE = 'counter/INCREASE'
const DECREASE = 'counter/DECREASE'

export const increase = () => ({type: INCREASE})
export const decrease = () => ({type: DECREASE})
```



### Creates initial state and reducer function

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



## todos module



### Defines action type

modules/todos.js

```javascript
const CHANGE_INPUT = 'todos/CHANGE_INPUT';
const INSERT = 'todos/INSERT';
const TOGGLE = 'todos/TOGGLE';
const REMOVE = 'todos/REMOVE';
```



### Create action generating function

modules/todos.js

```javascript
const CHANGE_INPUT = 'todos/CHANGE_INPUT';
const INSERT = 'todos/INSERT';
const TOGGLE = 'todos/TOGGLE';
const REMOVE = 'todos/REMOVE';

export const changeInput = input => ({
  type: CHANGE_INPUT,
  input
});

let id = 3;

export const insert = text => ({
  type: INSERT,
  todo: {
    id: id++,
    text,
    done: false
  }
});

export const toggle = id => ({
  type: TOGGLE,
  id
});

export const remove = id => ({
  type: REMOVE,
  id
});
```



### Creates initial state and reducer

```javascript
const CHANGE_INPUT = 'todos/CHANGE_INPUT';
const INSERT = 'todos/INSERT';
const TOGGLE = 'todos/TOGGLE';
const REMOVE = 'todos/REMOVE';

export const changeInput = input => ({
  type: CHANGE_INPUT,
  input
});

let id = 3;

export const insert = text => ({
  type: INSERT,
  todo: {
    id: id++,
    text,
    done: false
  }
});

export const toggle = id => ({
  type: TOGGLE,
  id
});

export const remove = id => ({
  type: REMOVE,
  id
});

const initialState = {
  input: '',
  todos: [
    {
      id: 1,
      text: 'HTML',
      done: true
    },
    {
      id: 2,
      text: 'CSS',
      done: false
    }
  ]
};

function todos(state = initialState, action) {
  switch (action.type) {
    case CHANGE_INPUT:
      return {
        ...state,
        input: action.input
      };
    case INSERT:
      return {
        ...state,
        todos: state.todos.concat(action.todo)
      };
    case TOGGLE:
      return {
        ...state,
        todos: state.todos.map(todo =>
          todo.id === action.id ? { ...todo, done: !todo.done } : todo
        )
      };
    case REMOVE:
      return {
        ...state,
        todos: state.todos.filter(todo => todo.id !== action.id)
      };
    default:
      return state;
  }
}

export default todos;
```



## Root reducer

Later, when you create a store using the createStore function, you must use only one reducer, so you need to merge the reducers you have created. You can do this easily using a utility function called combineReducers provided by Redux.

modules/index.js

```javascript
import { combineReducers } from 'redux';
import counter from './counter';
import todos from './todos';

const rootReducer = combineReducers({
  counter,
  todos
});

export default rootReducer;
```

If you set the file name as index.js, you can load it by typing only the directory name when you load it later.

```javascript
import rootReducer from './modules';
```

