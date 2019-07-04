# Template reference variable & Safe navigation operator

## Template reference variable

A template reference variable is a variable that contains a reference to a DOM element. If you declare a template reference variable by adding a hash symbol \(\#\) before the variable name within the element of the template, a reference to that element is assigned to the template reference variable, and JavaScript code in the template refers to it without a hash symbol. Template reference variables are only valid within a template and do not give any side effects to the component class. However, you can pass the value of a template reference variable to the component class through event binding.

```markup
<element #myelement>...</element>
```



```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `
    <div>
      <!-- template reference variable email declaration -->
      <input #email type='email' placeholder="Enter your email">
      <!-- template reference variable email reference -->
      <button (click)="checkEmail(email.value)">check form</button>
    </div>
    <span *ngIf="result">{{ result }}</span>
  `
})
export class AppComponent {
  result: string;

  checkEmail(email: string) {
    const regexr = /^[0-9a-zA-Z]([-_\.]?[0-9a-zA-Z])*@[0-9a-zA-Z]([-_\.]?[0-9a-zA-Z])*\.[a-zA-Z]{2,3}$/;

    if (regexr.test(email)) {
      this.result = '';
    } else {
      this.result = 'Email address format is invalid.';
    }
  };
}
```



## Safe navigation operator <a id="2-&#xC138;&#xC774;&#xD504;-&#xB0B4;&#xBE44;&#xAC8C;&#xC774;&#xC158;-&#xC5F0;&#xC0B0;&#xC790;safe-navigation-operator"></a>

The safe navigation operator `?` is used to avoid errors that occur when the property value of a component class is null or undefined. When the property value is null or undefined, or when interpolating an undeclared property, nothing is displayed without error. However, a TypeError is raised when referencing a property of an object property that is not declared. The safe navigation operator will terminate processing and will not raise an error even if it encounters a property that is null or undefined.

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `
    <!-- When obj is null or undefined, nothing is displayed. -->
    {{ obj }}
    <!-- ERROR TypeError: Cannot read property 'id' of undefined -->
    {{ obj.id }}
    <!-- The safe navigation operator terminates processing and does not raise 
    an error even if it encounters a null or undefined property. -->
    {{ obj?.id }}
  `
})
export class AppComponent { }
```



## Reference

Ungmo, L. \(2018\). _Angular Essentials._ Gyeonggi-do Bucheon-si: Rubypaper

