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



