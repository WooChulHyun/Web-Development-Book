# Closure

### Internal slot of function object \[\[Environment\]\]

The function definition is evaluated to create a function object. At this time, the created function object remembers the upper scope determined by the position where it is defined. In other words, every function object remembers a reference to its upper scope in its internal slot \[\[Environment\]\]. At this time, the reference of the remembered upper scope indicates the lexical environment of the currently running execution context.

