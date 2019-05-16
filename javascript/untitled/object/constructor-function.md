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

If you do not call the constructor function with the 'new' operator, it behaves as a regular function, not a constructor function.

```javascript
const circle3 = Circle(15);

console.log(circle3); // undefined

console.log(radius); // 15
```

### 

### \[\[Call\]\] and \[\[Constructor\]\]

An object whose inner method \[\[Call\]\] is implemented is called a callable. An object whose inner method \[\[Constructor\]\] implemented is called a constructor, and an object that does not implement \[\[Constructor\]\] is called a non-constructor .

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

