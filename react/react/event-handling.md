# Event Handling

## Notes on Using Events

* Event names must be written in camel case.

For example, onclick in HTML must be written onClick, and onkeyup also must be written onKeyUp in React.

* Rather than passing JavaScript code to execute on an event, pass a value in the form of a function.



* DOMyoso-eman ibenteuleul seoljeonghal su issseubnida. 25/5000 You can only set events on DOM elements.

We can set events on DOM elements such as divs, buttons, inputs, forms, and spans, but we can't set events on our own components. For example, &lt;MyComponent onClick={doSomething} /&gt;

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

