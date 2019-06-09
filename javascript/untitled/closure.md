# Closure

### Internal slot of function object \[\[Environment\]\]

The function definition is evaluated to create a function object. At this time, the created function object stores the upper scope determined by the position where it is defined. In other words, every function object stores a reference to its upper scope in its internal slot \[\[Environment\]\]. At this time, the reference of the stored upper scope indicates the lexical environment of the currently running execution context.

For example, defined function declaration in global environment is evaluated at the time the global code is evaluated to create a function object. The internal slot \[\[Environment\]\] of the created function object stores a reference to the global lexical environment, which is the lexical environment of the running execution context at the time when the function definition is evaluated, that is, the global code evaluation point.

A function declaration defined inside a function is evaluated at the time the outer function code is evaluated to create a function object. In this case, the internal slot \[\[Environment\]\] of the created function object stores the reference of the outer function lexical environment, which is the lexical environment of the running execution context at the time of evaluation of the function definition, that is, outer function lexical environment

The reference to the lexical environment of the currently running execution context stored in the internal slot \[\[Environment\]\] of the function object is the one level up scope. It is also the reference value to be stored in the "reference to the outer lexical environment" of the lexical environment to be created when it is called. The function object stores the reference of the lexical environment stored in the internal slot \[\[Environment\]\], that is, the upper scope as long as it exists.



