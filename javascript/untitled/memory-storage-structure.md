# Memory Storage Structure

### Variables and memory structures 1

Variable is used to remember the memory address.

A memory address is a kind of identifier that is used to distinguish between physical memory spaces.

In other words, a memory address is a unique address that identifies the exact location in the memory space.

When referring to a variable, it refers to the data stored in that address, not to the address in memory.

Therefore, variables must remember not only the address of the memory where the data is stored, but also the information about the length and type of the stored data.

The following figure shows how variables are stored in memory.

![](https://i.postimg.cc/GtX3zxDw/image.png)

As shown in the figure above, one memory space stores one byte of data consisting of 8 bits.

Therefore, the address of the memory is also incremented by 1 byte, and data is stored sequentially from the lowest address.

In the figure above, the length of the variable contains 4 memory spaces in total, so 4 bytes of data are stored in the corresponding variable.

At this point, the name of the variable will point to only the first memory address 0x10.

Thus, the length of the variable is 4, and you must know how the variable is constructed so that the data can be referenced correctly in that variable.



### Variables and memory structures 2

![](https://i.postimg.cc/jS25Cfsc/image.png)

* Code segment

Code segment is the area where our code is loaded. The compiled machine language is entered.

Read-only data

CPU reads and processes commands in this area

* Data segment

Data segment is where global variables, static variables are loaded.

Allocated at the same time as program starts and extinguished from memory at program termination.

* Heap segment

Heap segment is where memory is allocated dynamically. The size is determined at runtime.

Storage space for reference type.

* Stack segment

Stack segment is used to store local variables and parameters, and is returned when the function is called.

Because when a function is called its memory is allocated so it is called a call stack.

It is the first-in and last-out data structure.



Size is determined at compile time.

### Memory Allocation in JavaScript

In JavaScript, in order to make allocate memory allotments easier for programmers, JavaScript allocates memory when declaring values.

```javascript
var n = 100; // Memory Allocation for Numbers
var s = "Hellow"; // Memory Allocation for Characters
var o = {
  a: 10,
  b: null
}; // Memory allocation for objects and their values

var a = [10, null, "string"]; // (Same as object)
// Memory allocation for arrays and values in arrays

function f(a) {
  return a + 1;
} // Allocation for functions (functions are 'callable' objects)

// Function expressions also allocate objects
someElement.addEventListener(
  "click",
  function() {
    someElement.style.backgroundColor = "yellow";
  },
  false
);
```

Allocation via function call

Memory allocation also occurs in some functions.

```javascript
var d = new Date(); // Allocate memory for a Date object
var e = document.createElement("div"); // Allocate memory for DOM elements.
```

Some methods also cause memory allocation to contain new values or objects.

```javascript
var s = "abcdefg";
var s2 = s.substr(0, 3); // s2 is the new string
// Since strings are immutable in JavaScript,
// they do not allocate a new memory and simply store the range [0, 3].

var a = ["Hellow", "World"];
var a2 = ["Hi", "World"];
var a3 = a.concat(a2); // New array with 4 elements
```



### Variables and memory structures 3

#### **Data segment**

```javascript
var a = 10; //Allocate to data segment
var b = 20; //Allocate to data segment
```

![](https://i.postimg.cc/MZ4mX3Gv/data.png)



#### **Stack segment**

```javascript
var a = 10; //Allocate to data segment
var b = 20; //Allocate to data segment

function func1() {
  var c = 30;
  //Local variable c allocated to the stack segment

  func2(c);
  func3(c);

  return 0;
}

function func2(d) {
  var e = 40;
    //The parameter d and the local variable e are allocated to the stack segment
}

function func2(f) {
  var g = 50;
  //The parameter f and the local variable g are allocated to the stack segment
}
```

![](https://i.postimg.cc/KYjvwfyy/3-1.png)

![](https://i.postimg.cc/nzQVcLzR/3-2.png)



#### **Heap segment**

Heap segment: A space that is useful when you need to determine the amount of memory to allocate during program execution \(at runtime\)

Variables can store two types of data: primitive and reference values.

Primitive values are simple data and are Undefined, Null, Boolean, number, and string. Because it manipulates the actual value stored in the variable, we can think that it is accessed by 'value'. The primitive value has a fixed size and is stored in the stack memory.

A reference value is an object that consists of multiple values and is stored in memory, and is stored in the heap memory. When manipulating an object, manipulate the 'reference' for that object, not the object itself. Therefore, it is called 'access by reference'.

* Dynamic Property

The primitive values and reference values definitions similarly, but behave differently after assignment.

When dealing with reference values, you can add, change, and delete properties and methods at any time, and access them until you destroy the object or remove the property. primitive values have no properties, only reference values can be added dynamically.

```javascript
var name = "coca"; // primitive values
name.nickname = "Cola";

var person = new Object(); // reference values
person.nickname = "cocaCola";

console.log(name.nickname); // undefined
console.log(person.nickname); // 'cocaCola'
```

* Value copy

Primitive value: Copying the value itself and creates another variable and assigns it to the new variable. Therefore, two variables are completely separated.

Reference value: If you copy a reference value from one variable to another, pointer values that point to objects stored in the heap \(memory used by the browser\) are copied. So, both variables point to exactly the same object. Therefore, when one side is manipulated, it is reflected on the other side.

```javascript
// Copying primitive value
var origin = 3;
var clone = origin + 2;

console.log(origin); // 3
console.log(clone); // 5

// Copying reference value
var origin = new Object();
var clone = origin;

origin.num = 3;
clone.num = 5;

console.log(origin.num); // 5
console.log(clone.num); // 5
```

Need to know pointer.



### Garbage collection

