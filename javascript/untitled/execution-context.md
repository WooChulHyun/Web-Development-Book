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



