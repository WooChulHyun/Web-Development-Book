# Promise

### **Promise**

JavaScript uses a callback function as a pattern for asynchronous processing. However, the traditional callback pattern has poor readability and it is difficult to handle exceptions that occurred error during asynchronous processing, and it is also difficult to handle multiple asynchronous processing logic at once. ES6 introduced Promise as another pattern for asynchronous processing. Promise complements the disadvantages of traditional callback patterns and clearly expresses the timing of asynchronous processing.



### Callback Hell

Asynchronous processing model performs tasks in parallel. That is, even if the task has not been terminated, the next task is immediately executed without waiting. For example, when performing a task that fetches data from the server and displays it on the screen, it performs the following tasks immediately after requesting data from the server, without waiting until data is returned from the server \(Non-Blocking\). Then, when data is returned from the server, an event occurs and the event handler continues perform task with the data. Most of the JavaScript DOM events and Timer functions \(setTimeout, setInterval\) and Ajax requests work with the asynchronous processing model.

However, using a callback pattern for asynchronous processing has a disadvantage in that a callback hell \(nesting\) occurs due to nesting of multiple callback functions in order to guarantee a processing order. Callbacks cause low readability and cause errors.

```javascript
function ABC(callback) {
  setTimeout(() => {
    callback();
  }, 1000);
}

ABC(() => {
  console.log('A');
  ABC(() => {
    console.log('B');
    ABC(() => {
      console.log('C');
    });
  });
});
```



