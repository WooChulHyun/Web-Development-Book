# Installing and Using the TypeScript Compiler

If you install Node.js, npm is also installed. Install TypeScript globally using npm in a terminal as follows:

```bash
$ npm install -g typescript
```

Version check

```bash
$ tsc -v
Version 3.5.1
```

The TypeScript compiler \(tsc\) transforms a TypeScript file \(.ts\) into a JavaScript file.

```typescript
// person.ts
class Person {
  private name: string;

  constructor(name: string) {
    this.name = name;
  }

  sayHello() {
    return "Hello, " + this.name;
  }
}

const person = new Person('Lee');

console.log(person.sayHello());
```

Specify the name of the file to be transfiled after the tsc command. At this time, the extension .ts can be omitted.

```bash
$ tsc person
```

As a result of transfiling, a JavaScript file \(person.js\) is created in the same directory.

```javascript
// person.js
var Person = /** @class */ (function () {
    function Person(name) {
        this.name = name;
    }
    Person.prototype.sayHello = function () {
        return "Hello, " + this.name;
    };
    return Person;
}());
var person = new Person('Lee');
console.log(person.sayHello());
```

At this time, the JavaScript version of the transformed person.js is ES3. This is because the default version of the TypeScript compilation target JavaScript is ES3.

If you want to change the JavaScript version, use `--target` or `-t` as the compilation option. Currently, the JavaScript versions supported by tsc are ES3, ES5, ES6 \(ES2015\), ES2016, ES2017 \(ESNext\). For example, to enable transfiling with the ES6 version, add the following option:

```bash
$ tsc person -t es6
```

```javascript
// person.js
class Person {
    constructor(name) {
        this.name = name;
    }
    sayHello() {
        return "Hello, " + this.name;
    }
}
const person = new Person('Lee');
console.log(person.sayHello());
```

You can also transfile multiple TypeScript files at once.

```bash
$ tsc person student
```

```javascript
$ tsc *.ts
```

If you use the `--watch` or `-w` option, it detects when the contents of the file to be transfiled are changed and automatically performs the transfiling.

```bash
$ tsc student --watch
```



