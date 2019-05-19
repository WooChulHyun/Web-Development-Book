# this

## this

The 'this' value is determined when the function is called and executed. This 'this' value is 'a reference to the object to which the function belongs when the function is called' and is the object referenced by the 'this binding' component of the execution context.

```javascript
const circle = {
  radius: '5',
  area() {
        return Math.PI * this.radius * this.radius;
    }
};

console.log(circle.area()); // 78.53981633974483
```

In this code, we refer to the function as circle.area and execute it. The object to which circle.area belongs is circle. That is, the object pointed to by the 'this binding' component in the execution context in which the area method is called is circle. Therefore, the 'this' value points to circle, so the value of this.radius is '5'. The circle.area value is a reference to the function. Therefore, you can assign this value to a property of another object.

```javascript
const circle = {
  radius: '5',
  area() {
    return Math.PI * this.radius * this.radius;
  }
};

console.log(circle.area()); // 78.53981633974483

const circle2 = { radius: 10 };
circle2.area = circle.area;

console.log(circle2.area()); // 314.1592653589793
```

JavaScript functions are not tied to specific objects. Typically, several objects point to a function. Therefore, the object pointed to by 'this' will change depending on the state of the call. That is, the value pointed by 'this' is dynamically determined by the function call method.



## 5 Patters of Binding 'this'

#### 1. Global Reference

#### 2. Free Function Invocation

#### 3. .call or /apply Invocation

#### 4. Construction Mode

#### 5. Method Invocation

![](https://i.postimg.cc/k56q29YR/this1.png)

### 1. Global Reference // 2. Free Function Invocation

The methods 1 and 2 are the same.

The 'this' in the top-level code points to the global object. When the execution context is initialized, the 'this binding' component inside it is initialized to point to the global environment.

```javascript
console.log(this) // window
```

```javascript
var test = 123
test === window.test // true
```

![](https://i.postimg.cc/NjJrh1z8/this2.png)

```javascript
var name = 'Global variable';

function foo() {
  console.log(this.name);
}

foo(); // Global variable
```

In the above code, 'this' is window and foo \(\) is a function Invocation.

```javascript
var name = 'Global variable';

function outer() {
    function inner() {
        console.log(this.name);
    }
    inner()
}

outer(); // Global variable
```

As in the above example, if you invoke a nested function as well as a Generalized Functions, the global object is bound to 'this' in the nested function.

```javascript
var name = 'Global variable';

function outer() {
  let closure = function () {
    console.log(this.name);
  };
  return closure;
}

outer()(); // Global variable
```



Even if the nested function defined in the method is called as a Generalized Functions, the global object is bound to 'this' in the nested function.

```javascript
var name = 'Global variable';

const obj = {
  name: 'local variable',
  foo() {
    console.log("foo's this: ", this);  // {name: local variable, foo: ƒ}
    console.log("foo's this.value: ", this.name); // local variable

    function bar() {
      console.log("bar's this: ", this); // window
      console.log("bar's this.value: ", this.name); // Global variable
    }
    bar();
  }
};

obj.foo();
```

The global object is also bound to 'this' in the callback function. When any function is called as a Generalized Functions, the global object is bound to this.

```javascript
var name = 'Global variable';

const obj = {
  name: 'local variable',
  foo() {
    console.log("foo's this: ", this); // {name: local variable, foo: ƒ}
    setTimeout(function () {
      console.log("callback's this: ", this); // window
      console.log("callback's this.value: ", this.name); // Global variable
    }, 5000);
  }
};

obj.foo();
```

However, it is problematic that the 'this' of the nested function defined in the method or the callback function \(auxiliary function\) passed to the method binds the global object. A nested function or callback function acts as a helper function to help an external function, so it is often the case that it replaces some logic of an external function. However, the mismatch between 'this' in external function\(method, in above\) and 'this' in the nested function\(callback, in above\) makes it difficult to work with nested functions or callback functions as helper functions.

Here's how to make 'this binding' of a nested function or callback function inside a method match the 'this binding' of a method.

```javascript
var name = 'Global variable';

const obj = {
  name: 'local variable',
  foo() {
    const that = this;

    setTimeout(function () {
      console.log(that.name); // local variable
    }, 5000);
  }
};

obj.foo();
```

 

### 3. .call or /apply Invocation

The first argument to .call or .apply



