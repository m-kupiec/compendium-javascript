# JavaScript Reference Summary

## TOC

### Operation

- **Code Parsing & Execution**
  - Automatic Semicolon Insertion
  - Trailing Commas
  - Strict Mode
  - Declarations & Assignments
  - Hoisting
  - Scope
  - Lexical Environment
  - Closure
  - Execution Context
  - Event Loop
  - Memory Data Structures
  - Memory Life Cycle
- **Operators**
  - Arithmetic
  - Bitwise
  - Logical
  - Comparison
  - Assignment
  - Comma

### Data

- **Primitives**
  - Number
  - BigInt
  - String
  - Boolean
  - Symbol
  - Null
  - Undefined
- **Objects**
  - Referencing
  - Properties
  - Property Attributes
  - Accessor Properties
  - Methods
  - Reference Record
  - Optional Chaining
  - Destructuring
  - Looping
  - Prototypal Inheritance
- **Data Collections**
  - Array-Like Objects
  - Iterable Objects
  - Async Iterable Objects
  - Arrays
  - Maps
  - Sets
  - WeakMaps
  - WeakSets
- **Type Operations**
  - Checking
  - Conversion

### Code Structures

- **Functions**
  - Regular Functions
  - Constructor Functions
  - Generators
- **Classes**
  - Ontology
  - Inheritance
  - Encapsulation
- **Synchronous Control Flow**
  - Conditionals
  - Loops
  - Control Transfer
  - Error Handling
- **Asynchronous Control Flow**
  - Callback-Based
  - Promises
  - async/await

### Built-In Objects & Classes

- **`globalThis`**
  - `isFinite`/`isNaN`
  - `parseInt`/`parseFloat`
  - `eval`
- **`Object`**
  - `Object.prototype`
  - `Object.prototype.toString`
  - `Object.is`
  - `Object.`<`keys`/`values`/`entries`/`fromEntries`>
  - `Object.`<`getOwnPropertyDescriptor`/`getOwnPropertyDescriptors`>
  - `Object.`<`defineProperty`/`defineProperties`>
  - `Object.`<`preventExtensions`/`seal`/`freeze`>
  - `Object.`<`setPrototypeOf`/`getPrototypeOf`/`create`>
  - `Object.assign`
- **`Number`**
- **`BigInt`**
- **`String`**
  - `String.prototype.localeCompare`
  - `String.prototype.`<`indexOf`/`lastIndexOf`/`includes`/`startsWith`/`endsWith`>
  - `String.prototype.`<`at`/`slice`>
  - `String.prototype.`<`toLowerCase`/`toUpperCase`>
- **`Boolean`**
- **`Symbol`**
- **`Array`**
  - `Array.prototype.`<`indexOf`/`lastIndexOf`/`includes`>
  - `Array.prototype.`<`at`/`slice`>
  - `Array.prototype.`<`push`/`pop`/`unshift`/`shift`>
  - `Array.prototype.concat`
  - `Array.prototype.`<`sort`/`reverse`>
  - `Array.prototype.`<`toString`/`join`/`split`>
  - `Array.prototype`'s Iterative Methods
    - `Array.prototype.forEach`
    - `Array.prototype.`<`find`/`findLast`/`findIndex`/`findLastIndex`>
    - `Array.prototype.`<`some`/`every`>
    - `Array.prototype.`<`filter`/`map`>
    - `Array.prototype.`<`reduce`/`reduceRight`>
  - `Array.isArray`
  - `Array.from`
- **`Map`**
- **`WeakMap`**
- **`Set`**
- **`WeakSet`**
- **`Math`**
  - Other Methods
- **`Date`**
- **`JSON`**
  - `JSON.stringify`
  - `JSON.parse`
- **`Function`**
  - `Function.prototype.`<`call`/`apply`>
  - `Function.prototype.bind`
- **`Promise`**
  - `Promise.`<`all`/`allSettled`>
  - `Promise.`<`race`/`any`>
  - `Promise.`<`resolve`/`reject`>
- **`Error`**

### Programming Techniques

- **Objects**
  - Shallow Cloning Objects

# Operation

## Code Parsing & Execution

### Automatic Semicolon Insertion

Occurs an a line break in most cases with the notable exeption of a line immediately followed by:
- A parenthesis `(...)`
- A square bracket `[...]`

### Trailing Commas

Trailing commas are allowed in all comma-separated lists of values:
- No more than one in:
  - Object literals
  - Function parameters list
- Without restrictions in array literals (the array's length will be increased by the number of `n-1` trailing commas)

### Strict Mode

`"use strict"`:
- Enables modifications introduced in ES5
- Must be placed at the beginning of a script or a function

Strict mode is:
- Used in classes and modules by default
- Not used in the browser console by default

### Declarations & Assignments

A variable declared with `var` can be redeclared

Declaring a variable without a keyword (by an assignment) is possible (no `ReferenceError`) only if not in the strict mode

A variable declared with `const` cannot be reassigned

### Hoisting

At compile time the engine allocates memory by hoisting variable names and function declarations to the top of their corresponding scopes; functions are initialized immediately while variable initializations are done in-place

A `var` declaration (without the assignment) is hoisted to the top of its scope and given an initial value of `undefined`

No-keyword "declaration" (an assignment without a previous declaration) is not hoisted

A `let`/`const` declaration is hoisted but not initialized, so that the variable remains in a *temporal dead zone* until the initialization code is executed

### Scope

|Declaration |Code Block       |                 |Function             |                    |                    |
|------------|-----------------|-----------------|---------------------|--------------------|--------------------|
|            |**Module Scope** |**Global Scope** |**Module Scope**     |**Global Scope**    |                    |
|            |                 |                 |                     |**Declaration**     |**Expression**      |
|`function`  |Not Scoped *     |Not Scoped *     |Scoped               |Scoped              |Scoped              |
|            |-                |Added to `global`|-                    |-                   |-                   |
|`var`       |Not Scoped       |Not Scoped       |Scoped               |Scoped              |Scoped              |
|            |-                |Added to `global`|-                    |-                   |-                   |
|No keyword *|                 |                 |***After `()`***     |***After `()`***    |***After `()`***    |
|            |Not Scoped       |Not Scoped       |Not Scoped           |Not Scoped          |Not Scoped          |
|            |Added to `global`|Added to `global`|Added to `global`    |Added to `global`   |Added to `global`   |
|            |                 |                 |***Before `()`***    |***Before `()`***   |***Before `()`***   |
|            |                 |                 |Scoped               |Scoped              |Scoped              |
|            |                 |                 |-                    |-                   |-                   |
|`this`      |-                |-                |Added to `global` ***|Added to `global` **|Added to `global` **|

\* *Only when not in the strict mode*

\*\* *Because the value of `this` is the global object when not in the strict mode or `undefined` otherwise; Only when:*
- \*\* *not in the strict mode*
- \*\* *the function is called without an object*
- \*\*\* *the function was also not declared as an arrow function (function declaration/expression/named expression)*

### Lexical Environment

Every running scope (global, block, function) has its associated Lexical Environment (theoretical object existing in the specification) which consists of:

- A reference to the outer lexical environment
- An `Environment Record` object which stores as its properties:
  - `this`
  - local variables
  - local function declarations

Variables are stored and updated in their corresponding Lexical Environments

Lexical Environment is cleaned from memory by the garbage collector when it becomes unreachable

### Closure

All functions in JavaScript (if not created with `new`) are closures, i.e. they retain access to their outer variables because in a hidden `[[Environment]]` property they store a reference to the Lexical Environment in which they were created

### Execution Context

Execution context data structure stores information about a given function call, including:
- current place in the control flow
- current variables
- the value of `this`

Nested execution contexts are stored as frames in the call stack (LIFO order)

### Event Loop

JavaScript operates on a single thread, but its asynchronous behavior is facilitated by the Event Loop, a code execution management system:
1. The Memory Heap and Call Stack, components of the JavaScript engine, interact with the runtime environment, typically through its provided APIs or mechanisms
2. The runtime environment enqueues tasks into the Event Queue, representing asynchronous operations such as I/O events or timer callbacks
3. The Event Loop manages the execution flow by continuously checking the Call Stack's status; it dequeues tasks from the Event Queue and schedules them for execution (in an order influenced by factors such as task priorities and event types, rather than strictly adhering to a simple FIFO order)
   - `PromiseJobs` queue ("microtask queue" as called in V8) has higher priority than the callback queue

```js
setTimeout(console.log, 0, 5);
Promise.resolve().then(() => console.log(1));
Promise.resolve().then(() => console.log(2))
  .then(() => console.log(3));
console.log(4);

// 4 1 2 3 5
```

### Memory Data Structures

The Stack:
- Used for static memory allocation - the size of the data type (primitive data types) is known at compile time and a fixed amount of memory is reserved for it
- Stores (in the LIFO order):
  - Primitive values
  - References to non-primitive values
  - Function call frames

The Heap:
- Used for dynamic memory allocation at runtime - the size of the stored data is unknown at compile time or may change during runtime
- Stores:
  - Objects
  - Functions
  - Arrays
  - etc.

### Memory Life Cycle

Memory allocation:
- Variable declaration or assignment
- Object property declaration or assignment
- Function declaration
- Function call

Memory in use (reading from or writing to the allocated memory):
- Using variables
- Reassigning variables
- Passing arguments to functions

Garbage collection:
- Releasing/clearing memory using one of the algorithms used by the given JavaScript engine:
  - Reference counting:
    1. Counts references stored in the stack
    2. Releases allocated memory when the count is zero
  - Mark-and-sweep:
    1. Starts from the global object traversing all variables and marking the reachable ones
    2. Unmarked variables are garbage collected during the sweep phase

## Operators

### Arithmetic

The increment `++i` returns the new value, while `i++` returns the old value

### Bitwise

Operands are treated as 32-bit integers

Operators:
- AND ( & )
- OR ( | )
- XOR ( ^ )
- NOT ( ~ )
- LEFT SHIFT ( << )
- RIGHT SHIFT ( >> )
- ZERO-FILL RIGHT SHIFT ( >>> )

### Logical

AND (`&&`):
1. Evaluates operands from left to right
2. Converts each operand to `Boolean`
3. Returns the original value of the first operand that isn't `true` after conversion (or the last one if all are truthy)

OR (`||`):
1. Evaluates operands from left to right
2. Converts each operand to `Boolean`
3. Returns the original value of the first operand that isn't `false` after conversion (or the last one if all are falsy)

Nullish Coalescing (`??`):
1. Evaluates operands from left to right
2. Returns the original value of the first operand that isn't `null`/`undefined` (e.g. `0`, `NaN`, `""`, `false`)

When combining multiple operators:
- `&&` has higher precedence than `||`
- `??` has the same precedence as `||`
- Using `??` together with `&&`/`||` without parentheses is forbidden

### Comparison

Returns a boolean

Strings are compared according to the UTF-16 order

### Assignment

Returns the assigned value

Chained assignments are evaluated from right to left

For each arithmetical and bitwise operator, there is a corresponding modify-and-assign operator

### Comma

Each of the expressions separated with a comma is evaluated and the result of the last one is returned

Comma has a lower precedence than the assignment operator

# Data Types

## Primitives

### Number

Format:
- Stored in a binary form in the double precision floating-point format (64-bit) in accordance with the IEEE 754 standard
- Rounded to the nearest possible value which results in a loss of precision

Possible values:
- Integer (including `-0`)
- Floating point
- `Infinity`/`-Infinity`
- `NaN` (represents a computational error)

Decimal notations:
- `-1000000`
- `-1_000_000`
- `1e-6`

Non-decimal numeral systems:
- Binary (e.g. `0b101010` for `42`)
- Octal (e.g. `0o52` for `42`)
- Hexadecimal (e.g. `0x2A` for `42`)

### BigInt

Intended for values outside the range of 64-bit storage, i.e. from `-9007199254740991` [`-(2`<sup>`53`</sup>` - 1)`] to `-9007199254740991` [`(2`<sup>`53`</sup>` - 1)`]

Notation: `1n`

### String

Stored in UTF-16 format

Notations:
- Single quotes
- Double quotes
- Backticks
  - Allows multiple lines
  - Allows template literals
  - Allows tagged templates

Special characters:
- `\r\n`: New line (Windows text files)
- `\n`: New line
- `\t`: Tab
- `\`: Special character escaping

Reading/writing:
- Is immutable (characters cannot be changed)
- Accessing char at a non-found index results in an `undefined` value
- Destructuring assignment: `[a, b, c] = "123"`

### Boolean

Possible values: `true`/`false`

### Symbol

Represents a unique identifier

Symbol's description may be used for debugging:

```js
let id = Symbol("Description");

console.log(id.description); // "Description"
```

### Null

Represents an empty/unknown value

### Undefined

Represents a non-assigned value

## Objects

### Referencing

```js
let sourceObj = { a: 1 };

let arr = [sourceObj];
let obj = sourceObj;

sourceObj = null;
console.log(arr[0] === sourceObj); // false
console.log(obj === sourceObj); // false
console.log(arr[0]); // [object Object] { a: 1 }
console.log(obj); // [object Object] { a: 1 }
```

### Properties

Property name can be any `String` or `Symbol`; if of any other type, it's converted to `String`

Property value shorthand (`{ prop }`) may be used when the property name is the same as the property value

Properties which names would be valid integers (after conversion to number) are sorted, while the other properties are kept in creation order

`in` operator checks if a property with the given name exists in the object (even if its value is `undefined`)

`delete` operator is used to remove a property

### Property Attributes

Each data property has four attributes ("flags"), the last three all set to `true` by default:
- `value`
- `writable` (specifying if the property value can be changed)
  - When not in the strict mode, writing to a non-writable property will not result in an error, although the operation will not succeed
- `enumerable` (specifying if the property is to be listed in loops)
- `configurable` (specifying if the property can be deleted or its attributes modified)
  - It does not affect the possibility of changing the property value which is regulated by the `writable` attribute
  - Even if set to `false`, it still allows to change `writable` from `true` to `false` (only in this direction) to strengthen security

### Accessor Properties

Functions that execute on getting/setting a data property value

```js
const obj = {
  _val: 1,

  get val() {
    return this._val;
  },

  set val(value) {
    this._val = value;
  }
};
```

Accessor property's attributes:
- Removed:
  - ~~`value`~~
  - ~~`writable`~~
- Added:
  - `get`: `[Function]`/`undefined`
  - `set`: `[Function]`/`undefined`
- Remaining:
  - `enumerable`
  - `writable`

### Methods

```js
let obj = {
  f: function() {
    /* ... */
  }
}
```

```js
let obj = {
  f() {
    /* ... */
  }
}
```

When a function is called without an object, the value of `this` is:
- `undefined`, if in the strict mode
- Global object, if not in the strict mode

### Reference Record

Is a specification type, a result of a property access

It passes (from the `.` to the calling parentheses `()`) the value of `this` and the accessed property

If not followed by the calling parentheses `()`, it is discarded (and so `this` is lost) and the property value is passed instead:

```js
const obj = {
  val: 1,

  f() {
    console.log(this.val);
  }
};

const g = obj.f;
g(); // undefined

obj.f(); // 1
(obj.f)(); // 1
(true ? obj.f : null)(); // undefined
```

### Optional Chaining

This special syntax contruct stops the evaluation if the preceding value (of a declared variables) is `undefined`/`null` and returns `undefined`

Syntax:
- Accessing a property that may not exist:
  - `?.<propertyName>` (for dot notation)
  - `?.["<propertyName>"]` (for square bracket notation)
- Calling a method that may not exist:
  - `<methodName>.?.()`

Use cases:
- Can be used for:
  - Reading
  - Deleting
- Can't be used for:
  - Setting a value

### Destructuring

Assignment:

```js
let {
  a: {
    aOne: a1 = 1,
    aTwo: a2 = 2
  },

  f,

  ...rest
} = {
  a: {
    aTwo: 0
  },

  f() {},

  g1() {},
  g2() {},
};

console.log(a1, a2, f, rest);
// 1 0 [Function: f] { g1: [Function: g1], g2: [Function: g2] }
```

Shallow copy:

```js
let objCopy = { ...obj };
```

### Looping

`for (key in obj)` loop:
- Includes inherited propertied and methods
- Doesn't include symbolic properties

### Prototypal Inheritance

`__proto__`:
- A getter/setter for `[[Prototype]]` (a hidden property that either references to another object (the prototype) or is `null`)
- Its value must be an `Object` or `null` (or the assignment will be ignored); assigning in a circle will result in an error
- Outdated (moved to Annex B - optional for non-browser environments); since 2022 is allowed in object literals

Changing `[[Prototype]]` of an existing object is a very slow operation; `[[Prototype]]` should usually be set at the time of object creation

Between the prototype and the inheriting object, methods are shared but the state is not, e.g. assigning value to a non-existing property (which does exist in the prototype) will result in adding this property to the immediate object (not the prototype)

## Data Collections

### Array-Like Objects

An array-like object has numeric indices and the `length` property

```js
const arrayLike = {
  0: 'a',
  1: 'b',
  2: 'c',

  length: 3
};
```

### Iterable Objects

Iterables (unlike array-likes):
- Can be looped over using `for...of`
- Work with the spread syntax (`...`)

Built-in iterable objects:
- `String`
- `Array`
- `Map` (but not `WeakMap`)
- `Set` (but not `WeakSet`)

### Async Iterable Objects

Async iterables:
- Can be looped over using `for await...of`
- Don't work with the spread syntax (`...`) (which, according to ChatGPT, would require an async `Symbol.iterator` generator method to be implemented)

### Arrays

Empty elements:
- `new Array(n)` creates an array with `n` empty (not even `undefined`) elements
- `let arr = []; arr[n] = true;` creates an array with `n-1` empty (not even `undefined`) elements

When accessing an array's element, the value put in square brackets is converted to `String`:

```js
let arr = [true];

console.log(arr[0], arr[0n], arr["0"]);
// true true true
console.log(arr[""], arr[false], arr[null], arr[undefined], arr[Symbol()], arr[{}]);
// undefined undefined undefined undefined undefined undefined
```

An array may be truncated by decreasing the `length` property (or cleared by assigning `0` to it)

Destructuring:
- Assignment:

```js
let [a1, , a3 = 3, ...rest] = [1, 2, , 4, 5];

console.log(a1, a3, rest); // 1 3 [4, 5]
```

- Shallow copy:

```js
let arr = [...[1, 2, 3]];
```

Looping: `for (el of arr)`

### Maps

A keyed collection that allows keys of any type

Preserves the entry insertion order

Destructuring:

- Assignment:

```js
const [a, b] = map; // a and b then become two-item arrays
```

- Shallow copy:

```js
const mapCopy = new Map([...map]);
```

Looping: `for (entry of map)`

### Sets

A collection of unique values

Preserves the value insertion order

Destructuring:

- Assignment:

```js
const [a, b] = set; // a and b then become singular values
```

- Shallow copy:

```js
const setCopy = new Set([...set]);
```

Looping: `for (value of set)`

### WeakMaps

Requires an object for a property (or will result in `TypeError`)

A key is removed from the `WeakMap` and memory when there no longer exists any reference to it

### WeakSets

Requires an object for a value (or will result in `TypeError`)

A value is removed from the `WeakSet` and memory when there no longer exists any reference to it

## Type Operations

### Checking

`typeof` operator syntax: `typeof x`/`typeof(x)`

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

### Conversion

Unary-operator conversions:
- To `Number`: `+`/`-`
  - Irregurality: `+(`<`BigInt`>`)` &rightarrow; `TypeError`
- To `Boolean`: `!`/`!!`

Automatic conversions:
- Binary `+`:
  1. `Symbol` cannot be one of the operands (if it is, there will be an attempt to automatically convert it to `Number`/`String` which will result in `TypeError`)
  2. If one of the operands is `BigInt`, to prevent `TypeError`, the other one must also be `BigInt` or `String`/`Object`/`Array`
  3. Otherwise, if one of the operands is `String`/`Object`/`Array`, they are both converted to `String` (even if the second one is `BigInt`)
  4. Otherwise, if both the operands are either `Number`/`Boolean`/`null`/`undefined`, they are both converted to `Number`
- Binary `-`, `*`, `/`:
  1. `Symbol` cannot be one of the operands (if it is, there will be an attempt to automatically convert it to `Number` which will result in `TypeError`)
  2. If one of the operands is `BigInt`, to prevent `TypeError`, the other one must also be `BigInt` (not even `String`/`Object`/`Array`)
  3. Otherwise, if both the operands are either `Number`/`String`/`Boolean`/`null`/`undefined`/`Object`/`Array`, they are both converted to `Number`
- Comparison (`<`, `>`)
  1. `Symbol` cannot be one of the operands (if it is, there will be an attempt to automatically convert it to `Number` which will result in `TypeError`)
  2. If one of the operands is `BigInt`, the other one is converted to `BigInt`
  3. Otherwise, if one of the operands is either `Number`/`Boolean`/`null`/`undefined`, they are both converted to `Number`
  4. Otherwise, if both the operands are either `String`/`Object`/`Array`, they are both converted to `String`
- Regular equality check (`==`):
  1. Although `Symbol` can be one of the operands (with any other type as the second one), it does not equal (`==`) any other value
  2. `NaN`, `null`, and `undefined` do not equal (`==`) any other value
     - Examples:
       - `NaN != NaN`
       - `null != 0`; `null != 0n`
     - Irreguralities:
       - `null === null`
       - `undefined === undefined`
       - `null == undefined` (while naturally still: `null !== undefined`)
  3. If one of the operands is `BigInt`, the other one is converted to `BigInt`
  4. Otherwise, if one of the operands is either `Number`/`Boolean`/`null`/`undefined`, they are both converted to `Number`
  5. Otherwise, if both the operands are either `String`/`Object`/`Array`, they are both converted to `String`

Conversion rules:
- To `Number`:
  - `0.0`/`0.`/`0n` &rightarrow; `0`
  - `""`/`" "` &rightarrow; `0`; `"2"`/`"2."` &rightarrow; `2`; `"2.2"` &rightarrow; `2.2`; `"2n"` &rightarrow; `NaN`
  - `false` &rightarrow; `0`; `true` &rightarrow; `1`
  - `null` &rightarrow; `0`
  - `undefined` &rightarrow; `NaN`
  - `Symbol()` &rightarrow; `TypeError`
  - `{}` &rightarrow; `NaN`
  - `[]` &rightarrow; `0`; `[2]`/`[2.]` &rightarrow; `2`; `[0, 0]` &rightarrow; `NaN`
- To `BigInt`:
  - `0`/`0.0`/`0.` &rightarrow; `0n`; `0.2`/`Infinity`/`NaN` &rightarrow; `RangeError`
  - `""`/`" "`/`"0"` &rightarrow; `0n`; `"2"` &rightarrow; `2n`; `"2."`/`"2n"` &rightarrow; `SyntaxError`
  - `false` &rightarrow; `0n`; `true` &rightarrow; `1n`
  - `null` &rightarrow; `TypeError`
  - `undefined` &rightarrow; `TypeError`
  - `Symbol()` &rightarrow; `TypeError`
  - `{}` &rightarrow; `SyntaxError` (`{}` is firstly converted to `String`)
  - `[]` &rightarrow; `0n`; `[2]`/`[2.]` &rightarrow; `2n`; `[2n]` &rightarrow; `2n`; `[0, 0]` &rightarrow; `SyntaxError`
- To `String`:
  - `NaN` &rightarrow; `"NaN"`
  - `0n` &rightarrow; `"0"`
  - `false` &rightarrow; `"false"`
  - `null` &rightarrow; `"null"`
  - `undefined` &rightarrow; `"undefined"`
  - `Symbol("Description")` &rightarrow; `"Symbol(Description)"`
  - `{}` &rightarrow; `"[object Object]"`
  - `[0, 0]` &rightarrow; `"0,0"`
- To `Boolean`
  - `-0`/`0`/`NaN` &rightarrow; `false`; `-2`/`2`/`-Infinity`/`Infinity` &rightarrow; `true`
  - `-0n`/`0n` &rightarrow; `false`; `-2n`/`2n` &rightarrow; `true`
  - `""` &rightarrow; `false`; `" "`/`"0"` &rightarrow; `true`
  - `null` &rightarrow; `false`
  - `undefined` &rightarrow; `false`
  - `Symbol()` &rightarrow; `true`
  - `{}` &rightarrow; `true`
  - `[]`/`[0]`/`[false]` &rightarrow; `true`

# Code Structures

## Functions

### Regular Functions

|                             |Syntax                                          |Notes                                                      |
|-----------------------------|------------------------------------------------|-----------------------------------------------------------|
|**Function Declaration**     |`function f() {}`                               |Can be called before its declaration                       |
|**Function Expression**      |`const f = function() {}`                       |Can be called only after its creation                      |
|                             |                                                |Allows a conditional declaration                           |
|**Named Function Expression**|`const f = function func() {}`                  |Allows the function to call itself                         |
|**Arrow Function**           |`const f = () => {}`                            |Convenient for simple actions or as callbacks              |
|**Function Constructor**     |`(new Function('a', 'b', 'return a + b'))(1, 2)`|Converts strings into a function parameters and body       |
|                             |                                                |`[[Environment]]` references the global Lexical Environment|

Parameters and arguments:
- The spread syntax (`...`) may be used in the list of function's arguments
- Gathering the remaining arguments into an array:
    - `function f(a, b, ...rest) {}`
    - `...` must be placed at the end of the list of parameters
- Accessing all the arguments:
  - `arguments` (an automatically created array-like object)
  - Does not work for arrow functions' arguments
- Destructuring an object of arguments:
  - `function f({ arg1: a = 1, b = 2 } = {}) { return a + b; } f({ arg1: 3 });`

Function object properties:
- `name`
- `length`: number of parameters (not arguments); doesn't count the `...rest` parameter
- `prototype`: its value is an object containing only one property (`constructor`) that points to the function itself:
  - `f.prototype.constructor === f`
- Custom properties may be added as well

Returned value:
- Empty or no `return` results in returning `undefined`
- A semicolon is automatially placed at the end of a line containing the `return` keyword

### Constructor Functions

Creation/usage rules:
- The first letter of the function name must be capital
- Should be executed with the `new` operator
  - `new.target` is sometimes used (e.g. `function f() { if (!new.target) { return new f(); } }`) to test whether the function was called with `new` by returning:
    - `undefined` if the function was called without `new`
    - the function itself if it was called with `new`
- When executing with the `new` operator, parentheses may be omitted, but it's not a good practice
- Arrow function cannot be used as a constructor function because of not having `this` but rather taking it from the global Lexical Environment

Function object properties:
- The object strored in the `prototype` property will be set as the prototype for the object created with the constructor function
- Since by default `F.prototype.constructor === F`: `const f = new F()` &rightarrow; `f.constructor === F`
  - The default `prototype.constructor` property can be overridden:
    - `F.prototype = {}` &rightarrow; `const f = new F()` &rightarrow; `f.constructor !== F` & `typeof F1.prototype.constructor === "function"`

Returned value:
- Does not have the `return` statement as it returns `this`
- If there is a `return` statement then it returns:
  - an object passed with the `return`
  - `this`, if the `return` is not passing an object

### Generators

Generator function:
- Syntax: `function* f()` (preferred) or `function *f()`
- Returns a generator object
- Yielding another generator object is possible (generator composition)

Generator object:
- Is an iterable
- `next` method returns `{ value: <the next yielded value>, done: <true/false> }`
- `for...of` and the spread syntax (`...`) used on the object ignore the value returned with `return` (because it has `done: true`)

Basic example:

```js
function* generateNumbers() {
  yield 1;
  yield 2;
  yield 3; /* OR: return 3; then: `done: true` */
}

const generator = generateNumbers();

console.log(generator); // Object [Generator] {}
console.log(generator.next()); // { value: 1, done: false }
console.log(generator.next()); // { value: 2, done: false }
console.log(generator.next()); // { value: 3, done: false }
console.log(generator.next()); // { value: undefined, done: true }
```

Async generator:

```js
async function* generateNumbers() {
  for (let i = 0; i < 5; i++) {
    yield await new Promise(resolve => setTimeout(resolve, 200, i));
  }
}

let generator = generateNumbers();

(async () => {
  for await (let value of generator) console.log(value); // 0 1 2 3 4
})();
```

Stopping a generator with a specific condition:

```js
function* generate() {
  yield 1;
  yield 2;
  yield 3;
}

const generator = generate();

console.log(generator.next());
console.log(generator.return(4));
console.log(generator.next());
console.log(generator.return(5));
console.log(generator.next());
/*
{ value: 1, done: false }
{ value: 4, done: true }
{ value: undefined, done: true }
{ value: 5, done: true }
{ value: undefined, done: true }
*/
```

Passing values into a generator:

```js
function* generate() {
  let passed1 = yield 1;
  yield 2;
  let passed2 = yield 3;

  console.log(`Passed #1: ${passed1}`);

  yield 4;
  
  console.log(`Passed #2: ${passed2}`);
}

let generator = generate();

console.log(generator.next());
console.log(generator.next());
console.log(generator.next());
console.log(generator.next());
/*
{ value: 1, done: false }
{ value: 2, done: false }
{ value: 3, done: false }
Passed #1: undefined
{ value: 4, done: false }
*/

generator = generate();
console.log(generator.next());
console.log(generator.next());
console.log(generator.next());
console.log(generator.next());
console.log(generator.next());
/*
{ value: 1, done: false }
{ value: 2, done: false }
{ value: 3, done: false }
Passed #1: undefined
{ value: 4, done: false }
Passed #2: undefined
{ value: undefined, done: true }
*/

generator = generate();
console.log(generator.next());
console.log(generator.next(4));
console.log(generator.next());
console.log(generator.next(5));
console.log(generator.next());
/*
{ value: 1, done: false }
{ value: 2, done: false }
{ value: 3, done: false }
Passed #1: 4
{ value: 4, done: false }
Passed #2: 5
{ value: undefined, done: true }
*/
```

Throwing an error into a generator (inside or outside the generator function):

```js
function* generate() {
  try {
    yield 1;
    yield 2;
    yield 3;
  } catch (error) {
    console.log("Error handled");
  }
}

let generator = generate();

console.log(generator.next());
console.log("Error occurred", generator.throw(new Error()));
console.log(generator.next());
/*
{ value: 1, done: false }
Error handled
Error occurred { value: undefined, done: true }
{ value: undefined, done: true }
*/
```

```js
function* generate() {
  yield 1;
  yield 2;
  yield 3;
}

let generator = generate();

try {
  console.log(generator.next());
  console.log("Error occurred", generator.throw(new Error()));
  console.log(generator.next());
} catch (error) {
  console.log("Error handled");
}
/*
{ value: 1, done: false }
Error handled
*/
```

## Classes

### Ontology

...

### Inheritance

...

### Encapsulation

...

## Synchronous Control Flow

### Conditionals

|Conditional|Use case                            |Note                        |
|-----------|------------------------------------|----------------------------|
|`?`        |Returning one of the two values     |                            |
|`if`       |Executing different branches of code|                            |
|`switch`   |Comparing different value variants  |The equality check is strict|

```js
switch(x) {
  case 0:
    /* ... */
    break;

  case 1:
    /* ... */
    break;

  default:
    /* ... */
}
```

### Loops

```js
while (condition) {
  /* ... */
}
```

```js
do {
  /* ... */
} while (condition);
```

```js
for (;;) {
  /* ... */
}
```

### Control Transfer

|Directive |Result                      |Use Case                                      |Placement           |
|----------|----------------------------|----------------------------------------------|--------------------|
|`break`   |Breaks the whole loop       |Evaluating condition in the middle of the loop|Inside a block      |
|          |                            |                                              |Not allowed with `?`|
|`continue`|Breaks the current iteration|Avoiding conditional's nesting in the loop    |Inside a loop       |
|          |                            |                                              |Not allowed with `?`|

A label may be used to `break`/`continue` from a nested loop

### Error Handling

```js
try {
  /* ... */
  throw new Error("Message");
  /* ... */
} catch (error) {
  /* ... */
} finally {
  /* If an error hasn't been caught, the error will break the code exexution only after the "finally" block has been executed */
}
```

Scheduled functions are executed after the engine has already left the `try...catch` construct

## Asynchronous Control Flow

### Callback-Based

Rules:
- A callback function is passed as an argument to the function that has asynchronous code
- The first argument of the callback functions is reserved for an error

```js
function asyncF(string, callback) {
  setTimeout(() => {
    try {
      if (Math.random() > 0.5) throw new Error("Error");

      callback(null, string);
    } catch (error) {
      callback(error);
    }
  });
}

function callbackF(error, val) {
  console.log(error ? error.message : val);
}

asyncF("Test", callbackF); // "Test"
asyncF("Test", callbackF); // "Error message"
asyncF("Test", callbackF); // "Test"
```

Nested callbacks:

```js
function firstAsyncF(string, callback) {
  setTimeout(() => {
    try {
      if (Math.random() > 0.5) throw new Error("Error at Step 1");

      secondAsyncF(string, callback);
    } catch (error) {
      callback(error);
    }
  });
}

function secondAsyncF(string, callback) {
  setTimeout(() => {
    try {
      if (Math.random() > 0.5) throw new Error("Error at Step 2");

      callback(null, string);
    } catch (error) {
      callback(error);
    }
  });
}

function callbackF(error, val) {
  console.log(error ? error.message : val);
}

firstAsyncF("Full Success", callbackF); // "Error at Step 1"
firstAsyncF("Full Success", callbackF); // "Error at Step 2"
firstAsyncF("Full Success", callbackF); // "Full Success"
```

### Promises

Syntax:
- The executor function is passed as an argument to the promise constructor and is executed automatically
- Two callbacks (`resolve` and `reject`) are passed as arguments to the executor function to be later called with `value` or `error` respectively
- The promise constructor returns an object which has these inaccessible internal properties:
  - `state`: `pending` or settled (`fulfilled`/`rejected`)
  - `result`: `undefined`/`value`/`error`
- Consuming functions can be registered using these methods:
  - `finally` for executing finalizing procedures whether the promise was resolved or rejected
    - Doesn't return anything by default
    - Any returns are ignored
    - However, it's possible to throw an error that will be passed to the next handler instead of any previous result/error
  - `then` which receives two callbacks as its arguments
    - The first callback (success handler, `onFulfilled`) receives the result if the promise was resolved
    - The second callback (failure handler, `onRejected`) receives the error if the promise was rejected
  - `catch` which receives the failure handler as its argument
- Any handler added to an already settled promise will run immediately

```js
const promise = new Promise((resolve, reject) => {
  if (Math.random() > 0.5) {
    resolve("Success");
  } else {
    reject("Failure");
  }
});

promise
  .finally(() => console.log("Finalizing..."))
  .then((value) => console.log(value))
  .catch((error) => console.error(error));
```

Promise chaining/composition:
- Success/failure handler used in `then` may create and return
  - A new promise
  - A "thenable" object (an object containing `then` method; doesn't need to inherit from `Promise`) which will be treated as a promise
- `then` always returns a new promise

```js
new Promise(resolve => resolve("Ok"))
  .then(result => {})
  .then(result => console.log(result));
// undefined

new Promise(resolve => resolve("Ok"))
  .then(result => { return 0; })
  .then(result => console.log(result));
// 0

new Promise(resolve => resolve("Ok"))
  .then(result => { return new Promise(resolve => resolve(result)); })
  .then(result => console.log(result));
// "Ok"
```

Error handling:
- Errors coming from the code of the executor function or the promise handlers are automatically treated as a promise rejection
- If an error is successfully handled by a handler, the next success handler runs; if an error is not handled, the next failure handler runs
- If a promise rejection is not handled, a global error occurs, which can be caught in the browser using the `unhandledrejection` event (which would fire when the microtask queue is empty):

```js
window.addEventListener('unhandledrejection', (e) => {
  console.log("Gloabl error occured!", e.promise, e.reason);
});

new Promise((resolve, reject) => reject(new Error()))
  .then(() => console.log("Success!"));

/*
"Gloabl error occured!"
[object Promise] { ... }
[object Error] { ... }
*/
```

- Rules for handling errors:
  - `catch` should be used where/when handling expected errors is possible; unknown errors should be rethrown
  - `catch` may be omitted if errors cannot be handled
  - `unhandledrejection` (in the browser runtime environment) event handler should be used to inform (users, server) about unhandled errors

### async/await

`async` function always returns a promise - values other than a promise are wrapped in a resolved promise

`await`:
- Pauses the function execution until the promise is settled &rightarrow; Returns the result/error
- To avoid `SyntaxError`, `await` must be either:
  - Placed in an `async` function
  - Wrapped into an anonymous `async` function
  - Used at a module top-level
- Can also be used with "thenables"

```js
async function asyncF() {
  return await new Promise((resolve, reject) => setTimeout(() => {
    if (Math.random() > 0.5) {
      resolve("Success");
    } else {
      reject(new Error("Failure"));
    }
  }));
}

asyncF().then(console.log, console.error); // "Success" OR "Error: Failure"
```

The syntax also works for object/class methods:

```js
class Cl {
  async f() {
    return await Promise.resolve("Ok!");
  }
}

new Cl()
  .f()
  .then(console.log); // "Ok!"
```

Promise chaining/composition:

```js
// USING 'THEN' METHOD:
new Promise(resolve => resolve("Ok!"))
  .then(result => { return new Promise(resolve => resolve (result)) })
  .then(result => console.log(result));
// "Ok!"

// USING ASYNC/AWAIT SYNTAX:
(async () => {
  const result1 = await new Promise(resolve => resolve("Ok!"));
  const result2 = await new Promise(resolve => resolve(result1));
  console.log(result2);
})();
// "Ok!"
```

Error handling (either by `try...catch` or `catch` method):

```js
(async () => {
  try {
    let val = await Promise.reject(new Error("Failure"));
  } catch (error) {
    console.error(error.message);
  }
})();
// Failure

(async function f() {
  return await Promise.reject(new Error("Failure"));
})()
  .catch(error => console.log(error.message));
// Failure
```

# Built-In Objects & Classes

## `globalThis`

### `isFinite`/`isNaN`

- `isFinite(<value>)` checks whether a value converted to a number is not `NaN`/`Infinity`/`-Infinity`
- `isNaN(<value>)` checks whether a value converted to a number is `NaN`

### `parseInt`/`parseFloat`

- Extracting a number from a string:

```js
console.log(parseInt("1 USD")); // 1
console.log(parseFloat("1.5 USD")); // 1.5

console.log(parseInt("$1")); // NaN
console.log(parseFloat("$1.5")); // NaN
```

- Converting a number from a non-decimal numeral system:

```js
console.log(parseInt("0xff")); // 255
console.log(parseInt("111", 2)); // 7
```

### `eval`

```js
let a = 1;

const result = eval(`
  let b = 2;

  function f(a, b) {
    console.log(a + b);
  }

  f(a, b);

  a += 0.1;

  100 + 100;
`); // 3

console.log(result); // 200
console.log(a); // 1.1
```

Using `eval` negatively affects minification ratio as minifiers don't rename local variables potentially visible to the code string

Using outer local variables in `eval` negatively affects code maintenance; if `eval` doesn't use them, call it from the global object...

```js
let a = 1;

{
  let a = 2;

  eval(`console.log(a);`); // 2
}
```

```js
let a = 1; // Executed in the global context (not in a module)

{
  let a = 2;

  globalThis.eval(`console.log(a);`); // 1
}
```

... and if `eval` uses them, replace `eval` with `new Function`:

```js
let a = 1;

{
  let a = 2;

  // eval(`console.log(a);`); // 2
  // Replace with:
  (new Function('a', 'console.log(a)'))(a); // 2
}
```

## `Object`

### `Object.prototype`

- All objects inherit from `Object.prototype`:

```js
console.log(Function.prototype.__proto__ === Object.prototype); // true
console.log({}.__proto__ === Object.prototype); // true
console.log({}.toString === Object.prototype.toString); // true
```

- The value of `[[Prototype]]` for `Object.prototype` is `null`:

```js
console.log(Object.prototype.__proto__); // null
```

### `Object.prototype.toString`

Can display the type of:
- Primitives
- Built-in objects
- Objects with `Symbol.toStringTag`

```js
console.log({}.toString === Object.prototype.toString);             // true

console.log({}.toString.call(1));                                   // "[object Number]"
console.log({}.toString.call(1n));                                  // "[object BigInt]"
console.log({}.toString.call(true));                                // "[object Boolean]"
console.log({}.toString.call(""));                                  // "[object String]"
console.log({}.toString.call(null));                                // "[object Null]"
console.log({}.toString.call(undefined));                           // "[object Undefined]"
console.log({}.toString.call({}));                                  // "[object Object]"
console.log({}.toString.call({ [Symbol.toStringTag]: "Custom" }));  // "[object Custom]""
console.log({}.toString.call(Symbol()));                            // "[object Symbol]"
console.log({}.toString.call(new Array()));                         // "[object Array]""
console.log({}.toString.call(new Map()));                           // "[object Map]""
console.log({}.toString.call(new WeakMap()));                       // "[object WeakMap]""
console.log({}.toString.call(new Set()));                           // "[object Set]""
console.log({}.toString.call(new WeakSet()));                       // "[object WeakSet]""
console.log({}.toString.call(new Promise((resolve) => {})));        // "[object Promise]""
console.log({}.toString.call(() => {}));                            // "[object Function]""
console.log({}.toString.call(new SyntaxError()));                   // "[object Error]""    (*)

                                                                    // (*) Interesting case
```

### `Object.is`

Differs from strict comparison `===` in two edge cases:

```js
console.log(Object.is(NaN, NaN)); // true
console.log(Object.is(0, -0)); // false
```

### `Object.`<`keys`/`values`/`entries`/`fromEntries`>

Do not include:
- Symbolic properties
- Inherited properties

`Object.keys`/`Object.values`/`Object.entries` return an array

`Object.fromEntries` returns an object

### `Object.`<`getOwnPropertyDescriptor`/`getOwnPropertyDescriptors`>

Property descriptor is an object containing the property value and all its flags

`Object.getOwnPropertyDescriptors` allows to list non-enumerable property descriptors

```js
const obj = {
  a: 1,
  b: 2
};

console.log(Object.getOwnPropertyDescriptor(obj, 'a'));
// { value: 1, writable: true, enumerable: true, configurable: true }

console.log(Object.getOwnPropertyDescriptors(obj));
/*
{
  a: { value: 1, writable: true, enumerable: true, configurable: true },
  b: { value: 2, writable: true, enumerable: true, configurable: true }
}
*/
```

### `Object.`<`defineProperty`/`defineProperties`>

Creating/modifying property attributes (with all the flags set to `false` by default):

```js
const obj = {};

Object.defineProperties(obj, {
  'a': { value: 1 },
  'b': { value: 2, writable: true }
});
Object.defineProperty(obj, 'b', { value: 3 });

console.log(Object.getOwnPropertyDescriptors(obj));
/*
{
  a: { value: 1, writable: false, enumerable: false, configurable: false },
  b: { value: 3, writable: true, enumerable: false, configurable: false }
}
*/
```

### `Object.`<`preventExtensions`/`seal`/`freeze`>

These methods work for the whole object:
- `Object.preventExtensions` disallows adding new properties
- `Object.seal()` sets `configurable` attribute to `false` for all properties
- `Object.freeze()` sets `configurable` and `writable` attributes to `false` for all properties

These corresponding methods return `true` or `false`:
- `Object.isExtensible()`
- `Object.isSealed()`
- `Object.isFrozen()`

### `Object.`<`setPrototypeOf`/`getPrototypeOf`/`create`>

- `Object.setPrototypeOf`/`Object.getPrototypeOf` allows to set/get object `[[Prototype]]` in a modern way:

```js
const objProto = { a: 1 };
const obj = { b: 2 };

Object.setPrototypeOf(obj, objProto);
console.log(Object.getPrototypeOf(obj)); // [object Object] { a: 1 }
```

- `Object.create` allows to create a new object with a specified `[[Prototype]]` and optionally with additional specified property descriptors:

```js
const objProto = { a: 1 };

const obj = Object.create(objProto, {
  b: {
    value: 2
  }
});
console.log(Object.getPrototypeOf(obj)); // [object Object] { a: 1 }
console.log(Object.getOwnPropertyDescriptors(obj));
/*
[object Object] {
  b: [object Object] {
    configurable: false,
    enumerable: false,
    value: 2,
    writable: false
  }
}
*/
```

### `Object.assign`

`Object.assign(<target>, <...sources>)`:
- Returns a modified `<target>` containing copied properties from all the `<sources>`
- Special features:
  - Copies symbol properties
- Limitations:
  - Properties that are objects are copied by reference
  - Doesn't copy:
    - Non-enumerable properties
    - Accessor properties
    - Inherited properties

## `Number`

...

## `BigInt`

...

## `String`

### `String.prototype.localeCompare`

- Compares two strings according to the ECMA-402 internationalization standard
- Can be customized by additional parameters

```js
console.log("a".localeCompare("b") < 0); // true
console.log("b".localeCompare("b") === 0); // true
console.log("b".localeCompare("a") > 0); // true
```

Doesn't work well with numbers:

```js
console.log("2".localeCompare("10") < 0); // false
// console.log(2..localeCompare(10)); // TypeError
console.log(String.prototype.localeCompare.call(2, 10) < 0); // false
```

### `String.prototype.`<`indexOf`/`lastIndexOf`/`includes`/`startsWith`/`endsWith`>

```js
console.log("abcd-abcd".indexOf("e")); // -1
console.log("abcd-abcd".indexOf("ab")); // 0
console.log("abcd-abcd".indexOf("ab", 1)); // 5

console.log("abcd-abcd".lastIndexOf("e")); // -1
console.log("abcd-abcd".lastIndexOf("ab")); // 5
console.log("abcd-abcd".lastIndexOf("ab", 4)); // 0
```

```js
console.log("abcd".includes("ab")); // true
console.log("abcd".includes("ab", 1)); // false

console.log("abcd".startsWith("ab")); // true
console.log("abcd".startsWith("bc", 1)); // true

console.log("abcd".endsWith("cd")); // true
console.log("abcd".endsWith("bc", 3)); // true
```

### `String.prototype.`<`at`/`slice`>

```js
console.log("123".at(0)); // "1"
console.log("123".at(-1)); // "3"

console.log("abcd".slice()); // "abcd"
console.log("abcd".slice(1)); // "bcd"
console.log("abcd".slice(-1)); // "d"
console.log("abcd".slice(1, 2)); // "b"
console.log("abcd".slice(-3, -2)); // "b"
```

### `String.prototype.`<`toLowerCase`/`toUpperCase`>

```js
console.log("ABC".toLowerCase()); // "abc"
console.log("abc".toUpperCase()); // "ABC"
```

## `Boolean`

...

## `Symbol`

...

## `Array`

### `Array.prototype.`<`indexOf`/`lastIndexOf`/`includes`>

```js
const arr = [1, 2, 3, 1];

console.log(arr.indexOf(4)); // -1
console.log(arr.indexOf(1)); // 0
console.log(arr.indexOf(1, 1)); // 3

console.log(arr.lastIndexOf(4)); // -1
console.log(arr.lastIndexOf(1)); // 3
console.log(arr.lastIndexOf(1, 1)); // 0

console.log(arr.includes(2)); // true
console.log(arr.includes(2, 2)); // false

console.log([NaN].indexOf(NaN)); // -1 (doesn't work for NaN)
console.log([NaN].includes(NaN)); // true (works for NaN)
```

### `Array.prototype.`<`at`/`slice`>

```js
console.log([1, 2, 3].at(0)); // "1"
console.log([1, 2, 3].at(-1)); // "3"
```

```js
const arr = [1, 2, 3, 4];

console.log(arr.slice()); // [1, 2, 3, 4] (clone of the array)
console.log(arr.slice(1)); // [2, 3, 4]
console.log(arr.slice(-1)); // [4]
console.log(arr.slice(1, 2)); // [2]
console.log(arr.slice(-3, -2)); // [2]
```

### `Array.prototype.`<`push`/`pop`/`unshift`/`shift`>

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

### `Array.prototype.concat`

```js
console.log([1, 2].concat([3, 4, [5, 6]], 7, 8)); // [ 1, 2, 3, 4, [ 5, 6 ], 7, 8 ]
```

### `Array.prototype.`<`sort`/`reverse`>

Theses methods modify the array and return it

`Array.prototype.sort` sorts the elements as being converted to `String` so an ordering function may be needed:

```js
console.log([1, 2, 10].sort()); // [1, 10, 2]
console.log([1, 2, 10].sort((a, b) => a - b)); // [1, 2, 10]

console.log(["a", "ą", "z"].sort()); // ["a", "z", "ą"]
console.log(["a", "ą", "z"].sort((a, b) => a.localeCompare(b))); // ["a", "ą", "z"]
```

### `Array.prototype.`<`toString`/`join`/`split`>

```js
console.log([1, 2, 3].toString()); // "1,2,3"

console.log([1, 2, 3].join(", ")); // "1, 2, 3"

console.log("1, 2, 3".split(", ")); // ["1", "2", "3"]
console.log("1, 2, 3".split(", ", 2)); // ["1", "2"]
```

### `Array.prototype`'s Iterative Methods

All iterative methods except `reduce`/`reduceRight` accept `thisArg` (which then becomes `this` for the callback function) as an argument in addition to a callback function

```js
arr = [{a: 1}, {a: 2}, {a: 3}];

arr.forEach((item, index, array) => console.log(item.a)); // 1 2 3

console.log(arr.find((item, index, array) => item.a === 4));  // undefined
console.log(arr.find((item, index, array) => item.a > 1));    // { a: 2 }
console.log(arr.findLast((item, index, array) => item.a < 3)); // { a: 2 }

console.log(arr.findIndex((item, index, array) => item.a === 4)); // -1
console.log(arr.findIndex((item, index, array) => item.a > 1));   // 1
console.log(arr.findLastIndex((item, index, array) => item.a < 3)); // 1

console.log(arr.some((item, index, array) => item.a < 3));  // true
console.log(arr.every((item, index, array) => item.a > 0)); // true

console.log(arr.filter((item, index, array) => item.a > 1));  // [ { a: 2 }, { a: 3 } ]
console.log(arr.map((item, index, array) => item.a * 2));     // [ 2, 4, 6 ]

console.log(arr.reduce((accumulator, item, index, array) => accumulator += item.a, ""));      // "123"
console.log(arr.reduceRight((accumulator, item, index, array) => accumulator += item.a, "")); // "321"

// console.log([].reduce((accumulator, item, index, array) => accumulator += 1));
// TypeError: Reduce of empty array with no initial value
console.log(arr.reduce((accumulator, item, index, array) => accumulator += item.a));
// "[object Object]23"
console.log(arr.reduceRight((accumulator, item, index, array) => accumulator += item.a));
// "[object Object]21"
```

### `Array.isArray`

```js
console.log(typeof []); // "object"

console.log(Array.isArray([])); // true
```


### `Array.from`

Allows to make an array (shallow copy) from an iterable or an array-like object

## `Map`

...

## `WeakMap`

...

## `Set`

...

## `WeakSet`

...

## `Math`

### Other Methods

```js
console.log(Object.keys(Object.getOwnPropertyDescriptors(Math)));
/*
[
  'abs',    'acos',    'acosh',  'asin',
  'asinh',  'atan',    'atanh',  'atan2',
  'ceil',   'cbrt',    'expm1',  'clz32',
  'cos',    'cosh',    'exp',    'floor',
  'fround', 'hypot',   'imul',   'log',
  'log1p',  'log2',    'log10',  'max',
  'min',    'pow',     'random', 'round',
  'sign',   'sin',     'sinh',   'sqrt',
  'tan',    'tanh',    'trunc',  'E',
  'LN10',   'LN2',     'LOG10E', 'LOG2E',
  'PI',     'SQRT1_2', 'SQRT2'
]
*/
```

## `Date`

...

## `JSON`

### `JSON.stringify`

|Data Type         |Support    |
|------------------|-----------|
|`Number`          |Yes        |
|`BigInt`          |`TypeError`|
|`String`          |Yes        |
|`Boolean`         |Yes        |
|`Symbol`          |*Ignored*  |
|`null`            |Yes        |
|`undefined`       |*Ignored*  |
|`Object`          |Yes        |
|Circural Reference|`TypeError`|
|`Function`        |*Ignored*  |
|`Array`           |Yes        |

Output formatting:
- Strings are double-quoted
- Object property names are double-quoted
- All whitespace is removed by default (can be configured in the third argument)

The second (optional; e.g. to exclude circular references) argument of `JSON.stringify` can be:
- An array of explicitly specified property names to encode:
  - Property names must be passed as `String` each
  - Nested properties must be specified if they are to be included
- A mapping function (replacer)
  - To be called for each key/value pair (including nested objects and array items), e.g.:
    - `(key, value) => key === "ref" ? undefined : value)`
  - To address the entire object (which is passed to the function as the value of the first key, an empty one), e.g.:

```js
const objA = { a: 1 };
const objB = [2];

for (let obj of [objA, objB]) {
  console.log(JSON.stringify(obj, (key, value) => value === objA ? null : value));
}
// null
// [2]
```

The third (optional) argument of `JSON.stringify` is the number of spaces (or a string) to be used to format the output string, e.g.:
  - `JSON.stringify(obj, null, 2)`
  - `JSON.stringify(obj, null, '  ')`

Customizing JSON encoding:

```js
const obj = {
  a: 1,
  b: {
    b1: 2,
    b2: 3,

    toJSON() {
      return `${this.b1}|${this.b2}`;
    }
  },
  c: [4, 5]
};

console.log(JSON.stringify(obj)); // {"a":1,"b":"2|3","c":[4,5]}
```

### `JSON.parse`

The second (optional) argument is a mapping function (reviver) that is to be called for each key/value pair (including nested objects and array items)

```js
const json = '{"a":1,"b":{"date":"1970-01-02T10:00:00.000Z"},"c":[4,5]}';

console.log(JSON.parse(json));
// { a: 1, b: { date: '1970-01-02T10:00:00.000Z' }, c: [ 4, 5 ] }

console.log(
  JSON.parse(json, (key, value) => key === "date" ? new Date(value) : value)
    .b.date.getTime()
);
// 122400000
```

## `Function`

### `Function.prototype.`<`call`/`apply`>

Calling a function with a specified context (`this`):
- `call(<this>, <...args>)` receives its arguments as a list
- `apply(<this>, <[...args]>)` receives its arguments as an `Array`/array-like object

### `Function.prototype.bind`

Returns a function bound to:
- A specified context (`this`) passed as the first argument (may be `null`)
- A specified list of arguments passed after the first argument

## `Promise`

### `Promise.`<`all`/`allSettled`>

`Promise.all`:
- Executes many promises concurrently until:
  - All are resolved, or
  - Any of them is rejected
    - Then the resulting promise is immediately rejected while remaining source promises operations continue with their results being ignored
- Takes an iterable of:
  - Promises, or
  - Values to be passed "as is" to the resulting promise
- Returns a promise which either:
  - Rejects with a single error, or
  - Resolves with an array of results (ordered as the source promises)

`Promise.allSettled`:
- Executes many promises concurrently until all are settled (resolved/rejected)
- Takes an iterable of:
  - Promises, or
  - Values to be passed "as is" to the resulting promise
- Returns a promise which resolves with an array of objects (ordered as the source promises):
  - `{ status: "fulfilled", value: <result> }` for each fulfilled promise, or
  - `{ status: "rejected", reason: <error> }` for each rejected promise

### `Promise.`<`race`/`any`>

`Promise.race`:
- Executes many promises concurrently until any first of them is settled (resolved/rejected)
  - The remaining source promises operations continue with their results being ignored
- Takes an iterable of:
  - Promises, or
  - Values to be passed "as is" (but then only the first one will be passed)
- Returns a promise which either:
  - Rejects with a single error, or
  - Resolves with a single result

`Promise.any`:
- Executes many promises concurrently until:
  - Any first of them is resolved, or
  - All are rejected
- Takes an iterable of:
  - Promises, or
  - Values to be passed "as is" (but then only the first one will be passed)
- Returns a promise which either:
  - Rejects with with `AggregateError` object which stores an array of all the source promises errors in its `errors` property, or
  - Resolves with a single result

### `Promise.`<`resolve`/`reject`>

`Promise.resolve`:
- Returns a promise resolved with the passed value
- Used if `async`/`await` is not supported but a function must return a promise

`Promise.reject`:
- Returns a promise rejected with the passed error
- Almost never used

## `Error`

Properties:
- `name`
- `message`
- `stack`

Inheriting error objects:
- `AggregateError`
- `RangeError`
- `ReferenceError`
- `SyntaxError`
- `TypeError`

# Programming Techniques

## Objects

### Shallow Cloning Objects

- Method #1: `Object.assign`

```js
Object.assign(clonedObj1, obj);
```

- Method #2: A combination of `Object.defineProperties` and `Object.getOwnPropertyDescriptors`

```js
Object.defineProperties(clonedObj, Object.getOwnPropertyDescriptors(obj));
```

- Method #3: A combination of `Object.create`, `Object.getPrototypeOf`, and `Object.getOwnPropertyDescriptors`

```js
const clonedObj = Object.create(Object.getPrototypeOf(obj), Object.getOwnPropertyDescriptors(obj));
```

|Method|Attributes|Symbolic|Non-enumerable|Accessor|`[[Prototype]]`|
|:----:|:--------:|:------:|:------------:|:------:|:-------------:|
|#1    |-         |`Yes`   |-             |-       |-              |
|#2    |`Yes`     |`Yes`   |`Yes`         |`Yes`   |-              |
|#3    |`Yes`     |`Yes`   |`Yes`         |`Yes`   |`Yes`          |
