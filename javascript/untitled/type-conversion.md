# Type Conversion

## Type Conversion

All values in JavaScript have types. The type of the value can be converted to another type by the developer's intention. A developer's intentional conversion of value types is called explicit coercion or type casting.

JavaScript, a dynamic type language, is automatically implicitly converted by the JavaScript engine regardless of the developer's intent. This is called implicit coercion or type coercion.

#### 

## Explicit coercion / Type casting

There are a variety of ways to explicitly change types by developer intent. Using wrapper object\(String, Number, Boolean\) without the new operator, built-in methods provided by JavaScript, and implicit type conversion.

\*\*\*\*

### **Convert to string type**

To convert a non-string value to a string type:

* call the String constructor function without the new operator
* use the Object.prototype.toString method
* use string concatenation operators

```javascript
// 1. call the String constructor function without the new operator
console.log(String(1)); // "1"
console.log(String(NaN)); // "NaN"
console.log(String(Infinity)); // "Infinity"

console.log(String(true)); // "true"
console.log(String(false)); // "false"

// 2. use the Object.prototype.toString method
console.log((1).toString()); // "1"
console.log(NaN.toString()); // "NaN"
console.log(Infinity.toString()); // "Infinity"

console.log(true.toString()); // "true"
console.log(false.toString()); // "false"

// 3. use string concatenation operators
console.log(1 + ''); // "1"
console.log(NaN + ''); // "NaN"
console.log(Infinity + ''); // "Infinity"

console.log(true + ''); // "true"
console.log(false + ''); // "false"
```

\*\*\*\*

### **Convert to number type**

To convert a non-numeric value to a numeric type:

* call the Number constructor function without the new operator
* use the parseInt or parseFloat functions \(only strings can be converted\)
* + use unary concatenation operator
* \* use arithmetic operators

```javascript
// 1. call the Number constructor function without the new operator
console.log(Number('0')); // 0
console.log(Number('-1')); // -1
console.log(Number('10.53')); // 10.53

console.log(Number(true)); // 1
console.log(Number(false)); // 0

// 2. use the parseInt or parseFloat functions (only strings can be converted)
console.log(parseInt('0')); // 0
console.log(parseInt('-1')); // -1
console.log(parseFloat('10.53')); // 10.53

// + use unary concatenation operator
console.log(+'0'); // 0
console.log(+'-1'); // -1
console.log(+'10.53'); // 10.53

console.log(+true); // 1
console.log(+false); // 0

// 4. * use arithmetic operators
console.log('0' * 1); // 0
console.log('-1' * 1); // -1
console.log('10.53' * 1); // 10.53

console.log(true * 1); // 1
console.log(false * 1); // 0
```

\*\*\*\*

### **Convert to boolean type**

To convert a non-Boolean type to a Boolean type:

* call the Boolean constructor function without the new operator
* ! use negative logical operators twice

```javascript
// 1. call the Boolean constructor function without the new operator
console.log(Boolean('x')); // true
console.log(Boolean('')); // false
console.log(Boolean('false')); // true

console.log(Boolean(0)); // false
console.log(Boolean(1)); // true
console.log(Boolean(NaN)); // false
console.log(Boolean(Infinity)); // true

console.log(Boolean(null)); // false

console.log(Boolean(undefined)); // false

console.log(Boolean({})); // true
console.log(Boolean([])); // true

// 2. ! use negative logical operators twice
console.log(!!'x'); // true
console.log(!!''); // false
console.log(!!'false'); // true

console.log(!!0); // false
console.log(!!1); // true
console.log(!!NaN); // false
console.log(!!Infinity); // true

console.log(!!null); // false

console.log(!!undefined); // false

console.log(!!{}); // true
console.log(!![]); // true
```

#### 

## Implicit coercion / Type coercion

The JavaScript engine performs implicit type conversion when evaluating expressions, taking into account the context of the code.

When an implicit type conversion occurs, the type is automatically converted to one of the primitive types such as string, number, or boolean

\*\*\*\*

### **Convert to string type**

```javascript
0 + ''              // "0"
-0 + ''             // "0"
1 + ''              // "1"
-1 + ''             // "-1"
NaN + ''            // "NaN"
Infinity + ''       // "Infinity"
-Infinity + ''      // "-Infinity"

true + ''           // "true"
false + ''          // "false"

null + ''           // "null"

undefined + ''      // "undefined"

(Symbol()) + ''     // TypeError: Cannot convert a Symbol value to a string

({}) + ''           // "[object Object]"
Math + ''           // "[object Math]"
[] + ''             // ""
[10, 20] + ''       // "10,20"
(function(){}) + '' // "function(){}"
Array + ''          // "function Array() { [native code] }"
```

\*\*\*\*

### **Convert to number type**

```javascript
+'' + // 0
+'0' + // 0
+'1' + // 1
+'string' + // NaN
//
+true + // 1
+false + // 0
//
+null + // 0
//
+undefined + // NaN
//
Symbol() + // TypeError: Cannot convert a Symbol value to a number
//
+{} + // NaN
+[] + // 0
+[10, 20] + // NaN
```

\*\*\*\*

### **Convert to boolean type**

The JavaScript engine distinguishes values that are not Boolean types from Truthy values \(true values\) or Falsy values \(false values\). That is, the Truthy value is converted to true and the Falsy value is converted to false.

The values below are Falsy values that evaluate to false in the context that should be evaluated as a Boolean value as the conditional expression of the control statement.

* false
* undefined
* null
* 0, -0
* NaN
* '' \(Empty string\)

```javascript
// Returns true if the given argument is a False value,
// false if it is a Truthy value.
function isFalsy(v) {
  return !v;
}

// Returns true if the given argument is a Truthy value,
// false if it is a Falsy value.
function isTruthy(v) {
  return !!v;
}

// All return true.
console.log(isFalsy(false));
console.log(isFalsy(undefined));
console.log(isFalsy(null));
console.log(isFalsy(0));
console.log(isFalsy(NaN));
console.log(isFalsy(''));

// All return true.
console.log(isTruthy(true));
console.log(isTruthy('0'));
console.log(isTruthy({}));
console.log(isTruthy([]));

```

