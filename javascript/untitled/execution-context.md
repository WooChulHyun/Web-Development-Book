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

ThisBinding component is the place where reference to the object that called the function  are stored. The value pointed by ThisBinding will be 'this' in the execution context.



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

That is, a data stored in a separate object, such as a lexical environment or a global object with a 'with statement', does not copy the key / value pair of the object, but takes a reference to the entire object and binds it to a property called bindObject.

Generally only created in the global environment record.

