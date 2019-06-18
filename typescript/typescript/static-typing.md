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



