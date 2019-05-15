# Nested function

### Nested function

A function declared inside a function is called a nested function of external function. Nested functions can only be created at the top level of external functions. In other words, it can not be created inside a statement block such as an if statement or a while statement in a function.

```javascript
function outer() {
  let x = 1;

  function inner() {
    let y = 2;
    console.log(x + y); // 3
  }

  inner();
  console.log(x + y); // ReferenceError: y is not defined
}

outer();
```

