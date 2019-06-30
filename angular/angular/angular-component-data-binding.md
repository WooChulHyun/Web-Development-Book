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
    <p>{{ isTrue ? 'True' : 'False' }}</p>
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

  isTrue = true;

  siteaddress = window.location.href;

  sayHi() {
    return `Hi! my name is ${this.name}.`;
  }

  get sayHello() {
    return `Hello! my name is ${this.name}.`;
  }
}
```

![](https://i.postimg.cc/C5dZfwPJ/Data-Binding1.png)

### Property binding

Property binding is a template syntax used for one-way data binding between a property of a component class and a template, and binds the evaluation result of the expression to the DOM property of the HTML element.

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `
    <input type="text" [value]="name" />

    <p [innerHTML]="contents"></p>

    <img [src]="imageUrl" /><br />

    <button [disabled]="isDisabled">disabled button</button>
  `
})
export class AppComponent {
  name = 'Woochul';
  contents = 'Lorem ipsum dolor sit amet, consectetur adipisicing elit.';
  imageUrl = 'https://via.placeholder.com/350x150';
  isDisabled = true;
}
```

![](https://i.postimg.cc/jdZmV4q8/Data-Binding2.png)



### Attribute binding <a id="33-&#xC5B4;&#xD2B8;&#xB9AC;&#xBDF0;&#xD2B8;-&#xBC14;&#xC778;&#xB529;attribute-binding"></a>

Attribute binding binds the evaluation of an expression to an HTML attribute in a template syntax used for one-way data binding between the properties of the component class and the template.

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `
    <!-- property binding-->
    <input id="user" type="text" [value]="name">
    <!-- attributes binding-->
    <input id="user" type="text" [attr.value]="name">
  `
})
export class AppComponent {
  name = 'Woochul';
}
```

![](https://i.postimg.cc/zvvyp1Jw/Data-Binding3.png)

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `
    <table>
      <tr>
<!-- Since the colspan property does not exist, use the attributes binding. -->
        <td [attr.colspan]="length">A + B</td>
      </tr>
      <tr>
        <td>C</td><td>D</td>
      </tr>
    </table>
  `,
  styles: [`
    table, td {
      width: 200px;
      border: 1px solid black;
      text-align: center;
    }
  `]
})
export class AppComponent {
  length = 2;
}
```

![](https://i.postimg.cc/GmKH02HP/Data-Binding4.png)



### Class binding <a id="34-&#xD074;&#xB798;&#xC2A4;-&#xBC14;&#xC778;&#xB529;class-binding"></a>

Class bindings allow you to add or remove classes from the class attribute of an HTML element. Class bindings can be used in two ways:

```typescript
<element [class.className]="booleanExpression">...</element>
<element [class]="class-name-list">...</element>
```



