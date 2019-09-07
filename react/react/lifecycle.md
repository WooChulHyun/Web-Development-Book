# Lifecycle

## Lifecycle

Every react component has a lifecycle. Lifecycle methods can only be used on class type components. In functional components, you can use Hooks to do similar thing.

The lifecycle is divided into three categories: Mount, Update, and Unmount.



### Mount

The DOM is created and what appears in the web browser is called a mount. The methods to be called are:

* constructor: Class constructor method called every time a new component is created.
* getDerivedStateFromProps: Methods used to put values in props into state.
* render: Method to render the UI we prepared.
* componentDidMount: Method called after component appears in web browser.



### Update

There are four cases that component makes to updates.

* When props change 
* When state changes 
* When the parent component is re-rendered 
* When forcing a render with this.forceUpdate

The methods to be called are:

* getDerivedStateFromProps: This method is also called during the mount process and even before the update begins. It is used when you want to change the state value as the props change.
* shouldComponentUpdate: Method that determines whether the component should re-render or not. This method should return a value of true or false, returning true continues the next lifecycle method and returns false to stop the operation. That is, the component is not re-rendered. If you call this.forceUpdate \(\) in a specific function, you can skip this step and call the render function directly.
* render: re-render the component
* getSnapshotBeforeUpdate: Called just before a component change is reflected in the DOM.
* componentDidUpdate: Called after the component update operation is complete.



### Unmount

Removing a component from the DOM is called unmount.

The method to be called is:

* componentWillUnmount: Method called before the component disappears from the web browser.



## Lifecycle Methods

### render\(\)

It is the only required method of lifecycle methods. Within this method you can access this.props and this.state and return the react element. An element can be a tag, such as a div, or it can also be a component declared separately. If you don't want to show anything, you can return null or false. Inside this method, you should not use setState outside of event settings, nor should you access the browser's DOM. It should be handled by componentDidMount to get DOM information or change state.



### constructor

```javascript
constructor(props){...}
```

It works for the first time when you create a component with the component constructor method. This method allows you to set an initial state.



### getDerivedStateFromProps

New lifecycle method created after React v16.3. It is used to synchronize the state received from props to state. It is called when the component is mounted and updated.

```javascript
static getDerivedStateFromProps(nextProps, prevState) {
  if(nextProps.value !== prevState.value) {
    return {value: nextProps.value};
  }
  return null;
}
```



### componentDidMount

```javascript
componentDidMount() {...}
```

This will create the component and run it after the first render. Within it, you can call functions from other JavaScript libraries or frameworks, or handle asynchronous tasks such as event registration, setTimeout, setInterval, and network requests.



### shouldComponentUpdate

```javascript
shouldComponentUpdate(nextProps, nextState) {...}
```

This is a method that specifies whether to start re-rendering when changing props or state. This method must return a value of true or false. If you create a component and do not create this method separately, it always returns true by default. Within this method, the current props and state are accessed by this.props and this.state, and the new props or state to be set can be accessed by nextProps and nextState.



### getSanpshotBeforeUpdate

This method was created after React v16.3. This method is called just before the output from render is actually reflected in the browser. The value returned by this method can be passed as the third parameter, snapshot, in componentDidUpdate. It is mainly used when there is a need to refer to the value immediately before the update. \(E.g. maintain scrollbar position\)

```javascript
getSnapshotBeforeUpdate(prevProps, prevState) {
  if(prevState.array !== this.state.array) {
    const {scrollTop, scrollHeight} = this.list
    return {scrollTop, scrollHeight}
  }
}
```



### componentDidUpdate

```javascript
componentDidUpdate(prevProps, prevState, snapshot) {...}
```

This works after the re-render is completed. It works just after the update, you can do DOM-related processing. Here you can use prevProps or prevState to access the data which component previously had. Also, if there is a value returned by getSanpshotBeforeUpdate, the snapshot value can be passed here.



### componentWillUnmount

```javascript
componentWillUnmount() {...}
```

This works when the component is removed from the DOM. If you have events, timers, and custom DOM registered in componentDidMount, you will need to remove them here.



### componentDidCatch

The componentDidCatch method is new method in React v16 and allows an application to show an error UI when an error occurs during component rendering.

```javascript
componentDidCatch(error, info) {
  this.setState({
    error: true
  });
  console.log({error, info})
}
```

Here, error tells you which error occurred in the parameter, and the info parameter gives information about where the error occurred in the code. However, when you use this method, you can't catch errors that occur on the component itself, only catch errors that occur in the component passed via this.props.children.

