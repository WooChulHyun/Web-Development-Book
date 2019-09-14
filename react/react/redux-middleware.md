# Redux Middleware

## Initial preparation

```bash
npm i redux react-redux redux-actions
yarn add redux react-redux redux-actions
```



modules.counter.js

```javascript
import { createAction, handleActions } from 'redux-actions';

const INCREASE = 'counter/INCREASE';
const DECREASE = 'counter/DECREASE';

export const increase = createAction(INCREASE);
export const decrease = createAction(DECREASE);

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



modules.index.js

```javascript
import { combineReducers } from 'redux';
import counter from './counter';

const rootReducer = combineReducers({
  counter
});

export default rootReducer;
```



src/index.js

```javascript
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';
import * as serviceWorker from './serviceWorker';

import { createStore } from 'redux';
import rootReducer from './modules';
import { Provider } from 'react-redux';

const store = createStore(
  rootReducer,
  window.__REDUX_DEVTOOLS_EXTENSION__ && window.__REDUX_DEVTOOLS_EXTENSION__()
);

ReactDOM.render(
  <Provider store={store}>
    <App />
  </Provider>,
  document.getElementById('root')
);

serviceWorker.unregister();
```



components/Counter.js

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



containers/CounterContainer.js

```javascript
import React from 'react';
import { connect } from 'react-redux';
import Counter from '../components/counter/Counter';
import { increase, decrease } from '../modules/counter';

const CounterContainer = ({ number, increase, decrease }) => {
  return (
    <Counter number={number} onIncrease={increase} onDecrease={decrease} />
  );
};

export default connect(
  state => ({
    number: state.counter.number
  }),
  {
    increase,
    decrease
  }
)(CounterContainer);
```



 app.js

```javascript
import React from 'react';
import './App.css';
import CounterContainer from './containers/CounterContainer';

function App() {
  return (
    <div>
      <CounterContainer />
    </div>
  );
}

export default App;
```











