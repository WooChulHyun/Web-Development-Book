# Variable

## Variable

A variable is the name of a memory space or the memory space itself in which a value can be stored.

> Variable means anything that can vary. JavaScript includes variables which hold the data value and it can be changed anytime. JavaScript uses reserved keyword var to declare a variable. A variable must have a unique name. _\(JavaScript Variables - Tutorials Teacher\)_



## Variable Declaration

Variable declaration means registering a variable name \(identifier\) to let the JavaScript engine know the existence of a variable and manage it.

> Identifier: Variable names are also called identifiers. An identifier is a unique name that can be used to identify and distinguish certain values. Just as you distinguish a person by a unique name, the value can be referenced by a variable name that is a unique identifier specified in a language that a person can understand. The term identifier is not only used for variables. For example, the names of variables, functions, and classes are all identifiers because they are names that can distinguish between values. Therefore, an identifier is a higher concept than a variable name. All identifiers, such as names of variables, functions, classes, etc., signal the presence of an identifier to the JavaScript engine by a "declaration".

```javascript
var a;
var b, c;
```

After declaring a variable, We have not yet assigned a value to the variable. Therefore, the memory space allocated by the variable declaration may be considered to be empty, but the allocated memory space is implicitly allocated with the value undefined by the JavaScript engine. This is a unique feature of JavaScript.

```javascript
var a;
console.log(a); // --> undefined
```

The JavaScript engine performs variable declarations in two steps:

1. Declaration phase: Register a variable name to inform the JavaScript engine of the existence of a variable.
2. Initialization phase: Allocate memory space to store the value and implicitly assigns undefined.

If you do not go through the initialization phase, the reserved memory space may still contain values that were previously used by other applications. These values are called garbage values. Therefore, garbage value can be obtained by referring to a variable value immediately after allocating memory space and not allocating a value.



## Declaration / Definition

A definition is a definition of a variable by assigning a value to it. In other programming languages, strictly separate declarations and definitions.

In C the declaration is to inform the existence of the identifier, and the definition is to clarify the identity of the identifier by assigning a value to the identifier.

Variables in JavaScript are defined as undefined at the same time as declaration, so the distinction between declaration and definition is ambiguous. Therefore, JavaScript tends to use declarations and definitions in combination.

```javascript
var a = 1; // Declare a variable a and define a as 1
var b; // Declare the variable b. But internally b is defined as undefined.
b = 1; // The variable b is defined as 1
```



## Difference between declaring var inside window and not declaring.

```javascript
console.log(a); // --> ReferenceError: a is not defined
```

```javascript
var a = 1;
console.log(a); // --> 1
```

```javascript
a = 1;
console.log(a); // --> 1
```

The result is the same in here, but if you do not declare a variable, the JavaScript engine will automatically declare it as a variable\(global variable\).

Global variables and local variables have different scope ranges, so if you use them without declaring variables, they can cause bugs later on.



## Hoisting \(Variable declaration hoisting\)

Variable hoisting is a unique feature of JavaScript that behaves as if the variable declaration is pulled to the beginning of the code.

Programs are executed in order from the top to the bottom.

```javascript
console.log(a); // undefined
var a = 1;
console.log(a); // --> 1
```

The variable a is not declared yet on the first line, so ReferenceError is likely to occur, but undefined is output.

This is because even if you declare a variable in the middle of a program, the variable is created before another statement as declared at the beginning of the program. This is hoisting.

Before I show you an example, let's take a look at the way the JavaScript engine works.

When we type `var a = 1;`, JavaScript engine interpret as:

```javascript
var a;
a = 1;
```

Come back to hoisting again,

===&gt; Your code

```javascript
console.log(a); // undefined
var a = 1; // Same as `var a;` `a = 1;`
console.log(a); // --> 1
```

===&gt; JavaScript engine works

```javascript
var a;
console.log(a); // undefined
a = 1;
console.log(a); // --> 1
```

Variable declarations are executed first in parsing-time\(before run-time\), not at the run-time. That is, the JavaScript engine evaluates the entire code before executing the source code line by line. At this time, all declarations \(variable declaration statements, function declaration statements, etc.\) are found, and identifiers are registered and initialized. Then, run the source code one line at a time, except the declaration.



## Identifier Naming

Identifiers must follow these naming conventions:

1. The available characters are alphabet\(a to z, A to Z\), numbers \(0 to 9\), underscore \(\_\), dollar sign \($\)
2. Numbers are not allowed in the first letter. That is, the first letter must be one of the following: an alphabet\(a to z, A to Z\), underscore \(\_\), dollar sign \($\)
3. Reserved words can not be used as identifiers.

Reserved words:

|  |  |  |  |
| :--- | :--- | :--- | :--- |
| arguments | Array | await | Boolean |
| break | case | catch | class |
| const | continue | Date | decodeURI |
| decodeURIComponent | debugger | default | delete |
| do | else | encodeURI | encodeURIComponent |
| enum | Error | eval | EvalError |
| export | extents | false | finally |
| for | function | Function | if |
| Implements | import | in | Infinity |
| isFinite | isNaN | instanceof | interface |
| JSON | Math | NaN | new |
| null | Number | Object | package |
| parseFloat | ParseInt | protected | private |
| public | RangeError | RefferenceError | RegExp |
| return | string | super | switch |
| syntaxError | this | throw | true |
| try | TypeError | typeof | undefined |
| URIError | var | void | while |
| with | yield |  |  |

* camelCase \(lower camel case\)

Capitalize the first letter of the word after the second, and the rest in lower case.

Ex\) camelCase, newName   
   


* PascalCase \(upper camel case\)

The first letter of each word is capitalized and the rest are in lower case.

Ex\) PascalCase, NewName   
   


* Underscore \(snake case\)

All words are in lower case, and words and words are separated by Underscore\(\_\).

Ex\) new\_name

