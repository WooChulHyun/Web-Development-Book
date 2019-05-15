# let, const

### var VS let, const

The only way to declare variables up to ES5 was to use the 'var' keyword. Variables declared with the 'var' keyword have the following characteristics.   
 

* Function-level scope

'var' recognize only the code block of the function as a scope. Therefore, all variables created outside the global function are global variables.

Variables declared in the for statement can be referenced outside the code code block of the for statement. 



* Allow omission of the 'var' keyword

There is a good chance of mass-producing implicit global variables. 



* Allow Re-Declaring variables

There is a strong possibility that an unintended variable value change. 



* Variable hoisting

You can reference variables before declaring.   
 

Most problems are caused by global variables. Global variables have the advantage of being easy to use for simple applications, but it should be suppressed except in unavoidable circumstances. Global variables have a broad scope, which makes it difficult to determine where and how they will be used, and may cause unintended changes by an impure function, which increases complexity. Therefore, the narrower the scope of the variable is better.

ES6 introduced the 'let' and 'const' keywords to compensate for the shortcomings of the var keyword.



### let

#### **Block-level scope**

Most programming languages follow a block-level scope, but JavaScript\('var'\) follows a function-level scope.

* Function-level scope\('var'\):

Variables declared within a function are valid only within the function and can not be referenced outside the function. That is, a variable declared inside a function is a local variable, and all variables declared outside the function are global variables.



* Block-level scope\('let', 'const'\):

Variables declared in all code blocks \(functions, if statements, for statements, while statements, try / catch statements, etc.\) are only valid within the code block and can not be referenced outside the code block. That is, variables declared inside a code block are local variables.

```javascript
var x = "outer x"; // global variable
{
  var x = "inner x"; // global variable
  var y = "inner y"; // global variable

  console.log(x); // inner x
  console.log(y); // inner y
}
console.log(x); // inner x
console.log(y); // inner y
```

```javascript
let x = "outer x"; // global variable
{
  let x = "inner x"; // local variable
  let y = "inner y"; // local variable

  console.log(x); // inner x
  console.log(y); // inner y
}
console.log(x); // outer x
console.log(y); // ReferenceError: y is not defined
```



#### **Not allow Re-Declaring variables**

You could declare a variable with the same name as the 'var' keyword. However, the 'let' keyword can not declare duplicate variables with the same name. SyntaxError occurs if you declare variables more than once.

```javascript
var x = "abc";
var x = "def"; // Allow Re-Declaring variables

let y = "abc";
let y = "def"; // Uncaught SyntaxError: Identifier 'y' has already been declared
```



#### **Hoisting**

Javascript hoists all declarations \(var, let, const, function, class\) including let and const introduced in ES6.

However, unlike a variable declared with the 'var' keyword, a reference error occurs if a variable declared with the 'let' keyword when you reference the variable before the declaration. This is because the variable declared with the let keyword falls into the Temporal Dead Zone \(TDZ\) from the start of the scope to the declaration of the variable.

```javascript
console.log(x); // undefined
var x;

console.log(y); // Error: Uncaught ReferenceError: y is not defined
let y;
```

The variable is created in three steps:



* Declaration phase

Register the variable in the execution context of Variable Object. This variable object is the target to which the scope refers. 



* Initialization phase

It allocate memory space for variable registered in Variable Object. At this stage, the variable is initialized to 'undefined'. 



* Assignment phase

Assign the actual value to the variable initialized with 'undefined'.

Variables declared with the 'var' keyword are declared and initialized at once. That is, register the variable in the scope \(declaration step\), allocate space for the variable in memory, and initialize it with 'undefined' \(initialization step\). Therefore, even if the variable is accessed before the variable declaration, no error occurs because the variable exists in the scope. It just returns 'undefined'. The variable is assigned a value when it reaches the variable assignment statement. This phenomenon is called variable hoisting.

Our code:

```javascript
console.log(x); // undefined

var x;
console.log(x); // undefined

x = 1;
console.log(x); // 1
```

===&gt; javascript works

```javascript
var x; // Hoisting / Declared, Initialized
// At the beginning of the scope, the declaration and initialization steps are executed.
// So you can refer to a variable before the variable declaration.

console.log(x); // undefined

var x; // Hoisted
console.log(x); // undefined

x = 1; // The assign is executed in the assignment statement.
console.log(x); // 1
```

Variables declared with the 'let' keyword proceed separately from the declaration phase and the initialization phase. In other words, the variable is registered in the scope \(declaration step\) but the initialization step is done when reaches the variable statement. If you try to access a variable before initialization, a reference error \(ReferenceError\) occurs. This is because the variable has not been initialized yet. In other words, the memory space for the variables is not yet allocated. Therefore, variables can not be referenced from the start point of the scope to the initialization point. The interval from the start point of the scope to the initialization start point is called 'Temporal Dead Zone \(TDZ\)'.

Our code:

```javascript
console.log(x); // ReferenceError: x is not defined

let x;
console.log(x); // undefined

x = 1;
console.log(x); // 1
```

===&gt; javascript works

```javascript
let x; // Hoisting / Declared / TDZ
// At the beginning of the scope, only the declaration is executed.
// So you are not able to refer before the variable declaration statement.

console.log(x); // ReferenceError: x is not defined

let x; // Hoisted / declaration statement / Initialization is executed.
console.log(x); // undefined

x = 1; // The assign is executed in the assignment statement.
console.log(x); // 1
```

As a result, ES6 does not seem to be different from the case where hoisting does not occur. But it is not. Consider the example below.

```javascript
var x = 1; // global variable

{
  console.log(x); // 1
  var x = 2; // global variable
  console.log(x); // 2
}
console.log(x); // 2
```

```javascript
let x = 1; // global variable

{
  console.log(x); // 1
}
console.log(x); // 1
```

```javascript
let x = 1; // global variable

{
  console.log(x); // ReferenceError: x is not defined
  let x = 2; // local variable
  console.log(x); // 2
}
console.log(x); // 1
```



#### **Closure**

```javascript
var funcs = [];

for (var i = 0; i < 3; i++) {
  funcs.push(function() {
    console.log(i);
  });
  console.log(funcs[i]());
}

for (var j = 0; j < 3; j++) {
  funcs[j]();
}

console.log(funcs);
```

Result:

```javascript
0; // funcs = [[function (console.log(i))]]
// global variable 'i' is 0 now
// Example result = [0]

undefined; //because no return in
// function() {console.log(i);};

1; // funcs = [[function (console.log(i))], [function (console.log(i))]]
// global variable 'i' is 1 now
// Example result = [1, 1]

undefined; //because no return in
// function() {console.log(i);};

2; // funcs = [[function (console.log(i))], [function (console.log(i))], [function (console.log(i))]]
// global variable 'i' is 2 now
// Example result = [2, 2, 2]

undefined; //because no return in
// function() {console.log(i);};

3; // because global variable 'i' is 3
3; // because global variable 'i' is 3
3;
[([Function], [Function], [Function])]; // because global variable 'i' is 3
```

```javascript
var funcs = [];

for (let i = 0; i < 3; i++) {
  funcs.push(function() {
    console.log(i);
  });
  console.log(funcs[i]());
}

for (var j = 0; j < 3; j++) {
  funcs[j]();
}

console.log(funcs);
```

Result:

```javascript
0; // funcs = [[function (console.log(i))]]
// variable 'i' is not affected because it is outside the of the local scope.
// Example result = [0]

undefined; //because no return in
// function() {console.log(i);};

1; // funcs = [[function (console.log(i))], [function (console.log(i))]]
// variable 'i' is not affected because it is outside the of the local scope.
// Example result = [0, 1]

undefined; //because no return in
// function() {console.log(i);};

2; // funcs = [[function (console.log(i))], [function (console.log(i))], [function (console.log(i))]]
// variable 'i' is not affected because it is outside the of the local scope.
// Example result = [0, 1, 2]

undefined; //because no return in
// function() {console.log(i);};

0;
1;
2;
[([Function], [Function], [Function])];
```



#### **Global objects and let**

A global object is the only top-level object of all objects, usually a window object in the browser-side and a global object in the Server-side \(Node.js\).

If a variable declared with the 'var' keyword is used as a global variable, it becomes a property of the global object.

```javascript
var x = 123; // Global variable

console.log(window.x); // 123
```

If a variable declared with the 'let' keyword is used as a global variable, the let global variable is not a property of the global object. In other words, it can not be accessed like window.x. let global variables exist in an invisible conceptual block.

```javascript
let x = 123; // Global variable

console.log(window.x); // undefined
```



### const

'const' is used for constants \(unchangeable values\). However, it is not always used for constants. 'const' is mostly identical to let.



#### **Declaration and initialization**

'let' is free to reassign, but 'const' is not re-assignable.

```javascript
// Declares variable names as uppercase to indicate that they are constants.
const X = 123;
X = 456; // TypeError: Assignment to constant variable.
```

'const' must be assigned at the same time as declaration. Otherwise, SyntaxError occurs.

```javascript
const X; // SyntaxError: Missing initializer in const declaration
```



#### **const and objects**

'const' is not able to be reassigned. This means that if the type of the 'const' variable is an object, it can not change the reference to the object. However, the properties of the object are not protected. In other words, it is impossible to reassign, but you can change the contents of the assigned object \(adding, removing, changing property values\).

```javascript
const ANIMAL = { animal1: "lion" };
const ALPHABET = ["a"];

// animal = {}; // TypeError: Assignment to constant variable.

ANIMAL.animal1 = "tiger";
ANIMAL.animal2 = "turtle";
ALPHABET.push("b");

console.log(ANIMAL); // {animal1: "tiger", animal2: "turtle"}
console.log(ALPHABET); // ["a", "b"]
```

Even if the contents of the object are changed, the address value allocated to the object type variable is not changed. Therefore, it is better to use 'const' for object type variable declaration. If you need to explicitly change the address value\(reallocated\) of an object type variable, use 'let'.

