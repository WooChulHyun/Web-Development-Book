# Component iteration

## map

```javascript
import React from 'react';

const IterationSample = () => {
  const sample = ['Sample1', 'Sample2', 'Sample3', 'Sample4'];
  const sampleList = sample.map(sample => <li>{sample}</li>);
  return (
    <>
      <ul>{sampleList}</ul>
    </>
  );
};

export default IterationSample;
```

![](https://i.postimg.cc/JnrRxtkh/Iteration1.png)

It rendered as we want but warns that there is no key.



## Key

In React, key is used to find out which element changed when the component array was rendered. If there is no key, the list is compared sequentially to detect changes in the virtual DOM. But if you have a key, you can use this value to find out more quickly what happened.



### Key setting

The key value must always be unique. Therefore, high value of data should be set as key value.

```javascript
const sampleList = sample.map(sample => <li key={sample.id}>{sample.contents}</li>)
```

However, the example component created earlier does not have a unique number. In this case, you can use the index value which is an argument of the callback function passed to the map.

```javascript
import React from 'react';

const IterationSample = () => {
  const sample = ['Sample1', 'Sample2', 'Sample3', 'Sample4'];
  const sampleList = sample.map((sample, index) => (
    <li key={index}>{sample}</li>
  ));
  return (
    <>
      <ul>{sampleList}</ul>
    </>
  );
};

export default IterationSample;
```

However, using index as a key does not effectively re-render when the array changes. Therefore, it is best to refrain from using indexes as much as possible.



## Example

### Initial setting

```javascript
import React, { useState } from 'react';

const IterationSample = () => {
  const [sample, setSample] = useState([
    { id: 1, text: 'sample1' },
    { id: 2, text: 'sample2' },
    { id: 3, text: 'sample3' },
    { id: 4, text: 'sample4' }
  ]);

  const sampleList = sample.map(sample => (
    <li key={sample.id}>{sample.text}</li>
  ));
  return (
    <>
      <ul>{sampleList}</ul>
    </>
  );
};

export default IterationSample;
```



### Add date

```javascript
import React, { useState } from 'react';

const IterationSample = () => {
  const [sample, setSample] = useState([
    { id: 1, text: 'sample1' },
    { id: 2, text: 'sample2' },
    { id: 3, text: 'sample3' },
    { id: 4, text: 'sample4' }
  ]);
  const [inputText, setInputText] = useState('');

  const sampleList = sample.map(sample => (
    <li key={sample.id}>{sample.text}</li>
  ));

  const onChange = e => {
    setInputText(e.target.value);
  };

  const onClick = () => {
    const newContent = { id: generateID(), text: inputText };
    setSample([...sample, newContent]);
    console.log(sample);
  };

  const generateID = () => {
    return sample.length ? Math.max(...sample.map(item => item.id)) + 1 : 1;
  };

  return (
    <>
      <input value={inputText} onChange={onChange} />
      <button onClick={onClick}>Add</button>
      <ul>{sampleList}</ul>
    </>
  );
};

export default IterationSample;
```



## Delete data

```javascript
import React, { useState } from 'react';

const IterationSample = () => {
  const [sample, setSample] = useState([
    { id: 1, text: 'sample1' },
    { id: 2, text: 'sample2' },
    { id: 3, text: 'sample3' },
    { id: 4, text: 'sample4' }
  ]);
  const [inputText, setInputText] = useState('');

  const sampleList = sample.map(sample => (
    <li key={sample.id}>
      {sample.text}{' '}
      <button
        onClick={() => {
          deleteBtn(sample.id);
        }}
      >
        X
      </button>
    </li>
  ));

  const onChange = e => {
    setInputText(e.target.value);
  };

  const onClick = () => {
    const newContent = { id: generateID(), text: inputText };
    setSample([...sample, newContent]);
    console.log(sample);
  };

  const generateID = () => {
    return sample.length ? Math.max(...sample.map(item => item.id)) + 1 : 1;
  };

  const deleteBtn = id => {
    setSample(sample.filter(item => item.id !== id));
  };

  return (
    <>
      <input value={inputText} onChange={onChange} />
      <button onClick={onClick}>Add</button>
      <ul>{sampleList}</ul>
    </>
  );
};

export default IterationSample;
```

