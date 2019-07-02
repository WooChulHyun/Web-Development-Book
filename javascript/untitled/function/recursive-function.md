# Recursive function

## Recursive function

Calling a function itself is called a recursive call. A recursive function is a function that calls itself, that is, a function that performs a recursive call.

```javascript
function fact(n) {
  if (n <= 1) return 1;
  return fact(n - 1) * n;
}

console.log(fact(0)); // 0! = 1
console.log(fact(1)); // 1! = 1
console.log(fact(2)); // 2! = 1 * 2 = 2
console.log(fact(3)); // 3! = 1 * 2 * 3 = 6
console.log(fact(4)); // 4! = 1 * 2 * 3 * 4 = 24
console.log(fact(5)); // 5! = 1 * 2 * 3 * 4 * 5 = 120
```

Because a recursive function calls itself endlessly, it must create an escape condition that can stop the call. In the above example, the recursive call stops when the argument is less than or equal 1. If there is no escape condition, the function is called infinitely and a stack overflow error occurs.

Most recursive functions can be substituted by for or while statements.

```javascript
function fact(n) {
  if (n <= 1) return 1;

  let res = n;
  while (--n) res *= n;
  return res;
}

console.log(fact(0)); // 0! = 1
console.log(fact(1)); // 1! = 1
console.log(fact(2)); // 2! = 1 * 2 = 2
console.log(fact(3)); // 3! = 1 * 2 * 3 = 6
console.log(fact(4)); // 4! = 1 * 2 * 3 * 4 = 24
console.log(fact(5)); // 5! = 1 * 2 * 3 * 4 * 5 = 120
```

