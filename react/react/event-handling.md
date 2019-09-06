# Event Handling

## Notes on Using Events

* Event names must be written in camel case.

For example, onclick in HTML must be written onClick, and onkeyup also must be written onKeyUp in React.

* Rather than passing JavaScript code to execute on an event, pass a value in the form of a function.



* You can only set events on DOM elements.

We can set events on DOM elements such as divs, buttons, inputs, forms, and spans, but we can't set events on our own components. For example, `<MyComponent onClick={doSomething} />`

This code does not execute the doSomething function, but passes props named onClick to MyComponent.

Therefore, you cannot set the event on the component itself. But you can set as DOM event inside component using props passed to.

```javascript
<div onClick ={this.props.onClick}>
  {/* (...) */}
</div>
```



## Event type

React supports the following event types:

* Clipboard
* Composition
* Keyboard
* Focus
* Mouse
* Selection
* Touch
* UI
* Wheel
* Media
* Image
* Animation
* Transition



## onChange event

```javascript
import React, { Component } from 'react';

class Event extends Component {
  render() {
    return (
      <div>
        <h1>Event</h1>
        <input
          type='text'
          name='message'
          placeholder='Enter any value'
          onChange={e => console.log(e.target.value)}
        />
      </div>
    );
  }
}

export default Event;
```

![](https://i.postimg.cc/MGbfytjN/Event-Handling1.png)



## Put the input value in state

```javascript
import React, { Component } from 'react';

class Event extends Component {
  state = {
    message: ''
  };

  render() {
    const { message } = this.state;
    return (
      <div>
        <h1>Event</h1>
        <input
          type='text'
          name='message'
          placeholder='Enter any value'
          value={message}
          onChange={e => {
            this.setState({
              message: e.target.value
            });
          }}
        />
        <button
          onClick={() => {
            alert(this.state.message);
          }}
        >
          Check
        </button>
      </div>
    );
  }
}

export default Event;
```

![](https://i.postimg.cc/PqggWz1G/Event-Handling2.png)



## Control multiple inputs

```javascript
import React, { Component } from 'react';

class Event extends Component {
  state = {
    username: '',
    message: ''
  };

  onChange = e => {
    this.setState({
      [e.target.name]: e.target.value
    });
  };

  onClick = () => {
    alert(this.state.username + ': ' + this.state.message);
    this.setState({
      username: '',
      message: ''
    });
  };

  render() {
    const { username, message } = this.state;
    return (
      <div>
        <h1>Event</h1>
        <input
          type='text'
          name='username'
          placeholder='username'
          value={username}
          onChange={this.onChange}
        />
        <input
          type='text'
          name='message'
          placeholder='Enter any value'
          value={message}
          onChange={this.onChange}
        />
        <button onClick={this.onClick}>Check</button>
      </div>
    );
  }
}

export default Event;
```



## onKeyUp event

```javascript
import React, { Component } from 'react';

class Event extends Component {
  state = {
    username: '',
    message: ''
  };

  onChange = e => {
    this.setState({
      [e.target.name]: e.target.value
    });
  };

  onClick = () => {
    alert(this.state.username + ': ' + this.state.message);
    this.setState({
      username: '',
      message: ''
    });
  };

  onKeyUp = e => {
    if (e.key === 'Enter') {
      this.onClick();
    }
  };

  render() {
    const { username, message } = this.state;
    return (
      <div>
        <h1>Event</h1>
        <input
          type='text'
          name='username'
          placeholder='username'
          value={username}
          onChange={this.onChange}
        />
        <input
          type='text'
          name='message'
          placeholder='Enter any value'
          value={message}
          onChange={this.onChange}
          onKeyUp={this.onKeyUp}
        />
        <button onClick={this.onClick}>Check</button>
      </div>
    );
  }
}

export default Event;
```



## Implement as a functional component

```javascript
import React, { useState } from 'react';

const Event = () => {
  const [form, setForm] = useState({
    username: '',
    message: ''
  });

  const { username, message } = form;

  const onChange = e => {
    const newForm = { ...form, [e.target.name]: e.target.value };
    setForm(newForm);
  };

  const onClick = () => {
    alert(username + ': ' + message);
    setForm({
      username: '',
      message: ''
    });
  };

  const onKeyUp = e => {
    if (e.key === 'Enter') {
      onClick();
    }
  };

  return (
    <div>
      <h1>Event</h1>
      <input
        type='text'
        name='username'
        placeholder='username'
        value={username}
        onChange={onChange}
      />
      <input
        type='text'
        name='message'
        placeholder='Enter any value'
        value={message}
        onChange={onChange}
        onKeyUp={onKeyUp}
      />
      <button onClick={onClick}>Check</button>
    </div>
  );
};

export default Event;
```

