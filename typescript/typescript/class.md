# Class

## Class Definition

The Typescript class must pre-declare class properties in the class body.

```typescript
class Person {
  name: string;

  constructor(name: string) {
    this.name = name;
  }

  walk() {
    console.log(`${this.name} is walking.`);
  }
}

const person = new Person('Hyun');
person.walk(); // Hyun is walking
```



## Access modifier

The Typescript class supports public, private, and protected access modifiers supported by class-based object-oriented languages, and the semantics are also basically the same.

For Typescript, class properties and methods which is omitted access modifiers are implicitly declared public.

| Accessibility | public | protected  | private |
| :--- | :--- | :--- | :--- |
| Inside the class | ◯ | ◯ | ◯ |
| Inside child class | ◯ | ◯ | ✕ |
| Class instance | ◯ | ✕ | ✕ |

```typescript
class Foo {
  public x: string;
  protected y: string;
  private z: string;

  constructor(x: string, y: string, z: string) {
    // Public, protected, and private access modifiers can be 
    // referenced from within a class.
    this.x = x;
    this.y = y;
    this.z = z;
  }
}

const foo = new Foo('x', 'y', 'z');

// Public access modifier can be referenced 
// outside the class through class instances.
console.log(foo.x);

// Protected access modifier cannot be referenced 
// outside a class through a class instance.
console.log(foo.y);
// error TS2445: Property 'y' is protected and only accessible 
// within class 'Foo' and its subclasses.

// A private access modifier cannot be referenced 
// outside of a class through a class instance.
console.log(foo.z);
// error TS2341: Property 'z' is private and only accessible within class 'Foo'.

class Bar extends Foo {
  constructor(x: string, y: string, z: string) {
    super(x, y, z);

    // A public access modifier can be referenced from within a child class.
    console.log(this.x);

    // protected access modifier can be referenced from within a child class.
    console.log(this.y);

    // private access modifier cannot be referenced from within a child class.
    console.log(this.z);
    // error TS2341: Property 'z' is private and only accessible within class 'Foo'.
  }
}
```



## Declare Access modifier on Constructor Parameters

Access modifiers can also be declared in constructor parameters. At this time, the constructor parameters used with access modifiers are implicitly declared as class properties and implicitly initialized even if there is no separate initialization in the constructor.

```typescript
class Foo {
  /*
  The constructor parameter x to which the access modifier is declared
  and initialized with the class property.
  Since public is declared, x can also be referenced outside the class.
  */
  constructor(public x: string) { }
}

const foo = new Foo('Hello');
console.log(foo);   // Foo { x: 'Hello' }
console.log(foo.x); // Hello

class Bar {
  /*
  The constructor parameter x to which the access modifier is declared
  and initialized with the class property.
  Since private is declared, x can only be referenced from within a class.
  */
  constructor(private x: string) { }
}

const bar = new Bar('Hello');

console.log(bar); // Bar { x: 'Hello' }

console.log(bar.x); // Property 'x' is private and only accessible within class 'Bar'.
```

If you do not declare an access modifier in the constructor parameter, the constructor parameter becomes a local variable valid within the constructor, making it impossible to refer to it outside the constructor.

```typescript
class Foo {
  constructor(x: string) {
    console.log(x);
  }
}

const foo = new Foo('Hello');
console.log(foo); // Foo {}
```



## readonly keyword

Typescript can use the `readonly` keyword. Class properties for which `readonly` is declared can be assigned values only at declaration or within the constructor. Otherwise, value cannot be assigned and only readable.

```typescript
class Foo {
  private readonly MAX_LEN: number = 5;
  private readonly MSG: string;

  constructor() {
    this.MSG = 'hello';
  }

  log() {
    this.MAX_LEN = 10; 
    // Cannot assign to 'MAX_LEN' because it is a constant or a read-only property.
    this.MSG = 'Hi'; 
    // Cannot assign to 'MSG' because it is a constant or a read-only property.

    console.log(`MAX_LEN: ${this.MAX_LEN}`); // MAX_LEN: 5
    console.log(`MSG: ${this.MSG}`); // MSG: hello
  }
}

new Foo().log();
```



## static keyword

In Typescript, the `static` keyword can also be used for class properties. Like static methods, static class properties are called with the class name, not the instance, and can be called without creating an instance of the class.

```typescript
class Foo {
  static instanceCounter = 0;
  constructor() {
    Foo.instanceCounter++;
  }
}

var foo1 = new Foo();
var foo2 = new Foo();

console.log(Foo.instanceCounter);  // 2
console.log(foo2.instanceCounter); 
// error TS2339: Property 'instanceCounter' does not exist on type 'Foo'.
```



## abstract class

An abstract class contains one or more abstract methods and can also contain generic methods. An abstract method is a method in which only the method name and type are declared without content, and the `abstract` keyword is used when declaring. When you define an abstract class, you use the `abstract` keyword and you cannot create an instance directly, but only be used for inheritance. A class that inherits an abstract class must implement abstract methods of the abstract class.

```typescript
abstract class Animal {

  abstract makeSound(): void;

  move(): void {
    console.log('roaming the earth...');
  }
}

// new Animal();
// error TS2511: Cannot create an instance of the abstract class 'Animal'.

class Dog extends Animal {
  makeSound() {
    console.log('bowwow~~');
  }
}

const myDog = new Dog();
myDog.makeSound();
myDog.move();
```

All methods of interface's method are abstract methods, but an abstract class can contain one or more abstract methods and generic methods.

