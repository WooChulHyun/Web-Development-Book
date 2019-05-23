# property

## property definition

A property definition is a property that defines the value of a property attribute to manage the state of the property. For example, you can define whether the property value can be writable, property is enumerable, property is configurable.

When creating a property \(Object literal evaluation, Dynamic creation property\), the JavaScript engine automatically defaults to a property attribute that indicates the state of the property.

```javascript
const obj = {};

obj.prop = 10;

const descriptor = Object.getOwnPropertyDescriptor(obj, 'prop');
console.log(descriptor);
// The prop property of the obj object defines 
// the value, writable, enumerable, and configurable attributes.

// {value: 10, writable: true, enumerable: true, configurable: true}
```

Dynamic creation property is create and add a property when the property does not exist, property definition is defines the property attribute. The property attribute indicates the state of the property. The state of a property is the value of the property, the value is writable, enumerable, or configurable.



## Internal slot / method

