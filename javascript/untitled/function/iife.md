# IIFE

### Immediately Invoke Function Expression \(IIFE\)

A function that is immediately called at the same time as the definition of the function is called an Immediately Invoke Function Expression \(IIFE\). It is called only once and can not be called again. Immediately Invoke Function Expression generally use anonymous immediate functions that do not have function names.

```javascript
(function() {
    let a = 1;
    let b = 2;
    return a + b;
}());
```

