# ECMA-SCRIPT-2015 (ES6) Syntax and Feature Overview
The concept principles to be added in javascript 2015 (ES6)

ECMAScript 2015, also known as ES6, introduced many changes to JavaScript. Here is an overview/reference of some of the most common features and syntactical differences, with comparisons to ES5 where applicable.

> **Note:** A commonly accepted practice is to use `const` unless except in cases of loops and reassignment. However, in this resource I'll be using `let` in place of `var` for all ES6 examples.

## Legend

- Variable: `x`
- Object: `obj`
- Array: `arr`
- Function: `func`
- Parameter, method: `a`, `b`, `c`
- String: `str`

## Table of contents

- [Variable declaration](#variable-declaration)
- [Constant declaration](#constant-declaration)
- [Arrow function syntax](#arrow-functions)
- [Template literals](#template-literals)
- [Implicit returns](#implicit-returns)
- [Key/property shorthand](#keyproperty-shorthand)
- [Method definition shorthand](#method-properties-shorthand)
- [Destructuring (object matching)](#destructuring)
- [Array iteration (looping)](#array-iteration-looping)
- [Default parameters](#default-parameters)
- [Spread syntax](#spread-syntax)
- [Classes/constructor functions](#classesconstructor-functions)
- [Inheritance](#inheritance)
- [Modules - export/import](#modules---exportimport)
- [Promises/callbacks](#promisescallbacks)

## Variables and constant feature comparison

I explain the concepts of scope and the differences between `let`, `var`, and `const` in the [Understanding Variables, Scope, and Hoisting in JavaScript](https://www.digitalocean.com/community/tutorials/understanding-variables-scope-hoisting-in-javascript) resource on DigitalOcean. This table provides a brief overview.

| Keyword                                                                                       | Scope          | Hoisting | Can Be Reassigned | Can Be Redeclared |
| --------------------------------------------------------------------------------------------- | -------------- | -------- | ----------------- | ----------------- |
| [`var`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/var)     | Function scope | Yes      | Yes               | Yes               |
| [`let`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let)     | Block scope    | No       | Yes               | No                |
| [`const`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/const) | Block scope    | No       | No                | No                |

## Variable declaration

ES6 introduced the `let` keyword, which allows for block-scoped variables which cannot be hoisted or redeclared.

```js
// ES5
var x = 0;
```

```js
// ES6 
let x = 0;
```

- [MDN Reference: let](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let)

## Constant declaration

ES6 introduced the `const` keyword, which cannot be redeclared or reassigned, but is not immutable.

```js
// ES6
const CONST_IDENTIFIER = 0; // constants are uppercase by convention
```

- [MDN Reference: const](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/const)

## Arrow functions

The arrow function expression syntax is a shorter way of creating a function expression. Arrow functions do not have their own `this`, do not have prototypes, cannot be used for constructors, and should not be used as object methods.

```js
// ES5
function func(a, b, c) {}        // function declaration
var func = function(a, b, c) {}  // function expression
```

```js
// ES6
let func = a => {}         // parentheses optional with one parameter
let func = (a, b, c) => {} // parentheses required with multiple parameters
```

- [MDN Reference: Arrow functions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions)

## Template literals

### Concatenation/string interpolation

Expressions can be embedded in template literal strings.

```js
// ES5
var str = 'Release date: ' + date;
```

```js
// ES6
let str = `Release Date: ${date}`;
```

- [MDN Reference: Expression interpolation](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals#Expression_interpolation)

### Multi-line strings

Using template literal syntax, a JavaScript string can span multiple lines without the need for concatenation. 

```js
// ES5
var str = 'This text ' +
          'is on ' +
          'multiple lines';
```

```js
// ES6
let str = `This text
           is on
           multiple lines`;        
```

- [MDN Reference: Multi-line strings](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals#Multi-line_strings)

## Implicit returns

The `return` keyword is implied and can be omitted if using arrow functions without a block body.

```js
// ES5
function func(a, b, c) { return a + b + c; } 
```

```js
// ES6
let func = (a, b, c) => a + b + c; // curly brackets must be omitted
```

- [MDN Reference: Function body](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions#Function_body)

## Key/property shorthand

ES6 introduces a shorter notation for assigning properties to variables of the same name. 

```js
// ES5
var obj = { 
    a: a, 
    b: b
}
```

```js
// ES6
let obj = { 
    a, 
    b
}
```

- [MDN Reference: Property definitions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Object_initializer#Property_definitions)

## Method definition shorthand

The `function` keyword can be omitted when assigning methods on an object.

```js
// ES5
var obj = {
    a: function(c, d) {},
    b: function(e, f) {}
};
```

```js
// ES6
let obj = {
    a(c, d) {},
    b(e, f) {}
}
```

```js
obj.a(); // call method a
```

- [MDN Reference: Method definitions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Method_definitions)

## Destructuring

Use curly brackets to assign properties of an object to their own variable. 

```js
var obj = { a: 1, b: 2, c: 3 };
```

```js
// ES5
var a = obj.a;
var b = obj.b;
var c = obj.c;
```

```js
// ES6
let {a, b, c} = obj;
```

- [MDN Reference: Object initializer](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Object_initializer#New_notations_in_ECMAScript_2015)

## Array iteration (looping)

A more concise syntax has been introduced for iteration through arrays and other iterable objects.

```js
var arr = ['a', 'b', 'c'];
```

```js
// ES5
for (var i = 0; i < arr.length; i++) {
    console.log(arr[i]);
}
```

```js
// ES6
for (let i of arr) {
    console.log(i);
}
```

- [MDN Reference: for...of](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...of)

## Default parameters

Functions can be initialized with default parameters, which will be used only if an argument is not invoked through the function.

```js
// ES5
var func = function(a, b) {
    b = (b === undefined) ? 2 : b;
    return a + b;
}
```

```js
// ES6
let func = (a, b = 2) => {
    return a + b;
}
```

```js
func(10);   // returns 12
func(10, 5) // returns 15
```

- [MDN Reference: Default paramters](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Default_parameters)

## Spread syntax

Spread syntax can be used to expand an array.

```js
// ES6
let arr1 = [1, 2, 3];
let arr2 = ['a', 'b', 'c'];
let arr3 = [...arr1, ...arr2];

console.log(arr3); // [1, 2, 3, "a", "b", "c"]
```

Spread syntax can be used for function arguments.

```js
// ES6
let arr1 = [1, 2, 3];
let func = (a, b, c) => a + b + c;

console.log(func(...arr1);); // 6 
```

- [MDN Reference: Spread syntax](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax)

## Classes/constructor functions

ES6 introducess the `class` syntax on top of the prototype-based constructor function.

```js
// ES5
function Func(a, b) {
    this.a = a;
    this.b = b;
}

Func.prototype.getSum = function() {
    return this.a + this.b;
}

var x = new Func(3, 4);
```

```js
// ES6
class Func {
    constructor(a, b) {
        this.a = a;
        this.b = b;
    }

    getSum() {
        return this.a + this.b;
    }
}

let x = new Func(3, 4);
```

```js
x.getSum(); // returns 7
```

- [MDN Reference: Classes](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes)

## Inheritance

The `extends` keyword creates a subclass.

```js
// ES5
function Inheritance(a, b, c) {
    Func.call(this, a, b);

    this.c = c;
}

Inheritance.prototype.constructor = Inheritance;
Inheritance.prototype = Object.create(Func.prototype);
Inheritance.prototype.getProduct = function() {
    return this.a * this.b * this.c;
}

var y = new Inheritance(3, 4, 5);
```

```js
// ES6
class Inheritance extends Func {
    constructor(a, b, c) {
        super(a, b);

        this.c = c;
    }

    getProduct() {
        return this.a * this.b * this.c;
    }
}

let y = new Inheritance(3, 4, 5);
```

```js
y.getProduct(); // 60
```

- [MDN Reference: Subclassing with extends](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes#Sub_classing_with_extends)

## Modules - export/import

Modules can be created to export and import code between files.

```html
<!-- index.html -->
<script src="export.js"></script>
<script type="module" src="import.js"></script>
```

```js
// export.js
let func = a => a + a;
let obj = {};
let x = 0;

export { func, obj, x };
```

```js
// import.js
import { func, obj, x } from './export.js';

console.log(func(3), obj, x);
```

- [MDN Reference: export](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/export)
- [MDN Reference: import](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import)

## Promises/Callbacks

Promises represent the completion of an asynchronous function. They can be used as an alternative to chaining functions.

```js
// ES5 callback
function doSecond() {
    console.log('Do second.');
}

function doFirst(callback) {
    setTimeout(function() {
        console.log('Do first.');

        callback();
    }, 500);
}

doFirst(doSecond);
```

```js
// ES6 Promise
let doSecond = () => {
    console.log('Do second.');
}

let doFirst = new Promise((resolve, reject) => {
    setTimeout(() => {
        console.log('Do first.');
        
        resolve();
    }, 500);
});
  
doFirst.then(doSecond);
```

An example below using `XMLHttpRequest`, for demonstrative purposes only ([Fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API) would be the proper modern API to use).

```js
// ES5 callback
function makeRequest(method, url, callback) {
    var request = new XMLHttpRequest();

    request.open(method, url);
    request.onload = function() {
        callback(null, request.response);
    };
    request.onerror = function() {
        callback(request.response);
    };
    request.send();
}

makeRequest('GET', 'https://url.json', function (err, data) {
        if (err) { 
            throw new Error(err);
        } else {
            console.log(data);
        }
    }
);
```

```js
// ES6 Promise
function makeRequest(method, url) {
    return new Promise((resolve, reject) => {
        let request = new XMLHttpRequest();

        request.open(method, url);
        request.onload = resolve;
        request.onerror = reject;
        request.send();
    });
}

makeRequest('GET', 'https://url.json')
.then(event => {
    console.log(event.target.response);
})
.catch(err => {
    throw new Error(err);
});
```

- [MDN Reference](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Using_promises)
