# this

### this

The 'this' value is determined when the function is called and executed. This 'this' value is 'a reference to the object to which the function belongs when the function is called' and is the object referenced by the 'this binding' component of the execution context.

```javascript
const circle = {
  radius: '5',
  area() {
        return Math.PI * this.radius * this.radius;
    }
};

console.log(circle.area()); // 78.53981633974483
```

In this code, we refer to the function as circle.area and execute it. The object to which circle.area belongs is circle. That is, the object pointed to by the 'this binding' component in the execution context in which the area method is called is circle. Therefore, the 'this' value points to circle, so the value of this.radius is '5'. The circle.area value is a reference to the function. Therefore, you can assign this value to a property of another object.

```javascript
const circle = {
  radius: '5',
  area() {
    return Math.PI * this.radius * this.radius;
  }
};

console.log(circle.area()); // 78.53981633974483

const circle2 = { radius: 10 };
circle2.area = circle.area;

console.log(circle2.area()); // 314.1592653589793
```



