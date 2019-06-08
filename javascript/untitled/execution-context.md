# Execution Context

### Execution Context

Execution context is a core concept of JavaScript that contains the principles of operation such as identifier, scope, hoisting, and closure. Understanding the execution context correctly can help you understand how JavaScript manages the  identifiers and values bound to identifiers based on scope, why hoisting occurs, and how closures work.



### Executable Code

When the JavaScript engine encounters executable code, it evaluates the code and makes it the execution context. The types of executable code are:

| \*\*\*\* | \*\*\*\* |
| :--- | :--- |
| **Global code** | A global text code such as globally defined functions and classes but it does not include internal code of it. |
| **Function code** | Text code inside the function. It does not include internal code such as nested functions , classes, etc. in that function. |
| **Eval code** | It is the text code passed as an argument to the eval function which is built-in global function. |
| **Module code** | The text code inside the module. It does not include internal code such as functions , classes, etc. in that module. |

The reason for separating executable code into four types is that the process of creating an execution context \(initialization environment\) and management contents are different.

**Global code:** The global code must create a global scope and be associated with a global object. To do this, a global execution context is created when the global code is evaluated.

**Function code:** The function code must create a local scope and the created local scope must be connected to a member of the scope chain starting from the global scope, which is the top of the scope chain. To do this, the function execution context is created when the function code is evaluated.

**eval code:** The eval code creates its own unique scope in strict mode. To do this, the eval execution context is created when the eval code is evaluated.

**Module code:** The module code creates an independent scope for each module. To do this, the module execution context is created when the module code is evaluated.

![](https://i.postimg.cc/k4XJCxSG/execution-context1.png)



### Execution Context Structure

An execution context is an area in which executable code is actually executed and managed. It is made up of a number of components that manage all the information necessary for execution.

The main components are the LexicalEnvironment component, the VariableEnvironment component, and the ThisBinding component.

The code below is pseudo-code, so that cannot be executed, just for understanding.

```javascript
ExecutionContext = {
    LexicalEnvironment: {},
    VariableEnvironment: {},
    ThisBinding: null
}
```

![](https://i.postimg.cc/kg0S9Nx7/execution-context2.png)



#### LexicalEnvironment component

{% hint style="info" %}
**LexicalEnvironment and VariableEnvironment components** 

The LexicalEnvironment and VariableEnvironment components always refer to the same lexical environment, except for the special case with the 'with statement'. Therefore, in here, we will unify the two components into a lexical environment without distinction. When using the 'with statement', the LexicalEnvironment component binds the new lexical environment. The VariableEnvironment component is used to back to the original lexical environment after change the lexical environment. The 'with statement' is an disrecommend syntax like the eval function.
{% endhint %}

 

#### ThisBinding component

ThisBinding component is the place where reference to the object that called the function are stored. The value pointed by ThisBinding will be 'this' in the execution context.



### LexicalEnvironment component Structure

A lexical environment is an environment in which an identifier is declared. That is, it means a lexical scope. If the execution context stack manages the execution order of the code, the lexical environment manages the scope and the identifier. The lexical environment creates an object-like scope \(global, function, block scope\) and registers an identifier here. And manages the values bound to the registered identifiers. In other words, the lexical environment serves as a repository for registering and managing identifiers by separating the scope.

```javascript
ExecutionContext = {
    LexicalEnvironment: {
        EnvironmentRecord: {},
        OuterLexicalEnvironment Reference: {}
    },
    VariableEnvironment: {},
    ThisBinding: null
}
```

![](https://i.postimg.cc/0jkWn1QX/execution-context3.png)

**Environment Record:** It is a repository that registers the identifier included in the scope and manages the value bound to the registered identifier. Environmental records differ in content depending on the type of executable code.

**OuterLexicalEnvironment Reference:** Stores a reference to an external lexical environment. The external lexical environment is the lexical environment of the parent code that contains the executable code that created the execution context. This implements a scope chain, which is a Singly linked list.



### EnvironmentRecord Structure



```javascript
ExecutionContext = {
    LexicalEnvironment: {
        EnvironmentRecord: {
            DeclarativeEnvironmentRecord: {},
            ObjectEnvironmentRecord: {}
        },
        OuterLexicalEnvironment Reference: {}
    },
    VariableEnvironment: {},
    ThisBinding: null
}
```

![](https://i.postimg.cc/vZjxQ7w0/execution-context4.png)

**DeclarativeEnvironmentRecord:** It is the place where execution result of the functions, variables and catch statement are stored.

**ObjectEnvironmentRecord:** While a DeclarativeEnvironmentRecord manages a identifier and its execution result as a key / value pair, the ObjectEnvironmentRecord reads or writes data from a reference to an object stored separately outside the execution context.

That is, a data stored in a separate object, such as a lexical environment or a global object with a 'with statement', does not copy the key / value pair of the object, but takes a reference to the entire object and binds it to a property called bindingObject.

Generally only created in the global environment record.



### Creation of global environment and global objects

The JavaScript interpreter creates a global environment which is the lexical environment type as soon as it starts. The built-in JavaScript interpreter in the web browser creates a global environment when the new web pages is loaded. Then creates a global object and assigns a reference to the global object to the object environment record in the global environment.

```javascript
ExecutionContext = {
    LexicalEnvironment: {
        EnvironmentRecord: {
            DeclarativeEnvironmentRecord: {},
            ObjectEnvironmentRecord: {
                bindingObject: window
            }
        },
        OuterLexicalEnvironment Reference: null
    },
    VariableEnvironment: {},
    ThisBinding: window
}
```

![](https://i.postimg.cc/5t4JwKM8/execution-context5.png)

Because the window object is a global object in the web browser's JavaScript execution environment, the bindingObject property of the object environment record is assigned a reference to the global object window \(In node.js, bindingObject property of the object environment record will be 'global'\). This causes the variables in the global environment \(var // not let, const\) and functions \(function declaration\) to be searched in the window. Also, since there is no other lexical environment outside the global environment,  assign null to the outer lexical environment reference.This binding component in the global execution context is also assigned a reference to the window, so 'this' in the global execution context points to the window, and the properties of the global execution context are searched in this binding component.



### Evaluation of Program and Global Variables

After creating the global environment and global objects, it loads the JavaScript program. After the JavaScript program is loaded, the program is evaluated, and the global variable created at the top level with the var statement is added as a property of the environment record \(object environment record\) of the global environment.

The property name become the identifier name and the property value become undefined. Function, the function declaration created at the top level is created as a function object and recorded as a property in the environment record \(object environment record\) of the global environment.

![](https://i.postimg.cc/g22F61hg/execution-context6.png)

In other words, the entity of a global variable is a property of the environment record \(object environment record\) contained in the global object's property or in the execution context of the global object. Similarly, references to local variables and nested functions declared in functions are also properties of the environment record \(declarative environment record\) of the execution environment to which the function belongs.

{% hint style="info" %}
Unlike the diagrams described in Variable and Memory Structure page, variable, function, etc. are actually not stored directly in memory, stored as properties of the environment record \(object environment record or declarative environment record\) of the execution environment.
{% endhint %}

Functions and variables declared at the top level are already added to the object environment record in the phase of evaluating the program, so the entire program can refer to it anywhere in the code. This is the reality of the **hoisting** phenomenon.



### Execution Context Stack

After the program is evaluated, the program is executed, and the program is executed within the execution context. As mentioned earlier, execution contexts are created for each executable code\(global code, function code, eval code, module code\).

Execution contexts are managed in a structure called a stack. The stack is managed by last-in-first-out \(LIFO\). Pushing the data at the top of the stack is called push, and popping the data at the top of the stack is called pop.The execution context is pushed onto the stack and executed during program execution. The code that first to executed is the global code, so the bottom of the stack always has an execution context for executing global code. When a function is executed in global code, it pushes the execution context to execute the function on the stack. Then, when the function is finished and the control returns to the part where the function was called, it pops from the stack.If the executing function is a nested function defined inside a certain function, it creates a new execution context of the nested function and pushes it to the stack. The execution context of the nested function is not nested within the execution context of the external function\(recursive function is also same\).

Nested functions and recursive functions are pushed onto the stack as totally different functions. As such, the execution context of the function is pushed onto the stack each time it is called. And when the return statement is executed and control returns to the calling code, it pops from the stack. For this reason, the execution context stack is called the **call stack**.

```javascript
const x = 1;

function foo () {
  const y = 2;

  function bar () {
    const z = 3;
    console.log(x + y + z);
  }
  bar();
}

foo(); // 6
```

![](https://i.postimg.cc/3NStPr86/execution-context7.png)



## Process of creating the execution context and searching the identifier

```javascript
var x = 1;
const y = 2;

function foo (a) {
  var x = 3;
  const y = 4;

  function bar (b) {
    const z = 5;
    console.log(a + b + x + y + z);
}
  bar(10);
}

foo(20); // 42
```



### Create global object

Global objects are created before the global code is evaluated. At this time, global properties, global functions, and built-in objects are added to the global objects, and add client side Web API \(DOM, BOM, Canvas, XMLHttpRequest, Fetch, requestAnimationFrame, SVG, Web Storage, Web Component , Web worker, etc.\) or an API for a specific environment depending on the operating environment \(client side or server side\).

Global objects also inherit from Object.prototype. That is, the global object is also a member of the prototype chain.



![](https://i.postimg.cc/7LPRYVsR/execution-context8.png)



### Evaluating Global code

When the source code is loaded, the JavaScript engine evaluates the global code. The global code evaluation proceeds in the following order.

1. Create a global execution context
2. Create a global lexical environment

   2.1. Create global environment record

     2.1.1. Create object environment records

     2.1.2. Create declarative environment record

   2.2. Assign a reference to an outer lexical environment

   2.3. this binding



![](https://i.postimg.cc/pX5KHk4Q/execution-context9.png)

{% hint style="info" %}
The &lt;uninitialized&gt; in the above figure is the expression used to indicate that the initialization is not performed and can not be accessed. In fact, the value of &lt;uninitialized&gt;  is not bound.
{% endhint %}



\*\*\*\*

#### Create a global execution context

First, create a global execution context. And pushes the created global execution context to the execution context stack. At this time, the global execution context is the top of the execution context stack, that is, the running execution context.

![](https://i.postimg.cc/5y69VYRj/execution-context10.png)

####  

#### Create a global lexical environment

Create a global lexical environment and bind it to the LexicalEnvironment and VariableEnvironment components in the global execution context.

![](https://i.postimg.cc/JzyTk19J/execution-context11.png)



#### Create global environment record

The Global Environment Record, which is one of the components of the global lexical environment, consists of an Object Environment Record and a Declarative Environment Record. Object environment records and declarative environment records cooperate to manage global scopes and global objects.



![](https://i.postimg.cc/9F2w6VP2/execution-context12.png)



#### Create object environment records

Global variables declared with the var keyword and global functions defined with the function declaration are registered and managed in the object environment record.

The object environment record is associated with an object called bindingObject. The identifier registered in the object environment record is a property of bindingObject. If an identifier is retrieved from the object environment record, the property of the bindingObject is retrieved and returned.

The bindingObject which is bound to the object environment record of the global environment record is a global object\(in web browser, window // in node.js, global\). Therefore, the identifier registered in the object environment record of the global environment record, that is, the global variable declared with the var keyword, and the function defined by the function declaration are properties of the global object. At this time, if the registered identifier is retrieved from the object environment record of the global environment record, the property of the global object is retrieved and returned.

This is the mechanism by which the global variable defined by the var keyword and the global function defined by the function declaration become the property and method of the global object and can refer to the property of the global object without the global object's window. \(for example, window.alert is referred to as alert\)

The global variable x and the global function foo in the above example are properties and methods of the global object that are registered in the object environment record and bound to the bindingObject of the object environment record.

![](https://i.postimg.cc/wTb9d8nM/execution-context13.png)



#### Create declarative environment record

Declaration other then global variables declared with the var keyword and global functions declared by the function declaration, that is, global variables declared with the let and const keywords \(including function expressions assigned to variables declared with the let and const keywords\) are registered and managed in the declarative environment record.

The variable y is a variable declared with the const keyword. Therefore, the "declaration phase" and "initialization phase" proceed separately. Thus, the initialization phase, that is, before the variable assignment is executed, it falls into the Temporal Dead Dead \(TDZ\).

Variables declared with the let and const keywords also have variable hoisting. However, variables declared with the let and const keywords cannot be referenced because they fall into a temporary Dead Dead until the variable assignment statement is executed.

The global variable declared with the var keyword is a property of the global object. However, the global variables declared with the let and const keywords are not managed as properties of the global object but are managed separately in the declarative environment record of the global lexical environment. Therefore, a global variable declared with the let and const keywords is not a property of the global object.

![](https://i.postimg.cc/MTVK5PG5/execution-context14.png)



#### Assign a reference to an outer lexical environment

The reference to the outer lexical environment point to the lexical environment of the external code that contains the code currently being evaluated. This implements a scope chain.

The code currently being evaluated is the global code. Since there is no code that contains global code, assign a null to the outer lexical environment in the global lexical environment. This means that the global lexical environment is at the top of the scope chain.

![](https://i.postimg.cc/8CFhpSyC/execution-context15.png)



#### this binding

The global object is bound to this in the global environment record.

![](https://i.postimg.cc/zvDvfwJk/execution-context16.png)



### Executing Global Code

Now the global code starts running sequentially. Variable assignments are executed, assigning values ​​to global variables x, y. Then the function foo is called. Variable assignments and function calls must be retrieved before they can be executed.

When retrieving for an identifier, it retrieves the lexical environment of the running execution context for the identifier. Since the currently  running execution context is the global execution context, it searches for the identifiers x, y, and foo in the global lexical environment.

If an identifier cannot be retrieved from the lexical environment of a running execution context, it is moved to the lexical environment indicated by the outer lexical environment reference to retrieve the identifier. This is the operating principle of the scope chain. However, since the global lexical environment is the end point of the scope chain, identifiers that cannot be retrieved in the global lexical environment generate a reference error.

The variable assignment statement is to change the binding value by retrieving for the identifier registered in the lexical environment. The function call is to call the bound function object by retrieving for the identifier registered in the lexical environment.

![](https://i.postimg.cc/3wVpccFD/execution-context17.png)



### Evaluating foo function code

```javascript
var x = 1;
const y = 2;

function foo (a) {
  var x = 3;
  const y = 4;

  function bar (b) {
    const z = 5;
    console.log(a + b + x + y + z);
}
  bar(10);
}

foo(20); // 42
```

When the foo function is called, execution of the global code is paused, and control of the code is shifted into the function foo. And JavaScript begin to evaluate the function code. Function code evaluation is proceeds in the following order.

1. Create a function execution context
2. Create a functional lexical environment

   2.1. Create function environment records

   2.2. Assign a reference to an external lexical environment

   2.3. this binding



![](https://i.postimg.cc/XYBqHcQr/execution-context18.png)



#### Create a function execution context

First, create the execution context of the foo function. The created function execution context is pushed to the execution context stack.

![](https://i.postimg.cc/vHF0ZMNT/execution-context19.png)



#### Create a functional lexical environment

foo Function Creates a functional lexical environment and binds it to the LexicalEnvironment and VariableEnvironment components in the foo function execution context.

![](https://i.postimg.cc/zvtDppMP/execution-context20.png)



#### Create function environment records

Environment Records, one of the components that make up a lexical environment, register and manage parameters, arguments objects, and variables and function definitions declared in the function.

{% hint style="info" %}
The value received by the parameter is treated as var declaration.
{% endhint %}

![](https://i.postimg.cc/05T95MvS/execution-context21.png)



#### Assign a reference to an external lexical environment

A reference to an outer lexical environment stores a reference to the lexical environment of the running execution context at the time the foo function definition is evaluated.

The foo function is a global function defined in the global code. Therefore, the function foo is evaluated at the time of global code evaluation. At this point, the running execution context is the global execution context. Thus references to outer lexical environments store references to the global lexical environment.

![](https://i.postimg.cc/qRG2BVhh/execution-context22.png)

{% hint style="info" %}
Inner slot of function object \[\[Environment\]\] 

Every function in JavaScript saves the lexical environment of the currently running execution context in the function object's inner slot \[\[Environment\]\] when the function definition is evaluated and creates the function object. The inner slot \[\[Environment\]\] of the function object is the mechanism that implements the lexical scope. The inner slot \[\[Environment\]\] and the lexical scope of the function object are important clues to understand closure.
{% endhint %}



#### this binding

Since the foo function is called as a normal function, 'this' refers to the window. We now paused the execution of the global code and push the created foo function execution context to the execution context stack. At this time, the execution context of the foo function is the top of the execution context stack, that is, the running execution context.

![](https://i.postimg.cc/xdVR0STY/execution-context23.png)



### Executing foo Function code

Now the foo function code starts running sequentially. Parameters are assigned arguments, variable assignments are executed, and values are assigned to local variables x and y. The function bar is then called.

To do this, retrieve the necessary identifiers in the lexical environment of the running execution context. Since the currently running execution context is the foo function execution context, the identifier x, y is retrieved  in the foo function lexical environment. If an identifier cannot be retrieved from the lexical environment of a running execution context, it is moved to the lexical environment indicated by the outer lexical environment reference to retrieve the identifier.  Fortunately, all identifiers can be retrieved in the lexical context of the currently running execution context. Bind the value to the retrieved identifier.

![](https://i.postimg.cc/HLGFyK3s/execution-context24.png)



### Evaluating the bar function code

```javascript
var x = 1;
const y = 2;

function foo (a) {
  var x = 3;
  const y = 4;

  function bar (b) {
    const z = 5;
    console.log(a + b + x + y + z);
}
  bar(10);
}

foo(20); // 42
```

When the bar function is called, execution of the foo function code is paused, and control of the code is shifted into the function bar. And JavaScript begin to evaluate the function code. The creation process of the execution context and the lexical environment is the same as the evaluation of the foo function code. The generated bar function execution context and lexical environment are as follows.

![](https://i.postimg.cc/65xkTT64/execution-context25.png)



### Executing bar Function code

![](https://i.postimg.cc/mkgFSTBY/execution-context26.png)



Then `console.log (a + b + x + y + z);` is executed. This code is executed in the following order.



#### Retrieve the identifier console

First, the console identifier is retrieved in the scope chain. The scope chain is a continuation of the lexical environment, beginning with the lexical environment of the currently running execution context and to a to the outer lexical environment reference. Therefore, whenever an identifier is retrieved , it starts retrieving in the lexical environment of the currently running execution context.

The running context is the bar function execution context. Therefore, the bar function in the execution context starts retrieving for the console identifier in the bar lexical environment. Since there is no console identifier here, it goes to the foo function lexical environment pointed to by the top scope on the scope chain\(outer lexical environment reference\) , to retrieve the console identifier.

Since there is no console identifier here, it goes to the global scope \(global lexical environment\) pointed to by the outer lexical environment reference which is the top scope on the scope chain, to retrieve the console identifier.

The global lexical environment consists of an object environment record and a declarative environment record. The console identifier can be found in the object environment record's bindingObject, the global object.



#### Retrieve the log method

Now it retrieves the object bound to the console identifier, the log method, from the console object. At this point, the method is retrieved through the prototype chain of the console object. The log method is a property that is directly owned by the console object, not an inherited property.



#### Evaluation of expressions a + b + x + y + z

JavaScript retrieve the identifiers a, b, x, y, z which to be passed to the console.log method, to evaluate the expression a + b + x + y + z. The identifier is retrieved from a lexical environment starting with the lexical environment of the currently running execution context and move to other lexical environment through the outer lexical environment reference\(Scope chain\).

![](https://i.postimg.cc/FRm4F8S4/execution-context27.png)



### Call the console.log method

The created value \(42 // \(20 + 10 + 3 + 4 + 5\)\) that is evaluated from the expression `a + b + x + y + z`  is passed to console.log method and call.



###  **Ending** bar function code execution

When the console.log method is called and terminated, there is no more code to execute, so execution of the bar function code is terminated. At this time, the execution context of the bar function is popped and removed from the execution context stack, and the foo function execution context becomes the running execution context.

![](https://i.postimg.cc/7LrRk7vG/execution-context28.png)

{% hint style="info" %}
Note that even the bar function execution context stack is popped, the bar function lexical environment does not immediately removed. A lexical environment is an object that is referenced by an execution context but is independent. All values, including objects, are destroyed by the garbage collector only when they are not referenced by someone else. Even if the bar function execution context is popped, the bar function lexical environment does not disappear if someone refers to the bar function lexical environment.
{% endhint %}



### **Ending** foo function code execution

When the bar function terminates, foo function execution code is terminated because there is no more code to execute. At this time, the foo function execution context is popped and removed from the execution context stack, and the global execution context becomes the running execution context.

![](https://i.postimg.cc/ZRxncrmr/execution-context29.png)



### **Ending** global code execution

When the foo function terminates, the global code execution ends because there is no more code to execute. However, the termination of global code execution does not mean the removal of the global execution context from the execution context stack.

The global execution context is maintained without being removed from the execution context stack until the application is closed by exiting the browser. Therefore, the life cycle of global variables and global functions registered in the global lexical environment coincides with the life cycle of the application.

When an event such as a button click occurs, an event handler, which is a function to be called, is also pushed to the execution context stack.



## Execution context and block level scope

The variable declared with the let keyword follows a block-level scope \(Functions, if statements, for statements, while statements, try / catch statements, etc.\)

```javascript
const x = 1;

function foo () {
  const arr = [1, 2, 3];
<------------------------------- unilt here ------------------------------->
  for (let i = 0; i < arr.length; i++) {
    arr[i] += x;
  }

  console.log(arr);
}

foo(); // [ 2, 3, 4 ]
```

![](https://i.postimg.cc/SNFrv4cV/execution-context30.png)



```javascript
const x = 1;

function foo () {
  const arr = [1, 2, 3];
  
  for (let i = 0; i < arr.length; i++) {
    arr[i] += x;
    <------------------------------- unilt here ------------------------------->
  }

  console.log(arr);
}

foo(); // [ 2, 3, 4 ]
```

![](https://i.postimg.cc/gJ3DYBW3/execution-context31.png)



```javascript
const x = 1;

function foo () {
  const arr = [1, 2, 3];
  
  for (let i = 0; i < arr.length; i++) {
    arr[i] += x;
  }
<------------------------------- from here ------------------------------->
  console.log(arr);
}

foo(); // [ 2, 3, 4 ]
```

![](https://i.postimg.cc/XJgC1MW1/execution-context32.png)

