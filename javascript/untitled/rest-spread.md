# Rest / Spread

## Rest parameter

The Rest parameter means that the parameter is defined using the Spread operator \(...\). The Rest parameter allows to pass a list of arguments to inside a function as an array.

```javascript
function foo(...rest) {
  console.log(Array.isArray(rest)); // true
  console.log(rest); // [ 1, 2, 3, 4, 5 ]
}

foo(1, 2, 3, 4, 5);
```

```javascript
function foo(a, b, ...rest) {
  console.log(Array.isArray(rest)); // true
  console.log(a, b, rest); // [ 1, 2, 3, 4, 5 ]
}

foo(1, 2, 3, 4, 5); // 1 2 [3, 4, 5]
```

Because the 'arguments' are not arrays,  is array-like object, therefore they need to be converted to arrays to be controlled by array methods such as forEach.

You are not able to use 'arguments' in an arrow function, but you can use variable arguments in an arrow function by using the rest parameter.

```javascript
const foo = (...args) => {
  let s = 0;
  for (let i = 0; i < args.length; i++) s += args[i];
  return s;
};

foo(1, 2, 3, 4, 5);
// 15
```

The Rest parameter must be the last parameter.

```javascript
function foo(...rest, a, b) {
  console.log(Array.isArray(rest)); // true
  console.log(a, b, rest); // [ 1, 2, 3, 4, 5 ]
}

foo(1, 2, 3, 4, 5); 
// SyntaxError: Rest parameter must be last formal parameter
```



## Spread operator

The Spread Operator \(...\) separates the operands into individual elements. The operand of the Spread operator must be iterable.

```javascript
console.log(...[1, 2, 3]) // 1, 2, 3

// The string is iterable.
console.log(...'Hello');  // H e l l o

// Map and Set are iterable.
console.log(...new Map([['a', '1'], ['b', '2']]));  // [ 'a', '1' ] [ 'b', '2' ]
console.log(...new Set([1, 2, 3]));  // 1 2 3

// A non-iterable general object cannot be an operand of the Spread operator.
console.log(...{ a: 1, b: 2 });
// TypeError: Found non-callable @@iterator
```



### When used as an argument to a function

```javascript
// ES5
function foo(x, y, z) {
  console.log(x); // 1
  console.log(y); // 2
  console.log(z); // 3
}

const arr = [1, 2, 3];

foo.apply(null, arr);
// foo.call(null, 1, 2, 3);
```

```javascript
// ES6
function foo(x, y, z) {
  console.log(x); // 1
  console.log(y); // 2
  console.log(z); // 3
}

const arr = [1, 2, 3];

// ...[1, 2, 3] = [1, 2, 3] → 1, 2, 3
foo(...arr);
```

```javascript
function foo(v, w, x, y, z) {
  console.log(v); // 1
  console.log(w); // 2
  console.log(x); // 3
  console.log(y); // 4
  console.log(z); // 5
}

foo(1, ...[2, 3], 4, ...[5]);
```



### When used in arrays

#### concat

```javascript
// ES5
var arr = [1, 2, 3];
console.log(arr.concat([4, 5, 6])); // [ 1, 2, 3, 4, 5, 6 ]
```

```javascript
// ES6
const arr = [1, 2, 3];
console.log([...arr, 4, 5, 6]); // [ 1, 2, 3, 4, 5, 6 ]
```



#### push

```javascript
// ES5
var arr1 = [1, 2, 3];
var arr2 = [4, 5, 6];

Array.prototype.push.apply(arr1, arr2);

console.log(arr1); // [ 1, 2, 3, 4, 5, 6 ]
```

```javascript
// ES6
const arr1 = [1, 2, 3];
const arr2 = [4, 5, 6];

arr1.push(...arr2); // == arr1.push(4, 5, 6);

console.log(arr1); // [ 1, 2, 3, 4, 5, 6 ]
```



#### splice

```javascript
// ES5
var arr1 = [1, 2, 3, 6];
var arr2 = [4, 5];

Array.prototype.splice.apply(arr1, [3, 0].concat(arr2));

console.log(arr1); // [ 1, 2, 3, 4, 5, 6 ]
```

```javascript
// ES6
const arr1 = [1, 2, 3, 6];
const arr2 = [4, 5];

arr1.splice(3, 0, ...arr2); // == arr1.splice(3, 0, 4, 5);

console.log(arr1); // [ 1, 2, 3, 4, 5, 6 ]
```



#### copy <a id="324-copy"></a>

```text
// ES5
var arr  = [1, 2, 3];
var copy = arr.slice();

console.log(copy); // [ 1, 2, 3 ]

copy.push(4);

console.log(copy); // [ 1, 2, 3, 4 ]
console.log(arr);  // [ 1, 2, 3 ]
```

```text
// ES6
const arr = [1, 2, 3];
const copy = [...arr];

console.log(copy); // [ 1, 2, 3 ]

copy.push(4);

console.log(copy); // [ 1, 2, 3, 4 ]
console.log(arr);  // [ 1, 2, 3 ]
```



