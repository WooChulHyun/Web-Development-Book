# Angular Component - Template

## What is a template?

Templates define a view of a component that is the smallest unit of the UI using HTML and Angular's own Template Syntax. Dynamically changing data is managed by the component class and is included in static HTML by data binding of the template grammar.

Angular separates views and models \(data and business logic\) from templates and component classes.



## Template Syntax

The template syntax is Angular's own extended notation for creating templates, which supports data binding for data sharing between templates and component classes, and built-in directives that can dynamically change the DOM structure and style. Static views can be defined only by HTML, but they use template syntax to define views that change dynamically in conjunction with components.

The template syntax that Angular provides is as follows.

* Data binding
  * Interpolation
  * Property binding
  * Attribute binding
  * Class binding
  * Style binding
  * Event binding
  * Two-way binding
* Built-in directive
  * Built-in attribute directive
    * ngClass
    * ngStyle
  * Built-in structural directive
    * ngIf
    * ngFor
    * ngSwitch
* Template reference variable
* Template expression operator

Prohibited items in templates

* script element \(Security issues\)
* assignment operator \(=, +=, -=\)
* Increase / decrease operator \(++, --\)
* bitwise operators \(\|, &\)
* object creation operators \(new\)
* Built-in object with global scope \(window, document, location, console, etc.\)

The `html`, `body`, and `base` elements are not forbidden in the template, but should not be used.



## Reference

#### Ungmo, L. \(2018\). _Angular Essentials._ Gyeonggido Bucheon-si: Rubypaper

