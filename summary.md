# JavaScript Reference Summary

## TOC

### Basics

- Code Parsing & Execution
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
- Operators
  - Arithmetic
  - Bitwise
  - Logical
  - Comparison
  - Assignment
  - Increment/Decrement
  - Comma
- Synchronous Control Flow
- Error Handling

### Data Types

- Primitives
- Objects
- Type Conversion

### Data Collections

- Array-Like Objects
- Iterable Objects
- Async Iterable Objects

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

### Classes

- Ontology
- Inheritance
- Encapsulation

### Techniques

- ...

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

...

### Bitwise

...

### Logical

...

### Comparison

...

### Assignment

...

### Increment/Decrement

...

### Comma

...
