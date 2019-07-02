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

