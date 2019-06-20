# Interface

### Variable and interface

The interface can be used as a variable type. At this time, a variable declared as an interface as a type must conform to the interface. This is similar to defining a new type.

```typescript
interface Todo {
  id: number;
  content: string;
  completed: boolean;
}

let todo: Todo;

todo = { id: 1, content: 'typescript', completed: false };
```

```typescript
interface Todo {
  id: number;
  content: string;
  completed: boolean;
}

let todos: Todo[] = [];

function addTodo(todo: Todo) {
  todos = [...todos, todo];
}

const newTodo: Todo = { id: 1, content: 'typescript', completed: false };
addTodo(newTodo);
console.log(todos)
// [ { id: 1, content: 'typescript', completed: false } ]
```



### Function and Interface

```typescript
interface SquareFunc {
  (num: number): number;
}

const squareFunc: SquareFunc = function (num: number) {
  return num * num;
}

console.log(squareFunc(10)); // 100
```



### Class and interface

If you declare an interface after implements in a class declaration, that class must implement the specified interface. This has the advantage of maintaining the consistency of the classes that implement the interface. An interface is similar to a class in that it can have properties and methods, but it can not create instances directly.

```typescript
interface ITodo {
  id: number;
  content: string;
  completed: boolean;
}

class Todo implements ITodo {
  constructor (
    public id: number,
    public content: string,
    public completed: boolean
  ) { }
}

const todo = new Todo(1, 'Typescript', false);

console.log(todo);
```

```typescript
interface IPerson {
  name: string;
  sayHello(): void;
}

class Person implements IPerson {

  constructor(public name: string) {}

  sayHello() {
    console.log(`Hello ${this.name}`);
  }
}

function greeter(person: IPerson): void {
  person.sayHello();
}

const me = new Person('Lee');
greeter(me); // Hello Lee
```



### Optional properties

The properties of the interface must be implemented. However, there may be occasions when an optional property of an interface is required. An optional property has `?`

```typescript
interface UserInfo {
  username: string;
  password: string;
  age?    : number;
  address?: string;
}

const userInfo: UserInfo = {
  username: '123',
  password: '123456'
}

console.log(userInfo);
```



