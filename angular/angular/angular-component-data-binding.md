# Angular Component - Data Binding

### Data Binding

Angular supports one-way data binding and two-way data binding. 

Angular provides the following seven data bindings:

| Data Binding |  Data Flow | grammar |
| :--- | :--- | :--- |
| Interpolation | Component class ⟹ Template | {{ expression }} |
| Property Binding | Component class ⟹ Template | \[property\]=”expression” |
| Attribute Binding | Component class ⟹ Template | \[attr.attribute-name\]=”expression” |
| Class Binding | Component class ⟹ Template | \[class.class-name\]=”expression” |
| Style binding | Component class ⟹ Template | \[style.style-name\]=”expression” |
| Event binding | Component class ⟸ Template | \(event\)=”statement” |
| Two-way binding | Component class ⟺ Template | \[\(ngModel\)\]=”property” |



### Interpolation

The form in which the expression is opened and closed with two curly braces is called interpolation. Interpolation is a template grammar used for one-way data binding, which converts the evaluation result of an expression into a string and binds it to a template.

```typescript
import { Component } from '@angular/core';
@Component({
  selector: 'app-root',
  template: `
    <p>name: {{ name }}</p>
    <p>Uppercase name: {{ name.toUpperCase() }}</p>
    <p>name.length: {{ name.length }}</p>
    <p>age: {{ age }}</p>
    <p>admin: {{ admin }}</p>
    <p>address: {{ address.city }} {{ address.country }}</p>
    <p>gender: {{ gender }}</p>
    <p>sayHi(): {{ sayHi() }}</p>
    <p>age * 10: {{ age * 10 }}</p>
    <p>age > 10: {{ age > 10 }}</p>
    <p>'stirng': {{ 'stirng' }}</p>
    <p>Site Address: {{ siteaddress }}</p>
    <p>1 + 1 = {{ 1 + 1 }}</p>
    <p>get: {{ sayHello }}</p>
  `
})
export class AppComponent {
  name = 'Angular';
  age = 20;
  admin = true;
  address = {
    city: 'Seoul',
    country: 'Korea'
  };

  siteaddress = window.location.href;

  sayHi() {
    return `Hi! my name is ${this.name}.`;
  }

  get sayHello() {
    return `Hello! my name is ${this.name}.`;
  }
}
```

![](https://i.postimg.cc/dtSVndCC/Data-Binding1.png)

