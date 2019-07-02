# Object Literal

## Object

In JavaScript, all values except primitive types are objects.

A primitive type represents only one value, but an object / reference type is a complex data structure that consists of several types of values \(primitive type values or other objects\) as a unit. The value of the primitive type is an immutable value, but the value of the object type is a mutable value.

An object is a set of properties consisting of a key and a value. You can use any value that is available in JavaScript as the value of the property. Function in JavaScript is first-class objects, so they can be treated as values. Therefore, you can use a function as a property value. If the property value is a function, it is called a method to distinguish it from a normal function.

#### 

## Way to create an object

* Object literal
* Object constructor function
* Constructor function
* Object.create method
* Class \(ES6\)
  * Class-based object-oriented languages such as C ++ and Java create objects by defining classes in advance and creating instances by calling the constructor with the new operator at the required time.
  * Instance
    * An instance is an substance created by a class and stored in memory. In object-oriented programming, objects are concepts that include classes and instances. The class function as a template for creating instances. An instance is a term that focuses on the fact that an object is actually stored in memory.

\*\*\*\*

### **Create an object whit object literal**

```javascript
const PERSON = { name: 'Hyun', gender: 'male' };
```

Here, `{ name: 'Hyun', gender: 'male' }` is an object literal, and the object literal is assigned to the variable person.

`name: 'Hyun'` and `gender: 'male'` are properties of object, `name` and `gender` are property keys ,and `Hyun` and `male` are property values.

Quotation marks must be used for names that do not follow the identifier naming convention.

```javascript
const PERSON = {
  last_name: 'Hyun',
  'first-name': 'Woochul', // <-- Quotation marks
  gender: 'male'
};
```

If you use a value other than a string or symbol value in a property key, it becomes a string through implicit type conversion.

```javascript
const FOO = {
  0: 3,
  1: 4,
  2: 5
};

for (const KEY in FOO) {
  console.log(KEY, typeof KEY);
}

// 0 string
// 1 string
// 2 string
```

#### 

## Method

All the values available in JavaScript can be used as property values. A function is an object \(a first-class object\). Thus, a function can be treated as a value and can be the value of a property.

If the property value is a function, it is called a method to distinguish it from a normal function. In other words, a method means a function restricted in an object.

```javascript
const CIRCLE = {
  center: { x: 3.0, y: 4.0 },
  radius: 5.0,
  area() {
    return Math.PI * this.radius * this.radius;
  }
};

console.log(CIRCLE.area()); // 78.53981633974483
```

#### 

## Way to access a property

To access property values, use dot notation which uses \(.\) operator, or the bracket notation which uses bracket \(\[...\]\) operator.

```javascript
const PERSON = {
  last_name: 'Hyun',
  first_name: 'Woochul',
  gender: 'male'
};

console.log(PERSON.last_name); // Hyun
console.log(PERSON.first_name); // Woochul
console.log(PERSON.age); // undefined
```

#### 

## Add property

```javascript
const PERSON = {
  last_name: 'Hyun',
  first_name: 'Woochul',
  gender: 'male'
};

PERSON.age = 1;

console.log(PERSON);
// {last_name: 'Hyun', first_name: 'Woochul', gender: 'male', age: 1}
```

```javascript
const PERSON = {
  last_name: 'Hyun',
  first_name: 'Woochul',
  gender: 'male'
};

PERSON.age = 5;

console.log(PERSON);
// {last_name: 'Hyun', first_name: 'Woochul', gender: 'male', age: 5}
```

#### 

## Delete property

```javascript
const PERSON = {
  last_name: 'Hyun',
  first_name: 'Woochul',
  gender: 'male',
  age: 5
};

delete PERSON.age;

console.log(PERSON);

// {last_name: 'Hyun', first_name: 'Woochul', gender: 'male'}
```

#### 

## Use the in operator to check for property

```javascript
const PERSON = {
  last_name: 'Hyun',
  first_name: 'Woochul',
  gender: 'male'
};

console.log('last_name' in PERSON); // true
console.log('age' in PERSON); // false
console.log('toString' in PERSON); // true
```



## ES6

When the variable name and the property key are the same name:

```javascript
// ES5

var a = 1;
var b = 2;

var obj = {
  a: a,
  b: b
};

console.log(obj); // {a: 1, b: 2}
```

```javascript
// ES6

const a = 1;
const b = 2;

const obj = { a, b };

console.log(obj); // {a: 1, b: 2}
```

In ES6, you can also dynamically create a property key inside an object literal.

```javascript
// ES5

var a = 1;
var i = 0;

var obj = {};

obj[a + "-" + ++i] = i;
obj[a + "-" + ++i] = i;

console.log(obj); // {1-1: 1, 1-2: 2}
```

```javascript
// ES6

const A = 1;
let i = 0;

const obj = {
  [`${A}-${++i}`]: i,
  [`${A}-${++i}`]: i
};

console.log(obj); // {1-1: 1, 1-2: 2}
```

In ES6, when declaring a method, you can use shortened expressions without the function keyword.

```javascript
// ES5

var obj = {
  number: 1,
  plus3: function() {
    console.log(3 + this.number); // 4
  }
};
```

```javascript
// ES6

const OBJ = {
  number: 1,
  plus3() {
    console.log(3 + this.number); // 4
  }
};
```

