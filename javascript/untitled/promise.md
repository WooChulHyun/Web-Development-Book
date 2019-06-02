# Promise

### **Promise**

JavaScript uses a callback function as a pattern for asynchronous processing. However, the traditional callback pattern has poor readability and it is difficult to handle exceptions that occurred error during asynchronous processing, and it is also difficult to handle multiple asynchronous processing logic at once. ES6 introduced Promise as another pattern for asynchronous processing. Promise complements the disadvantages of traditional callback patterns and clearly expresses the timing of asynchronous processing.



### Callback

#### Callback Hell

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



#### Limitations of error handling

The most serious problem with callback type asynchronous processing is that it is difficult to handle errors.

```javascript
try {
  setTimeout(() => { throw new Error('Error!'); }, 1000);
} catch (e) {
  console.log('Cannot catch error');
  console.log(e);
}
```

When the setTimeout function is executed within a try block, the callback function is executed after 1 second and this callback function throws an error. However, this error is not caught in the catch block.

The callback function of the asynchronous processing function is moved to the event queue when the corresponding event \(tick event of timer function, readystatechange event of XMLHttpRequest, etc.\) occurs, and then moved to the call stack when the call stack is empty. Because the setTimeout function is an asynchronous function, it does not wait for the callback function to be executed and to be immediately terminated and removed from the call stack. When the tick event occurs, the callback function of the setTimeout function is moved to the event queue and then moved to the call stack when the call stack is empty and executed. At this point, the setTimeout function has already been removed from the call stack. This means that calling the callback function of the setTimeout function is not a setTimeout function. This is because the setTimeout function must exist in the call stack if the caller of the setTimeout function's callback function is a setTimeout function.

Exceptions are propagated towards the caller. However, as mentioned above, calling the callback function of the setTimeout function is not a setTimeout function. Therefore, any errors that occur within the callback function of the setTimeout function are not caught in the catch block, and the process is terminated.



### Promise Basic

Promises are instantiated through the Promise constructor function. The Promise constructor function takes a callback function to perform the asynchronous processing. The callback function receives the resolve and reject functions as arguments.

**resolve:** A callback function that should be called when processing in a function is complete. You can pass any value to the resolve function as an argument. This value is passed to a function that performs the following processing.

**reject:** A callback function that should be called when processing in a function fails. You can pass any value to the reject function as an argument. In most cases, you use the error message string as an argument.

```javascript
const promise = new Promise((resolve, reject) => {

  if (/* Asynchronous processing succeeded */) {
    resolve('result');
  }
  else { /* Asynchronous processing Failed */
    reject('failure reason');
  }
});
```

Promise has state information such as whether the asynchronous processing has been fulfilled or rejected.

| State | Meaning |  |
| :--- | :--- | :--- |
| pending | Asynchronous processing has not been yet performed | The resolve or reject function has not been yet called |
|  fulfilled | Asynchronous processing is performed \(success\) | When the resolve function is called |
|  rejected | Asynchronous processing is performed \(failed\) | When the reject function is called |
| settled | Asynchronous processing is performed \(success or failed\) | When the resolve or reject function is called |

```javascript
const promise = new Promise((resolve, reject) => {
  setTimeout(() => {
    console.log('A');
    resolve();
  }, 1000);
});

promise.then(() => {
  console.log('B');
});

console.log(promise);

setTimeout(() => {
    console.log(promise);
}, 2000);

// Promise { pending }
// A
// B
// Promise { resolved }
```



### The resolve function and the then method which terminate Promise

The resolve function turns Promise off. The value passed to the resolve function is passed to the function passed as an argument to the then method, which is then used for further processing.

```javascript
promise.then(onFullfilled)
```

The onFullfilled function is a 'success callback function' and is called when the processing in promise is finished successfully. The onFullfilled function takes a response as an argument. This is the argument passed when executing the resolve function in promise.

```javascript
const promise = new Promise((resolve, reject) => {
  setTimeout(() => {
    const name = prompt('Your name');
    resolve(name);
  }, 1000);
});

promise.then((name) => {
  console.log(`Hello ${name}`);
});
```



### Reject function and catch method to treat Promise as failure

The reject function turns Promise off. Like the resolve function, you can also pass a value to the reject function. When the reject function is executed, the function passed to the then method is not executed. Instead, the function passed to the catch method is executed.

```javascript
promise.catch(onRejected)
```

The onRejected function is called a 'failed callback function' and is called when processing in promise has failed. The onRejected function takes an error as an argument, which is the argument passed when the reject function is executed in promise.

```javascript
const promise = new Promise((resolve, reject) => {
  setTimeout(() => {
    const n = parseInt(prompt('enter a number less than 10'));
    if (n < 10) {
      resolve(n);
    } else {
      reject(`error: ${n} is a number greater than or equal to 10.`);
    }
  }, 1000);
});

promise
  .then((num) => {
    console.log(`Your number is ${num}`);
  })
  .catch((error) => {
    console.log(error);
  });
```



###  then's second argument

You can specify a 'failed callback function' as the second argument to the then method. Then you can write what you want to handle in the then method and what you want to handle in the catch method in the one then method.

```javascript
promise.then(onFullfilled, onRejected)
```

```javascript
const promise = new Promise((resolve, reject) => {
  setTimeout(() => {
    const n = parseInt(prompt('enter a number less than 10'));
    if (n < 10) {
      resolve(n);
    } else {
      reject(`error: ${n} is a number greater than or equal to 10.`);
    }
  }, 1000);
});

promise.then((num) => {
  console.log(`Your number is ${num}`);
}),
(error) => {
  console.log(error);
};
```



### Error handling for Promise

The catch method is similar to the second callback function in the then method in that it handles errors, but there are subtle differences. The second callback function of the then method catches only the error that occurred in asynchronous processing \(the state in which the reject function was called\). However, the catch method catches not only errors that occur in asynchronous processing \(the state in which the reject function was called\) but also errors that occur inside the then method. Therefore, using the catch method for error handling is more efficient.



### Promise Chaining

If another asynchronous function needs to be called with the result of the processing of the asynchronous function, the function call is nested and the callback hell occurs which increases the complexity. Promises can chaining subsequent processing methods to connect multiple promises. This solves the callback hell.

```javascript
function power() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      const n = parseInt(prompt('enter a number less than 10'));
      if (n < 10) {
        resolve(n);
      } else {
        reject(`error: ${n} is a number greater than or equal to 10.`);
      }
    }, 1000);
  });
}
power()
  .then((num) => {
    console.log(`Your number is ${num}`);
  })
  .then(() => {
    console.log(' is a number less than or equal to 10.');
  })
  .catch((error) => {
    console.log(error);
  });
```

See the difference

```javascript
function power() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      const n = parseInt(prompt('enter a number less than 10'));
      if (n < 10) {
        resolve(n);
      } else {
        reject(`error: ${n} is a number greater than or equal to 10.`);
      }
    }, 1000);
  });
}
power()
  .then((num) => {
    console.log(`Your number is ${num}`);
    return power();
  })
  .then((num) => {
    console.log(`Your number to the power of 2 is ${num ** 2}`);
  })
  .catch((error) => {
    console.log(error);
  });
```

