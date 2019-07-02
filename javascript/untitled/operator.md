# Operator

## Operator

An operator creates one value by performing arithmetic, assignment, comparison, logic, and type operations on one or more expressions. At this time, the object of the operation is called an operand. The operand is also an expression because it is evaluated and become a single value, and also an expression that combines the operand with the operator is expression.



## Arithmetic Operator

The Arithmetic Operator performs a mathematical computation on the operands to produce new numeric values. If arithmetic is not possible, NaN is returned.

Arithmetic operators can be classified into dyadic arithmetic operators and unary arithmetic operators according to the number of operands.



### **Dyadic arithmetic operators**

Dyadic arithmetic operators perform arithmetic operations on two operands to produce numeric type values.

All dyadic arithmetic operators have no side effects that change the value of the operand. In other words, any arithmetic operation does not change the value of the operand. It always creates new values.

| Operator | Meaning | Example |
| :--- | :--- | :--- |
| + | Plus | a + b |
| - | Subtract | a - b |
| \* | Multiply | a \* b |
| / | Division | a / b |
| % | Remainder | a % b |

A few things to keep in mind when using arithmetic dyadic operators.

* The result is a floating point even if you divide the integer.

```javascript
7 / 2; // 3.5
```

* The operand of the remaining operators\(%\) is floating point.

The sign is the same as first operand.

```javascript
15 % 4; // 3
5 % 1.5; // 0.5
```

* If one of the operands is a string, the + operator makes remaining operands to string

```javascript
1 + '2 month'; //  12 month
//Change the number 1 to the string '1' and combine it with '2 month'.
```

Others

If it can not be calculated, it is evaluated as NaN. It evaluates to 1 if the operand of the arithmetic operator is true, or to 0 if false and null. If undefined, it evaluates to NaN.

```javascript
0 / 0; // NaN
'One' * 1; // NaN
true + true; // 2
1 + null; // 1
1 + undefined; // NaN
```

\*\*\*\*

### **Unary arithmetic operator**

Unary arithmetic operators perform arithmetic operations on a single operand to produce a numeric type value. Note that unlike dyadic arithmetic operators, the increment / decrement \(++ / --\) operator has side effects that change the value of the operand. In other words, the increment / decrement operation changes the value of the operand.

| Operator | Meaning | Example | Example meaning |
| :--- | :--- | :--- | :--- |
| ++ | Increase operator | a++ | Plus 1 to a then then evaluate the value of a |
|  |  | ++a | Evaluate the value of a then plus 1 to a |
| -- | Decrease operator | a-- | Subtract 1 to a then then evaluate the value of a |
|  |  | --a | Evaluate the value of a then subtract 1 to a |
| + | Do not process anything | +a | Evaluate to the same value as a. |
| - | Sign inversion | -a | Evaluate the value after invert the sign of a |

```javascript
let x = 3;
let y;

// Postfix increment operator
y = x++;
console.log(y, x); // 3 4

// Prefix increment operator
y = ++x;
console.log(y, x); // 5 5

// Postfix decrement operator
y = x--;
console.log(y, x); // 5 4

// Prefix decrement operator
y = --x;
console.log(y, x); // 3 3
```

#### 

## Assignment Operator

| Operator | Example | Meaning |
| :--- | :--- | :--- |
| += | a += b | a = a + b |
| -= | a -= b | a = a - b |
| \*= | a \*= b | a = a \* b |
| /= | a /= b | a = a / b |
| %= | a %= b | a = a % b |

```javascript
let x;

x = 10;
console.log(x); // 10

x += 5; // x = x + 5;
console.log(x); // 15

x -= 5; // x = x - 5;
console.log(x); // 10

x *= 5; // x = x * 5;
console.log(x); // 50

x /= 5; // x = x / 5;
console.log(x); // 10

x %= 5; // x = x % 5;
console.log(x); // 0
```



## Comparison Operator

| Operator | Meaning | Example | Description |
| :--- | :--- | :--- | :--- |
| == | Loose equality | a == b | true if a and b are equal in value, false otherwise |
| != | Inequality | a != b | true if a and b are not equal in value, false otherwise |
| === | Strict equality | a === b | true if a and b are equal in value and type, false otherwise |
| !== | Strict inequality | a !== b | true if a and b are not equal in value and type, false otherwise |
| &gt; | Greater than | a &gt; b | true if a value is greater than b, false otherwise |
| &lt; | Less than | a &lt; b | true if b value is greater than a, false otherwise |
| &gt;= | Greater than or equal | a &gt;= b | true if a value is greater than or equal b, false otherwise |
| &lt;= | Less than or equal | a &lt;= b | true if b value is greater than or equal a, false otherwise |

```javascript
const a = [1, 2, 3];
const b = [1, 2, 3];
const c = a;

console.log(a == b); // false
console.log(a == c); // true
```

```javascript
undefined == null; // true
1 == '1'; // true
'oxff' == 255; // true
true == 1; // true
true == '1'; // true
```

```javascript
undefined === null; // false
1 === '1'; // false
'oxff' === 255; // false
true === 1; // false
true === '1'; // false
NaN === NaN; // false
```

#### 

## Logical Operator

| Operator | Meaning | Example | Description |
| :--- | :--- | :--- | :--- |
| && | Logical AND | a && b | true if both a and b are true, false otherwise |
| II | Logical OR | a II b | true if either a or b is true, false otherwise |
| ! | Logical NOT | !a | false if a is true, true if a is false |

```javascript
console.log(true && true); // true
console.log(true && false); // false
console.log(false && true); // false
console.log(false && false); // false

console.log(true || true); // true
console.log(true || false); // true
console.log(false || true); // true
console.log(false || false); // false

console.log(!true); // false
console.log(!false); // true
```

The operation result of the logical OR \(\|\|\) operator and logical AND \(&&\) operator may not be a Boolean value. These two operators always return one of the operands.

```javascript
true && anything; // anything
false && anything; // false

true || anything; // true
false || anything; // anything
```

```javascript
'Cat' && 'Dog'; // Dog
false && 'Dog'; // false
'Cat' && false; // false

'Cat' || 'Dog'; // 'Cat'
false || 'Dog'; // 'Dog'
'Cat' || false; // 'Cat'
```

#### 

## Other Operators

| Operator | Meaning |
| :--- | :--- |
| typeof | Check the data type |
| ?: | Conditional operator \(ternary operator\) |
| void | Returns an undefined value |
| , | Operate consecutive operands in left-to-right order |
| delete | Remove an object's properties or array elements |
| new | Create a new object |
| in | Check whether object contains property |
| instanceof | Check the type of object |
| eval\(\) | Evaluates JavaScript code represented as a string |

Actually, eval\(\) is function.

\*\*\*\*

### **typeof Operator**

```javascript
typeof ''; // "string"
typeof 1; // "number"
typeof NaN; // "number" <-- do not use(bug), use (===)
typeof true; // "boolean"
typeof undefined; // "undefined"
typeof Symbol(); // "symbol"
typeof null; // "object"
typeof []; // "object"
typeof {}; // "object"
typeof new Date(); // "object"
typeof /test/gi; // "object"
typeof function() {}; // "function"
```

\*\*\*\*

### **Ternary Operator**

\(Conditional expression\) `?` value to return when the conditional expression is true `:` alue to return when the conditional expression is false

```javascript
let number = a % 2 === 0 ? 'even' : 'odd';

// same

if (a % 2 === 0) {
  number = 'even';
} else {
  number = 'odd';
}
```

```javascript
n === undefined ? array[array.length - 1] : n === 0 ? [] : array.slice(-n);

// same

if (n === undefined) {
  return array[array.length - 1];
}
if (n === 0) {
  return [];
} else {
  return array.slice(-n);
}
```

\*\*\*\*

### **Comma operator**

The comma \(,\) operator evaluates the operands in sequence starting with the left operand and returns the result of the evaluation of the last operand after evaluation of the last operand.

```javascript
let x, y, z;
(x = 1), (y = 2), (z = 3); // 3
```

You can put only three statements in the brackets of the for statement, but in this example, using the comma operator to execute more statements.

```javascript
for (let i = 1, sum = 0; i <= 10; i++) {
  sum += i;
}
```

