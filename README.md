# JavaScript Reference

## TOC

- [Data](#data)
- [Basic Operators](#basic-operators)
- [Control Flow](#control-flow)
- [Functions](#functions)
- [Built-In Objects](#built-in-objects)
- [Miscellaneous](#miscellaneous)
- [Programming](#programming)
- [Runtime Environments](#runtime-environments)

## Data

### Variables

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/variables)

#### 💠 Declaration

```js
let a = 1;
let b = 2;
```

or:

```js
let a = 1,
  b = 2;
```

A variable declared with `const` cannot be reassigned

#### 💠 Naming

> 📖 [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Lexical_grammar#keywords)

Varaible name may contain:
- letters (non-latin are not recommended)
- digits (except on the first position)
- select symbols ('$', '_')

Variable name must not be a keyword

Variable name is case-sensitive

Hard-coded values may be stored in uppercase constants:

```js
const COLOR_WHITE = "#FFF";
```

#### 💠 Typing

> [The Modern JavaScript Tutorial](https://javascript.info/types)

Dynamic typing: variable can change its data type

### Data Types

#### Primitives

##### 💠 Number

> 📖 [The Modern JavaScript Tutorial: Data types](https://javascript.info/types)
> 📖 [The Modern JavaScript Tutorial: Numbers](https://javascript.info/number)

Is stored in 64-bit format IEEE-754 (double precision floating point number)

Is stored in a binary form, rounding given number to the nearest possible value, resulting in a loss of precision:

```js
console.log((0.1).toFixed(20)); // "0.10000000000000000555"

// Multiply-and-divide method does not fix the problem:
console.log(((0.1 * 1e2) / 1e2).toFixed(20)); // "0.10000000000000000555"

// It's recommended to cut the 'tail' using toFixed()
```

May have the following values:
- integer (including `0` and `-0`)
- floating point
- `Infinity`
- `-Infinity`
- `NaN` (represents a computational error)

May be written in the following ways:
- `1000000`
- `1_000_000`
- `1e6` (or `1e-6` for the opposite)

Supported non-decimal numeral systems:
- binary (e.g. `0b101010` for `42`)
- octal (e.g. `0o52` for `42`)
- hexadecimal (e.g. (`0x2A` for `42`)

Multiply-and-divide method of rounding a number to float:

```js
console.log(Math.round(1.2345 * 1e2) / 1e2); // 1.23
```

##### 💠 BigInt

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/types)

For values larger than (2<sup>53</sup> - 1) or less than -(2<sup>53</sup> - 1) - that's `9007199254740991` and `-9007199254740991` - to avoid a precision error (not all digits fitting into the 64-bit storage)

Requires adding `n` to the end of the integer

Not supported in Internet Explorer

##### 💠 String

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/types)

Three type of quotes:
- Single
- Double
- Backticks

##### 💠 Boolean

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/types)

Has one of the two values: `true`/`false`

##### 💠 Symbol

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/symbol)

###### Nature

Represents a unique identifier

```js
let id = Symbol("description");
```

Symbol's description doesn't affect anything but is useful for debugging purposes (is accessible via `Symbol('').description`)

Symbols are not automatically converted to strings and in some environments such attempts may result in TypeError (e.g. when using alert())

###### Use in Objects

When used as a property name in an object literal, it must be enclosed in square brackets because it's then passed as a variable

Properties with symbolic names are skipped by `for...in` loops and `Object.keys()` but not by `Object.assign()`

##### 💠 null

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/types)

Represents empty or unknown value

##### 💠 undefined

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/types)

Represent not assigned value

It's recommended to assing `null` instead of `undefined` to a variable

#### Object

##### 💠 Creation Syntax

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/object)

```js
let a = {}; // Object literal

let b = new Object(); // Object contructor
```

##### 💠 Properties

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/object)

###### Naming

In object literal, multiword property names must be placed within quotes

Generally, property name doesn't have to follow the rules for naming variables (can be a keyword, can contain spaces/digits on the first position/special characters) - it can be any string or symbol

Property name of a type other than string/symbol is automatically converted to string (whether used in object literal or square bracket notation)

Property named `__proto__` must have an object for its value

###### Order

Properties which names would be valid integers (after conversion to number) are sorted, while the other properties are kept in creation order

###### Availability

Accessing non-existing property will result in getting `undefined`

`in` operator checks if a property with the given name exists in the object (even if its value is `undefined`)

`delete` operator is used to remove a property

###### Access Notations

The dot notation may be used when property name follows the rules for naming variables (no spaces, no digits on the first position, letters and `$`/`_` allowed) with the exception that the accessed property name may be a keyword

Square bracket notation is used when dot acceess notation doesn't work:
- multiword property names
- property name returned from an expression
- computed properties: property name returned from an expression and used in object literal

##### 💠 Methods

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/object-methods)

###### Syntax

```js
let obj = {
  a: function() {
    ...
  }
}
```

is almost equivalent (with some differencec related to inheritance) to the following:

```js
let obj = {
  a() {
    ...
  }
}
```

###### this Keyword

`this` is used to access the method-calling object

`this` is evaluated at runtime (can be used in functions, not only in object methods)

`this` inside an arrow function is refering to the outer context

When a function is called without an object, the value of `this` is:
- `undefined` when in strinct mode
- global object when not in strinct mode

##### 💠 Property Value Shorthand

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/object#property-value-shorthand)

Used when property name is the same as the property value

```js
function a(b, c) {
  return {
    b,
    c: d
  };
}
```

##### 💠 for...in Loop

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/object#forin)

```js
for (key in obj) {
  ...
}
```

##### 💠 Referencing

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/object-copy)

Variable assigned to an object stores its reference not the object itself

Copying a variable assigne to an object copies the reference

Objects declared with `const` can be modified since `const` applies to the reference

##### 💠 Optional Chaining

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/optional-chaining)

`?.` is not an operator but a syntax construct

`?.` stops the evaluation if the preceeding value is `undefined`/`null` and returns `undefined`

Works only for declared variables

May be used for short-cirtuit evaluations, e.g. `a?.b(c)`

`?.[]` is used when square bracket notation is needed

`?.()` is used to call a function that may not exist

Can be used for reading and deleting property but not for setting property value

Overusing `?.` may result in more difficult debugging, so it should be used only when the existence of the preceding property is optional

### Data Type Operations

#### 💠 The typeof Operator

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/types#type-typeof)

Syntax:
- `typeof x`
- `typeof(x)`

Returns a string

```js
typeof 1 // "number"
typeof 1n // "bigint"
typeof true // "boolean"
typeof "a" // "string"
typeof null // "object" (*)
typeof undefined // "undefined"
typeof Symbol("id") // "symbol"
typeof Math // "object"
typeof alert // "function" (*)

// * Incorrect behavior
```

#### 💠 Type Conversion

> 📖 [The Modern JavaScript Tutorial: Type Conversions](https://javascript.info/type-conversions)
> 📖 [The Modern JavaScript Tutorial: Basic operators, maths](https://javascript.info/operators)

##### String

Value is converted to string automatically when the string form is needed in a function

If one of the operands of the `+` operator is a string, the second one is also converted to a string
- `1 + 1 + '1'` is converted to `'21'`
- `'1' + 1 + 1` is converted to `'111'`

`String(value)`: converts a value to string explicitly

Rules:
- `false` is converted to `"false"`
- `null` is convertet to `"null"`
- etc.

##### Numeric

Value is converted to number automatically in mathematical functions and expressions

Unary `+` operator converts the operand to number

`Number(value)`: converts a value to number explicitly

Rules:
- Strings
  - Whitespace (spaces, `\t`, `\n`, etc.) from the beginning and the end of the string are removed
  - `"10"` is converted to `10`
  - Empty string is converted to `0`
  - String that doesn't represent a valid number is converted to `NaN`
- `true`/`false` is converted to `1`/`0`
- `null` is converted to `0`
- `undefined` is converted to `NaN`

##### Boolean

Value is converted to boolean automatically in logical operations

`!!` operator converts the operand to boolean

`Boolean(value)`: converts a value to boolean explicitly

Rules:
- Numbers
  - `1`/`0` is converted to `true`/`false`
  - `NaN` is converted to `false`
- Strings
  - Empty string is converted to `false`
  - Non-empty string (e.g. `"0"`) is coverted to `true`
- `null` is converted to `false`
- `undefined` is converted to `false`
- Objects are not converted to boolean but are always `true`

## Basic Operators

> 📖 [The Modern JavaScript Tutorial: Basic operators, maths](https://javascript.info/operators)
> 📖 [The Modern JavaScript Tutorial: Comparisons](https://javascript.info/comparison)
> 📖 [The Modern JavaScript Tutorial: Object references and copying](https://javascript.info/object-copy)

### 💠 Comma

Each of the expressions separated with comma is evaluated and the result of the last one is returned, e.g. `(1 + 2, 3 + 4)` returns `7`

`,` has lower precedence than `=` operator

### 💠 Assignment Operator

`=` operator returns the assigned value

Chained assignments are evaluated from right to left.

For each arithmetical and bitwise operator there is a corresponding modify-and-assign operator, e.g. `*=`

### 💠 Increment/Decrement Operator

`++a` returns the new value, while `a++` return the old value

### 💠 Bitwise Operators

Operands are treated as 32-bit integers

Operators:
- AND ( & )
- OR ( | )
- XOR ( ^ )
- NOT ( ~ )
- LEFT SHIFT ( << )
- RIGHT SHIFT ( >> )
- ZERO-FILL RIGHT SHIFT ( >>> )

### 💠 Comparison Operators

Comparison operation returns a boolean

Strings are compared in Unicode order

Values of different types are compared after being converted to numbers - this also applies to regular equality check operator `==` with the exceptions:
- `null == undefined` is true
- `null` and `undefined` does not equal `==` any other value

Values of different types are compared without being converted to numbers when the strict equality operator `===` is used

Objects are compared with other objects or with other types after being converted to primitives

### 💠 Logical Operators

> 📖 [The Modern JavaScript Tutorial: Logical operators](https://javascript.info/logical-operators)
> 📖 [The Modern JavaScript Tutorial: Nullish coalescing operator '??'](https://javascript.info/nullish-coalescing-operator)

#### OR/AND Operators

`||` evaluates operands from left to right, converts each to boolean, and returns the original value of the first truthy operand (returns the last one if all are false); used for:
- getting the first truthy value from a given list
- short-circuit evaluation, e.g. `false || console.log('Ok!')`

`&&` evaluates operands from left to right, converts each to boolean, and returns the original value of the first falsy operand (returns the last one of all are true)

The precedence of `&&` is higher than `||`

It's not recommended to replace `if` statements with `||`/`&&`

#### NOT Operator

`!` converts its operand to bolean and inverts the value

`!!` is used to convert a value to boolean

#### Nullish Coalescing Operator

`??` is used to return the first value that isn't `null`/`undefined` (while in contrast to `||` operator, the value may be `0`, `NaN`, `''`, `false`)

`??` has the same precedence as `||`

It's forbidden to use `??` together with `&&`/`||` without parentheses

## Control Flow

### 💠 Conditionals

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/ifelse)

`if` statement: used when execturing different branches of code

Conditional `?` operator (ternary operator): used when returning one of the two values

`switch` statement: used when comparing different value variants

Equality check in `switch` statemt is strict

Example:

```js
switch(x) {
  case 1:
    ...
    [break;]

  case 2:
    ...
    [break;]

  default:
    ...
    [break;]
}
```

### 💠 Loops

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/while-for)

```js
while (condition) {
  ...
}
```

```js
do {
  ...
} while (condition);
```

```js
for (;;) {
  ...
}
```

### 💠 Control Transfer

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/while-for)

#### Operation

`break` directive breaks the loop

`break` directive combined with an infinite loop is used when the loop condition must be evaluated in the middle instead of the beginning or the end of the loop

`continue` directive break the current iteration of the loop

#### Use Cases

`continue` directive is used to decrease nesting, for example:

```js
while (a) {
  if (b) {
    c();
  }
}
```

may be replaced with:

```js
while (a) {
  if (!b) continue;

  c();
}
```

`break`/`continue` is not allowed to use with the ternary operator `?`

#### Labels

Labels are used to break from a nested loop, for example:

```js
a:
while (b) {
  while (c) {
    if (d) break a;
  }
}
```

`continue` breaks the current iteration of the outer loop

#### Possible Placement

`break` directive must be placed inside a block:

```js
a:
{
  ...
  break a;
}
```

`continue` directive must be placed inside a loop

## Functions

### 💠 Function Declaration

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/function-basics)

```js
function a(b) {
  ...
}
```

Can be called before its declaration

### 💠 Function Expression

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/function-expressions)

```js
let a = function(b) {
  ...
};
```

Can be called only after its creation

Function expressions can be used when a conditional declaration is needed or when a function expression doesn't fit the situation

### 💠 Arrow Function

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/arrow-functions-basics)

```js
let a = (b, c) => {
  return d;
}

let e = (f, g) => h;

let i = j => k;

let l = () => m;
```

Are convenient for simple one-line actions or being used as callbacks

### 💠 Returned Value

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/function-basics)

`return;` or no `return` at all effects in returning `undefined`

JavaScript assumes a semicolon after `return`, so it's not possible to place the returned value in a new line

## Built-In Objects

### General

#### 💠 Constructors

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/primitives-methods)

Constructors (functions called with `new`) for `Number`/`String`/`Boolean` objects are for internal use only

```js
console.log(new Number(0) ? 1 : 2); // 1
```

### Object

#### 💠 Cloning

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/object-copy)

`Object.assign(target, ...sources)` returns modified `target` (now containing copied properties from all the sources; object properties are copied by reference)

### Number

#### 💠 General

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/number#tostring-base)

To call a method dorectly on a number, `..` must be used

```js
console.log(255..toString(16)); // ff
```

#### 💠 Numeral System Conversion

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/number#tostring-base)

```js
console.log((255).toString(16)); // ff
```

#### 💠 Rounding to Float

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/number#rounding)

```js
console.log((1.2345).toFixed(2)); // "1.23" (string)
```

### Symbol

#### 💠 Global Symbol Registry

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/symbol#global-symbols)

Global symbol registry allow to create an access global symbols (accessible from anywhere in the code) with unique desccriptions

`Symbol.for(descriptionString)` is used to access (or create when absent) 

### Math

#### 💠 Rounding to Integer

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/number#rounding)

```js
console.log(Math.floor(1.5), Math.floor(-1.5)); // 1, -2
console.log(Math.ceil(1.5), Math.ceil(-1.5)); // 2, -1
console.log(Math.round(1.5), Math.round(-1.5)); // 2, -1
console.log(Math.trunc(1.5), Math.trunc(-1.5)); // 1, -1
```

## Miscellaneous

### 💠 ES5 & 'use strict'

#### Usage

> 📖 [The Modern JavaScript Tutorial: The modern mode, "use strict"](https://javascript.info/strict-mode)

`'use strict'` enables modifications introduced in ES5

Must be placed at the beginning of a script or a function

Used in classes and modules by default

Not used in the browser console by default

#### Effects

##### Variable Declaration

> 📖 [The Modern JavaScript Tutorial: Variables](https://javascript.info/variables#variable-naming)

Forces variable declaration, as it's possible to simply assign a value without a declaration when not using `'use strict'`:

```js
a = 1;
```

##### Function Declaration

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/function-expressions#function-expression-vs-function-declaration)

Makes the function visible only within the block scope in which it was declared

##### this Value

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/object-methods#this-is-not-bound)

When a function is called without an object, the value of `this` is:
- `undefined` when in strinct mode
- global object when not in strinct mode

### 💠 Automatic semicolon insertion

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/structure#semicolon)
> 
> 📖 [ECMA-262](https://tc39.es/ecma262/#sec-automatic-semicolon-insertion)

Occurs an a line break in most cases

#### Example Exception #1

```js
a = b + c
(d + e).f()
```

is transformed into:

```js
a = b + c(d + e).f()
```

#### Example Exception #2

```js
a()
[b, c].d()
```

is transformed into:

```js
a()[b, c].d()
```

## Programming

### OOP

#### 💠 Constructor Function

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/constructor-new)

The first letter of the function name must by capital

Should be executed with the `new` operator

When executing with the `new` operator, parentheses may be omitted, but it's not a good practice

Does not have the `return` statement as it returns `this`

If there is `return` statement then it returns:
- object called with `return`
- `this` if `return` is not calling an object

```js
function Abc() {
  this.d = e;
  this.f = g;
}

let abc = new Abc();
```

`new.target` is sometimes used to test whether the function was called with `new` by returning:
- `undefined` if the function was called without `new`
- the function itself if it was called with `new`

```js
function Abc() {
  if (!new.target) {
    return new Abc();
  }

  this.a = b;
}

let abc = Abc();
```

### Design Patterns

#### Miscellaneous

##### 💠 Immediately Invoked Function Expression (IIFE)

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/constructor-new#constructor-function)

```js
let abc = new function() {
  ...
}
```

Used when performing complex initialization for a single object to keep the code organized and to avoid polluting the global scope with temporary variables or functions

##### 💠 Symbol-Based Encapsulation

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/symbol#hidden-properties)

Used for third-party code objects when it's unsafe to add properties to them in danger of affecting pre-defined behavior

##### 💠 Private Members

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/symbol#hidden-properties)

Used when exposing object to scripts which may add their own properties

## Runtime Environments

### Browser

#### 💠 Execution

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/hello-world#the-script-tag)

```html
<!DOCTYPE html>
<html>
  <body>
    <p>Paragraph before</p>
    <script>
      console.log("Script");
    </script>
    <p>Paragraph after</p>
  </body>
</html>
```

`type="text/javascript"`: Not required anymore (was required in HTML4)

`<script language=…>`: Not used anymore (JavaScript has become the default language)

`<script type="text/javascript"><!-- ... //--></script>`: Hid the code from browsers that didn't support the `<script>` tag

`src` attribute: Allows loading external scripts (from a file/URL) that will be cached by the browser; the `<script>` content is ignored when `src` is set

#### 💠 Global Objects

#### window

##### Instance Methods

###### Modal Window

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/alert-prompt-confirm)

`alert(string)`:
- displays a message in a modal window with 'Ok' button
- returns `undefined`

`prompt(string, [optionalDefaultInputFieldValue])`:
- Internet Explorer inserts `'undefined'` in the input field when no parameter is provided, so it's good to provide an empty string `prompt(string, '')`
- displays a message in a modal window with 'Ok' and 'Cancel' buttons
- returns input field's value or `null`

`confirm(string)`:
- displays a message in a modal window with 'Ok' and 'Cancel' buttons
- return `true` or `false`
