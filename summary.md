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

A `var` declaration (without the assignment) is hoisted to the top of its scope and given an initial value of `undefined`

No-keyword declaration (an assignment without a previous declaration) is not hoisted

A `let`/`const` declaration is hoisted but not initialized, so that the variable remains in a *temporal dead zone* until the initialization code is executed

### Scope

...

### Lexical Environment

...

### Closure

...
