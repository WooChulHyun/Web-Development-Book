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

