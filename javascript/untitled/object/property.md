# property

### property definition

A property definition is a property that defines the value of a property attribute to manage the state of the property. For example, you can define whether the property value can be writable, property is enumerable, property is configurable.

When creating a property \(Object literal evaluation, Dynamic creation property\), the JavaScript engine automatically defaults to a property attribute that indicates the state of the property.

```javascript
const obj = {};

obj.prop = 10;

const descriptor = Object.getOwnPropertyDescriptor(obj, 'prop');
console.log(descriptor);
// The prop property of the obj object defines 
// the value, writable, enumerable, and configurable attributes.

// {value: 10, writable: true, enumerable: true, configurable: true}
```

Dynamic creation property is create and add a property when the property does not exist, property definition is defines the property attribute. The property attribute indicates the state of the property. The state of a property is the value of the property, the value is writable, enumerable, or configurable.



### Internal slot / method

The internal slot and the internal method define the internal state and internal operational associated with the object required by the ECMAScript specification. In other words, the internal slots and internal methods are pseudo properties and pseudo methods used by the ECMAScript specification to describe the algorithm that the JavaScript engine executes the code. Names enclosed in double brackets \(\[\[...\]\]\) appearing in the ECMAScript specification are internal slots and internal methods.

The internal slots and internal methods define the internal implementation specifications of the JavaScript engine. The JavaScript engine only needs to satisfy the specifications of the internal slots and internal methods defined in the ECMAScript specification, but does not expose them to the outside.

That is, the internal slots and internal methods are not properties of the object. Therefore, internal slots and internal methods do not, in principle, provide a way to access or call directly. However, there are some ways to access indirectly to some internal slots and internal implementations.



### Accessor property

The accessor property allows you to automatically handle the operation which you want to when reading and writing properties.



#### Property type

* Data property: A general property consisting of keys and values. \(property for saving value\)



* Accessor property:  A property that has accessor function instead of a value to use when reading or writing the value of another data property.



#### Accessor property

Accessors are methods that allow object-oriented programming to read or write the value of an object's property from outside the object. By using the accessor properties, you can prevent the improperly data modifies, hide certain data from the outside, and pass it on as appropriate values when attempting to read data from outside.

For a single accessor property, you can define a getter function that takes charge of reading the property and a setter function that takes charge of the write the property. The accessor property can define both the getter and setter functions, or just one. \(You can also use one or more getter and setters functions\)

To define getters and setters for the accessor property, you have to write a function with the get and set keyword instead of the function keyword. The getter has no arguments, and the setter has one argument. When attempting to read the value of the accessor property, the getter is called and the setter is called when it tries to write the value. If attempts to read an accessor property without a getter, return undefined. If you try to write on an accessor property that does not have a setter, nothing happens.

```javascript
const XY = {
  x: 10,
  y: 2,
  get multiplication() {
    return this.x * this.y;
  },
  get division() {
    return this.x / this.y;
  },
  set changeXY(obj) {
    this.x = obj.x;
    this.y = obj.y;
  }
};

console.log(XY.x); // 10
console.log(XY.y); // 2
console.log(XY.multiplication); // 20
console.log(XY.division); // 5

XY.changeXY = { x: 100, y: 10 };
console.log(XY.x); // 100
console.log(XY.y); // 10
console.log(XY.multiplication); // 1000
console.log(XY.division); // 10
```



### Property attributes



