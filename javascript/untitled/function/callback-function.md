# Callback function

## Callback function

Because JavaScript functions are first-class objects, you can pass functions as arguments to functions. A function that is passed as an argument to another function is called a callback function.

```javascript
function print(f) {
  let string = 'Hello';
  return f(string);
}

let res1 = print((str) => {
    return str.toUpperCase();
});

let res2 = print((str) => {
    return str.toLowerCase();
});

console.log(res1, res2); // HELLO hello
```

The print function receives a function as an argument. The function passed as an argument to the print function is called when the print function calls. The function passed to the print function as an argument is called a callback function.

If you need to call the callback function elsewhere, or if the function that receives the callback function is called frequently, it is more efficient to define the callback function outside the function and then pass the variable pointing to the callback function.

```javascript
function print(f) {
  const string = 'Hello';
  return f(string);
}

let toUpperCase = function (str) {
  return str.toUpperCase();
};

let res = print(toUpperCase);
console.log(res); // HELLO

```

A callback function is a common pattern used for asynchronous processing, mainly used for event handling and Ajax communication.

```javascript
document.getElementById('myButton').addEventListener('click', () => {
  console.log('button clicked!');
});

setTimeout(() => {
  console.log('1 second');
}, 1000);
```

```javascript
button.onclick = function () {...};

button.addEventListener("click), function() {...}, false);
```

Callback functions are also used in higher-order functions.

```javascript
let res = [1, 2, 3].map((item) => {
    return item * 2;
});

console.log(res); // [ 2, 4, 6 ]

res = [1, 2, 3].filter((item) => {
    return item % 2;
});

console.log(res); // [ 1, 3 ]
```

