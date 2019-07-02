# Built-in directive

## What is Built-in directive?

A directive is an "instruction \(command\) for managing all of the DOM \(shape, behavior, etc.\)". It is used in the form of an HTML element or attribute to convey a directive to the element in which the directive is used.

A directive is a separate implementation of the common concerns available across the application, reducing component complexity and improving readability. Components can also be seen as directives in a larger sense because they manage the DOM, such as creating views and handling events.

The Angular directive provides three types of directives:

* Component Directives
  * It is a directive for displaying the template of the component. Defines the name of any directive in the seletor property of the @Component decorator's metadata object.
* Attribute Directives
  * Attribute directives are used with attributes of HTML elements to control the shape or behavior of host elements. There are built-in attribute directives such as ngClass and ngStyle.
* Structural Directives
  * The structure directive changes the DOM layout through iterative creation \(ngFor\) of DOM elements, addition or removal by condition \(ngIf, ngSwitch\).



## Built-in attribute directive

The built-in attribute directive is an attribute directive provided by Angular, such as the ngClass and ngStyle directives.



### ngClass

Add or remove multiple CSS classes. Using class binding is a better way when adding or removing a class.

```markup
<element [ngClass]="string | array | object">...</element>
```

The ngClass directive reflects the bound string, array, or object in the class attribute of the HTML element. The values that can be bound to the ngClass directive are:



* A string with CSS class names separated by space. All CSS class names listed in the string are reflected in the class attribute.

```markup
<div [ngClass]="'text-bold color-blue'">...</div>
```



* An array consisting of the elements of the CSS class name. All CSS class names that are elements of the array are reflected in the class attribute.

```markup
<div [ngClass]="['text-bold', 'color-blue']">...</div>
```



* An object that has a CSS class name as a property name and a boolean type as a property value. Only properties whose property value is true are reflected in the class attribute.

```markup
<div [ngClass]="{ 'text-bold': true, 'color-blue': false }">...</div>
```



When a class is already specified by the class attribute, the ngClass directive merges the class attribute to create a new HTML class attribute.

```markup
<div class="class1 class2" [ngClass]="['class2', 'class3']">...</div>
```

The code above will be merged with the class declared in the class attribute and the class bound to the ngClass directive.

```markup
<div class="class1 class2 class3">...</div>
```

For class bindings \(\[class\]\) that target multiple classes, it works differently from deleting existing class attributes and creating new class attributes based on the list of bound classes.



```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `
    <ul>
      <li [ngClass]="stringCssClasses">bold blue</li>
      <li [ngClass]="ArrayCssClasses">italic red</li>
      <li [ngClass]="ObjectCssClasses">bold red</li>
      <li [ngClass]="getCSSClasses('italic-blue')">italic blue</li>
    </ul>
  `,
  styles: [`
    .text-bold   { font-weight: bold; }
    .text-italic { font-style: italic; }
    .color-blue  { color: blue; }
    .color-red   { color: red; }
  `]
})
export class AppComponent {
  state = true;

  stringCssClasses = 'text-bold color-blue';
  ArrayCssClasses = ['text-italic', 'color-red'];
  ObjectCssClasses = {
    'text-bold': this.state,
    'text-italic': !this.state,
    'color-blue': !this.state,
    'color-red': this.state
  };

  getCSSClasses(flag: string) {
    let classes;
    if (flag === 'italic-blue') {
      classes = {
        'text-bold': !this.state,
        'text-italic': this.state,
        'color-red': !this.state,
        'color-blue': this.state
      };
    } else {
      classes = {
        'text-bold': this.state,
        'text-italic': !this.state,
        'color-red': this.state,
        'color-blue': !this.state
      };
    }
    return classes;
  }
}
```

![](https://i.postimg.cc/3Nrf6hMF/Built-in-Directive1.png)

### ngStyle

Add or remove multiple inline styles. When adding or removing a single inline style, it is a better to use style binding.

```markup
<element [ngStyle]="object">...</element>
```



The ngStyle directive reflects the bound object to the style attribute of the HTML element. An object bound to the ngStyle directive has a CSS property as a property name and a CSS property value as a property value. At this time, if the CSS property value requires a unit, add a unit to the CSS property.

```markup
<div [ngStyle]="{ color: 'red', 'width.px': 100 }"></div>
```



When style is already specified by the style attribute, the ngStyle directive merges the HTML style attribute to create a new HTML style attribute.

```markup
<div style="color: red; width: 100px;" 
[ngStyle]="{ color: 'blue', 'height.px': 100 }">...</div>
```

The above code merges the style declared in the style attribute with the style bound to the ngStyle directive, and it will be converted as follows.

```markup
<div style="color: blue; width: 100px; height: 100px;">...</div>
```



```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `
    <div>
      Width: <input type="text" [(ngModel)]="width">
      <button (click)="increaseWidth()">+</button>
      <button (click)="decreaseWidth()">-</button>
    </div>
    <div>
      Height: <input type="text" [(ngModel)]="height">
      <button (click)="increaseHeight()">+</button>
      <button (click)="decreaseHeight()">-</button>
    </div>
    <button (click)="isShow=!isShow">{{ isShow ? 'Hide' : 'Show' }}</button>
    <div
      [ngStyle]="{
        'width.px': width,
        'height.px': height,
        'background-color': bgColor,
        'visibility': isShow ? 'visible' : 'hidden'
      }">
    </div>
  `
})
export class AppComponent {
  width = 200;
  height = 200;
  bgColor = '#4caf50';
  isShow = true;

  increaseWidth()  { this.width  += 10; }
  decreaseWidth()  { this.width  -= 10; }
  increaseHeight() { this.height += 10; }
  decreaseHeight() { this.height -= 10; }
}
```

![](https://i.postimg.cc/gJ92vYXj/Built-in-Directive2.png)



## Built-in structural directive

The built-in structure directive changes the structure of the view through iterative creation \(ngFor\) of DOM elements, addition or removal by condition \(ngIf, ngSwitch\).

{% hint style="info" %}
A host element \(the element for which the directive is declared\) only can have one structure directive.
{% endhint %}



### ngIf

The ngIf directive adds a host element to the DOM if the result of the right-side expression is true, and removes the host element from the DOM if the result of the right-side expression is false. The expression on the right should be evaluated as true or false.

```markup
<element *ngIf="expression">...</element>
```

The \* \(asterisk\) prepended to the ngIf directive is a syntactic sugar of the following syntax: That is, the above code is converted into the following code.

```markup
<ng-template [ngIf]="expression">
  <element>...</element>
</ng-template>
```

When Angular meet `*ngIf`, it wraps the host element into an `ng-template` directive and converts `*ngIf` to a property binding. The `*ngFor` and `*ngSwitch` directives follow the same pattern.

{% hint style="info" %}
The `ng-template` directive is defined as part of the component template, but is simply annotated and not rendered in the view when it is simply defined, and then rendered into the view only if the value bound to `*ngIf` evaluates to true. The `ng-template` directive is typically used when you need to add a templated view snippet to the host view.
{% endhint %}



```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `
    <p *ngIf="isShow">Lorem ipsum dolor sit amet</p>

    <p [style.display]="isShow ? 'block' : 'none'">Lorem ipsum dolor sit amet</p>

    <button (click)="isShow=!isShow">{{ isShow ? 'Hide' : 'Show' }}</button>
  `,
  styles: [`
    p { background-color: #CDDC39; }
  `]
})
export class AppComponent {
  isShow = true;
}
```

![](https://i.postimg.cc/3xjBxLvV/Built-in-Directive3.png)



You can also implement display / hide of elements using style binding or class binding without using the ngIf directive. However, elements not marked by style binding or class binding are not rendered by the browser, but remain in the DOM. Elements removed by the ngIf directive do not remain in the DOM,  completely removed, preventing unnecessary resource wastage.

![](https://i.postimg.cc/DfdpZw3B/Built-in-Directive4.png)



