# Prototype

### Problems with method definition in constructor

If you define a method after 'this' in the constructor, the same method is added to every instance created by that constructor. Therefore, if you create multiple instances with the constructor containing the method, you will create multiple method as many as  you create instances and you will waste the memory.

```javascript
function Circle(radius) {
  this.radius = radius;
  this.area = function () {
    return Math.PI * this.radius * this.radius;
  };
}

const circle1 = new Circle(2);
const circle2 = new Circle(5);
```

![](https://i.postimg.cc/wxJXxGW1/1.png)

Every object \(instance\) created by the Circle constructor function has a radius property and a area method. The value of the radius property is typically different instance by instance. \(The radius property may be the same if multiple instances of the same state are needed.\) But the area method is used for all instances and it is exactly same.



## Prototype

In JavaScript, only functions have a prototype property.

```javascript
function F() {}
console.log(F.prototype); // {constructor: ƒ}
console.log((function () {}).hasOwnProperty('prototype')); // true

const a = {};
console.log(a.prototype); //undefined
console.log({}.hasOwnProperty('prototype')); // false
```

The object which is pointed from the prototype property of the function is called the prototype object of the function. The prototype property defaults to an empty object.

![](https://i.postimg.cc/G2MpJYx8/2.png)

Properties of a prototype object can be used as properties of that instance in all instances created by the constructor.

```javascript
function F() {}

F.prototype.prop = 'prototype value';

const obj = new F();
console.log(obj.prop); // prototype value

obj.prop = 'instance value';
console.log(obj.prop); // instance value
console.log(F.prototype.prop); // prototype value
```

#### 

#### Example

```javascript
function Circle(radius) {
  this.radius = radius;
}

Circle.prototype.area = function () {
  return Math.PI * this.radius * this.radius;
};

const circle1 = new Circle(2);
const circle2 = new Circle(5);

console.log('radous: ' + circle1.radius, '// area: ' + circle1.area());
// radous: 2 // area: 12.566370614359172
console.log('radous: ' + circle2.radius, '// area: ' + circle2.area());
// radous: 5 // area: 78.53981633974483
```

![](https://i.postimg.cc/wMnFMw39/3.png)

### 

### Prototype Object

A prototype is an object that acts as the parent object and provides shared properties \(including methods\) to other objects. A descendant \(child\) object that inherits the prototype can freely use the properties of its parent object as its own properties.

All objects have an internal slot called \[\[Prototype\]\]. This is an object different from the prototype property of the function object.

Every object has one prototype. The prototype is null or an object. And all the prototypes are linked with the constructor function. That is, objects, prototypes and constructor functions are linked together.

An object can access its prototype, that is, the object pointed to its \[\[Prototype\]\] internal slot, via the `__proto__` accessor property, as shown above. And prototypes can access constructor functions through constructor properties. The prototype function can access the prototype through the prototype property.

![](https://i.postimg.cc/zGqBfnZZ/4.png)



## The object's `__proto__` accessor property

All objects can access their prototype ,that is, \[\[Prototype\]\] internal slots via the `__proto__`accessor property. \(The `__proto__` property of an object points to the parent object that inherited the object.\)

Thus, an object can use the properties of the parent object pointed to by the `__proto__` property.

```javascript
const objA = {
  name: 'Kim',
  sayHello() {
    console.log('Hello! ' + this.name); // Hello Lee <-- result
  }
};

const objB = {
  name: 'Lee'
};

objB.__proto__ = objA;
const objC = {};
objC.__proto__ = objB;
console.log(objC.sayHello());
```

The three objects in the above code are linked by using the `__proto__` property.

![](https://i.postimg.cc/6qkRD09S/5.png)



## Function object's Prototype property

A function object also has a prototype property in addition to the `__proto__` accessor property. The prototype property of a function object points to the prototype of the instance to be created by the constructor function.

Prototype objects basically have a constructor property and internal properties \[\[Prototype\]\]\(`__proto__`\).\(except method shorthand expression and the arrow function, these do not have constructor\)

```javascript
function Person(name) {
  this.name = name;
}

const me = new Person('Kim');

console.log(Person.prototype === me.__proto__);  // true
```

![](https://i.postimg.cc/65SmBN8D/6.png)

### constructor property

Every prototype has a constructor property. This constructor property points to a constructor function. This connection is made when the constructor function is created, that is, when the function object is created.

```javascript
function Person(name) {
  this.name = name;
}

const me = new Person('Kim');

console.log(me.constructor === Person);  // true
```

![](https://i.postimg.cc/65SmBN8D/6.png)

In the above example, the Person constructor function created the me object. At this time, the me object is connected to the constructor function through the constructor property of the prototype. The me object does not have a constructor property, but Person.prototye has a constructor property. The me object inherits the constructor property from the Person.prototye.



### The function's`__proto__` accessor property

The inner property \[\[Prototype\]\] of the prototype object of the function object points to Object.prototype by default. That is, the prototype object prototype is Object.prototype.

So the instance created by the constructor can use the properties of Object.prototype. Also, the prototype of Object.prototype points to null.

![](https://i.postimg.cc/rp617618/7.png)



### Prototype chain

```javascript
function Circle(radius) {
  this.radius = radius;
}

Circle.prototype.area = function () {
  return Math.PI * this.radius * this.radius;
};

const circle1 = new Circle(2);

console.log('radous: ' + circle1.radius, '// area: ' + circle1.area());
// radous: 2 // area: 12.566370614359172
```

![](https://i.postimg.cc/v8KCYhqP/8.png)

When JavaScript tries to access an object's properties \(including methods\), if there is no property to access that object, it follows the link pointed to by the `__proto__` accessor property to sequentially search in properties of the prototype that act as its parent. This is called a prototype chain.

```javascript
// hasOwnProperty is Object.prototype's method
// The radius object searches the hasOwnProperty method follow the prototype chain.
console.log(circle1.hasOwnProperty('radius')); // true
```

When you call a method like circle1.hasOwnProperty \('radius'\), the JavaScript engine searches for the method through the following process:

First, it looks for the hasOwnProperty method on the circle1 object that called the hasOwnProperty method. Since the circle1 object does not have a hasOwnProperty method, it navigates to the prototype chain \(ie, Circle.prototype in the example above\) which is bound to the `__proto__` accessor property and searches for the hasOwnProperty method.

Because Circle.prototype also does not have a hasOwnProperty method, go to the prototype chain, that is, to the prototype bound to the `__proto__` accessor property \(in this case, Object.prototype\) and search for the hasOwnProperty method.

There is a hasOwnProperty method in Object.prototype. The JavaScript engine calls the Object.prototype.hasOwnProperty method. At this time, the circle1 object is bound to this in the Object.prototype.hasOwnProperty method.

```javascript
Object.prototype.hasOwnProperty.call(circle1, 'radius');
```

In contrast, identifiers that are not properties are searched in the scope chain. In other words, the JavaScript engine searches identifiers from the hierarchical structure of the scope, which is a nested relationship of functions. Thus, the scope chain is a mechanism for searching for identifiers.

```javascript
circle1.hasOwnProperty('radius');
```

In the above example, first searches the identifier circle1 in the scope chain. The identifier circle1 is declared globally and is searched from the global scope. After searching the identifier circle1, search the hasOwnProperty method from the circle1 object's prototype chain.

Thus, the scope chain and the prototype chain do not operate independently of each other, but rather cooperate to find identifiers and properties.



### Encapsulation



