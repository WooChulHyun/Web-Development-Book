# Arrow function

### Declaration of the arrow function

An arrow function expression is abbreviated expression of a function literal \(an anonymous function\). However, it is not exactly the same as a function literal.

```javascript
// Way to specify parameters
() => { ... } // If there are no parameters
x => { ... } // If there is one parameter, the parentheses can be omitted.
(x, y) => { ... } // If there are multiple parameters, 
                  // the parentheses can not be omitted.
                  
// Way to specify function body
x => { return x * x }  // single line block
x => x * x             // If the function body is a single-line statement, 
                       // you can omit the braces and return implicitly. 
                       // It is the same as above expression.
                       
() => { return { a: 1 }; }
() => ({ a: 1 })  // Use parentheses when returning objects.

() => {           // multi line block.
const x = 10;
return x * x;
};

// IIFE
(x => x * x)(3) // 9
```



### Calling the arrow function

The arrow function can only be used as an anonymous function. So, to call the arrow function, use a function expression.

```javascript
// ES5
var pow = function (x) { return x * x; };
console.log(pow(10)); // 100

// ES6
const pow = x => x * x;
console.log(pow(10)); // 100
```

It can be used as a callback function. In this case, the expression is simpler than a normal function expression.

```javascript
// ES5
var arr = [1, 2, 3];
var pow = arr.map(function (x) {
  return x * x;
});

console.log(pow); // [ 1, 4, 9 ]

// ES6
const arr = [1, 2, 3];
const pow = arr.map(x => x * x);

console.log(pow); // [ 1, 4, 9 ]
```



### Difference between function literals and arrow functions

#### The value of this is determined when defining the function.

The arrow function statically determines the object which is bound to 'this' when declaring the function. Unlike regular functions, which are determined dynamically, 'this' in the arrow function always points to 'this' in the one level up scope. This is called 'Lexical this'. 

```javascript
const obj = {
  say() {
    console.log(this);
    (function () {
      console.log(this);
    }());
    (() => console.log(this))();
  }
};

obj.say();

// {say: ƒ}
// Window {postMessage: ƒ, blur: ƒ, focus: ƒ, close: ƒ, parent: Window, …}
// {say: ƒ}
```

```javascript
function Prefixer(prefix) {
  this.prefix = prefix;
}

Prefixer.prototype.prefixArray = function (arr) {
  // this points to this in the parent scope prefixArray method.
  return arr.map(x => `${this.prefix}  ${x}`);
};

const pre = new Prefixer('Hi');
console.log(pre.prefixArray(['Lee', 'Kim']));
// ["Hi  Lee", "Hi  Kim"]
```

The arrow function cannot change 'this' by using the call, apply, or bind methods.

```javascript
window.x = 1;
const normal = function () { return this.x; };
const arrow = () => this.x;

console.log(normal.call({ x: 10 })); // 10
console.log(arrow.call({ x: 10 }));  // 1
```

```javascript
const f = function () {
  console.log(this.name);
};
const g = () => console.log(this.name);

const woochul = { name: 'Woochul' };
f.call(woochul); // Woochul
g.call(woochul); // ""
```



#### There is no arguments variable.

```javascript
const f = () => console.log(arguments);
f(); // ReferenceError: arguments is not defined
```



#### Can not be used as a constructor.

```javascript
const Person = (name, age) => {
  this.name = name;
  this.age = age;
};

const woochul = new Person('Woochul', 1);
// TypeError: Person is not a constructor
```



### Case that do not use the arrow function

#### Method

```javascript
const person = {
  name: 'Hyun',
  sayHi: () => console.log(`Hi ${this.name}`)
};

person.sayHi(); // Hi undefined
```

The 'this' inside the arrow function defined by the method points to the global object 'window' that is the parent context, not the object that owns the method, ie, the object that called the method.

```javascript
const person = {
  name: 'Hyun',
  sayHi() {
    console.log(`Hi ${this.name}`);
  }
};

person.sayHi(); // Hi Hyun
```



#### prototype

```javascript
const person = {
  name: 'Hyun',
};

Object.prototype.sayHi = () => console.log(`Hi ${this.name}`);

person.sayHi(); // Hi undefined
```

The same problem occurs when defining an object's method with an arrow function.

```javascript
const person = {
  name: 'Hyun',
};

Object.prototype.sayHi = function() {
  console.log(`Hi ${this.name}`);
};

person.sayHi(); // Hi Hyun
```



#### Constructor function

Same as above example

```javascript
  this.name = name;
  this.age = age;
};

const woochul = new Person('Woochul', 1);
// TypeError: Person is not a constructor
```



#### Callback function of addEventListener function

If you define the callback function of the addEventListener function as an arrow function, this points to the global object 'window', which is the parent context.

```javascript
const button = document.getElementById('myButton');

button.addEventListener('click', () => {
  console.log(this === window); // => true
  this.innerHTML = 'Clicked button';
});
```

Therefore, if you use 'this' in the callback function of the addEventListener function, you must use the general function defined by the function keyword. Inside the callback function of the addEventListener function defined as a generic function, 'this' points to the element bound to the event listener \(currentTarget\).

```javascript
const button = document.getElementById('myButton');

button.addEventListener('click', function() {
  console.log(this === button); // => true
  this.innerHTML = 'Clicked button';
});
```

