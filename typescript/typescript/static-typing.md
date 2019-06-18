# Static Typing

### Type Declaration

TypeScript can declare a type by specifying the type after the variable name.

```typescript
let foo: string = 'hello';
```

If you assign a value that does not match the declared type, an error occurs at compile time.

```typescript
let bar: number = true; // error TS2322: Type 'true' is not assignable to type 'number'.
```

This type declaration helps developers predict code. The type declaration also allows for strong type checking to detect basic errors before runtime, such as grammar errors or assignments of values that do not match the type.

The type declaration method for the parameter and return value of the function is as follows. As with regular variables, an error occurs if a value that does not match the declared type is given.

```typescript
function multiply1(x: number, y: number): number {
  return x * y;
}

const multiply2 = (x: number, y: number): number => x * y;

console.log(multiply1(10, 2));
console.log(multiply2(10, 3));

console.log(multiply1(true, 1)); 
// error TS2345: Argument of type 'true' is not assignable to parameter of type 
// 'number'.
```

TypeScript is superset \(upper extension\) of ES5, ES6, so JavaScript type can be used as it is. In addition to JavaScript types, TypeScript-specific types are also provided.

| Type | JS | TS |
| :--- | :--- | :--- |
| boolean | ◯ | ◯ |
| null | ◯ | ◯ |
| undefined | ◯ | ◯ |
| number | ◯ | ◯ |
| string | ◯ | ◯ |
| symbol | ◯ | ◯ |
| object | ◯ | ◯ |
| array |  | ◯ |
| tuple |  | ◯ |
| enum |  | ◯ |
| any |  | ◯ |
| void |  | ◯ |
| never |  | ◯ |



#### Here's how to pre-declare various types:

```typescript
// boolean
let isDone: boolean = false;

// null
let n: null = null;

// undefined
let u: undefined = undefined;

// number
let decimal: number = 6;
let hex: number = 0xf00d;
let binary: number = 0b1010;
let octal: number = 0o744;

// string
let color: string = "blue";
color = 'red';
let myName: string = `Lee`;
let greeting: string = `Hello, my name is ${ myName }.`;

// object
const obj: object = {};

// array
let list1: any[] = [1, 'two', true];
let list2: number[] = [1, 2, 3];
let list3: Array<number> = [1, 2, 3];

// tuple
let tuple: [string, number];
tuple = ['hello', 10]; // OK
tuple = [10, 'hello']; // Error
tuple = ['hello', 10, 'world', 100]; // Error
tuple.push(true); // Error

// enum
enum Color1 {Red, Green, Blue};
let c1: Color1 = Color1.Green;

console.log(c1); // 1

enum Color2 {Red = 1, Green, Blue};
let c2: Color2 = Color2.Green;

console.log(c2); // 2

enum Color3 {Red = 1, Green = 2, Blue = 4};
let c3: Color3 = Color3.Blue;

console.log(c3); // 4

/*
any: Used for variables that can not be type inference 
     or do not require type checking.
     You can assign any type of value, 
     such as a variable declared with the var keyword.
*/
let notSure: any = 4;
notSure = 'maybe a string instead';
notSure = false; // okay, definitely a boolean

// void : Generally used when there is no return value in function.
function warnUser(): void {
  console.log("This is my warning message");
}

// never : A value that never occurs
function infiniteLoop(): never {
  while (true) {}
}

function error(message: string): never {
  throw new Error(message);
}
```

The type is case-sensitive, so you need to be careful. As we have seen above, TypeScript's built-in types are all lowercase.

```typescript
// string
let primiteveStr: string;
primiteveStr = 'hello'; // OK
primiteveStr = new String('hello'); // Error
/*
Type 'String' is not assignable to type 'string'.
'string' is a primitive, but 'String' is a wrapper object. 
Prefer using 'string' when possible.
*/

// String
let objectStr: String;
objectStr = 'hello'; // OK
objectStr = new String('hello'); // OK
```



### Static Typing

C-family languages such as C and Java should declare the type explicitly according to the type of the value to be assigned to the variable when declaring the variable \(Type declaration\) and assign a value according to the declared type. This is called static typing.

JavaScript is either a dynamic typed language or a loosely typed language. This means that Type Inference will be dynamically inferred during the assignment of values without variable type declaration. The dynamic type language can be used to assign different types of values to the same variable even after the type of the variable is determined by type inference. This is called dynamic typing.

```javascript
//JavaScript
var foo;

console.log(typeof foo);  // undefined

foo = null;
console.log(typeof foo);  // object

foo = {};
console.log(typeof foo);  // object

foo = 3;
console.log(typeof foo);  // number

foo = 3.14;
console.log(typeof foo);  // number

foo = "Hi there";
console.log(typeof foo);  // string

foo = true;
console.log(typeof foo);  // boolean
```

The most unique feature of TypeScript is that it supports static typing. A static type language explicitly declares a type, and cannot change its type once it has been determined. If a value of the wrong type is assigned or returned, the compiler detects it and raises an error.

```typescript
let foo: string,
    bar: number,
    baz: boolean; 

foo = 'Hello';
bar = 123;
baz = 'true'; // error: Type '"true"' is not assignable to type 'boolean'.

function add(x: number, y: number): number {
  return x + y;
}

console.log(add(10, 10)); // 20
console.log(add('10', '10'));
// error TS2345: Argument of type '"10"' is not assignable 
// to parameter of type 'number'.
```

The advantage of static typing is that it improves code readability, predictability, and stability, which is well suited for large-scale projects.



### Type Inference

If the type declaration is omitted, the type is dynamically determined during the assignment of the value. This is called type inference.

```typescript
let foo = 123; // foo is number type
```

In the above code, the type is not declared in the variable foo, but the type of the variable is determined by type inference. The dynamic type language can be used to assign different types of values to the same variable even after the type of the variable is determined by type inference. However, a static type language cannot change its type after its type has been determined. Since TypeScript is a static type language, assigning a value of another type to an error occurs after the type is determined by type inference.

```typescript
let foo = 123; // foo is number type
foo = 'hi';    // error: Type '"hi"' is not assignable to type 'number'.
```

If the type declaration is omitted and a value is not assigned, and the type cannot be inferred, it becomes an `any` type. A variable of `any` type can be reassigned to any type of variable, such as a variable declared with the `var` keyword in JavaScript. It is better not to use it because it eliminates the advantage of using TypeScript.

```typescript
let foo; // Same as -> let foo: any

foo = 'Hello';
console.log(typeof foo); // string

foo = true;
console.log(typeof foo); // boolean
```

