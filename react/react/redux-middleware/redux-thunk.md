# redux-thunk

## redux-thunk

```bash
npm i redux-thunk
yarn add redux-thunk
```

The redux-thunk library allows you to create thunk functions and dispatch. Then redux middleware takes the function and calls it with the store's dispatch and getState as parameters.

```javascript
const sampleThunk = () => (dispatch, getState) => {
    // dispatch: can dispatches new actions
    // getState: can refers current state
}
```



index.js

```javascript
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';
import * as serviceWorker from './serviceWorker';

import { createStore, applyMiddleware, compose } from 'redux';
import rootReducer from './modules';
import { Provider } from 'react-redux';
// import loggerMiddleware from './lib/loggerMiddleware';
import { createLogger } from 'redux-logger';
import ReduxThunk from 'redux-thunk';

const composeEnhancer = window.__REDUX_DEVTOOLS_EXTENSION_COMPOSE__ || compose;
const logger = createLogger();

const store = createStore(
  rootReducer,
  composeEnhancer(applyMiddleware(logger, ReduxThunk))
);

ReactDOM.render(
  <Provider store={store}>
    <App />
  </Provider>,
  document.getElementById('root')
);

serviceWorker.unregister();
```



### Create thunk generating function

moudles/counter.js

```javascript
import { createAction, handleActions } from 'redux-actions';

const INCREASE = 'counter/INCREASE';
const DECREASE = 'counter/DECREASE';

export const increase = createAction(INCREASE);
export const decrease = createAction(DECREASE);

export const increaseAsync = () => dispatch => {
  setTimeout(() => {
    dispatch(increase());
  }, 1000);
};

export const decreaseAsync = () => dispatch => {
  setTimeout(() => {
    dispatch(decrease());
  }, 1000);
};

const initState = {
  number: 0
};

const counter = handleActions(
  {
    [INCREASE]: (state, action) => ({ number: state.number + 1 }),
    [DECREASE]: (state, action) => ({ number: state.number - 1 })
  },
  initState
);

export default counter;
```



container/CounterContainer.js

```javascript
import React from 'react';
import { connect } from 'react-redux';
import Counter from '../components/counter/Counter';
import { increaseAsync, decreaseAsync } from '../modules/counter';

const CounterContainer = ({ number, increaseAsync, decreaseAsync }) => {
  return (
    <Counter
      number={number}
      onIncrease={increaseAsync}
      onDecrease={decreaseAsync}
    />
  );
};

export default connect(
  state => ({
    number: state.counter.number
  }),
  {
    increaseAsync,
    decreaseAsync
  }
)(CounterContainer);
```

![](https://i.postimg.cc/PrpPv5cV/Rdux-middleware3.png)



### Web request asynchronous operation

```bash
npm i axios
yarn add axios
```



lib/api.js

```javascript
import axios from 'axios';

export const getPost = id =>
  axios.get(`https://jsonplaceholder.typicode.com/posts/${id}`);

export const getUsers = id =>
  axios.get(`https://jsonplaceholder.typicode.com/users`);
```



