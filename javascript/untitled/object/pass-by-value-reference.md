# Pass By Value/Reference

### Pass By Value

The values of primitive types \(numbers, strings, boolean, null, undefined, symbol\), are immutable values. In other words, once created, the primitive value is read-only and can not be changed. Not changeable is a statement of the value, not the variable.

The fact that you can not change a value is different from the meaning that you can not reassign. The variable can be changed by reassigning the new value. That's why it's called a variable.

```javascript
let a;

a = 10;

a = 20;
```

If you reassign a new primitive value to a primitive variable, the variable does not modify the primitive value itself in the memory space before the reassignment, but rather reserves the new memory space and stores the reassigned primitive value. In other words, the address of the memory space that the variable refers to is changed.

```javascript
let a = 10;

let b = a;

console.log(a, b); // 10  10
console.log(a === b); // true
a = 100;

console.log(a === b); // false

console.log(a); // 100
console.log(b); // 10
```

If the assigned variable \(a in the example above\) is a primitive type, the assigned variable value is copied and transmitted. This is called pass by value.

In the above example, if you assign the variable a to the variable b, the value of the variable a is copied and assigned to the variable b.



### Pass By Reference

The value of an object \(reference\) type, that is, an object is a mutable value.

A variable that has been assigned a primitive value has its primitive value as its value. However, the variable to which the object is assigned a reference value as a value. The reference value is the address of the memory space in which the generated object is stored, itself.

The memory space allocated by the variable to which is assigned object stores address of the memory space where the created object is actually stored. This value is called the reference value. Variables can access the object through this reference value.

```javascript
const A = 10;
const B = 10;

//Primitive values are true when the values are compared
//because the values are stored directly in memory.
console.log(A === B); // true

const C = { a: 1 };
const D = { a: 1 };

//The reference value is false when the value is compared
//because the reference value is stored in memory.
console.log(C === D); // false

const E = { a: 1 };
const F = E;

// Reference value is same
console.log(E === F); // true
```

> Shallow copy and deep copy: A shallow copy is a copy of a reference value, and a deep copy is a copy of the object itself as a primitive value.

If you assign a variable \(original, E\) pointing to an object to another variable \(copy, F\), the original reference value is copied and transmitted. This is referred to as pass-by reference.

```javascript
const E = { a: 1 };
const F = E;

// Reference value is same
console.log(E === F); // true
```

```javascript
const E = { a: 1 };
const F = E;

// Reference value is same
console.log(E === F); // true

F.b = 2;
E.a = 3;

console.log(E); // {a: 3, b: 2}
console.log(F); // {a: 3, b: 2}
console.log(E === F); // true
```

```javascript
const A = { a: 1 };

const B = { a: 1 };

console.log(A === B); // false

console.log(A.a === B.a); // true
```

