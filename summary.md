# JavaScript Reference Summary

## TOC

### Basics

- Variables
  - Declaration
  - Hoisting
  - Scope
  - Lexical Environment
  - Closure
- Strict Mode
- Operators
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

### Internals

- Event Loop
- Memory

### Techniques

## Variables

### Declaration

A variable declared with `var` can be redeclared

A variable declared with `const` cannot be reassigned

### Hoisting

At compile time the engine allocates memory by hoisting variable names and function declarations to the top of their corresponding scopes; functions are initialized immediately while variable initializations are done in-place

A `var` declaration (without the assignment) is hoisted to the top of its scope and given an initial value of `undefined`

No-keyword "declaration" (an assignment without a previous declaration) is not hoisted

A `let`/`const` declaration is hoisted but not initialized, so that the variable remains in a *temporal dead zone* until the initialization code is executed

### Scope

|Declaration|Code Block       |                 |Function           |                 |                 |
|-----------|-----------------|-----------------|-------------------|-----------------|-----------------|
|           |**Module Scope** |**Global Scope** |**Module Scope**   |**Global Scope** |                 |
|           |                 |                 |                   |**Declaration**  |**Expression**   |
|`function` |Not Scoped       |Not Scoped       |Scoped             |Scoped           |Scoped           |
|           |-                |Added to `global`|-                  |-                |-                |
|`var`      |Not Scoped       |Not Scoped       |Scoped             |Scoped           |Scoped           |
|           |-                |Added to `global`|-                  |-                |-                |
|No keyword |                 |                 |***After `()`***   |***After `()`*** |***After `()`*** |
|           |Not Scoped       |Not Scoped       |Not Scoped         |Not Scoped       |Not Scoped       |
|           |Added to `global`|Added to `global`|Added to `global`  |Added to `global`|Added to `global`|
|           |                 |                 |***Before `()`***  |***Before `()`***|***Before `()`***|
|           |                 |                 |Scoped             |Scoped           |Scoped           |
|           |                 |                 |-                  |-                |-                |

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
