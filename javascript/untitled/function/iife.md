# IIFE

## Immediately Invoke Function Expression \(IIFE\)

A function that is immediately called at the same time as the definition of the function is called an Immediately Invoke Function Expression \(IIFE\). It is called only once and can not be called again. Immediately Invoke Function Expression generally use anonymous immediate functions that do not have function names.

```javascript
(function () {
  const a = 1;
  const b = 2;
  return a + b;
}());
```

You can also use an immediate invoke function expression with a function name. However, since the function name is an identifier that can be referenced only by the function body, it can not call the immediate invoke function expression again.

```javascript
(function add() {
  const a = 1;
  const b = 2;
  return a + b;
}());

add(); // ReferenceError: foo is not defined
```

### Way to use the Immediate Execution Function

```javascript
(function () {
  // ...
}());

(function () {
  // ...
})();

!function () {
  // ...
}();

+function () {
  // ...
}();
```

First and second way are used the most.

```javascript
let add = (function () {
  let a = 1;
  let b = 2;
  return a + b;
}());

console.log(add); // 3

add = (function (a, b) {
  return a + b;
}(1, 2));

console.log(add); // 3
```

