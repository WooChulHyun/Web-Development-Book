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



#### Singulary Class Binding

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



#### Polynomial Class Binding

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

