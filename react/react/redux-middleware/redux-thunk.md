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

modules/counter.js

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

export const getUsers = () =>
  axios.get(`https://jsonplaceholder.typicode.com/users`);
```



modules/sample.js

```javascript
import { handleActions } from 'redux-actions';
import * as api from '../lib/api';

const GET_POST = 'sample/GET_POST';
const GET_POST_SUCCESS = 'sample/GET_POST_SUCCESS';
const GET_POST_FAILURE = 'sample/GET_POST_FAILURE';

const GET_USERS = 'sample/GET_USERS';
const GET_USERS_SUCCESS = 'sample/GET_USERS_SUCCESS';
const GET_USERS_FAILURE = 'sample/GET_USERS_FAILURE';

export const getPostThunk = id => async dispatch => {
  dispatch({ type: GET_POST });
  try {
    const response = await api.getPost(id);
    dispatch({
      type: GET_POST_SUCCESS,
      payload: response.data
    });
  } catch (e) {
    dispatch({
      type: GET_POST_FAILURE,
      payload: e,
      error: true
    });
    throw e;
  }
};

export const getUserThunk = id => async dispatch => {
  dispatch({ type: GET_USERS });
  try {
    const response = await api.getUsers(id);
    dispatch({
      type: GET_USERS_SUCCESS,
      payload: response.data
    });
  } catch (e) {
    dispatch({
      type: GET_USERS_FAILURE,
      payload: e,
      error: true
    });
    throw e;
  }
};

const initialState = {
  loading: {
    GET_POST: false,
    GET_USERS: false
  },
  post: null,
  users: null
};

const sample = handleActions(
  {
    [GET_POST]: state => ({
      ...state,
      loading: {
        ...state.loading,
        GET_POST: true
      }
    }),
    [GET_POST_SUCCESS]: (state, action) => ({
      ...state,
      loading: {
        ...state.loading,
        GET_POST: false
      },
      post: action.payload
    }),
    [GET_POST_FAILURE]: (state, action) => ({
      ...state,
      loading: {
        ...state.loading,
        GET_POST: false
      }
    }),
    [GET_USERS]: state => ({
      ...state,
      loading: {
        ...state.loading,
        GET_USERS: true
      }
    }),
    [GET_USERS_SUCCESS]: (state, action) => ({
      ...state,
      loading: {
        ...state.loading,
        GET_USERS: false
      },
      users: action.payload
    }),
    [GET_USERS_FAILURE]: (state, action) => ({
      ...state,
      loading: {
        ...state.loading,
        GET_USER: false
      }
    })
  },
  initialState
);

export default sample;
```



modules/index.js

```javascript
import { combineReducers } from 'redux';
import sample from './sample';

const rootReducer = combineReducers({
  sample
});

export default rootReducer;
```



components/Sample.js

```javascript
import React from 'react';

const sample = ({ loadingPost, loadingUsers, post, users }) => {
  return (
    <div>
      <section>
        <h1>Post</h1>
        {loadingPost && 'loading...'}
        {!loadingPost && post && (
          <div>
            <h3>{post.title}</h3>
            <h3>{post.body}</h3>
          </div>
        )}
      </section>
      <hr />
      <section>
        <h1>User</h1>
        {loadingUsers && 'loading...'}
        {!loadingUsers && users && (
          <ul>
            {users.map(user => (
              <li key={user.id}>
                {user.username} ({user.email})
              </li>
            ))}
          </ul>
        )}
      </section>
    </div>
  );
};

export default sample;
```



containers/SampleContainer.js

```javascript
import React, { useEffect } from 'react';
import { connect } from 'react-redux';
import Sample from '../components/sample';
import { getPostThunk, getUserThunk } from '../modules/sample';

const SampleContainer = ({
  getPostThunk,
  getUserThunk,
  post,
  users,
  loadingPost,
  loadingUsers
}) => {
  useEffect(() => {
    getPostThunk(1);
    getUserThunk();
  }, [getPostThunk, getUserThunk]);
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
  ({ sample }) => ({
    post: sample.post,
    users: sample.users,
    loadingPost: sample.loading.GET_POST,
    loadingUsers: sample.loading.GET_USERS
  }),
  {
    getPostThunk,
    getUserThunk
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

![](https://i.postimg.cc/63RGSQ9j/redux-think1.png)



## Refactoring

### API request

lib/createRequestThunk.js

```javascript
export default function createRequestThunk(type, request) {
  const SUCCESS = `${type}_SUCCESS`;
  const FAILURE = `${type}_FAILURE`;
  return params => async dispatch => {
    dispatch({ type });
    try {
      const response = await request(params);
      dispatch({
        type: SUCCESS,
        payload: response.data
      });
    } catch (e) {
      dispatch({
        type: FAILURE,
        payload: e,
        error: true
      });
      throw e;
    }
  };
}
```



modules/sample.js

```javascript
import { handleActions } from 'redux-actions';
import * as api from '../lib/api';
import createRequestThunk from '../lib/createRequestThunk';

const GET_POST = 'sample/GET_POST';
const GET_POST_SUCCESS = 'sample/GET_POST_SUCCESS';
const GET_POST_FAILURE = 'sample/GET_POST_FAILURE';

const GET_USERS = 'sample/GET_USERS';
const GET_USERS_SUCCESS = 'sample/GET_USERS_SUCCESS';
const GET_USERS_FAILURE = 'sample/GET_USERS_FAILURE';

export const getPostThunk = createRequestThunk(GET_POST, api.getPost);
export const getUserThunk = createRequestThunk(GET_USERS, api.getUsers);

const initialState = {
  loading: {
    GET_POST: false,
    GET_USERS: false
  },
  post: null,
  users: null
};

(...)
```

Separates the thunk function, which has repeated logic that works every time an API request is made.



### Loading

modules/loading.js

```javascript
import { createAction, handleActions } from 'redux-actions';

const START_LOADING = 'loading/START_LOADING';
const FINISH_LOADING = 'loading/FINISH_LOADING';

export const startLoading = createAction(
  START_LOADING,
  requestType => requestType
);

export const finishLoading = createAction(
  FINISH_LOADING,
  requestType => requestType
);

const initialState = {};

const loading = handleActions(
  {
    [START_LOADING]: (state, action) => ({
      ...state,
      [action.payload]: true
    }),
    [FINISH_LOADING]: (state, action) => ({
      ...state,
      [action.payload]: false
    })
  },
  initialState
);

export default loading;
```



modules/index.js

```javascript
import { combineReducers } from 'redux';
import sample from './sample';
import loading from './loading';

const rootReducer = combineReducers({
  sample,
  loading
});

export default rootReducer;
```



lib/createRequestThunk.js

```javascript
import { startLoading, finishLoading } from '../modules/loading';

export default function createRequestThunk(type, request) {
  const SUCCESS = `${type}_SUCCESS`;
  const FAILURE = `${type}_FAILURE`;
  return params => async dispatch => {
    dispatch(startLoading(type));
    try {
      const response = await request(params);
      dispatch({
        type: SUCCESS,
        payload: response.data
      });
      dispatch(finishLoading(type));
    } catch (e) {
      dispatch({
        type: FAILURE,
        payload: e,
        error: true
      });
      dispatch(startLoading(type));
      throw e;
    }
  };
}
```



containers/SampleContainer.js

```javascript
import React, { useEffect } from 'react';
import { connect } from 'react-redux';
import Sample from '../components/sample';
import { getPostThunk, getUserThunk } from '../modules/sample';

const SampleContainer = ({
  getPostThunk,
  getUserThunk,
  post,
  users,
  loadingPost,
  loadingUsers
}) => {
  useEffect(() => {
    getPostThunk(1);
    getUserThunk();
  }, [getPostThunk, getUserThunk]);
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
    getPostThunk,
    getUserThunk
  }
)(SampleContainer);
```



modules/sample.js

```javascript
import { handleActions } from 'redux-actions';
import * as api from '../lib/api';
import createRequestThunk from '../lib/createRequestThunk';

const GET_POST = 'sample/GET_POST';
const GET_POST_SUCCESS = 'sample/GET_POST_SUCCESS';
// const GET_POST_FAILURE = 'sample/GET_POST_FAILURE';

const GET_USERS = 'sample/GET_USERS';
const GET_USERS_SUCCESS = 'sample/GET_USERS_SUCCESS';
// const GET_USERS_FAILURE = 'sample/GET_USERS_FAILURE';

export const getPostThunk = createRequestThunk(GET_POST, api.getPost);
export const getUserThunk = createRequestThunk(GET_USERS, api.getUsers);

const initialState = {
  post: null,
  users: null
};

const sample = handleActions(
  {
    [GET_POST_SUCCESS]: (state, action) => ({
      ...state,
      post: action.payload
    }),
    [GET_USERS_SUCCESS]: (state, action) => ({
      ...state,
      users: action.payload
    })
  },
  initialState
);

export default sample;
```



#### error control:

SampleContainer.js

```javascript
import React, { useEffect } from 'react';
import { connect } from 'react-redux';
import Sample from '../components/sample';
import { getPostThunk, getUserThunk } from '../modules/sample';

const SampleContainer = ({
  getPostThunk,
  getUserThunk,
  post,
  users,
  loadingPost,
  loadingUsers
}) => {
  useEffect(() => {
    const fn = async () => {
      try {
        await getPostThunk(1);
        await getUserThunk();
      } catch (e) {
        console.log(e);
      }
    };
    fn();
  }, [getPostThunk, getUserThunk]);
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
    getPostThunk,
    getUserThunk
  }
)(SampleContainer);
```

