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



## Use dynamic context

You can also pass a function as a value of the Context.

App.js

```javascript
import React from 'react';
import './App.css';
import ColorBox from './components/colorBox/ColorBox';
import { ColorProvider } from './contexts/color';
import SelectColors from './components/selectColor/SelectColor';

function App() {
  return (
    <ColorProvider>
      <div>
        <SelectColors />
        <ColorBox />
      </div>
    </ColorProvider>
  );
}

export default App;
```



Color.js

```javascript
import React, { createContext, useState } from 'react';

const ColorContext = createContext({
  state: { color: 'black', subcolor: 'red' },
  actions: {
    setColor: () => {},
    setSubcolor: () => {}
  }
});

const ColorProvider = ({ children }) => {
  const [color, setColor] = useState('black');
  const [subcolor, setSubcolor] = useState('red');

  const value = {
    state: { color, subcolor },
    actions: { setColor, setSubcolor }
  };

  return (
    <ColorContext.Provider value={value}>{children}</ColorContext.Provider>
  );
};

const ColorConsumer = ColorContext.Consumer;

export { ColorProvider, ColorConsumer };

export default ColorContext;
```



ColorBox.js

```javascript
import React from 'react';
import ColorContext from '../../contexts/color';

const ColorBox = () => {
  return (
    <ColorContext.Consumer>
      {value => (
        <>
          <div
            style={{
              width: '64px',
              height: '64px',
              background: value.state.color
            }}
          ></div>
          <div
            style={{
              width: '32px',
              height: '32px',
              background: value.state.subcolor
            }}
          ></div>
        </>
      )}
    </ColorContext.Consumer>
  );
};

export default ColorBox;
```



SelectColor.js

```javascript
import React from 'react';
import { ColorConsumer } from '../../contexts/color';

const colors = ['red', 'orange', 'yellow', 'green', 'blue', 'indigo', 'violet'];

const SelectColor = () => {
  return (
    <div>
      <h2>Choose Color</h2>
      <ColorConsumer>
        {({ actions }) => (
          <div style={{ display: 'flex' }}>
            {colors.map(color => (
              <div
                key={color}
                style={{
                  background: color,
                  width: '24px',
                  height: '24px',
                  cursor: 'pointer'
                }}
                onClick={() => actions.setColor(color)}
                onContextMenu={e => {
                  e.preventDefault();
                  actions.setSubcolor(color);
                }}
              />
            ))}
          </div>
        )}
      </ColorConsumer>
    </div>
  );
};

export default SelectColor;
```

![](https://i.postimg.cc/rsvgLRH2/Context-API3.png)



## useContext

Among the hooks built into React, the hook called useContext makes it easy to use Context in functional components.

ColorBox.js

```javascript
import React, { useContext } from 'react';
import ColorContext from '../../contexts/color';

const ColorBox = () => {
  const { state } = useContext(ColorContext);
  return (
    <>
      <div
        style={{
          width: '64px',
          height: '64px',
          background: state.color
        }}
      ></div>
      <div
        style={{
          width: '32px',
          height: '32px',
          background: state.subcolor
        }}
      ></div>
    </>
  );
};

export default ColorBox;
```

