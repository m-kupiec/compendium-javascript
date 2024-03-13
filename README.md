# JavaScript Reference

## TOC

- [Data](#data)
- [Basic Operators](#basic-operators)
- [Control Flow](#control-flow)
- [Functions](#functions)
- [Classes](#classes)
- [Scope](#scope)
- [Built-In Objects](#built-in-objects)
- [Miscellaneous](#miscellaneous)
- [Programming](#programming)
- [Runtime Environments](#runtime-environments)

## Data

### Variables

> 📖 [The Modern JavaScript Tutorial: Variables](https://javascript.info/variables)
>
> 📖 [The Modern JavaScript Tutorial: The old "var"](https://javascript.info/var)

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

A varable declared with `var` can be redeclared:

```js
var a = 1;
var a = 2;

console.log(a); // 2
```

`var` declarations (without the assignment) are hoisted (raised) to the top of the function or global script:

```js
console.log(a); // undefined (declared but not yet assigned)

var a = 1;
```

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

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/types)

Dynamic typing: variable can change its data type

### Data Types

#### Primitives

##### 💠 Number

> 📖 [The Modern JavaScript Tutorial: Data types](https://javascript.info/types)
> 
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
- `NaN` (represents a computational error; `NaN !== NaN`)

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

> 📖 [The Modern JavaScript Tutorial: Data types](https://javascript.info/types)
> 
> 📖 [The Modern JavaScript Tutorial: Strings](https://javascript.info/string)
> 
> 📖 [The Modern JavaScript Tutorial](https://javascript.info/destructuring-assignment#array-destructuring)

Is stored in UTF-16 format

Three type of quotes:
- Single
- Double
- Backticks
  - Used for template literals `${…}` and tagged templates (a string and ebmbedded expressions being processed by a function)
  - Allow multiline strings

Special characters:
- `\n`: new line
- `\t`: new line
- `\`: special character escaping

Accessing char at an non-found index results in `undefined`

Is immutable (characters cannot be changed)

String destructuring assignment:

```js
let [a, b, c] = "123";

console.log(a, b, c); // "1" "2" "3"
```

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

> 📖 [The Modern JavaScript Tutorial: Object methods, "this"](https://javascript.info/object-methods)
>
> 📖 [The Modern JavaScript Tutorial: Arrow functions revisited](https://javascript.info/arrow-functions)

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

##### 💠 Destructuring Assignment

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/destructuring-assignment)

```js
const {
  cVal,
  aVal: a,
  dVal: d = Math.random().toFixed(),
  ...more
} = {
  aVal: 1,
  bVal: 2,
  cVal: 3,
  eMore: 5
};

let x, y;
({x, y} = {x: 1, y: 2}); // Expression wrapped in parentheses to avoid treating {x, y} as a code block

console.log(a, cVal, d, more); // 1 3 "1" [object Object] { bVal: 2, eMore: 5 }
console.log(x, y);
```

Nested destructuring:

```js
const {
  a: {
    a1,
    a2
  },
  b
} = {
  a: {
    a1: 1,
    a2: 2
  },
  b: 3
};

// console.log(a); // ReferenceError: a is not defined
console.log(a1, a2, b); // 1, 2, 3
```

##### 💠 `for...in` Loop

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/object#forin)

```js
for (key in obj) {
  ...
}
```

Inherited properties are included:

```js
const obj1 = { a: 1 };
const obj2 = { b: 2, __proto__: obj1 };

for (let key in obj2) {
  console.log(`${key}: ${obj2[key]}`); // "b: 2" "a: 1"
}
```

##### 💠 Referencing

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/object-copy)

Variable assigned to an object stores its reference not the object itself

Copying a variable assigne to an object copies the reference

Objects declared with `const` can be modified since `const` applies to the reference

##### 💠 Copying

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/rest-parameters-spread#copy-an-array-object)

An object may be copied (in a non-nested way) using spread syntax:

```js
console.log({...{ a: 1, b: 2, c: 3 }}); // [object Object] { a: 1, b: 2, c: 3 }
```

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

##### 💠 Property Descriptor

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/property-descriptors)

Each property has three attributes ("flags"), all set to `true` by default:
- `writable` (specifying if the property value can be changed)
- `enumerable` (specifying if the property is to be listed in loops)
- `configurable` (specifying if the property can be deleted or its attributes modified)
  - it does not affect the possibility to change the property value which is regulated by the `writable` attribute
  - even if set to `false`, it still allows to change `writable` from `true` to `false` (only in this direction) to strengthen security

##### 💠 Accessor Properties

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/property-accessors)

Accessor properties are functions that execute on getting or setting a data property value

```js
const obj = {
  a: 1,
  b: 2,
  
  get ab() {
    return this.a + this.b;
  },
  
  set ab(value) {
    this.a = String(value)[0];
    this.b = String(value).slice(1);
  }
};

console.log(obj.ab); // 3
obj.ab = 345;
console.log(obj.a, obj.b); // "3" "45"
```

Accessor property has no `value` (and in consequence no `writable`), but does have `get` and `set` (in addition to `enumerable` and `configurable`)

##### 💠 Prototypal Inheritance

> 📖 [The Modern JavaScript Tutorial: Prototypal inheritance](https://javascript.info/prototype-inheritance)
>
> 📖 [The Modern JavaScript Tutorial: Native prototypes](https://javascript.info/native-prototypes)
>
> 📖 [The Modern JavaScript Tutorial: Prototype methods, objects without __proto__](https://javascript.info/prototype-methods#brief-history)

`[[Prototype]]` is a hideen property that either references to another object (the prototype) or is `null`

`__proto__` is an outdated (moved to Annex B - optional for non-browser environments) getter/setter for `[[Prototype]]` (it's preferable to use `Object.getPrototypeOf`/`Object.setPrototypeOf` instead)

Since 2022 is it allowed to used `__proto__` in object literals

Changing `[[Prototype]]` of existing objects is a very slow operation; `[[Prototype]]` usually should be set at the time of object creation

```js
const obj1 = { a: 1 };
const obj2 = { b: 2 };

obj2.__proto__ = obj1;
console.log(obj2); // [object Object] { a: 1, b: 2 }
```

Assigning `__proto__` in a circle will result in error

`__proto__` can be assigned either an object or `null`, as other assignments are ignored:

```js
const obj1 = { a: 1 };
const obj2 = { b: 2 };

obj2.__proto__ = 3;
console.log(obj2); // [object Object] { b: 2 }
```

All objects inherit from `Object.prototype`; the value of `[[Prototype]]` for `Object.prototype` is `null`:

```js
const obj = {};

console.log(obj.__proto__ === Object.prototype); // true
console.log(obj.toString === Object.prototype.toString); // true
console.log(obj.toString === Object.prototype.toString); // true

console.log(Object.prototype.__proto__); // null
```

Assigning value to a non-existing property (which does exist in the prototype) will result in adding this property to the immediate object (not the prototype) as long as accessor properties are not used:

```js
const obj1 = {
  a: 1,
  
  set b(val) {
    this._b = val;
  },
  
  get b() {
    return this._b;
  }
};

const obj2 = {
  __proto__: obj1
};

console.log(obj1); // [object Object] { a: 1, b: undefined }
console.log(obj2); // [object Object] { a: 1, b: undefined }

obj2.a = 0;
console.log(obj1); // [object Object] { a: 1, b: undefined }
console.log(obj2); // [object Object] { a: 0, b: undefined }

obj2.b = 2;
console.log(obj1); // [object Object] { a: 1, b: undefined }
console.log(obj2); // [object Object] { _b: 2, a: 0, b: 2 }
```

Between the prototype and the inheriring object, methods are shared but the state is not:

```js
const obj1 = {
  _a: 1,
  
  set a(val) {
    this._a = val;
  },
  
  get a() {
    return this._a;
  }
};

const obj2 = {
  __proto__: obj1
};

console.log(obj1); // [object Object] { _a: 1, a: 1 }
console.log(obj2); // [object Object] { _a: 1, a: 1 }

obj2.a = 0;
console.log(obj1); // [object Object] { _a: 1, a: 1 }
console.log(obj2); // [object Object] { _a: 0, a: 0 }
```

### Data Type Operations

#### 💠 `typeof` Operator

> 📖 [The Modern JavaScript Tutorial: Data types](https://javascript.info/types#type-typeof)
>
> 📖 [The Modern JavaScript Tutorial: Class checking: "instanceof"](https://javascript.info/instanceof#bonus-object-prototype-tostring-for-the-type)

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

When `typeof` is not sufficient, `Object.prototype.toString` can display the type of primitives, objects with Symbol.toStringTag, and built-in objects

#### 💠 Type Conversion

> 📖 [The Modern JavaScript Tutorial: Type Conversions](https://javascript.info/type-conversions)
> 
> 📖 [The Modern JavaScript Tutorial: Basic operators, maths](https://javascript.info/operators)
>
> 📖 [The Modern JavaScript Tutorial: Arrays](https://javascript.info/array)

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

`[1, 2, 3]` is converted to `"1,2,3"`

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

##### Type-Coercion Side-Effect

```js
console.log("1" + 2); // "12" (not 3 as intended)
```

### Data Collections

#### Array

> 📖 [The Modern JavaScript Tutorial: Arrays](https://javascript.info/array)
> 
> 📖 [The Modern JavaScript Tutorial: Destructuring assignment](https://javascript.info/destructuring-assignment#array-destructuring)
>
> 📖 [The Modern JavaScript Tutorial: Rest parameters and spread syntax](https://javascript.info/rest-parameters-spread)

Ia a kind of object

```js
let arr1 = [];
let arr2 = new Array();

let arr3 = [1, 2, 3];
let arr4 = new Array(1, 2, 3);
```

`new Array(n)` creates an array with n `undefined` elements

Accessing array element at an non-found index results in `undefined`

```js
for (el of [1, 2, 3]) {
  console.log(el); // 1 2 3
}
```

Array may be truncated by decreasing `length` property (or cleared by assigning `0` to it)

Array destructuring assignment:

```js
let [a, b = Math.random().toFixed()] = [];
let [name, , surname, ...business] = 'John Albert Doe CEO MicroMedix'.split(' ');

console.log(a, b); // undefined, "1"
console.log(name, surname); // "John" "Doe"
console.log(business); // ["CEO", "MicroMedix"]
```

Arrays may be copied or merged using spread syntax:

```js
console.log([...[1, 2, 3]]); // [1, 2, 3]

console.log([...[1, 2], 3, ...[4, 5]]); // [1, 2, 3, 4, 5]
```

## Basic Operators

> 📖 [The Modern JavaScript Tutorial: Basic operators, maths](https://javascript.info/operators)
> 
> 📖 [The Modern JavaScript Tutorial: Comparisons](https://javascript.info/comparison)
> 
> 📖 [The Modern JavaScript Tutorial: Object references and copying](https://javascript.info/object-copy)
>
> 📖 [The Modern JavaScript Tutorial: Strings](https://javascript.info/string#comparing-strings)
>
> 📖 [The Modern JavaScript Tutorial: Arrays](https://javascript.info/array)

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

Strings are compared according to the UTF-16 order

Values of different types are compared after being converted to numbers - this also applies to regular equality check operator `==` with the exceptions:
- `null == undefined` is true
- `null` and `undefined` does not equal `==` any other value
- `NaN` does not equal `NaN` nor any other value

Values of different types are compared without being converted to numbers when the strict equality operator `===` is used

Objects are compared with other objects or with other types after being converted to primitives

Arrays are compared with other arrays or with other types after being converted to strings:

```js
console.log([] == []); // false
console.log([1, 2] < [3, 4]); // true
console.log([] == 0); // true
console.log([1] == '1'); // true
```

### 💠 Logical Operators

> 📖 [The Modern JavaScript Tutorial: Logical operators](https://javascript.info/logical-operators)
> 
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

### 💠 Named Function Expression (NFE)

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/function-object#named-function-expression)

Allows the function to call itself:

```js
const a = function f(arg) {
  if (arg != undefined) {
    console.log(arg);
  } else {
    f('abc');
  }
}

// f(); // ReferenceError: f is not defined
a(); // "abc"
a('def'); // "def"
```

### 💠 Constructor Function

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/constructor-new)
>
> 📖 [The Modern JavaScript Tutorial: Arrow functions revisited](https://javascript.info/arrow-functions)
>
> 📖 [The Modern JavaScript Tutorial: F.prototype](https://javascript.info/function-prototype)

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

Arrow function cannot be used as a constructor function because of not having `this` but rather taking it from the global Lexical Environment

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

If a constructor function has `prototype` property which value is an object, then this object will be used as the prototype for the object created with the constructor function:

```js
function Abc() {
  this.b = 2;
}

const obj = { a: 1 };

let abc = new Abc();
console.log(abc); // [object Object] { b: 2 }

Abc.prototype = obj;
abc = new Abc();
console.log(abc); // [object Object] { a: 1, b: 2 }
```

Every function has a `prototype` property which value is an object containing only one property (`constructor`) that points to the function itself:

```js
function f() {}

function Abc() {}

console.log(f.prototype.constructor == f); // true
console.log(Abc.prototype.constructor == Abc); // true

let abc = new Abc();
console.log(abc.constructor == Abc); // true

abc = new abc.constructor();
console.log(abc.constructor == Abc); // true
```

`constructor` value is not determined by the language, so the property can be modified:

```js
function Abc() {}

console.log(Abc.prototype.constructor == Abc); // true

let abc = new Abc();
console.log(abc.constructor == Abc); // true

Abc.prototype = {};
abc = new Abc();
console.log(abc.constructor == Abc); // false
```

### 💠 Function Constructor

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/new-function)

Converts strings into a function parameters and body:

```js
const funcBody1 = 'console.log(a * b)';
const funcBody2 = 'console.log(true)';
const f1 = new Function('a', 'b', funcBody1);
const f2 = new Function(funcBody2);

f1(2, 3); // 6
f2(); // true
```

`[[Environment]]` then references the global Lexical Environment

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

### 💠 Destructuring Parameters Object

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/destructuring-assignment#smart-function-parameters)

```js
function f({aVal: a = true, bVal = true} = {}) {
  console.log(a, bVal);
}

f(); // true true
f({aVal: false}); // false true
```

### 💠 Gathering Remaining Parameters

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/rest-parameters-spread)

#### Using `...`

`...` gathers arguments into an array

```js
function f(a, b, ...c) {
  console.log(a, b, c);
}

f(1, 2, 3, 4, 5, 6); // 1 2 [3, 4, 5, 6]
```

`...` must be at the end of the list of parameters

#### Using `arguments`

`arguments` is an array-like object

```js
function f(a, b) {
  console.log(arguments);
}

f(1, 2, 3, 4, 5, 6); // [object Arguments] { 0: 1, 1: 2, 2: 3, 3: 4, 4: 5, 5: 6 }
```

Does not work in arrow functions:

```js
function f(a, b) {
  const arrow = (a, b) => console.log(arguments);
  
  arrow();
}

f(1, 2, 3, 4, 5, 6); // [object Arguments] { 0: 1, 1: 2, 2: 3, 3: 4, 4: 5, 5: 6 }
```

### 💠 Spread Syntax

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/rest-parameters-spread#spread-syntax)

```js
const a = [1, 2, 3];
const b = [7, 8, 9];

console.log(Math.max(0, ...a, 4, 5, 6, ...b)); // 9
```

### 💠 Function Object

> 📖 [The Modern JavaScript Tutorial: Function object, NFE](https://javascript.info/function-object)
>
> 📖 [The Modern JavaScript Tutorial: Function expressions](https://javascript.info/function-expressions#function-is-a-value)

Function is a value that can be printed:

```js
function f(a) {
  alert(a);
}

console.log(f); // function f(a) { alert(a); }
```

`name` of the function/method:

```js
function f() {}

console.log(f.name); // "f"
```

`length` returns the number of function/method parameters:

```js
function f(a, b, ...handlers) {
  for (let handler of handlers) {
    if (handler.length == 0) {
      handler();
    } else {
      handler(a, b);
    }
  }
}

f(2, 3, (a, b) => console.log(a * b), () => console.log(0)); // 6 0
```

Custom properties may be added as well:

```js
function f() {
  f.a = f.a != undefined ? f.a + 1 : 0;
}

console.log(f.a); // undefined
f();
console.log(f.a); // 0
f();
console.log(f.a); // 1
```

## Classes

### 💠 Definition

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/class)

There's no comma between class methods

`new` calls `constructor` method

`class` creates a function:
- the function name is taken from the class name
- the function code is taken from `contructor` method
- the function stores class methods in `prototype`

```js
class Cl {
  
  constructor(a) {
    this.a = a;
  }
  
  f() {
    alert(this.a);
  }

}
  
const cl = new Cl(1);
cl.f(); // 1

console.log(typeof Cl); // "function"
console.log(Cl === Cl.prototype.constructor); // true
console.log(Cl.prototype.f); // f() { alert(this.a); }
console.log(Object.getOwnPropertyNames(Cl.prototype)); // ["constructor", "f"]
```

`class` syntax can be rewritten in the following way:

```js
class Cl1 {
  
  constructor(a) {
    this.a = a;
  }
  
  f() {
    console.log(this.a);
  }

}
  
const cl1 = new Cl1(1);
cl1.f(); // 1

// ---
// Rewritten without using `class` syntax:
// ---

function Cl2(a) {
  this.a = a;
}

Cl2.prototype.f = function() {
  console.log(this.a);
}

const cl2 = new Cl2(1);
cl2.f(); // 1
```

The relationship between a class and its instance is that of an object that inherits properties and methods from the class:

```js
class Cl {
  constructor(a) {
    this.a = a;
  }
  
  f() {}
}

const cl = new Cl(1);

console.log(cl); // [object Object] { a: 1 }
console.log(cl.__proto__ === Cl.prototype); // true
console.log(cl.__proto__.constructor === Cl); // true
console.log(cl.__proto__.constructor === Cl.prototype.constructor); // true
console.log(cl.__proto__.f === cl.f); // true
console.log(cl.__proto__.f === Cl.prototype.f); // true
```

However, `class` is not just a 'syntactic sugar' for defining constructor function together with its `prototype` methods:
- the function created using `class` syntax has an internal `[[IsClassConstructor]]` property set to `true` which requires the function to be called with `new` (among other things)
- all class methods are non-enumerable
- class uses strict mode
- there are also many other features brought by the `class` syntax

### 💠 Class Expression

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/class#class-expression)

```js
let Cl = class {
  constructor(a) {
    this.a = a;
  }
};

let cl = new Cl(1);
console.log(cl); // [object Object] { a: 1 }
```

In named class expressions, the class name is visible inside the body:

```js
let Cl1 = class Cl2 {
  f() {
    alert(Cl2);
  }
};

let cl1 = new Cl1(1);

cl1.f();
/*
class Cl2 {
  f() {
    alert(Cl2);
  }
};
*/
```

Classes can be also made dynamically:

```js
function f() {
  return class {
    g(a) {
      console.log(a);
    }
  }
}

const Cl = f();
const cl1 = new Cl();

cl1.g(1); // 1
```

### 💠 Getters/Setters

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/class#getters-setters)

```js
class Cl {
  get a() {
    return this._a;
  }
  
  set a(val) {
    this._a = val;
  }
}

const cl = new Cl();
cl.a = 1;
console.log(cl.a); // 1
```

Getters and setters are created in the class `prototype`

### 💠 Computed Method Name

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/class#computed-names)

```js
class Cl {
  ['a' + 'b'](c) {
    console.log(c);
  }
}

const cl = new Cl();

cl.ab(1); // 1
```

### 💠 Class Fields

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/class#class-fields)

Class fields are not set in the `prototype` but on the individual objects:

```js
class Cl {
  a = 1;

  f() {
    console.log(this.a);
  }
}

const cl = new Cl();

console.log(cl); // [object Object] { a: 1 }
cl.f(); // 1
```

This allows to define methods (using `f = () => {...}`) that will not loose `this` when passed as callbacks to another context:

```js
class Cl1 {
  constructor(a) {
    this.a = a;
  }

  f() {
    console.log(this.a);
  }
}

class Cl2 {
  constructor(a) {
    this.a = a;
  }
  
  f = function() {
    console.log(this.a);
  }
}

class Cl3 {
  constructor(a) {
    this.a = a;
  }
  
  f = () => {
    console.log(this.a);
  }
}

const cl1 = new Cl1(1);
const cl2 = new Cl2(1);
const cl3 = new Cl3(1);

setTimeout(cl1.f); // undefined
setTimeout(cl2.f); // undefined
setTimeout(cl3.f); // 1
```

### 💠 Class Inheritance

> 📖 [The Modern JavaScript Tutorial: Class inheritance](https://javascript.info/class-inheritance)
>
> 📖 [The Modern JavaScript Tutorial: Extending built-in classes](https://javascript.info/extend-natives)
>
> 📖 [The Modern JavaScript Tutorial: Class checking: "instanceof"](https://javascript.info/instanceof)

#### Extending Classes

In the example below, `B.prototype.[[Prototype]]` is `A.prototype`:

```js
class A {
  a() {
    console.log("A");
  }
}

class B extends A {}

const b = new B();

b.a(); // "A"

console.log(B.prototype.__proto__ === A.prototype); // true
```

`extends` works with expressions as well (useful in design patterns where classes are generated by functions):

```js
class A {
  a() {
    console.log("A");
  }
}

class B extends (function() { return A; })() {}

const b = new B();

b.a(); // "A"

console.log(B.prototype.__proto__ === A.prototype); // true
```

#### Extending Built-In Classes

When extendin built-in classes, their methods (like `filter`, `map`, etc.) use the inherited class object constructor for createing the returned object:

```js
class MyArray extends Array {
  f() {
    return this.map(el => '*');
  }
}

const myArr = new MyArray(3).fill(true);
const newArr = myArr.filter(() => true);

console.log(newArr.constructor === MyArray); // true
console.log(newArr.__proto__ === MyArray.prototype); // true
console.log(newArr.f()); // ["*", "*", "*"]
```

This can be modified using `Symbol.species` static getter which returns the constructor to be used for new object creation:

```js
class MyArray extends Array {
  static get [Symbol.species]() {
    return Array;
  }

  f() {
    return this.map(el => '*');
  }
}

const myArr = new MyArray(3).fill(true);
const newArr = myArr.filter(() => true);

console.log(newArr.constructor === MyArray); // false
console.log(newArr.__proto__ === MyArray.prototype); // false
// console.log(newArr.f()); // ["*", "*", "*"] // TypeError: newArr.f is not a function

console.log(newArr.constructor === Array); // true
console.log(newArr.__proto__ === Array.prototype); // true
```

#### Overriding/Extending Methods

```js
class A {
  f() {
    console.log("A");
  }
  
  g() {
    console.log("A.g");
  }
}

class B extends A {
  f() {
    console.log("B");
  }
}

class C extends A {
  f() {
    super.f();
    console.log("C");
    super.g();
    this.g();
  }
  
  g() {
    console.log("C.g");
  }
}

const a = new A();
const b = new B();
const c = new C();

a.f(); // "A"
b.f(); // "B"
c.f(); // "A" "C" "A.g" "C.g"
```

#### Using `super` in Arrow Functions

```js
class A {
  f() {
    console.log("A");
  }
}

class B extends A {
  f() {
    setTimeout(() => super.f());
    console.log("B");
  }
  
  g() {
    // setTimeout(function() { super.f(); }); // SyntaxError: 'super' keyword unexpected here
    console.log("B");
  }
}

const b = new B();

b.f(); // "B" "A"
```

#### Overriding/Extending Contructor

A default constructor is created when a class extending another class has none:

```js
constructor(...args) {
  super(...args);
}
```

Inheriting class contructor has an internal `[[ConstructorKind]]` property set to `"derived"`, so when it is executed with `new`, it doesn't assign an empty object to `this` (as is done with regular functions executed with `new`) but leaves this job to the base class constructor; that's why it must call `super` (to create the object for `this`) and do this before using `this`:

```js
class A {
  constructor(a) {
    this.a = a;
  }
}

class B extends A {
  constructor(a) {
    super(a);
  }
}

const b = new B(1);

console.log(b); // [object Object] { a: 1 }
```

#### Overriding Class Fields

In the parent class, fields are initialized before constructor; however, in an inheriting classes, fields are initialized immediately after `super()`; that's why the parent class constructor uses its own fields (not the overriding ones) but still uses overriding methods:

```js
class A {
  val = "A";

  constructor() {
    console.log(this.val);
    this.f();
  }

  f() {
    console.log("f: A");
  }
}

class B extends A {
  val = "B";
  val2 = "B2";

  constructor() {
    super();
    console.log(this.val2);
  }

  f() {
    console.log("f: B");
  }
}

class C extends B {
  val = "C";
  val2 = "C2";

  f() {
    console.log("f: C");
  }
}

new A(); // "A" "f: A"
new B(); // "A" "f: B" "B2"
new C(); // "A" "f: C" "B2"
```

The above situation occurs only when fields are used by the parent class constructor; it can be "fixed" by using methods or accessor properties instead of fields:

```js
class A {
  val = "A";

  f() {
    console.log(this.val);
    console.log("f: A");
  }
}

class B extends A {
  val = "B";
  val2 = "B2";

  f() {
    console.log(this.val);
    console.log("f: B");
    console.log(this.val2);
  }
}

class C extends B {
  val = "C";
  val2 = "C2";

  f() {
    console.log(this.val);
    console.log("f: C");
    console.log(this.val2);
  }
}

(new A()).f(); // "A" "f: A"
(new B()).f(); // "B" "f: B" "B2"
(new C()).f(); // "C" "f: C" "C2"
```

#### Checking Class Instance

`instanceof` operator take inheritance into account:

```js
class A {}
class B extends A {}
class C extends B {}

const a = new A();
const b = new B();
const c = new C();

console.log(a instanceof A); // true
console.log(b instanceof A); // true
console.log(c instanceof A); // true
console.log(b instanceof B); // true
console.log(c instanceof B); // true
console.log(c instanceof C); // true

console.log(A.prototype.isPrototypeOf(a)); // true
console.log(A.prototype.isPrototypeOf(b)); // true
console.log(A.prototype.isPrototypeOf(c)); // true
console.log(B.prototype.isPrototypeOf(b)); // true
console.log(B.prototype.isPrototypeOf(c)); // true
console.log(C.prototype.isPrototypeOf(c)); // true
```

Checking rules may be modified using `Symbol.hasInstance` static method:

```js
class A {
  static [Symbol.hasInstance](obj) {
    return Boolean(obj.f);
  }
}
class B extends A {}
class C extends B { f() {} }

const a = new A();
const b = new B();
const c = new C();

console.log(a instanceof A); // false
console.log(b instanceof A); // false
console.log(c instanceof A); // true
console.log(b instanceof B); // false
console.log(c instanceof B); // true
console.log(c instanceof C); // true
```

### 💠 Static Properties and Methods

> 📖 [The Modern JavaScript Tutorial: Static properties and methods](https://javascript.info/static-properties-methods)
>
> 📖 [The Modern JavaScript Tutorial: Extending built-in classes](https://javascript.info/extend-natives#no-static-inheritance-in-built-ins)

#### Static Methods

Static methods are such that do not belong to particular class objects but rather to the whole class itself:

```js
class Abc {
  constructor(val) {
    this.val = val;
  }
  
  static f(a, b) {
    return +a.val - +b.val;
  }
}

const objA = new Abc(1);
const objB = new Abc(2);

console.log(Abc.f(objA, objB)); // -1
console.log(objA.f); // undefined
```

Static methods may be used as factory methods or for executing database operations (search, save, remove)

#### Static Properties

```js
class Cl {
  a = 1;
  static b = 2;
}

const cl = new Cl();

console.log(cl.a); // 1
console.log(cl.b); // undefined

console.log(Cl.a); // undefined
console.log(Cl.b); // 2

Cl.c = 3;
console.log(Cl.c); // 3
```

#### Static Properties/Methods Inheritance

Static properties/methods are inherited

```js
class Abc {
  constructor(val) {
    this.val = val;
  }
  
  static f(a, b) {
    return +a.val - +b.val;
  }
}

class Def extends Abc {}

const objA = new Abc(1);
const objB = new Abc(2);

console.log(Abc.f(objA, objB)); // -1
console.log(Def.f(objA, objB)); // -1
```

This does not apply to built-in objects for which static fields are not inherited:

```js
console.log(Array.prototype.__proto__ === Object.prototype); // true
console.log(Object.keys); // function keys() { [native code] }
console.log(Array.keys); // undefined
```

### 💠 Public, Protected, and Private Properties/Methods

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/private-protected-properties-methods)

Public fields are accessible from anywhere; protected fields are accessible only inside the class and the inheriting classes; private fields are accessible only inside the class

Protected fields are emulated in JavaScript usually by prefixing their names with `_`

A property can be made "read-only" (with value set at the time of creation):
- by providing a getter without a corresponding setter (shorter syntax), or
- by providing getter/setter methods (e.g. getValue, setValue; allows to pass multiple arguments)

Private fields names are prefixed with `#`; `this['#fieldName']` syntax is not supported for private fields

## Scope

> 📖 [The Modern JavaScript Tutorial: Variable scope, closure](https://javascript.info/closure)
>
> 📖 [The Modern JavaScript Tutorial: The old "var"](https://javascript.info/var)

### 💠 Global/Block/Function Scope

```js
{
  let a = 1;
  console.log(a); // 1
}

// console.log(a); // ReferenceError: a is not defined
```

`var` is not restricted by a code block (conditionals, loops), but by a function it is:

```js
function f() {
  {
    var a = 0;
  }
  
  console.log(a);
}

f(); // 0
// console.log(a); // ReferenceError: a is not defined
```

### 💠 Lexical Environment

Every running scope (global, block, function) has its associated Lexical Environment (theoretical object existing in the specification) which consists of:
- `Environment Record` object: stores local variables, `this`, and local function declarations as its properties
- Reference to the outer lexical environment

Lexical Envirnonment is cleaned from memory by the garbage collector when it becomes unreachable

### 💠 Closure

Returned nested functions retain access to their outer variables, because in a hidden `[[Environment]]` property they store reference to the Lexical Environment in which these nested functions were created

Variables are stored and updated in their corresponding Lexical Environments

```js
function f1() {
  let a = 0;
  
  return function() {
    console.log(a++);
  }
}

const f2 = f1();

f2(); // 0
f2(); // 1
```

All functions in JavaScript (if not created with `new`) are closures, i.e. they remember where they were created and can access their outer variables

## Built-In Objects

### General

#### 💠 Constructors

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/primitives-methods)

Constructors (functions called with `new`) for `Number`/`String`/`Boolean` objects are for internal use only

```js
console.log(new Number(0) ? 1 : 2); // 1
```

#### 💠 Inheritance

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/native-prototypes)

```js
console.log(Function.prototype.__proto__ === Object.prototype); // true
console.log(Number.prototype.__proto__ === Object.prototype); // true
console.log(String.prototype.__proto__ === Object.prototype); // true
console.log(Array.prototype.__proto__ === Object.prototype); // true
// ...
```

#### 💠 Native Prototype Modification

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/native-prototypes#native-prototype-change)

Modifying native prototypes is recommended only when creating polyfills:

```js
if(!String.prototype.abc) {
  String.prototype.abc = function() {
    return `abc_${this}`;
  };
}

console.log("def".abc()); // "abc_def"
```

### Global Object

#### 💠 General

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/global-object)

`globalThis` is a standarized name for the global object (`window` in a browser or `global` in Node.js)

Function declarations and global functions/variables declared with `var` become methods/properties of the global object (not applicable in modules)

It is also possible to add a property to the global object directly:

```js
window.a = {b: 1};

console.log(window.a.b); // 1
console.log(a.b); // 1
```

It is used to test modern language features support and to create polyfills:

```js
if (!window.Promise) {
  console.log("Promise is not supported - Creating polyfill..");
  
  // window.Promise = ... // Polyfill implementation
}
```

#### 💠 Testing Numbers

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/number#tests-isfinite-and-isnan)

`isNaN(value)` tests if the value converted to number is `NaN`:

```js
console.log(isNaN("a")); // true
```

`isFinite(value)` tests if the value converted to number is not `NaN`/`Infinity`/`-Infinity`:

```js
console.log(isFinite("1")); // true
```

#### 💠 Extracting Number

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/number#parseint-and-parsefloat)

```js
console.log(parseInt("1 USD")); // 1
console.log(parseFloat("1.5 USD")); // 1.5

console.log(parseInt("$1")); // NaN
console.log(parseFloat("$1.5")); // NaN

console.log(parseInt("0xff")); // 255
console.log(parseInt("111", 2)); // 7
```

### Object

#### 💠 Comparison

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/number#tests-isfinite-and-isnan)
> 
> 📖 [ECMA-262](https://tc39.es/ecma262/#sec-samevalue)

Comparison using `Object.is` differs from strict comparison `===` in two edge cases:

```js
console.log(Object.is(NaN, NaN)); // true
console.log(Object.is(0, -0)); // false
```

#### 💠 Accessing Property Descriptors

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/property-descriptors)

Property desciptor (an object containing the property value and its all flags) can be get using `Object.getOwnPropertyDescriptor()` while all descriptors can be get using `Object.getOwnPropertyDescriptors`

Flags can be changed using `Object.defineProperty()` or `Object.defineProperties()`

```js
let obj = {
  a: 1,
  b: 2
};

console.log(Object.getOwnPropertyDescriptor(obj, 'a'));
/*
[object Object] {
  configurable: true,
  enumerable: true,
  value: 1,
  writable: true
}
*/

Object.defineProperty(obj, 'a', { value: 3, writable: false });
console.log(Object.getOwnPropertyDescriptor(obj, 'a'));
/*
[object Object] {
  configurable: true,
  enumerable: true,
  value: 3,
  writable: false
}
*/

Object.defineProperties(obj, {
  b: { value: -2, writable: false },
  c: { value: 4, writable: true }
});
console.log(Object.getOwnPropertyDescriptors(obj));
/*
[object Object] {
  a: [object Object] {
    configurable: true,
    enumerable: true,
    value: 3,
    writable: false
  },
  b: [object Object] {
    configurable: true,
    enumerable: true,
    value: -2,
    writable: false
  },
  c: [object Object] {
    configurable: false,
    enumerable: false,
    value: 4,
    writable: true
  }
}
*/
```

Property created using `Object.defineProperty()` has all the flags set to `false` by default:

```js
let obj = {
  a: 1,
  b: 2
};

Object.defineProperty(obj, 'c', { value: 3 });
console.log(Object.getOwnPropertyDescriptor(obj, 'c'));
/*
[object Object] {
  configurable: false,
  enumerable: false,
  value: 3,
  writable: false
}
*/
```

#### 💠 Cloning

> 📖 [The Modern JavaScript Tutorial: Object references and copying](https://javascript.info/object-copy)
>
> 📖 [The Modern JavaScript Tutorial: Symbol type](https://javascript.info/symbol#symbols-are-skipped-by-for-in)
>
> 📖 [The Modern JavaScript Tutorial: Property flags and descriptors](https://javascript.info/property-descriptors#object-getownpropertydescriptors)
>
> 📖 [The Modern JavaScript Tutorial: Prototype methods, objects without __proto__](https://javascript.info/prototype-methods)

Method #1: `Object.assign(target, ...sources)` returns modified `target` (now containing copied properties from all the sources; both string and symbol properties are copied; object properties are copied by reference; non-enumerable, accessor, and `[[Prototype]]` properties are not copied)

Method #2: Combination of `Object.defineProperties` and `Object.getOwnPropertyDescriptors` allows to copy symbolic, non-enumerable, and accessor properties; includes property attributes; `[[Prototype]]` property is not copied

Method #3: Combination of `Object.create`, `Object.getPrototypeOf`, and `Object.getOwnPropertyDescriptors` allows to copy symbolic, non-enumerable, accessor and `[[Prototype]]` properties; includes property attributes

```js
const id = Symbol("description");
const objProto = { p: 99 };
const obj = {
  a: 1,
  b: 2,
  [id]: 3,
  __proto__: objProto,
  
  get c() {
    return this._c | 0;
  }
};
let clonedObj1 = {};
let clonedObj2 = {};
let clonedObj3 = {};

Object.defineProperty(obj, 'b', { enumerable: false });

// METHOD #1: Object.assign()
//
// Clones accessor and symbolic properties
// Does not clone non-enumerable nor [[Prototype]] properties

Object.assign(clonedObj1, obj);
console.log(Object.getOwnPropertyDescriptors(clonedObj1));
/*
[object Object] {
  a: [object Object] {
    configurable: true,
    enumerable: true,
    value: 1,
    writable: true
  },
  c: [object Object] {
    configurable: true,
    enumerable: true,
    value: 0,
    writable: true
  }
}
*/
console.log(clonedObj1[id]); // 3
console.log(clonedObj1.__proto__); // [object Object] { ... }

// METHOD #2: Object.defineProperties() + Object.getOwnPropertyDescriptors()
//
// Clones accessor, non-enumerable, and symbolic properties
// Does not clone [[Prototype]] property

Object.defineProperties(clonedObj2, Object.getOwnPropertyDescriptors(obj));
console.log(Object.getOwnPropertyDescriptors(clonedObj2));
/*
[object Object] {
  a: [object Object] {
    configurable: true,
    enumerable: true,
    value: 1,
    writable: true
  },
  b: [object Object] {
    configurable: true,
    enumerable: false,
    value: 2,
    writable: true
  },
  c: [object Object] {
    configurable: true,
    enumerable: true,
    get: get c() {
      return this._c | 0;
    },
    set: undefined
  }
}
*/
console.log(clonedObj2[id]); // 3
console.log(clonedObj2.__proto__); // [object Object] { ... }

// METHOD #3: Object.create() + Object.getPrototypeOf() + Object.getOwnPropertyDescriptors()
//
// Clones accessor, non-enumerable, symbolic, and [[Prototype]] properties

clonedObj3 = Object.create(Object.getPrototypeOf(obj), Object.getOwnPropertyDescriptors(obj));
console.log(Object.getOwnPropertyDescriptors(clonedObj3));
/*
[object Object] {
  a: [object Object] {
    configurable: true,
    enumerable: true,
    value: 1,
    writable: true
  },
  b: [object Object] {
    configurable: true,
    enumerable: false,
    value: 2,
    writable: true
  },
  c: [object Object] {
    configurable: true,
    enumerable: true,
    get: get c() {
      return this._c | 0;
    },
    set: undefined
  }
}
*/
console.log(clonedObj3[id]); // 3
console.log(clonedObj3.__proto__); // [object Object] { p: 99 }
```

#### 💠 Accessing Non-Enumerable Properties

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/property-descriptors#object-getownpropertydescriptors)

`Object.getOwnPropertyDescriptors` allows to list non-enumerable property descriptors:

```js
const obj = {
  a: 1,
  b: 2
};

Object.defineProperty(obj, 'b', { enumerable: false });
console.log(Object.getOwnPropertyDescriptors(obj));
```

#### 💠 Setting Permissions for the Entire Object

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/property-descriptors#sealing-an-object-globally)

Although rarely used, these methods work for the whole object:
- `Object.preventExtensions()` disallows adding new properties to the object
- `Object.seal()` sets `configurable` attribute to `false` for all properties of the object
- `Object.freeze()` sets `configurable` and `writable` attributes to `false` for all properties of the object

These corresponding methods return `true` or `false`:
- `Object.isExtensible()`
- `Object.isSealed()`
- `Object.isFrozen()`

#### 💠 Object/Array Conversion

Object to array conversion:

```js
const obj = {a: 1, b: 2, c: 3};

console.log(Object.keys(obj)); // ["a", "b", "c"]
console.log(Object.values(obj)); // [1, 2, 3]
console.log(Object.entries(obj)); // [["a", 1], ["b", 2], ["c", 3]]
```

Array to object conversion:

```js
const arr = [["a", 1], ["b", 2], ["c", 3]];

console.log(Object.fromEntries(arr)); // [object Object] { a: 1, b: 2, c: 3 }
```

`Object.keys`/`Object.values`/`Object.entries` do not include properties that use symbols as keys nor inherited properties:

```js
const obj1 = { a: 1 };
const obj2 = { b: 2, __proto__: obj1 };

for (let key in obj2) {
  console.log(`${key}: ${obj2[key]}`); // "b: 2" "a: 1"
}

console.log(obj2); // [object Object] { a: 1, b: 2 }

console.log(Object.keys(obj2)); // ["b"]
console.log(Object.values(obj2)); // [2]
console.log(Object.entries(obj2)); // [["b", 2]]
```

#### 💠 Working With Object `[[Prototype]]` Property

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/prototype-methods)

`Object.setPrototypeOf`/`Object.getPrototypeOf` allow to set/get object `[[Prototype]]` in a modern way

`Object.create` allows to create a new object with a specified `[[Prototype]]` and optionally with additional specified property descriptors

Changing `[[Prototype]]` of existing objects is a very slow operation; `[[Prototype]]` usually should be set at the time of object creation

```js
const objProto = { a: 1 };
const obj1 = { b: 2 };

Object.setPrototypeOf(obj1, objProto);
console.log(Object.getPrototypeOf(obj1)); // [object Object] { a: 1 }

const obj2 = Object.create(objProto, {
  c: {
    value: 3
  }
});
console.log(Object.getPrototypeOf(obj2)); // [object Object] { a: 1 }
console.log(Object.getOwnPropertyDescriptors(obj2));
/*
[object Object] {
  c: [object Object] {
    configurable: false,
    enumerable: false,
    value: 3,
    writable: false
  }
}
*/
```

#### 💠 Using `Object.prototype.toString` for Advanced Type Checking

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/instanceof#bonus-object-prototype-tostring-for-the-type)

`Object.prototype.toString` can display type of primitives, objects with `Symbol.toStringTag`, and built-in objects:

```js
class A {}
class B extends A {
  [Symbol.toStringTag] = "B";
}

const a = new A();
const b = new B();

console.log({}.toString === Object.prototype.toString); // true
console.log({}.toString.call(1)); // "[object Number]"
console.log({}.toString.call(1n)); // "[object BigInt]"
console.log({}.toString.call(true)); // "[object Boolean]"
console.log({}.toString.call("")); // "[object String]"
console.log({}.toString.call(null)); // "[object Null]"
console.log({}.toString.call(undefined)); // "[object Undefined]"
console.log({}.toString.call(a)); // "[object Object]"
console.log({}.toString.call(b)); // "[object B]
//console.log({}.toString.call(new Symbol())); // TypeError: Symbol is not a constructor
console.log({}.toString.call(new Array())); // "[object Array]
```

### Number

#### 💠 General

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/number#tostring-base)

To call a method directly on a number, `..` must be used

```js
console.log(255..toString(16)); // ff
```

#### 💠 Testing Numbers

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/number#tests-isfinite-and-isnan)

`Number.isNaN(value)` tests if the value belongs to the `number` type and is `NaN`:

```js
console.log(Number.isNaN(NaN)); // true
```

`Number.isFinite(value)` tests if the value belongs to the `number` type and is not `NaN`/`Infinity`/`-Infinity`:

```js
console.log(Number.isFinite(1)); // true
console.log(Number.isFinite("1")); // false
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

### String

#### 💠 Accessing Characters

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/string#accessing-characters)

```js
console.log("123".at(0)); // "1"
console.log("123".at(-1)); // "3"
```

#### 💠 Searching for a Substring

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/string#searching-for-a-substring)
>
> 📖 [MDN: String.prototype.startsWith()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/startsWith)
>
> 📖 [MDN: String.prototype.endsWith()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/endsWith)

```js
console.log("abcd-abcd".indexOf("e")); // -1
console.log("abcd-abcd".indexOf("ab")); // 0
console.log("abcd-abcd".indexOf("ab", 1)); // 5
console.log("abcd-abcd".indexOf("ab", -99)); // 0

console.log("abcd-abcd".lastIndexOf("e")); // -1
console.log("abcd-abcd".lastIndexOf("ab")); // 5
console.log("abcd-abcd".lastIndexOf("ab", 4)); // 0
console.log("abcd-abcd".lastIndexOf("ab", -99)); // 0
```

```js
console.log("abcd".includes("ab")); // true
console.log("abcd".includes("ab", 1)); // false

console.log("abcd".startsWith("ab")); // true
console.log("abcd".startsWith("bc", 1)); // true

console.log("abcd".endsWith("cd")); // true
console.log("abcd".endsWith("bc", 3)); // true
```

#### 💠 Getting a Substring

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/string#getting-a-substring)

```js
console.log("abcd".slice(1)); // "bcd"
console.log("abcd".slice(1, 2)); // "b"
console.log("abcd".slice(-1)); // "d"
console.log("abcd".slice(-3, -1)); // "bc"
```

#### 💠 Changing the Case

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/string#changing-the-case)

```js
console.log("ABC".toLowerCase()); // "abc"
console.log("abc".toUpperCase()); // "ABC"
```

#### 💠 Comparing Strings

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/string#comparing-strings)
>
> 📖 [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/localeCompare)

`String.prototype.localeCompare()` compares two strings according to the ECMA-402 internationalization standard

```js
console.log("a".localeCompare("b") < 0); // true
console.log("b".localeCompare("b") === 0); // true
console.log("b".localeCompare("a") > 0); // true
```

Behavior of `String.prototype.localeCompare()` can be customized by additional parameters

### Symbol

#### 💠 Global Symbol Registry

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/symbol#global-symbols)

Global symbol registry allow to create an access global symbols (accessible from anywhere in the code) with unique desccriptions

`Symbol.for(descriptionString)` is used to access (or create when absent) 

#### 💠 Customizing `Object.prototype.toString`

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/instanceof#bonus-object-prototype-tostring-for-the-type)

```js
class A {}
class B extends A {
  [Symbol.toStringTag] = "B";
}

const a = new A();
const b = new B();

console.log({}.toString.call(a)); // "[object Object]"
console.log({}.toString.call(b)); // "[object B]
console.log(Object.prototype.toString.call(b)); // "[object B]
```

### Array

#### 💠 Accessing Elements

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/array#get-last-elements-with-at)

```js
console.log([1, 2, 3].at(0)); // "1"
console.log([1, 2, 3].at(-1)); // "3"
```

#### 💠 Adding/Removing Elements

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/array)

```js
const arr = [1, 2, 3];

console.log(arr.push(4)); // 4
console.log(arr); // [1, 2, 3, 4]

console.log(arr.pop()); // 4
console.log(arr); // [1, 2, 3]

console.log(arr.unshift(0)); // 0 (length)
console.log(arr); // [0, 1, 2, 3]

console.log(arr.shift()); // 0
console.log(arr); // [1, 2, 3]
```

#### 💠 Modifying/Cloning Array

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/array-methods#slice)

```js
const arr = [1, 2, 3, 4];

console.log(arr.slice()); // [1, 2, 3, 4] (clone of the array)
console.log(arr.slice(1)); // [2, 3, 4]
console.log(arr.slice(1, 2)); // [2]
console.log(arr.slice(-1)); // [4]
console.log(arr.slice(-3, -1)); // [2, 3]
```

#### 💠 Concatenating Arrays

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/array-methods#concat)

```js
console.log([1, 2].concat([3, 4], 5, 6)); // [1, 2, 3, 4, 5, 6]
```

#### 💠 Reordering Elements

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/array-methods)

Both `Array.prototype.reverse()` and `Array.prototype.sort()` modify the array and return it

`Array.prototype.sort()` sorts the elements as being converted to strings so an ordering function may be needed:

```js
console.log([1, 2, 11].sort()); // [1, 11, 2]
console.log([1, 2, 11].sort((a, b) => a - b)); // [1, 2, 11]
```

An ordering function may also be needed when dealing with special characters:

```js
console.log(["a", "ą", "z"].sort()); // ["a", "z", "ą"]
console.log(["a", "ą", "z"].sort((a, b) => a.localeCompare(b))); // ["a", "ą", "z"]
```

#### 💠 Searching for an Element

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/array-methods#indexof-lastindexof-and-includes)

```js
const arr = [1, 2, 3, 1];

console.log(arr.indexOf(4)); // -1
console.log(arr.indexOf(1)); // 0
console.log(arr.indexOf(1, 1)); // 3
console.log(arr.indexOf(1, -99)); // 0

console.log(arr.lastIndexOf(4)); // -1
console.log(arr.lastIndexOf(1)); // 3
console.log(arr.lastIndexOf(1, 1)); // 0
console.log(arr.lastIndexOf(1, -99)); // -1

console.log(arr.includes(2)); // true
console.log(arr.includes(2, 2)); // false

console.log([NaN].indexOf(NaN)); // -1 (doesn't work for NaN)
console.log([NaN].includes(NaN)); // true (works for NaN)
```

#### 💠 Array/String Conversion

> 📖 [The Modern JavaScript Tutorial: Array](https://javascript.info/array#tostring)
>
> 📖 [The Modern JavaScript Tutorial: Array methods](https://javascript.info/array-methods#split-and-join)

```js
console.log([1, 2, 3].toString()); // "1,2,3"

console.log([1, 2, 3].join(", ")); // "1, 2, 3"
console.log("1, 2, 3".split(", ", 2)); // ["1", "2"]
```

#### 💠 Checking Type

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/array-methods#array-isarray)

```js
// typeof does not help for arrays:
console.log(typeof {}); // "object"
console.log(typeof []); // "object"

// Array.isArray() must be used:
console.log(Array.isArray({})); // false
console.log(Array.isArray([])); // true
```

#### 💠 Iterative Methods

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/array-methods)
>
> 📖 [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array#iterative_methods)

All iterative methods except `reduce`/`reduceRight` accept `thisArg` as an argument in addition to a callback function - `thisArg` becomes `this` for the callback function

```js
arr = [{a: 1}, {a: 2}, {a: 3}];

arr.forEach((item, index, array) => console.log(item.a)); // 1 2 3

console.log(arr.find((item, index, array) => item.a === 2)); // [object Object] { a: 2 }
console.log(arr.find((item, index, array) => item.a === 4)); // undefined
console.log(arr.findLast((item, index, array) => item.a < 3)); // [object Object] { a: 2 }

console.log(arr.findIndex((item, index, array) => item.a === 2)); // 1
console.log(arr.findIndex((item, index, array) => item.a === 4)); // -1
console.log(arr.findLastIndex((item, index, array) => item.a === 2)); // 1
console.log(arr.findLastIndex((item, index, array) => item.a === 4)); // -1

console.log(arr.some((item, index, array) => item.a < 3)); // true
console.log(arr.every((item, index, array) => item.a > 0)); // true

console.log(arr.filter((item, index, array) => item.a !== 1)); // [[object Object] { a: 2 }, [object Object] { a: 3 }]

console.log(arr.map((item, index, array) => item.a * 2)); // [2, 4, 6]

console.log([].reduce((accumulator, item, index, array) => accumulator += 1)); // TypeError: Reduce of empty array with no initial value
console.log(arr.reduce((accumulator, item, index, array) => accumulator += item.a)); // "[object Object]23"
console.log(arr.reduce((accumulator, item, index, array) => accumulator += item.a, 100)); // 106
console.log(arr.reduceRight((accumulator, item, index, array) => accumulator += item.a, 100)); // 106
```

### Math

#### 💠 Rounding to Integer

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/number#rounding)

```js
console.log(Math.floor(1.5), Math.floor(-1.5)); // 1, -2
console.log(Math.ceil(1.5), Math.ceil(-1.5)); // 2, -1
console.log(Math.round(1.5), Math.round(-1.5)); // 2, -1
console.log(Math.trunc(1.5), Math.trunc(-1.5)); // 1, -1
```

#### 💠 Getting Random Number

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/number#other-math-functions)

`Math.random()` returns a random number from the interval <0; 1)

#### 💠 Getting Min/Max Value

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/number#other-math-functions)

```js
console.log(Math.min(1, 2, 3)); // 1
console.log(Math.max(1, 2, 3)); // 3
```

### Function

#### 💠 Calling Function With a Context

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/call-apply-decorators)
>
> 📖 [MDN: Function.prototype.call()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/call)
>
> 📖 [MDN: Function.prototype.apply()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/apply)

Arguments for `call()` are provided infividually while for `apply()` as an array/array-like object

```js
function printObj(ifUpperCase = false) {
  console.log(ifUpperCase ? this.a.toUpperCase() : this.a);
}

const obj = { a: 'abc' };

printObj.call(); // undefined ('a' is not a property of [object Window])
printObj.call(obj); // "abc"
printObj.call(obj, true); // "ABC"

printObj.apply(); // undefined ('a' is not a property of [object Window])
printObj.apply(obj); // "abc"
printObj.apply(obj, [true]); // "ABC"
```

#### 💠 Binding Context or Arguments to a Function

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/bind)

Context bound using `Function.prototype.bind()`:

```js
let obj = {
  a: 1,
  
  m(b) {
    console.log(this.a + b);
  }
};

let n = obj.m.bind(obj);

setTimeout(n, 0, 100); // 101
setTimeout(() => obj = null); // Will not break after this change in the original object
setTimeout(n, 0, 100); // 101
```

Arguments bound using `Function.prototype.bind()`:

```js
function greet(name) {
  console.log(`Hello, ${name}`);
}

let greetAdmin = greet.bind(null, 'Admin');

greet('Admin'); // "Hello, Admin"
greetAdmin(); // "Hello, Admin"
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

Prevents accidental creation of global variables when assigning value without declaration inside a function that is called afterwards:

```js
function f() {
  a = 1;
}

f();
console.log(a); // 1
```

##### Function Declaration

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/function-expressions#function-expression-vs-function-declaration)

Makes the function visible only within the block scope in which it was declared

##### this Value

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/object-methods#this-is-not-bound)

When a function is called without an object, the value of `this` is:
- `undefined` when in strinct mode
- global object when not in strinct mode

##### Writing to a Non-Writible Property

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/property-descriptors#non-writable)

When not in strict mode, writing to a non-writable property will not result in an error, although the operation will not succeed

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

### Techniques

#### 💠 Immediately Invoked Function Expression (IIFE)

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/var#iife)

Used in the past to emulate code block with `var`

```js
(function () {
  var a = 1;
  
  console.log(a); // 1
})();

// console.log(a); // ReferenceError: a is not defined
```

This may be also accomplished in several other ways:

```js
(function () {
  ...
}());

!function () {
  ...
}();

+function () {
  ...
}();
```

#### 💠 Immediately Called Constructor Function

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/constructor-new#constructor-function)

```js
let abc = new function() {
  ...
}
```

Used when performing complex initialization for a single object to keep the code organized and to avoid polluting the global scope with temporary variables or functions

#### 💠 Property Backward Compatibility

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/property-accessors#using-for-compatibility)

When a property is no longer needed, instead of changing all relevant places in the code, a getter may be used:

```js
function Abc(a, c) {
  this.a = a;
  this.c = c;
  
  Object.defineProperty(this, 'b', {
    get() {
      return 2;
    }
  })
}

const abc = new Abc(1, 3);

console.log(abc); // [object Object] { a: 1, c: 3 }
console.log(abc.b); // 2
```

#### 💠 Property-Based Encapsulation

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/property-accessors#smarter-getters-setters)

The convention is to treat the properties with name starting with `_` as internal properties

```js
const obj = {
  _a: 1,
  
  get a() {
    return this._a;
  },
  
  set a(value) {
    this._a = Number(value);
  }
};

console.log(obj.a); // 1
obj.a = "23";
console.log(obj.a); // 23
```

#### 💠 Symbol-Based Encapsulation

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/symbol#hidden-properties)

Used for third-party code objects when it's unsafe to add properties to them in danger of affecting pre-defined behavior

#### 💠 Private Members

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/symbol#hidden-properties)

Used when exposing object to scripts which may add their own properties

#### 💠 Call Forwarding

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/call-apply-decorators)

It's a technique in which the context and all arguments of a function are passed to another function

```js
function f(a, b) {
  this.a = a;
  this.b = b;
  
  console.log(this);
}

function wrapper1(func, ...args) {
  const obj = {c: 3};
  
  func.call(obj, ...args);
}

function wrapper2(func, ...args) {
  const obj = {c: 3};
  
  func.apply(obj, args);
}

wrapper1(f, 1, 2); // [object Object] { a: 1, b: 2, c: 3 }
wrapper2(f, 1, 2); // [object Object] { a: 1, b: 2, c: 3 }
```

#### 💠 Method Borrowing

> 📖 [The Modern JavaScript Tutorial: Decorators and forwarding, call/apply](https://javascript.info/call-apply-decorators#method-borrowing)
>
> 📖 [The Modern JavaScript Tutorial: Native prototypes](https://javascript.info/native-prototypes#borrowing-from-prototypes)

It's a technique in which a method is called in the context of another object:

```js
const arrayLike = {
  0: 'a',
  1: 'b',
  2: 'c',
  length: 3
};

// console.log(arrayLike.join()); // TypeError: arrayLike.join is not a function
console.log([].join.call(arrayLike)); // "a,b,c"
```

May be also achieved using native prototypes:

```js
const arrayLike = {
  0: 'a',
  1: 'b',
  2: 'c',
  length: 3
};

arrayLike.join = Array.prototype.join;
console.log(arrayLike.join()); // "a,b,c"
```

Object can have only one prototype but it can inherit single methods from multiple objects at the same time

#### 💠 Passing a Method Without Losing `this`

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/bind)

`this` is lost when a method is passed as a callback:

```js
let obj = {
  a: 1,
  
  m() {
    console.log(this.a);
  }
};

setTimeout(obj.m); // undefined (no "m" property - in window object for broser or in timer object for Node.js)
setTimeout(() => obj.m()); // 1 (works when called inside a wrapping function)
setTimeout(() => obj = null); // Will break after this change in the original object
// setTimeout(() => obj.m()); // TypeError: Cannot read properties of null (reading 'm')
```

The solution is to use `Function.prototype.bind()`:

```js
let obj = {
  a: 1,
  
  m(b) {
    console.log(this.a + b);
  }
};

let n = obj.m.bind(obj);

setTimeout(n, 0, 100); // 101
setTimeout(() => obj = null); // Will not break after this change in the original object
setTimeout(n, 0, 100); // 101
```

#### 💠 Partial Application

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/bind#partial-functions)

It's a technique in which a new function is created based on another one with some fixed parameters:

```js
function greet(name) {
  console.log(`Hello, ${name}`);
}

let greetAdmin = greet.bind(null, 'Admin');

greet('Admin'); // "Hello, Admin"
greetAdmin(); // "Hello, Admin"
```

#### 💠 'Very Plain'/'Pure Dictionary' Objects

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/prototype-methods#very-plain)

Used in associative arrays to avoid the defualt inheritance of built-in methods and `__proto__` getter/setter from `Object.prototype` which could cause side effects (hard-to-notice bugs or even vulnerabilities in the server-side JavaScript code)

```js
let obj = {};

obj.__proto__ = 0;
console.log(obj.__proto__); // [object Object] { ... } --> Not 0

obj = { __proto__: null };

obj.__proto__ = 0;
console.log(obj.__proto__); // 0
```

Can be also created using `Object.create(null)`:

```js
let obj = {};

obj.__proto__ = 0;
console.log(obj.__proto__); // [object Object] { ... } --> Not 0

obj = Object.create(null);

obj.__proto__ = 0;
console.log(obj.__proto__); // 0
```

Such implementations result in the absence of any built-in object methods (e.g. `Object.prototype.toString()`) in the created 'very plain' object; however, methods that are not in the prototype (e.g. `Object.keys`) are still accessible

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

###### Scheduling

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/settimeout-setinterval)

```js
function f(a, b) {
  console.log(a * b);
}

const timerId1 = setTimeout(f, 1000, 2, 3);
const timerId2 = setInterval(f, 1000, 4, 5);

setTimeout(clearTimeout, 1500, timerId1);
setTimeout(clearInterval, 2500, timerId2);

setTimeout("console.log('abc')", 1000);
```

Real time interval when using `setInterval` is less then the specified value as the time of callback function execution is included in the specified value

Time intercal when using nested `setTimeout` is more then the specified calue as the time of callback function execution is added to the specified value

Interval depends on the operating system performance, so the exact value is not guaranteed

In browser runtime environemnt, interval (both for `setInterval` and `setTimeout`) becomes 4+ ms after five nested timers:

```js
function f(callTime) {
  let interval = Date.now() - callTime;
  
  console.log(interval);
  
  if (interval < 10) {
    setTimeout(f, 0, Date.now());
  }
}

setTimeout(f, 0, Date.now());
// 1 1 0 0 714
// 1 1 0 1 898
// 2 1 0 1 5
```

The callback function and its outer variables are kept in memory until the scheduling is cleared using `clearTimeout`/`clearInterval`
