# Constructor function

### Object constructor function

Calling the Object constructor function with the new operator creates and returns an empty object. After creating an empty object, you can complete the object by adding a property or method.

```javascript
const person = new Object();

person.name = 'Hyun';
person.sayHello = function () {
  console.log('Hi! My name is ' + this.name);
};

console.log(person); // {name: "Hyun", sayHello: ƒ}
person.sayHello(); // Hi! My name is Hyun

```

The object created by the constructor function is called an instance.

{% hint style="info" %}
Ins**t**ance:

Because the constructor function is also an object, the the object created by constructor function or the class is called an instance to distinguish it from other objects.
{% endhint %}

In addition to the Object constructor functions, JavaScript provides built-in intrinsic constructor functions such as String, Number, Boolean, Function, Array, Date, and RegExp.

```javascript
const strObj = new String('Lee');
console.log(typeof strObj); // object
console.log(strObj); // String {"Lee"}

const numObj = new Number(123);
console.log(typeof numObj); // object
console.log(numObj); // Number {123}

const boolObj = new Boolean(true);
console.log(typeof boolObj); // object
console.log(boolObj); // Boolean {true}

const func = new Function('x', 'return x * x');
console.log(typeof func); // function
console.dir(func); // ƒ anonymous(x )

const arr = new Array(1, 2, 3);
console.log(typeof arr); // object
console.log(arr); // (3) [1, 2, 3]

const regExp = new RegExp(/ab+c/i);
console.log(typeof regExp); // object
console.log(regExp); // /ab+c/i

const date = new Date();
console.log(typeof date); // object
console.log(date); // Tue May 16 2019 11:11:26 GMT+0900

```

### 

### Constructor function

{% hint style="info" %}
Function that is expected to create an object with the 'new' operator is called the constructor. The constructor name usually uses Pascal notation to capitalize the first letter to indicate that it is a constructor.
{% endhint %}

The object creation method by object literal is intuitive and simple. However, object creation by object literal creates only one object. Therefore, if you need to create multiple objects with the same properties, it is inefficient because you must create the same property each time.

```javascript
const circle1 = {
  radius: 5,
  area() {
    return Math.PI * this.radius * this.radius;
  }
};

console.log(circle1.area()); // 78.53981633974483

const circle2 = {
  radius: 10,
  area() {
    return Math.PI * this.radius * this.radius;
  }
};

console.log(circle2.area()); // 314.1592653589793
```

You can avoid this duplication by creating an object with a constructor function.

```javascript
function Circle(radius) {
  this.radius = radius;
  this.area = function () {
    return Math.PI * this.radius * this.radius;
  };
}

const circle1 = new Circle(5);
const circle2 = new Circle(10);

console.log(circle1.area()); // 78.53981633974483
console.log(circle2.area()); // 314.1592653589793

```

If you do not call the constructor function with the 'new' operator, it operate as a regular function, not a constructor function.

```javascript
const circle3 = Circle(15);

console.log(circle3); // undefined

console.log(radius); // 15
```

### 

### \[\[Call\]\] and \[\[Constructor\]\]

An object whose internal method \[\[Call\]\] is implemented is called a callable. An object whose internal method \[\[Constructor\]\] implemented is called a constructor, and an object that does not implement \[\[Constructor\]\] is called a non-constructor .

A callable is an object that can be called, that is, a function, and a constructor is an object that can be called as a constructor function. The ability to be called as a constructor function means it can be called with the new \(or super\) operator.

When the function is called as a normal function, the internal method \[\[Call\]\] is called and the internal method \[\[Constructor\]\] is called when it is called as a constructor function with the new \(or super\) operator.

```javascript
function foo() {}

[[Call]]
foo();

[[Constructor]]
new foo();
```

Since an object that can not be called is not a function object, that is, a function object, must be callable. Therefore, all function objects can be called by implementing \[\[Call\]\]. However, not all function objects implement \[\[Constructor\]\]. In other words, a function object can be a constructor or a non-constructor.

In conclusion, function objects are 'callable and constructor' or 'callable and non-constructor'. That is, all function objects can be called, but not all function objects can be called as constructor functions.



### constructor and non-constructor

```javascript
function foo() {}
const bar = function() {};
const baz = {
    a: function() {}
};

new foo(); // OK
new bar(); // OK
new baz.a(); // OK

const arrow = () => {};

new arrow(); // TypeError: arrow is not a constructor

const obj = {
  x() {}
};

new obj.x(); // TypeError: obj.x is not a constructor
```

As you can see in the example above, the normal function is a constructor, the arrow function and shortened expressions are non-constructor.

Function objects that are non-constructors do not implement the internal method \[\[Constructor\]\]. Therefore, calling a non-constructor function object as a constructor function results in an error.



### Examples

```javascript
function Circle(radius) {
  this.radius = radius;
  this.area = function () {
    return Math.PI * this.radius * this.radius;
  };
}

const circle1 = new Circle(5);
const circle2 = new Circle(10);

console.log(circle1); // Circle {radius: 5, area: f}
console.log(circle2); // Circle {radius: 10, area: f}

```

If an object other than 'this' is explicitly returned, 'this' will not be returned and the object specified in the return statement will be returned.

```javascript
function Circle(radius) {
  this.radius = radius;
  this.area = function () {
    return Math.PI * this.radius * this.radius;
  };
  return {};
}

const circle1 = new Circle(5);
const circle2 = new Circle(10);

console.log(circle1.area()); // TypeError: circle1.area is not a function
console.log(circle2.area()); // TypeError: circle2.area is not a function

```

```javascript
function Circle(radius) {
  this.radius = radius;
  this.area = function () {
    return Math.PI * this.radius * this.radius;
  };
  return {};
}

const circle1 = new Circle(5);
const circle2 = new Circle(10);

console.log(circle1); // {}
console.log(circle2); // {}
```

However, if you explicitly return a primitive type value, the return of the primitive type is ignored and 'this' is returned.

```javascript
function Circle(radius) {
  this.radius = radius;
  this.area = function () {
    return Math.PI * this.radius * this.radius;
  };
  return 100;
}

const circle1 = new Circle(5);
const circle2 = new Circle(10);

console.log(circle1); // Circle {radius: 5, area: f}
console.log(circle2); // Circle {radius: 10, area: f}
```



### new

There is no special formal difference between the generic function and the constructor function. When you call a function with the new operator, the function acts as a constructor function. However, the function to be called with the new operator must be a constructor, not a non-constructor.

```javascript
// generic function
function add(x, y) {
  return x + y;
}

let inst = new add();
console.log(inst); // {}

function createUser(name, role) {
  return { name, role };
}

inst = new createUser('Hyun', 'admin');
console.log(inst); // {name: "Hyun", role: "admin"}
```

Calling the constructor function without the new operator is called as a normal function. In other words, \[\[Call\]\] is called instead of calling the function object's internal method \[\[Constructor\]\].

```javascript
function Circle(radius) {
  this.radius = radius;
  this.area = function () {
    return Math.PI * this.radius * this.radius;
  };
}

// Calling the constructor function without the new operator is called 
// as a normal function.
const circle = Circle(5);
console.log(circle); // undefined

// 'this' inside the generic function points to the global object window.
console.log(radius); // 5
console.log(area()); // 78.53981633974483

circle.area(); // TypeError: Cannot read property 'area' of undefined
```

