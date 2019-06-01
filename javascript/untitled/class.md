# Class

### Class

```javascript
function Circle(radius) {
  this.radius = radius;
}

Circle.prototype.area = function () {
  return Math.PI * this.radius * this.radius;
};
```

```javascript
const Circle = (function () {
  const _radis = '';
  
  // constructor function
  function ConsCircle(radius) {
    _radius = radius;
  }

  ConsCircle.prototype.area = function () {
    return Math.PI * _radius * _radius;
  };

  return ConsCircle;
}());
```

If you modify the previous code\(first code\) with the class syntax, it looks like this:

```javascript
class Circle {
  constructor(radius) {
    this.radius = radius;
  }

  // prototype method
  area() {
    return Math.PI * this.radius * this.radius;
  }
}
```



### constructor

The constructor is a special method for creating an instance and initializing a class field.

{% hint style="info" %}
Class Fields \(Class Members\) 

Encapsulated parameters inside the class. It can be determined to be a data member or a member variable. Class fields are instance properties or static properties. 
{% endhint %}

```javascript
// Class declaration
class Circle {

  // constructor. A name that can not be changed.
  constructor(radius) {
  
    // 'this' points to the instance that the class will create.
    // _radius is a class field.
    this._radius = radius;
  }

  // prototype method
  area() {
    return Math.PI * this._radius * this._radius;
  }
}

const circle = new Circle('2');
console.log(me); // Circle {_radius: "2"}
console.log(circle.area()); // 12.566370614359172
```

There can only be one constructor in a class, and if the class contains more than one constructor, a syntax error occurs. When you create an instance, the thing that you call with new operator is constructor and the value that is passed to constructor's parameter assign class field. 

The constructor can be omitted. If you omit the constructor, it operate the same as including the constructor \(\) {} in the class. That is, it creates an empty object. So to add a property to an instance, you need to dynamically add the property after you create the instance.

```javascript
class Foo { }

const foo = new Foo();
console.log(foo); // Foo {}

// Dynamic property assignment and initialization
foo.num = 1;
console.log(foo); // Foo { num: 1 }
```

The constructor executes the creation and initialization of class fields at the same time as the instance creation. So if you need to initialize the class field, you should not omit the constructor.



### Class field

You can only declare methods in the class body. If you declare a class field \(member variable\) in a class body, a syntax error occurs.

```javascript
class Foo {
  radius = ''; // SyntaxError

  constructor() {}
}
```

{% hint style="info" %}
Running the above example on a modern browser \(Chrome 72+\) or newer Node.js \(version 12+\) will work. This is because the modern browser and the latest Node.js have implemented proposals that can directly declare instance fields and declare private instance fields in the class body

Class field declarations proposal

at the stage 3 \(candidate\) stage of the TC39 process as of May 2019.
{% endhint %}

The class field declared inside the constructor binds to this, which points to the instance that the class will create. As a result, the class field becomes a property of the instance that the class will create, and can be referenced from outside the class through an instance of the class. That is, it is always public.

```javascript
class Foo {
  constructor(name = '') {
    this.name = name; // public Class field
  }
}

const foo = new Foo('Lee');
console.log(foo.name); // Can be referenced outside the class.
```



### Class field declarations proposal

As of May 2019, several new standards for class have been proposed which is Class field declarations proposal and Static class features in the stage 3 \(candidate\) phase of the TC39 process.

* Field declarations
* Private field
* Static public fields

```javascript
class Foo {
  x = 1;            // Field declaration
  #p = 0;           // Private field
  static y = 20;    // Static public field
  static #sp = 30;  // Static private field
  static #sm() {    // Static private method
     console.log('static private method');
   }

  bar() {
    this.#p = 10; 
    this.p = 40; // Add a new public p field dynamically.
    return this.#p;
  }
}

const foo = new Foo();
console.log(foo); // Foo {#p: 10, x: 1}
console.log(foo.x); // 1
console.log(foo.#p); // SyntaxError: //expected 10
console.log(Foo.y); // 20
console.log(Foo.#sp); // SyntaxError: //expected 30
console.log(foo.bar()); // 10
```



### getter, setter

#### getter

A getter is used when it is necessary to manipulate the value of a class field whenever a class field is accessed. A getter is defined with the get keyword before the method name. At this time, the method name is used like the class field name. In other words, the getter is used not as a call but as a property, and the method is called at reference time.

```javascript
class Foo {
  constructor(arr = []) {
    this._arr = arr;
  }

  get firstElem() {
    return this._arr.length ? this._arr[0] : null;
  }
}

const foo = new Foo([1, 2]);
console.log(foo.firstElem); // 1
console.log(foo._arr); // Array(2) [1, 2]
```



#### setter

A setter is used when it is necessary to manipulate the value of a class field whenever a value is assigned to a class field. A setter is defined with the set keyword before the method name. At this time, the method name is used like the class field name. In other words, the setter is not used to call, but as a property to assign a value, and the method is called at the time of assignment.

```javascript
class Foo {
  constructor(arr = []) {
    this._arr = arr;
  }

  get firstElem() {
    return this._arr.length ? this._arr[0] : null;
  }

  set firstElem(elem) {
    this._arr = [elem, ...this._arr];
  }
}

const foo = new Foo([1, 2]);

foo.firstElem = 100;

console.log(foo.firstElem); // 100
console.log(foo._arr); //Array(3) [100, 1, 2]
```



### Static method

Use the static keyword to define the static methods of the class. Static methods are called with the class name, not the instance of the class. Therefore, you can invoke it without creating an instance of the class.

```javascript
class Foo {
  constructor(prop) {
    this.prop = prop;
  }

  static staticMethod() {
    /*
    Static methods can not use 'this'.
    Within a static method, 'this' refers to the class itself, 
    not to an instance of the class.
    */
    return 'staticMethod';
    console.log(this) // -------------> see below code block
  }

  prototypeMethod() {
    return this.prop;
  }
}

console.log(Foo.staticMethod()); // staticMethod

const foo = new Foo(123);

console.log(foo.staticMethod()); 
// Uncaught TypeError: foo.staticMethod is not a function
```

```javascript
// console.log(this) above is:

class Foo {
  constructor(prop) {
    this.prop = prop;
  }

  static staticMethod() {
    /*
    Static methods can not use 'this'.
    Within a static method, 'this' refers to the class itself, 
    not to an instance of the class.
    */
    return 'staticMethod';
    console.log(this) // -------------> see below code block
  }

  prototypeMethod() {
    return this.prop;
  }
}
```

Because static methods are called with the class name, you can use them without creating an instance of the class. However, static methods can not use 'this'. In other words, methods that do not need to use 'this' inside a method can be made static methods.

The following code in ES5 works exactly the same as the code in ES6 class.

```javascript
var Foo = (function () {

  function Foo(prop) {
    this.prop = prop;
  }

  Foo.staticMethod = function () {
    return 'staticMethod';
  };

  Foo.prototype.prototypeMethod = function () {
    return this.prop;
  };

  return Foo;
}());

var foo = new Foo(123);
console.log(foo.prototypeMethod()); // 123
console.log(Foo.staticMethod()); // staticMethod
console.log(foo.staticMethod()); 
// Uncaught TypeError: foo.staticMethod is not a function
```

The static method staticMethod is the method of the constructor function Foo, and the generic method prototypeMethod is the method of prototype object Foo.prototype. So staticMethod can not be called from foo.

![](https://i.postimg.cc/NFjFqYRr/class1.png)



### Class inheritance

In languages such as C ++ or Java, the upper class that inherits to lower class is called super class, and lower class that inherits from upper class is called sub class.

#### extends and super

The extends keyword is used to define a sub class that inherits from the base class. Here we define a child class Cylinder that inherits from the parent class Circle.

The super keyword is used when referencing the parent class\(super class\) or when calling the constructor of the parent class.

Sub class constructors, method can override the super class constructor.

```javascript
// base class (super class)
class Circle {
  constructor(radius) {
    this.radius = radius; 
  }

  getDiameter() {
    return 2 * this.radius;
  }

  getPerimeter() {
    return 2 * Math.PI * this.radius;
  }

  getArea() {
    return Math.PI * Math.pow(this.radius, 2);
  }
}

// sub class 
class Cylinder extends Circle {
  constructor(radius, height) {
    // Here super method invokes the constructor of the parent class 
    // and passes arguments.
    super(radius);
    this.height = height;
  }

  // It override the getArea method of the parent class.
  getArea() {
    // Here super keyword is a reference to the super class
    return (this.height * super.getPerimeter()) + (2 * super.getArea());
  }

  getVolume() {
    // Here super keyword is a reference to the super class
    return super.getArea() * this.height;
  }
}

const cylinder = new Cylinder(2, 10);

console.log(cylinder.getDiameter());  // 4
console.log(cylinder.getPerimeter()); // 12.566370614359172
console.log(cylinder.getArea());      // 150.79644737231007
console.log(cylinder.getVolume());    // 125.66370614359172

console.log(cylinder instanceof Cylinder); // true
console.log(cylinder instanceof Circle);   // true
```



