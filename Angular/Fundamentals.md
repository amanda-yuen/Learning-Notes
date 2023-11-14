# Angular Fundamentals
https://angular.io/guide/what-is-angular


## Javascript Classes

Recall:
- Class = template for creating objects
- Static properties cannot be directly accessed on instances of the class. Instead, they're accessed on the class itself.
- The constructor method is a special method for creating and initializing an object created with a class. There can only be one special method with the name "constructor" in a class — a SyntaxError is thrown if the class contains more than one occurrence of a constructor method. Use the super keyword to call the constructor of the super class.

Class Declaration 
- temporal dead zone restrictions (if the variable has not been initialized with a value, any attempt to access it throw a ReferenceError. The variable is initialized with a value when execution reaches the code where it was declared. If no initial value was specified with the declaration, it will be initialized as undefined.)
- let/const behave as if they are not hoisted (you cannot use a class before it is declared).
```
class Rectangle {
  constructor(height, width) {
    this.height = height;
    this.width = width;
  }
}
```

Class Expression - class can also have a name
```
const Rectangle = class {
  constructor(height, width) {
    this.height = height;
    this.width = width;
  }
};
```

### Evaluation Order:
1. The `extends` clause - must evaluate to a valid constructor function or null, or a TypeError is thrown.
2. The `constructor` method - substituted with default if not defined
3. The class property keys evaulated in the order of declaration. If the property key is computed, the computed expression is evaluated, with the `this` value set to the `this` value surrounding the class (not the class itself). None of the property values are evaluated yet.
4. Methods and accessors are installed in the order of declaration.
5. The class elements' values are evaluated in the order of declaration: 
    - For each instance field (public or private), its initializer expression is saved. The initializer is evaluated during instance creation.
    - For each static field (public or private), its initializer is evaluated with this set to the class itself, and the property is created on the class.
    - Static initialization blocks are evaluated with this set to the class itself.

## Typescript Fundamentals
TypeScript offers all of JavaScript’s features, and an additional layer on top of these: TypeScript’s type system. For example, JavaScript provides language primitives like string and number, but it doesn’t check that you’ve consistently assigned these. TypeScript does.