# Function Basic

## Function

A function in a programming language is defined as a unit of execution by implementing a series of processes as statements and wrapping them in code blocks. Functions in the programming language also take input as functions of mathematics and make output. In this case, a variable receiving the input is called a parameter, an input is an argument, and an output is a return value. Also, since there may be several functions, you can use function names that are identifiers to distinguish specific functions.

```javascript
// add is function name
// x and y are parameters
function add(x, y) {
  // x + y is return value
  return x + y;
}

// 1 and 2 are arguments
add(1, 2);
```

Functions are created through Function Definition. Functions in JavaScript can be defined in a variety of ways.

A function definition does not execute the function. To execute the function, you needed to pass an argument to the function through a parameter to instruct the execution of the function. This is called function call / invoke. When a function is called, the statements in the code block are executed in a lump and the result is returned.

```javascript
function add(x, y) {
  return x + y;
}

// function call / invoke with arguments
add(1, 2);
```

#### 

## Function literal

Functions can be created as function literals. A function literal consists of a function keyword, a function name, a parameter list, and a function body.

```javascript
// ADD is variable name
// add is function name
const ADD = function add(x, y) {
  return x + y;
};

// function add(x, y) {return x + y} is Function literal
```

* Function name

The function name is an identifier. Therefore, identifier naming convention must follow.

A function name is an identifier that can be referenced only within a function body.

The function name can be omitted. A function with a function name is called a named function, and a function without a function name is called an anonymous function.

* Parameter list

Wrap 0 or more parameters in parentheses and separate them with commas.

Parameters are assigned arguments.

Parameters are treated the same as variables in the function body.

#### 

## Four ways to define function

* Function Declaration/Function Statement

```javascript
function add(x, y) {
  return x + y;
}
```

* Function Expression

```javascript
const ADD = function(x, y) {
  return x + y;
};
```

* Function Constructor \(do not use\)

```javascript
const ADD = new Function('x', 'y', 'return x + y');
```

* Arrow Function

```javascript
const ADD = (x, y) => x + y;
```

#### 

## Function Declaration/Function Statement

Function Declaration is the same as function literal notation. However, function declarations can not omit function names.

```javascript
function add(x, y) {
  return x + y;
}

console.log(add(2, 3)); // 5
```

Above, I wrote "A function name is an identifier that can be referenced only within a function body."

This means that the function name, add, can not be referenced outside the function body. In the above code, however, the function name is referenced outside the function body, even though it is an identifier that can not be referenced outside the function body.

The JavaScript engine implicitly declares an identifier with the same name as the function name and assign the generated function object.

```javascript
var add = function add(x, y) {
  return x + y;
};

console.log(add(2, 3)); // 5
```

The function is called with the variable pointing to the function object, not the function name. In other words, "add" that called the function is not a function name, but the variable "add" that JavaScript engine creates implicitly. Since the function name matches the variable name, it seems to be called by the function name, but it is actually called with the variable name.

#### 

## Function Expression

JavaScript functions are objects. An object in JavaScript can be assigned to a variable as like a value, the value of a property, or an element of an array. These objects are called first-class objects. Functions in JavaScript are first-class objects. When a function is a first-class object, it means that a function can be freely used as a value.

Since functions are first-class objects, you can assign a function object created by a function literal to a variable. These function definition methods are called function expressions.

```javascript
const ADD = function(x, y) {
  return x + y;
};

console.log(ADD(2, 3)); // 5
```

Function names of function literals can be omitted. These functions are called anonymous functions. Function literals in function expressions generally omit function names.

As we have seen in the function declaration, when calling a function, you should use a variable that points to the function object, not the function name. A function can not be called by a function name because it is a valid identifier only within the function body.

```javascript
const ADD = function a(x, y) {
  return x + y;
};

console.log(ADD(2, 3)); // 5

console.log(a(2, 3)); // ReferenceError: foo is not defined
```

#### 

## Arrow function

Newly introduced in the ES6, the Arrow function can be declared in a simpler way using the arrow \(=&gt;, Fat arrow\) instead of the function keyword. An arrow function is always defined as an anonymous function.

```javascript
const ADD = (x, y) => x + y;

console.log(ADD(2, 3)); // 5
```

However, it is not designed to completely replace existing function declarations or function expressions. Therefore, you can not use the arrow function in all situations. Arrow function has different this binding method way, there is no prototype property, and no arguments object is created.



## Hoisting \(Function Declaration / Function Expression\)

```javascript
console.dir(add); // ƒ add(x, y)
console.dir(pow); // undefined

console.log(add(2, 3)); // 5
console.log(pow(5)); // TypeError: sub is not a function

function add(x, y) {
  return x + y;
}

let pow = function(x) {
  return x * x;
};
```

A function defined by a function declaration statement can be called before the function declaration statement. However, functions defined by function expressions can not be called before function expressions. This is because the function defined by the function declaration and the function defined by the function expression are generated at different times.

The function declaration statement process the declaration phase, the initialization phase, and the assign phase at the same time.

The variable declaration of the function expression is executed before runtime and initialized to undefined, but not assign value yet.

```javascript
function add(x, y) {
  return x + y;
}

let pow;

console.dir(add); // ƒ add(x, y)
console.dir(pow); // undefined

console.log(add(2, 3)); // 5
console.log(pow(5)); // TypeError: sub is not a function

pow = function(x) {
  return x * x;
};

console.log(pow(5)); // 25
```

#### 

## arguments

If the number of arguments is less than the parameter, the omitted parameter is undefined.

```javascript
function f(x, y) {
  console.log('x: ' + x + ', y: ' + y);
}

f(2); // x: 2, y: undefined
```

```javascript
function f(x, y) {
  console.log(arguments);
  // In browser, not in Node
  // Arguments(2) [2, 3, callee: ƒ, Symbol(Symbol.iterator): ƒ]
  console.log('x: ' + x + ', y: ' + y);
}

f(2, 3); // x: 2, y: 3
```

If the number of arguments are greater than the parameters, the excess arguments are ignored.

But, the excess arguments are not just discarded. All arguments are implicitly stored in the properties of the arguments object.

```javascript
function f(x, y) {
  console.log(arguments);
  // In browser, not in Node
  // Arguments(3) [2, 3, 5, callee: ƒ, Symbol(Symbol.iterator): ƒ]
  console.log('x: ' + x + ', y: ' + y);
}

f(2, 3, 5); // x: 2, y: 3
```

```javascript
function f(x, y) {
  arguments[1] = 5;
  console.log('x: ' + x + ', y: ' + y);
}

f(2, 3); // x: 2, y: 5
```

#### 

## Number of parameters

Parameters are meaningful in order. Therefore, if the number of parameters increases, you must consider the order of the arguments to be passed when calling the function. This makes the function difficult to use and increases the chance of causing mistakes.

Therefore, it is recommended that no more than 3 parameters be used. If more parameters are needed, it is advantageous to declare one parameter and pass the object as an argument.

When you use an object as an argument, you do not have to worry about the order of the parameters if you specify exactly the property key. However, note that if you change the object passed from outside the function, the outside object also will be changed.

#### 

## return

The function can return the execution result using the return keyword.

The return statement returns the value specified after the return keyword. If you do not explicitly specify the return value after the return keyword, undefined is returned.

Also, the function can omit the return statement. At this point, the function returns undefined implicitly.

```javascript
function add(x, y) {
  const sum = x + y;
}

add(2, 3); // undefined
```

```javascript
function add(x, y) {
  const sum = x + y;
  return sum;
}

add(2, 3); // 5
```

The return statement make to stop the execution of the function and exits the function body. Therefore, if there is another statement after the return statement, the statement is not executed and is ignored.

```javascript
function add(x, y) {
  const sum = x + y;
  console.log(sum); // 5
  return sum;
  console.log(sum); // output nothing
}

add(2, 3); // 5
```

