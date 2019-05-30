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

All properties - data properties and accessor properties - have internal slots / methods that define their state and operation. These are called property attributes. This property attribute is automatically defined by default when the JavaScript engine creates the property. You can control the detailed operation of each property \(Value, Writable, Enumerable, Configurable\) by setting the defined property attributes.

#### Data properties have the following property attributes:

* \[\[Value\]\]

The value returned by the internal method \[\[Get\]\] when a property value is accessed with a property key.

When a property value is stored by a property key, the value is stored in \[\[Value\]\]. If there is no property at this time, create a property and store the value in \[\[Value\]\] of the created property.



* \[\[Writable\]\]

Indicates whether the property value can be changed and has a Boolean value.

If the value of \[\[Writable\]\] is false, the value of \[\[Value\]\] of the property can not be changed.



* \[\[Enumerable\]\]

Indicates whether the property can be enumerated and has a Boolean value.

If the value of \[\[Enumerable\]\] is false, the property can not be enumerated with the `for / in` statement or the `Object.keys` method.



* \[\[Configurable\]\]

Indicates whether the property can be redefined and has a Boolean value.

If the value of \[\[Configurable\]\] is false, deletion of the property or modification of the property attribute value is prohibited. However, if \[\[Writable\]\] is true, changing \[\[Value\]\] / and changing \[\[Writable\]\] value to false is allowed.



#### Accessor properties have the following property attributes:

* \[\[Get\]\]

Accessor function that is called when reading the value of a data property through an accessor property. That is, when accessing a property value with an accessor property key, the value of the property attribute \[\[Get\]\], that is, the getter function is called, and the result is returned as the property value.



* \[\[Set\]\]

Accessor function that is called when storing the value of a data property through an accessor property. That is, when you store a property value with the accessor property key, the value of the property attribute \[\[Set\]\], that is, the setter function is called, and the result is stored as a property value.



* \[\[Enumerable\]\]

Same as \[\[Enumerable\]\] in the data property.



* \[\[Configurable\]\]

Same as \[\[Configurable\]\] in the data property.



### Property descriptor and  Methods for reading and writing property

Property attributes can be set with property descriptors.



#### Get property descriptor: Object.getOwnPropertyDescriptor

The Object.getOwnPropertyDescriptor method gets the property descriptor for the object property. The first argument is a reference to the object, and the second argument is a property name.

```javascript
const woochul = { name: 'Woochul' };

const descriptor = Object.getOwnPropertyDescriptor(woochul, 'name');

console.log(descriptor);

// {value: "Woochul", writable: true, enumerable: true, configurable: true}
```

Like above, default value of \[\[Writable\]\], \[\[Enumerable\]\], \[\[Configurable\]\] is true and  value of \[\[Value\]\] represents the property value if property is created by default without a property definition. This is same even if you add properties dynamically.

If you specify a property that inherits from a prototype or property that is not exist, it returns undefined.

```javascript
console.log(Object.getOwnPropertyDescriptor({}, 'name')); // undefined
console.log(Object.getOwnPropertyDescriptor(woochul, 'toString')); //undefined
```

Thus, the Object.getOwnPropertyDescriptor method can only get the property descriptor for that object.



#### Set property descriptor: Object.defineProperty

The Object.defineProperty method sets the property descriptor on the object's property. The first argument is a reference to the object, the second argument is a string representing the property name, and the third argument is a reference to the property descriptor.

```javascript
const obj = {};
Object.defineProperty(obj, 'firstName', {
  value: 'Woochul',
  writable: true,
  enumerable: true,
  configurable: true
});

console.log(Object.getOwnPropertyDescriptor(obj, 'firstName'));

// Object {value: "Woochul", writable: true, enumerable: true, configurable: true}
```

When you use this method, you can omit each property in the property descriptor. The attribute values corresponding to the omitted properties are:

|  |  |
| :--- | :--- |
| \[\[Value\]\] | undefined |
| \[\[Get\]\] | undefined |
| \[\[Set\]\] | undefined |
| \[\[Writable\]\] | false |
| \[\[Enumerable\]\] | false |
| \[\[Configurable\]\] | false |

```javascript
const obj = {};
Object.defineProperty(obj, 'firstName', {
  value: 'Woochul',
  writable: true,
  enumerable: true,
  configurable: true
});

Object.defineProperty(obj, 'lastName', {
  value: 'Hyun'
});

console.log(Object.getOwnPropertyDescriptor(obj, 'firstName'));
// Object {value: "Woochul", writable: true, enumerable: true, configurable: true}

console.log(Object.getOwnPropertyDescriptor(obj, 'lastName'));
// Object {value: "Hyun", writable: false, enumerable: false, configurable: false}

console.log(Object.keys(obj));
// The value of [[Enumerable]] is false, so it is not listed.
// Array(1) ["first_name"]

obj.lastName = 'Kim';
// The value of [[Writable]] is false, so it cannot be changeed.
console.log(obj);
// Object {firstName: "Woochul", lastName: "Hyun"}

delete obj.lastName;
// The value of [[Configurable]] is false, so it cannot be deleted.
console.log(obj);
// Object {firstName: "Woochul", lastName: "Hyun"}
```

You can change the property value of a property.

```javascript
Object.defineProperty(obj, 'firstName', {
  value: 'Woochul',
  writable: false,
  enumerable: false,
  configurable: true
});

console.log(Object.keys(obj));
// The value of [[Enumerable]] is false, so it is not listed.
// Array(0) []

obj.firstName = 'Kim';
// The value of [[Writable]] is false, so it cannot be changeed.

console.log(obj);
// Object {firstName: "Woochul", lastName: "Hyun"}
```

Once you change the configurable value to false, you can not change the value of any other internal property only except writable value true to false\(not false to true\). Also, configurable value can not be changed to true.

```javascript
const obj = {};
Object.defineProperty(obj, 'firstName', {
  value: 'Woochul',
  writable: true,
  enumerable: true,
  configurable: true
});

Object.defineProperty(obj, 'lastName', {
  value: 'Hyun',
  writable: true,
  enumerable: true,
  configurable: true
});

Object.defineProperty(obj, 'fullName', {
  get() {
    // === get() {
    return `${this.firstName} ${this.lastName}`;
  },

  set(name) {
    // === set(name) {
    [this.firstName, this.lastName] = name.split(' ');
  },
  enumerable: true,
  configurable: true
});
const descriptor = Object.getOwnPropertyDescriptor(obj, 'fullName');

console.log(descriptor);
// {get: ƒ, set: ƒ, enumerable: true, configurable: true}

console.log(
  'obj.fullName: ' + obj.fullName,
  '/ obj.firstNmae: ' + obj.firstName,
  '/ obj.lastName: ' + obj.lastName
);
// obj.fullName: Woochul Hyun / obj.firstNmae: Woochul / obj.lastName: Hyun

obj.fullName = 'abc def';

console.log(
  'obj.fullName: ' + obj.fullName,
  '/ obj.firstNmae: ' + obj.firstName,
  '/ obj.lastName: ' + obj.lastName
);
// obj.fullName: abc def / obj.firstNmae: abc / obj.lastName: def
```



#### Set property descriptors in once: Object.defineProperties

The Object.defineProperty method can only define one property at a time. You can define multiple properties at once using the Object.defineProperties method.

```javascript
const obj = {};

Object.defineProperties(obj, {
  firstName: {
    value: 'Woochul',
    writable: true,
    enumerable: true,
    configurable: true
  },
  lastName: {
    value: 'Hyun',
    writable: true,
    enumerable: true,
    configurable: true
  },

  fullName: {
    get() {
      return `${this.firstName} ${this.lastName}`;
    },
    set(name) {
      [this.firstName, this.lastName] = name.split(' ');
    },
    enumerable: true,
    configurable: true
  }
});

console.log(obj); // {firstName: "Woochul", lastName: "Hyun"}

obj.fullName = 'abc def';
console.log(obj); // {firstName: "abc", lastName: "def"}
```

