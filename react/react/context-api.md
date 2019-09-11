# Context API

## Consumer

color.js

```javascript
import { createContext } from 'react';

const ColorContext = createContext({ color: 'black' });

export default ColorContext;
```

After creating a new context via createContext, to display the color contained within the ColorContext in the ColorBox component, we have to receive colors through the Consumer component inside the ColorContext, not getting the colors as props.



```javascript
import React from 'react';
import ColorContext from '../../contexts/color';

const ColorBox = () => {
  return (
    <ColorContext.Consumer>
      {value => (
        <div
          style={{
            width: '64px',
            height: '64px',
            background: value.color
          }}
        ></div>
      )}
    </ColorContext.Consumer>
  );
};

export default ColorBox;
```

You need to open the curly braces between the Consumers and put the function in them. This pattern is called Function as a child, or Render Props. In place of the children of the component, you must pass a function that is not a regular JSX or string.

![](https://i.postimg.cc/13fMG2BY/Context-API1.png)



## Provider

Provider allows you to change the value of a Context.

```javascript
import React from 'react';
import ColorContext from '../../contexts/color';

const ColorBox = () => {
  return (
    <ColorContext.Provider value={{ color: 'red' }}>
      <ColorContext.Consumer>
        {value => (
          <div
            style={{
              width: '64px',
              height: '64px',
              background: value.color
            }}
          ></div>
        )}
      </ColorContext.Consumer>
    </ColorContext.Provider>
  );
};

export default ColorBox;
```

![](https://i.postimg.cc/WzdBtvSm/Context-API2.png)



