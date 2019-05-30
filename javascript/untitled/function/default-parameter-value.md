# Default Parameter value

### Default Parameter value

In ES5, default values cannot be set for parameters. Therefore, you need to check inside the function to see if the appropriate arguments have been passed.

```javascript
// ES5
function plus(x, y) {
  x = x || 0; // If you do not assign an argument to parameter x, 
              // assign a default value of 0.
  y = y || 0; // If you do not assign an argument to parameter y, 
              // assign a default value of 0.

  return x + y;
}

console.log(plus());      // 0
console.log(plus(1, 2));  // 3
console.log(plus(1));     // 1
console.log(plus('', 2)); // 2
```

In ES6, parameter defaults can be set to simplify parameter checking and initialization in the function.

```javascript
// ES6
function plus(x = 0, y = 0) {
  return x + y;
}

console.log(plus());      // 0
console.log(plus(1, 2));  // 3
console.log(plus(1));     // 1
console.log(plus('', 2)); // 2
```

