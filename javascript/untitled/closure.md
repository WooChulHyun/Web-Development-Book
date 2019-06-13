# Closure

### Internal slot of function object \[\[Environment\]\]

The function definition is evaluated to create a function object. At this time, the created function object stores the upper scope determined by the position where it is defined. In other words, every function object stores a reference to its upper scope in its internal slot \[\[Environment\]\]. At this time, the reference of the stored upper scope indicates the lexical environment of the currently running execution context.

For example, defined function declaration in global environment is evaluated at the time the global code is evaluated to create a function object. The internal slot \[\[Environment\]\] of the created function object stores a reference to the global lexical environment, which is the lexical environment of the running execution context at the time when the function definition is evaluated, that is, the global code evaluation point.

A function declaration defined inside a function is evaluated at the time the outer function code is evaluated to create a function object. In this case, the internal slot \[\[Environment\]\] of the created function object stores the reference of the outer function lexical environment, which is the lexical environment of the running execution context at the time of evaluation of the function definition, that is, outer function lexical environment

The reference to the lexical environment of the currently running execution context stored in the internal slot \[\[Environment\]\] of the function object is the one level up scope. It is also the reference value to be stored in the "reference to the outer lexical environment" of the lexical environment to be created when it is called. The function object stores the reference of the lexical environment stored in the internal slot \[\[Environment\]\], that is, the upper scope as long as it exists.



### Lexical scope

```javascript
const x = 1;

function foo() {
  const x = 10;

  bar();
}

function bar() {
  console.log(x);
}

foo(); // 1
bar(); // 1
```

![](https://i.postimg.cc/7Z13NcK5/Closure1.png)

Both functions foo and bar are defined with function declarations in global environment. So both functions foo and bar are evaluated at the time global code is evaluated to create a function object and become a property of the global object window. The internal slot \[\[Environment\]\] of the created function object stores a reference to the global lexical environment, which is the lexical environment of the running execution context at the time when the function definition is evaluated, that is, the global code evaluation point.

At this time, the reference to the outer lexical environment, which is a component of the function lexical environment, is assigned to the reference of the lexical environment stored in the internal slot \[\[Environment\]\] of the function object. In other words, the reference to the lexical environment stored in the internal slot \[\[Environment\]\] of the function object is the upper scope of the function. This is the entity of the lexical scope that determines the upper scope according to the position of the function definition.



### Closure and lexical environment

```javascript
const x = 1;

// ①
function outer() {
  const x = 10;
  const inner = function () { console.log(x); }; // ②
  return inner;
}

const innerFunc = outer(); // ③
innerFunc(); // ④ 10
```

All functions in JavaScript remember their upper scopes. The upper scope that all functions remember is maintained no matter where you call the function. Therefore, regardless of where you call the function, the function can always refer to the variable of the upper scope that it memorizes and can change the variable value of the upper scope.

In the above example, the inner function stores the upper scope determined by its defined position in the internal slot \[\[Environment\]\] when it is evaluated. At this time, the stored upper scope is maintained as long as the inner function exists.

In the above example, when the outer function is evaluated and a function object is created \(①\), the lexical environment of the currently running execution context, that is, the global lexical environment, is stored as a upper scope in the internal slot \[\[Environment\]\] of the outer function object .

![](https://i.postimg.cc/BZNvwGF8/Closure2.png)

When the outer function is called, the lexical environment of the outer function is created, and the global lexical environment previously stored in the internal slot \[\[Environment\]\] of the outer function object is assigned to the "outer lexical environment reference" of the outer function lexical environment.

And the nested inner function is evaluated\(② The inner function is evaluated at runtime because it is defined as a function expression.\). At this time, the internal slot \[\[Environment\]\] of nested inner function stores the lexical environment of the currently running execution context, that is, the lexical environment of the outer function, as the upper scope.

![](https://i.postimg.cc/wMfwkrFK/Closure3.png)

When the execution of the outer function ends, the inner function is returned, and the life cycle of the outer function is terminated\(③\). That is, the execution context of the outer function is popped from the execution context stack. At this point, the execution context of the outer function is popped from the execution context stack, but lexical environment of the outer function is not going to be popped. This is because the lexical environment of the outer function is referenced by the internal slot \[\[Environment\]\] of the inner function and is therefore not subject to garbage collection.

![](https://i.postimg.cc/RVcrc7ng/Closure4.png)

When the inner function returned by the outer function is called \(④\), the execution context of the inner function is created and pushed to the execution context stack. The reference to the outer lexical environment of the lexical environment is assigned a reference value stored in the internal slot \[\[Environment\]\] of the inner function object.

![](https://i.postimg.cc/g0bH3h8H/Closure5.png)

The nested inner function survived longer than the outer function. At this time, the inner function stores the upper scope determined by the position where the inner function is defined, regardless of whether the outer function is viable \(whether the execution context is viable\) or not.

The nested inner function can refer to the upper scope, so you inner function can refer to the identifier of the upper scope and change the value of the identifier.



###  

