# JavaScript Reference Summary

## TOC

### Basics

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
- **Synchronous Control Flow**
  - Conditionals
  - Loops
  - Control Transfer
  - Error Handling

### Data Types

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
  - Arrays
  - Array-Like Objects
  - Iterable Objects
  - Async Iterable Objects
  - Maps
  - WeakMaps
  - Sets
  - WeakSets
- **Type Operations**
  - Checking
  - Conversion

### Classes

- Ontology
- Inheritance
- Encapsulation

### Functions

- Creation
- Usage
- Function Objects
- Constructor Functions
- Generators
- Async Generators

### Asynchronous Control Flow

- Callback-Based
- Promises
- async/await

### Built-In Objects

- Global Scope Objects
- Global Object
- Object
- Number
- String
- Symbol
- Array
- Map
- WeakMap
- Set
- WeakSet
- Math
- Date
- JSON
- Error

### Techniques

- ...

# Basics

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

### Arrays

`new Array(n)` creates an array with `n` empty (not even `undefined`) elements

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

### WeakMaps

...

### Sets

...

### WeakSets

...

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
