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





