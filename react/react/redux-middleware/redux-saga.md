# redux-saga

## redux-saga

```bash
npm i redux-saga
yarn add redux-saga
```



moudles/counterSaga.js

```javascript
import { createAction, handleActions } from 'redux-actions';
import { delay, put, takeEvery, takeLatest } from 'redux-saga/effects';

const INCREASE = 'counter/INCREASE';
const DECREASE = 'counter/DECREASE';

const INCREASE_ASYNC = 'counter/INCREASE_ASYNC';
const DECREASE_ASYNC = 'counter/DECREASE_ASYNC';

export const increase = createAction(INCREASE);
export const decrease = createAction(DECREASE);

export const increaseAsync = createAction(INCREASE_ASYNC);
export const decreaseAsync = createAction(DECREASE_ASYNC);

function* increaseSaga() {
  yield delay(1000);
  yield put(increase());
}

function* decreaseSage() {
  yield delay(1000);
  yield put(decrease());
}

export function* counterSaga() {
  yield takeEvery(INCREASE_ASYNC, increaseSaga);
  yield takeLatest(INCREASE_ASYNC, decreaseSage);
}

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



modules/index.js

```javascript
import { combineReducers } from 'redux';
import { all } from 'redux-saga/effects';
import counter from './counter';
import { counterSaga } from './counterSaga';
import sample from './sample';
import loading from './loading';

const rootReducer = combineReducers({
  counter,
  sample,
  loading,
  counterSaga
});

export function* rootSaga() {
  yield all([counterSaga()]);
}

export default rootReducer;
```



src/index.js

```javascript
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';
import * as serviceWorker from './serviceWorker';

import { createStore, applyMiddleware, compose } from 'redux';
import rootReducer, { rootSaga } from './modules';
import { Provider } from 'react-redux';
// import loggerMiddleware from './lib/loggerMiddleware';
import { createLogger } from 'redux-logger';
import ReduxThunk from 'redux-thunk';
import createSagaMiddleware from 'redux-saga';

const composeEnhancer = window.__REDUX_DEVTOOLS_EXTENSION_COMPOSE__ || compose;
const logger = createLogger();
const sagaMiddleware = createSagaMiddleware();

const store = createStore(
  rootReducer,
  composeEnhancer(applyMiddleware(logger, ReduxThunk, sagaMiddleware))
);

sagaMiddleware.run(rootSaga);

ReactDOM.render(
  <Provider store={store}>
    <App />
  </Provider>,
  document.getElementById('root')
);

serviceWorker.unregister();
```



App.js

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

export const getUsers = () =>
  axios.get(`https://jsonplaceholder.typicode.com/users`);
```



modules/sampleSage.js

```javascript
import { createAction, handleActions } from 'redux-actions';
import * as api from '../lib/api';
import { put, call, takeLatest } from 'redux-saga/effects';
import { startLoading, finishLoading } from './loading';

const GET_POST = 'sample/GET_POST';
const GET_POST_SUCCESS = 'sample/GET_POST_SUCCESS';
const GET_POST_FAILURE = 'sample/GET_POST_FAILURE';

const GET_USERS = 'sample/GET_USERS';
const GET_USERS_SUCCESS = 'sample/GET_USERS_SUCCESS';
const GET_USERS_FAILURE = 'sample/GET_USERS_FAILURE';

export const getPostAsync = createAction(GET_POST, id => id);
export const getUserAsync = createAction(GET_USERS);

function* getPostSaga(action) {
  yield put(startLoading(GET_POST));

  try {
    const post = yield call(api.getPost, action.payload);
    yield put({
      type: GET_POST_SUCCESS,
      payload: post.data
    });
  } catch (e) {
    yield put({
      type: GET_POST_FAILURE,
      payload: e,
      error: true
    });
  }
  yield put(finishLoading(GET_POST));
}

function* getUserSaga() {
  yield put(startLoading(GET_USERS));

  try {
    const user = yield call(api.getUsers);
    yield put({
      type: GET_USERS_SUCCESS,
      payload: user.data
    });
  } catch (e) {
    yield put({
      type: GET_USERS_FAILURE,
      payload: e,
      error: true
    });
  }
  yield put(finishLoading(GET_USERS));
}

export function* sampleSaga() {
  yield takeLatest(GET_POST, getPostSaga);
  yield takeLatest(GET_USERS, getUserSaga);
}

const initialState = {
  post: null,
  users: null
};

const sample = handleActions(
  {
    [GET_POST_SUCCESS]: (state, action) => ({
      ...state,
      loading: {
        ...state.loading,
        GET_POST: false
      },
      post: action.payload
    }),
    [GET_USERS_SUCCESS]: (state, action) => ({
      ...state,
      loading: {
        ...state.loading,
        GET_USERS: false
      },
      users: action.payload
    })
  },
  initialState
);

export default sample;
```



modules/index.js

```javascript
import { combineReducers } from 'redux';
import { all } from 'redux-saga/effects';
import counter from './counter';
import { counterSaga } from './counterSaga';
import { sampleSaga } from './sampleSaga';
import sample from './sample';
import loading from './loading';

const rootReducer = combineReducers({
  counter,
  sample,
  loading,
  counterSaga,
  sampleSaga
});

export function* rootSaga() {
  yield all([counterSaga(), sampleSaga()]);
}

export default rootReducer;
```



containers/SampleContainer.js

```javascript
import React, { useEffect } from 'react';
import { connect } from 'react-redux';
import Sample from '../components/sample';
import { getPostAsync, getUserAsync } from '../modules/sampleSaga';

const SampleContainer = ({
  getPostAsync,
  getUserAsync,
  post,
  users,
  loadingPost,
  loadingUsers
}) => {
  useEffect(() => {
    const fn = async () => {
      try {
        await getPostAsync(1);
        await getUserAsync();
      } catch (e) {
        console.log(e);
      }
    };
    fn();
  }, [getPostAsync, getUserAsync]);
  return (
    <Sample
      post={post}
      users={users}
      loadingPost={loadingPost}
      loadingUsers={loadingUsers}
    />
  );
};

export default connect(
  ({ sample, loading }) => ({
    post: sample.post,
    users: sample.users,
    loadingPost: loading.GET_POST,
    loadingUsers: loading.GET_USERS
  }),
  {
    getPostAsync,
    getUserAsync
  }
)(SampleContainer);
```



App.js

```javascript
import React from 'react';
import './App.css';
import SampleContainer from './containers/SampleContainer';

function App() {
  return (
    <div>
      <SampleContainer />
    </div>
  );
}

export default App;
```

