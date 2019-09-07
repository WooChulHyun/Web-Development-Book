# ref

## ref

Using the id to name the DOM in HTML, ref\(reference\) is the way to name the DOM in the React project.

{% hint style="info" %}
You can also use id inside react components. But not recommended. For example, suppose you use the same component multiple times. The id must be unique, but you may have multiple DOMs with the same id.

If you use ref, this problem does not occur because ref does not work globally, but only inside a component.
{% endhint %}



## ref usage

### callback function

One way to create ref is to use a callback function. Pass the callback function called ref to props on the element to be ref. This callback function receives a ref value as a parameter. Then set the ref received as a parameter inside the function as a member variable of the component.

```javascript
<input ref={(ref) => {this.input = ref}} />
```

Then, this.input points to the DOM of the input element. The name does not have to be input, but can be freely named.



### createRef

Another way to create a ref is to use a built-in function called createFef in React. This feature was introduced in React v16.3 and does not work in previous versions.

```javascript
import React, { Component } from 'react';

class RefSample extends Component {
  input = React.createRef();
  
  focus = () => {
    this.input.current.focus();
  }
  
  render() {
    return (
      <div>
        <input ref={this.input} />
      </div>
    )
  }
}

export default RefSample;
```

The difference with using the callback function is that you need to put `.current`.



## Example

ValidationSampel.css

```css
.success {
  background-color: lightgreen;
}

.failure {
  background-color: lightcoral;
}
```



ValidationSample.js

```javascript
import React, { Component } from 'react';
import './ValidationSample.css';

class ValidationSample extends Component {
  state = {
    password: '',
    clicked: false,
    validated: false
  };

  onChange = e => {
    this.setState({
      password: e.target.value
    });
  };

  onClick = () => {
    this.setState({
      clicked: true,
      validated: this.state.password === '0000'
    });
    this.input.focus();
  };

  render() {
    return (
      <div>
        <input
          ref={ref => (this.input = ref)}
          type='password'
          value={this.state.password}
          onChange={this.onChange}
          className={
            this.state.clicked
              ? this.state.validated
                ? 'success'
                : 'failure'
              : ''
          }
        />
        <button onClick={this.onClick}>Check</button>
      </div>
    );
  }
}

export default ValidationSample;
```



## Ref to component

In React, you can also use ref in a component. This method is mainly used when the DOM inside a component is used outside the component.

```javascript
<MyComponent ref={(ref) => {this.myComponent=ref}} />
```

This makes you to access methods and member variables inside MyComponent. That is, you can access to internal refs. \(E.g. myComponent.onClick, myComponent.input, etc.\)



## Example

App.js

```javascript
import React, { Component } from 'react';
import ScrollBox from './ScrollBox/ScrollBox';

class App extends Component {
  render() {
    return (
      <div>
        <ScrollBox ref={ref => (this.scrollBox = ref)} />
        <button onClick={() => this.scrollBox.scrollToBottom()}>
          Scroll to Buttom
        </button>
      </div>
    );
  }
}
export default App;
```



ScrollBox.js

```javascript
import React, { Component } from 'react';
class ScrollBox extends Component {
  scrollToBottom = () => {
    const { scrollHeight, clientHeight } = this.box;
    this.box.scrollTop = scrollHeight - clientHeight;
  };

  render() {
    const style = {
      border: '1px solid black',
      height: '300px',
      width: '300px',
      overflow: 'auto',
      position: 'relative'
    };
    const innerStyle = {
      width: '100%',
      height: '650px',
      background: 'linear-gradient(white, black)'
    };
    return (
      <div
        style={style}
        ref={ref => {
          this.box = ref;
        }}
      >
        <div style={innerStyle} />
      </div>
    );
  }
}
export default ScrollBox;
```

