# Angular Component - Data Binding

## Data Binding

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



## Interpolation

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

## Property binding

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



## Attribute binding

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



## Class binding

Class bindings allow you to add or remove classes from the class attribute of an HTML element. Class bindings can be used in two ways:

```typescript
<element [class.className]="booleanExpression">...</element>
<element [class]="class-name-list">...</element>
```



### Singulary Class Binding

On the left side of the class binding, specify the class name to reflect in the class attribute of the HTML element after the class, and bind expressions that can be evaluated as true or false on the right side.

```markup
<div [class.classB]="isTrue">...</div>
```

In the above example, if the value of the expression on the right side isTrue is true, add the class alert, which is specified after the class on the left side, to the class attribute, and if the value of isTrue is false, delete it from the class attribute.



```markup
<div class="classA" [class.classB]="isTrue">...</div>
```

If the value of isTrue is true, the above example is converted to:

```markup
<div class="classA classB">...</div>
```

If the value of isTrue is false, the above example is converted to:

```markup
<div class="classA">...</div>
```



Let's look at the case where the classA class is already applied as shown below.

```markup
<div class="classA " [class.classA]="isTrue">...</div>
```

If the value of isTrue is true, the above example is converted to:

```markup
<div class="classA">...</div>
```

If the value of isTrue is false, the above example is converted to:

```markup
<div>...</div>
```



### Polynomial Class Binding

On the left side of the class binding, specify class. On the right side, bind the list of classes \(class list separated by space\) to be reflected in the class attribute of the HTML element.

```markup
<div [class]="my-classes">...</div>
```

It is similar to property binding to a class property of a DOM object, but there is no class property in the DOM object. Therefore, polynomial class bindings are not property bindings and manipulate the attributes of HTML elements just like Singulary class bindings.

The polynomial class binding reflects the value of the right-hand expression my-classes in the class attribute. In the above example, if the value of my-classes is 'my-class1 my-class2', the above code will be converted to:

```markup
<div class="my-class1 my-class2">...</div>
```



If the class has already been applied:

```markup
<div class="my-class1 my-class2" [class]="my-classes">...</div>
```

If the value of my-classes is 'my-class3 my-class4', the above example is converted as below.

```markup
<div class="my-class3 my-class4">...</div>
```



Thus, when a class is already specified by the class attribute of an HTML element, a Singulary class binding \(\[class.class-name\]\) that targets one class merges the class attribute to create a new class attribute . However, a polynomial class binding \(\[class\]\) that targets multiple classes deletes the existing class attribute and creates a new class attribute based on the list of bound classes. In other words, class binding takes precedence over existing class attributes. Therefore, existing class attributes are reset by class binding. That time, the location of the class binding is not affected.



```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `
    <div [class.text-large]="isLarge">text-large</div>
    <div class="text-small color-red" [class.color-red]="isRed">text-small</div>
    <div [class]="myClasses">text-large color-red</div>
    <div class="text-small color-blue" [class]="myClasses">text-large color-red</div>
  `,
  styles: [`
    .text-small { font-size: 18px;}
    .text-large { font-size: 36px;}
    .color-blue { color: blue;}
    .color-red { color: red;}
  `]
})
export class AppComponent {
  isLarge = true;
  isRed = false;
  myClasses = 'text-large color-red';
}
```

![](https://i.postimg.cc/Cx35WYDB/Data-Binding5.png)

Class bindings are mainly used to add or remove a class by condition. Class bindings can be used to specify multiple classes, but more control is possible using the ngClass directive.



## Style binding

Style binding allows you to specify styles in the style attribute of an HTML element.

```markup
<element [style.style-property]="expression">...</element>
```

On the left side of the style binding, specify the CSS property name to be reflected in the style attribute after style, and bind the expression on the right side that can be evaluated as the value of the CSS property. If the CSS property value requires a unit, add a unit to the CSS property.

```markup
<div [style.background-color]="'white'"
     [style.font-size.px]="'16'">...</div>
```

Note that when styles are already specified by the style attribute, the non-overlapping styles are added to the style attribute, and the duplicate styles are reset to the value of the style binding. In other words, style binding takes precedence over the existing style attribute.

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `
    <button class="btn"
      [style.background-color]="isActive ? '#4CAF50' : '#f44336'"
      [style.font-size.em]="isActive ? '1.2' : '1'"
      (click)="isActive=!isActive">Toggle</button>
  `,
  styles: [`
    .btn {
      background-color: #4CAF50;
      border: none;
      border-radius: 8px;
      color: white;
      padding: 10px;
      cursor: pointer;
      outline: none;
    }
  `]
})
export class AppComponent {
  isActive = false;
}
```

![](https://i.postimg.cc/vHpXSgPW/Data-Binding6.png)

Click Toggle Button

![](https://i.postimg.cc/BQgH2jrS/Data-Binding7.png)



## Event binding

An event binding is calling an event handler when an event occurs by changing the state of the view \(button click, check box check, text input, etc.\).

All of the data bindings discussed so far have moved data from the component class to the template, but event binding moves the data from the template to the component class.

```markup
<element (event)="statement">...</element>
```

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `
    <input type="text" [value]="name" (input)="setName($event)">
    <button (click)="clearName()">clear</button>
    <p>name: {{ name }}</p>
  `
})
export class AppComponent {
  name = '';

  setName(event) {
    console.log(event);
    this.name = event.target.value;
  }

  clearName() {
    this.name = '';
  }
}
```

![](https://i.postimg.cc/zfkM01JJ/Data-Binding8.png)



## Two-way data binding

Two-way data binding refers to the mutual reflection of changes in the state of views and component classes. In other words, if the state of the view changes, the state of the component class changes, if the state of the component class changes, the state of the view also changes.

```markup
<element [(ngModel)]="property">...</element>
```

Write the ngModel directive in the form of an event binding \(\(\)\) and a property binding \(\[\]\), write the property on the right side that the view and component classes will share. To use the ngModel directive, you must register the FormsModule in the module.

```typescript
// src/app/app.module.ts
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';

import { FormsModule } from '@angular/forms';  // <----------------

import { AppComponent } from './app.component';

@NgModule({
  declarations: [AppComponent],
  imports: [BrowserModule, FormsModule],  // <----------------
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```



```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `
    <input type="text" [(ngModel)]="name">
    <p>name: {{ name }}</p>
  `
})
export class AppComponent {
  name = '';
}
```

![](https://i.postimg.cc/SRpbvfB4/Data-Binding9.png)

The name property of the component class is two-way bound to the input element of the template. That is, if the value property of the input element changes, the name property of the component class changes to the same value, and if the name property of the component class changes, the value property of the input element also changes to the same value.

In fact, Angular does not support two-way binding. As can be inferred from \[\(\)\] \(this is called Banana in a box\), two-way binding is only a shorthand syntax for event binding and property binding. That is, the actual behavior of two-way binding is a combination of event binding and property binding. The above code can be expressed as an event binding and a property binding:

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `
    <input type="text" [value]="name" (input)="name=$event.target.value">
    <p>name: {{ name }}</p>
  `
})
export class AppComponent {
  name = '';
}
```

`<input type="text" [(ngModel)]="name">` and `<input type="text" [value]="name" (input)="name=$event.target.vale">` work exactly the same.

ngModel is a directive that can be used to easily create two-way bindings implemented with event binding and property binding, and can only be used with DOM elements related to user input \(input, textarea, select, and other form control elements\). When we express ngModel as an event binding and a property binding:

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `
    <input [ngModel]="name" (ngModelChange)="name=$event">
    <p>name: {{ name }}</p>
  `
})
export class AppComponent {
  name = '';
}
```

The property binding \[ngModel\] updates the properties of the DOM element associated with user input \(the value property of the input element in the example above\). The event binding \(ngModelChange\) receives the event and informs the change of the DOM through the event handler. At this time, ngModelChange internally extracts the value of the property related to user input \(in the above example, target.value\) in $event and emits the event.

Two-way bindings do not necessarily use only the ngModel directive, and you can also write custom two-way data bindings.

