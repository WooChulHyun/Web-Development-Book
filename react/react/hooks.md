# Hooks

## useuseState

One useState function can manage only one state value. If the component has multiple states to manage, useState can be used multiple times.

App.js

```javascript
import React from 'react';
import Info from './hooksFils/Info';

const App = () => {
  return <Info />;
};

export default App;
```



Info.js

```javascript
import React, { useState } from 'react';

const Info = () => {
  const [name, setName] = useState('');
  const [nickname, setNickname] = useState('');

  const changeName = e => {
    setName(e.target.value);
  };

  const changeNickname = e => {
    setNickname(e.target.value);
  };

  return (
    <div>
      <div>
        <input value={name} onChange={changeName} />
        <input value={nickname} onChange={changeNickname} />
      </div>
      <div>
        <div>
          <b>Name: </b> {name}
        </div>
        <div>
          <b>Nickname: </b> {nickname}
        </div>
      </div>
    </div>
  );
};

export default Info;
```

![](https://i.postimg.cc/mr5pHP4M/Hooks1.png)



## useEffect

useEffect is a Hook that can be set to perform a specific action each time a React component is rendered. It is similar to the combination of componentDidMount and componentDidUpdate for class components.

```javascript
import React, { useState, useEffect } from 'react';

const Info = () => {
  const [name, setName] = useState('');

  useEffect(() => {
    console.log('rendering completed 1');
    console.log({
      name
    });
  });

  const [nickname, setNickname] = useState('');

  useEffect(() => {
    console.log('rendering completed 2');
    console.log({
      nickname
    });
  });

  const changeName = e => {
    setName(e.target.value);
  };

  const changeNickname = e => {
    setNickname(e.target.value);
  };

  return (
    <div>
      <div>
        <input value={name} onChange={changeName} />
        <input value={nickname} onChange={changeNickname} />
      </div>
      <div>
        <div>
          <b>Name: </b> {name}
        </div>
        <div>
          <b>Nickname: </b> {nickname}
        </div>
      </div>
    </div>
  );
};

export default Info;
```

![](https://i.postimg.cc/J4B84Hff/Hooks2.png)

![](https://i.postimg.cc/qRhrhtt6/Hooks3.png)



### When you want to make useEffect to run only when a certain value is updated

As you can see in the picture above, both useEffects are working together whether name or nickname are changing.

The problem can be solved by just putting a value to detect the change in the array passed as the second parameter of useEffect.

```javascript
import React, { useState, useEffect } from 'react';

const Info = () => {
  const [name, setName] = useState('');

  useEffect(() => {
    console.log('rendering completed 1');
    console.log({
      name
    });
  }, [name]);

  const [nickname, setNickname] = useState('');

  useEffect(() => {
    console.log('rendering completed 2');
    console.log({
      nickname
    });
  }, [nickname]);

  const changeName = e => {
    setName(e.target.value);
  };

  const changeNickname = e => {
    setNickname(e.target.value);
  };

  return (
    <div>
      <div>
        <input value={name} onChange={changeName} />
        <input value={nickname} onChange={changeNickname} />
      </div>
      <div>
        <div>
          <b>Name: </b> {name}
        </div>
        <div>
          <b>Nickname: </b> {nickname}
        </div>
      </div>
    </div>
  );
};

export default Info;
```

![](https://i.postimg.cc/7ZkQS5RJ/Hooks4.png)



### Way to run only when mounted

Put an empty array as the second parameter of useEffect.

```javascript
import React, { useState, useEffect } from 'react';

const Info = () => {
  const [name, setName] = useState('');

  useEffect(() => {
    console.log('Mounted 1');
  }, []);

  const [nickname, setNickname] = useState('');

  useEffect(() => {
    console.log('Mounted 2');
  }, []);

  const changeName = e => {
    setName(e.target.value);
  };

  const changeNickname = e => {
    setNickname(e.target.value);
  };

  return (
    <div>
      <div>
        <input value={name} onChange={changeName} />
        <input value={nickname} onChange={changeNickname} />
      </div>
      <div>
        <div>
          <b>Name: </b> {name}
        </div>
        <div>
          <b>Nickname: </b> {nickname}
        </div>
      </div>
    </div>
  );
};

export default Info;
```

![](https://i.postimg.cc/HkYRfJtD/Hooks5.png)



### Cleanup

If you want to do something before the component is unmounted or to be updated, useEffect should return the cleanup function.

```javascript
import React, { useState, useEffect } from 'react';

const Info = () => {
  const [name, setName] = useState('');
  const [nickname, setNickname] = useState('');

  useEffect(() => {
    console.log('Effect');
    console.log({ name, nickname });
    return () => {
      console.log('Cleanup');
      console.log({ name, nickname });
    };
  });

  const changeName = e => {
    setName(e.target.value);
  };

  const changeNickname = e => {
    setNickname(e.target.value);
  };

  return (
    <div>
      <div>
        <input value={name} onChange={changeName} />
        <input value={nickname} onChange={changeNickname} />
      </div>
      <div>
        <div>
          <b>Name: </b> {name}
        </div>
        <div>
          <b>Nickname: </b> {nickname}
        </div>
      </div>
    </div>
  );
};

export default Info;
```

![](https://i.postimg.cc/vTMDyLBt/Hooks6.png)

![](https://i.postimg.cc/8z35cVc5/Hooks7.png)



If you want to use the cleanup function only when it is unmounted, you can put an empty array in the second parameter of the useEffect function.

```javascript
  useEffect(() => {
    console.log('Effect');
    return () => {
      console.log('Cleanup');
    };
  }, []);
```



## useReducer

```javascript
const [state, dispatch] = useReducer(reducer, initialArg, init);
```

Alternative function for useState. useReducer is a hook used when you want to update various states to different values according to various component situations than useState.

The reducer returns a new state by receiving state and action value for the update. 

```javascript
(state, action) => newState 
```

Creating a new state in the reducer function must be kept invariability.

The action value is mainly composed of the following form.

```javascript
{
  type: 'INCREMENT'
  // You can add if you need
}
```

In Redux, the action object used must have a type field indicating what action it is, but the action object used by useReducer does not necessarily have a type. It can be a string or a number or an object.



```javascript
import React, { useReducer } from 'react';

const initialState = { value: 0 };

function reducer(state, action) {
  switch (action.type) {
    case 'increment':
      return { value: state.value + 1 };
    case 'decrement':
      return { value: state.value - 1 };
    default:
      throw state;
  }
}

const Counter = () => {
  const [state, dispatch] = useReducer(reducer, initialState);

  return (
    <>
      Count: {state.value}
      <button onClick={() => dispatch({ type: 'increment' })}>+</button>
      <button onClick={() => dispatch({ type: 'decrement' })}>-</button>
    </>
  );
};

export default Counter;
```



## useMemo

```javascript
import React, { useState } from 'react';

const getAverage = numbers => {
  console.log('Calculating average value..');
  if (numbers.length === 0) return 0;
  const sum = numbers.reduce((a, b) => a + b);
  return sum / numbers.length;
};

const Average = () => {
  const [list, setList] = useState([]);
  const [number, setNumber] = useState('');

  const onChange = e => {
    setNumber(e.target.value);
  };
  
  const onInsert = () => {
    const nextList = list.concat(parseInt(number));
    setList(nextList);
    setNumber('');
  };

  return (
    <div>
      <input value={number} onChange={onChange} />
      <button onClick={onInsert}>Add</button>
      <ul>
        {list.map((value, index) => (
          <li key={index}>{value}</li>
        ))}
      </ul>
      <div>
        <b>Average:</b> {getAverage(list)}
      </div>
    </div>
  );
};

export default Average;
```

![](https://i.postimg.cc/TPqgQkHj/Hooks8.png)



Every time you type in the input, the average value is calculated. This is a waste. You can use useMemo Hook to optimize. The operation is executed only when a certain value is changed during the rendering process, and if the certain value is not changed, the previous operation is used again.

```javascript
import React, { useState, useMemo } from 'react';

const getAverage = numbers => {
  console.log('Calculating average value..');
  if (numbers.length === 0) return 0;
  const sum = numbers.reduce((a, b) => a + b);
  return sum / numbers.length;
};

const Average = () => {
  const [list, setList] = useState([]);
  const [number, setNumber] = useState('');

  const onChange = e => {
    setNumber(e.target.value);
  };

  const onInsert = () => {
    const nextList = list.concat(parseInt(number));
    setList(nextList);
    setNumber('');
  };

  const avg = useMemo(() => getAverage(list), [list]);

  return (
    <div>
      <input value={number} onChange={onChange} />
      <button onClick={onInsert}>Add</button>
      <ul>
        {list.map((value, index) => (
          <li key={index}>{value}</li>
        ))}
      </ul>
      <div>
        <b>Average:</b> {avg}
      </div>
    </div>
  );
};

export default Average;
```

![](https://i.postimg.cc/SKRFy5FV/Hooks9.png)



## useCallback

In the code above, there are functions called onChange and onInsert. This declaration creates a new functions each time the component is rerendered.

```javascript
import React, { useState, useCallback, useMemo } from 'react';

const getAverage = numbers => {
  console.log('Calculating average value..');
  if (numbers.length === 0) return 0;
  const sum = numbers.reduce((a, b) => a + b);
  return sum / numbers.length;
};

const Average = () => {
  const [list, setList] = useState([]);
  const [number, setNumber] = useState('');

  const onChange = useCallback(e => {
    setNumber(e.target.value);
  }, []);

  const onInsert = useCallback(() => {
    const nextList = list.concat(parseInt(number));
    setList(nextList);
    setNumber('');
  }, [list, number]);

  const avg = useMemo(() => getAverage(list), [list]);

  return (
    <div>
      <input value={number} onChange={onChange} />
      <button onClick={onInsert}>Add</button>
      <ul>
        {list.map((value, index) => (
          <li key={index}>{value}</li>
        ))}
      </ul>
      <div>
        <b>Average:</b> {avg}
      </div>
    </div>
  );
};

export default Average;
```

The first parameter of useCallbak is the function you want to create, and the second parameter is an array. This array must be told when the function should be created.

If you put an empty array like onChange, the function will be created only once when the component is rendered. If you put number and list in the array like onInsert, the function will be created whenever the number or list are changed.

When you need to depend on a state value inside a function, you must include that value in the second parameter. For example, onChange doesn't care if the array is empty because it just sets the value without looking up the existing value, but since onInsert looks up the existing number and list and creates the nextList, you have to put the number and list in the array.



## useRef

useRef Hook makes ref easy to use in functional components.

```javascript
import React, { useState, useCallback, useMemo, useRef } from 'react';

const getAverage = numbers => {
  console.log('Calculating average value..');
  if (numbers.length === 0) return 0;
  const sum = numbers.reduce((a, b) => a + b);
  return sum / numbers.length;
};

const Average = () => {
  const [list, setList] = useState([]);
  const [number, setNumber] = useState('');
  const inputEl = useRef(null);

  const onChange = useCallback(e => {
    setNumber(e.target.value);
  }, []);

  const onInsert = useCallback(() => {
    const nextList = list.concat(parseInt(number));
    setList(nextList);
    setNumber('');
    inputEl.current.focus();
  }, [list, number]);

  const avg = useMemo(() => getAverage(list), [list]);

  return (
    <div>
      <input value={number} onChange={onChange} ref={inputEl} />
      <button onClick={onInsert}>Add</button>
      <ul>
        {list.map((value, index) => (
          <li key={index}>{value}</li>
        ))}
      </ul>
      <div>
        <b>Average:</b> {avg}
      </div>
    </div>
  );
};

export default Average;
```





