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



