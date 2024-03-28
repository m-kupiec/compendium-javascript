# JavaScript Reference

## TOC

- [Data](#data)
- [Basic Operators](#basic-operators)
- [Control Flow](#control-flow)
- [Functions](#functions)
- [Classes](#classes)
- [Scope](#scope)
- [Built-In Objects](#built-in-objects)
- [Internal Mechanics](#internal-mechanics)
- [Programming Techniques](#programming-techniques)

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

`var` declarations (but not assignments without declaration) are hoisted (without the assignment) to the top of the function or global script:

```js
// console.log(a); // ReferenceError: a is not defined
a = 1;
console.log(a); // 1

console.log(b); // undefined (declared but not yet assigned)
var b = 2;
console.log(b); // 2

// console.log(c); // ReferenceError: Cannot access 'c' before initialization
let c = 3;
console.log(c); // 3
```

#### 💠 Naming

> 📖 [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Lexical_grammar#keywords)

Variable name may contain:
- letters (non-Latin are not recommended)
- digits (except in the first position)
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

Is stored in a binary form, rounding the given number to the nearest possible value, resulting in a loss of precision:

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

Three types of quotes:
- Single
- Double
- Backticks
  - Used for template literals `${…}` and tagged templates (a string and embedded expressions being processed by a function)
  - Allow multiline strings

Special characters:
- `\n`: new line
- `\t`: new line
- `\`: special character escaping

Accessing char at a non-found index results in an `undefined` value

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

Represents an empty or unknown value

##### 💠 undefined

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/types)

Represent not assigned value

It's recommended to assign `null` instead of `undefined` to a variable

#### Object

##### 💠 Creation Syntax

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/object)

```js
let a = {}; // Object literal

let b = new Object(); // Object constructor
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

Accessing non-existing properties will result in getting `undefined` values

`in` operator checks if a property with the given name exists in the object (even if its value is `undefined`)

`delete` operator is used to remove a property

###### Access Notations

The dot notation may be used when the property name follows the rules for naming variables (no spaces, no digits on the first position, letters and `$`/`_` allowed) with the exception that the accessed property name may be a keyword

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

is almost equivalent (with some differences related to inheritance) to the following:

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

`this` inside an arrow function is referring to the outer context

When a function is called without an object, the value of `this` is:
- `undefined` when in strict mode
- global object when not in strict mode

##### 💠 Property Value Shorthand

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/object#property-value-shorthand)

Used when the property name is the same as the property value

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

Variable assigned to an object stores its reference, not the object itself

Copying a variable assigned to an object copies the reference

Objects declared with `const` can be modified since `const` applies to the reference

```js
let sourceObj = { a: 1 };

let arr = [sourceObj];
let obj = sourceObj;
console.log(sourceObj === arr[0]); // true
console.log(sourceObj === obj); // true

sourceObj = null;
console.log(sourceObj === arr[0]); // false
console.log(sourceObj === obj); // false
console.log(arr[0]); // [object Object] { a: 1 }
console.log(obj); // [object Object] { a: 1 }
```

##### 💠 Copying

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/rest-parameters-spread#copy-an-array-object)

An object may be copied (in a non-nested way) using spread syntax:

```js
console.log({...{ a: 1, b: 2, c: 3 }}); // [object Object] { a: 1, b: 2, c: 3 }
```

##### 💠 Optional Chaining

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/optional-chaining)

`?.` is not an operator but a syntax construct

`?.` stops the evaluation if the preceding value is `undefined`/`null` and returns `undefined`

Works only for declared variables

May be used for short-circuit evaluations, e.g. `a?.b(c)`

`?.[]` is used when square bracket notation is needed

`?.()` is used to call a function that may not exist

Can be used for reading and deleting property but not for setting the property value

Overusing `?.` may result in more difficult debugging, so it should be used only when the existence of the preceding property is optional

##### 💠 Property Descriptor

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/property-descriptors)

Each property has three attributes ("flags"), all set to `true` by default:
- `writable` (specifying if the property value can be changed)
- `enumerable` (specifying if the property is to be listed in loops)
- `configurable` (specifying if the property can be deleted or its attributes modified)
  - it does not affect the possibility of changing the property value which is regulated by the `writable` attribute
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

Accessor property has no `value` (and in consequence no `writable`) but does have `get` and `set` (in addition to `enumerable` and `configurable`)

##### 💠 Prototypal Inheritance

> 📖 [The Modern JavaScript Tutorial: Prototypal inheritance](https://javascript.info/prototype-inheritance)
>
> 📖 [The Modern JavaScript Tutorial: Native prototypes](https://javascript.info/native-prototypes)
>
> 📖 [The Modern JavaScript Tutorial: Prototype methods, objects without __proto__](https://javascript.info/prototype-methods#brief-history)

`[[Prototype]]` is a hidden property that either references to another object (the prototype) or is `null`

`__proto__` is an outdated (moved to Annex B - optional for non-browser environments) getter/setter for `[[Prototype]]` (it's preferable to use `Object.getPrototypeOf`/`Object.setPrototypeOf` instead)

Since 2022 is it allowed to used `__proto__` in object literals

Changing `[[Prototype]]` of existing objects is a very slow operation; `[[Prototype]]` usually should be set at the time of object creation

```js
const obj1 = { a: 1 };
const obj2 = { b: 2 };

obj2.__proto__ = obj1;
console.log(obj2); // [object Object] { a: 1, b: 2 }
```

Assigning `__proto__` in a circle will result in an error

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

Between the prototype and the inheriting object, methods are shared but the state is not:

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

When `typeof` is not sufficient, `Object.prototype.toString` can display the type of primitives, objects with `Symbol.toStringTag`, and built-in objects

#### 💠 Type Conversion

> 📖 [The Modern JavaScript Tutorial: Type Conversions](https://javascript.info/type-conversions)
> 
> 📖 [The Modern JavaScript Tutorial: Basic operators, maths](https://javascript.info/operators)
>
> 📖 [The Modern JavaScript Tutorial: Object to primitive conversion](https://javascript.info/object-toprimitive)
>
> 📖 [The Modern JavaScript Tutorial: Arrays](https://javascript.info/array)

##### String

Value is converted to string automatically when the string form is needed in a function

If one of the operands of the `+` operator is a string, the second one is also converted to a string
- `1 + 1 + '1'` is converted to `'21'`
- `'1' + 1 + 1` is converted to `'111'`

`String(value)`: converts a value to a string explicitly

Rules:
- `false` is converted to `"false"`
- `null` is converted to `"null"`
- etc.

`[1, 2, 3]` is converted to `"1,2,3"`

##### Numeric

Value is converted to a number automatically in mathematical functions and expressions

Unary `+` operator converts the operand to a number

`Number(value)`: converts a value to number explicitly

Rules:
- Strings
  - Whitespace (spaces, `\t`, `\n`, etc.) from the beginning and the end of the string are removed
  - `"10"` is converted to `10`
  - An empty string is converted to `0`
  - String that doesn't represent a valid number is converted to `NaN`
- `true`/`false` is converted to `1`/`0`
- `null` is converted to `0`
- `undefined` is converted to `NaN`

##### Boolean

Value is converted to a boolean automatically in logical operations

`!!` operator converts the operand to a boolean

`Boolean(value)`: converts a value to a boolean explicitly

Rules:
- Numbers
  - `1`/`0` is converted to `true`/`false`
  - `NaN` is converted to `false`
- Strings
  - An empty string is converted to `false`
  - Non-empty string (e.g. `"0"`) is coverted to `true`
- `null` is converted to `false`
- `undefined` is converted to `false`
- Objects are not converted to boolean but are always `true`

##### Object-to-Primitive Conversion

There are three hints (variants of type conversion):
- `"string"` when doing operations that expect string (e.g. alert, obj[indexingObj])
- `"number"` when using arithmetic operators (except binary plus) or greater/less comparison
- `"default"` when using the binary plus or loose comparison (with a string/number/symbol); implemented for all built-in objects except `Date` in the same way as `"number"`

Firstly, `[Symbol.toPrimitive](hint)` is called (if exists; must return a primitive value or will result in error); otherwise, for `"string"` hint, `toString`/`valueOf` (depending on which is found and returns a primitive; `valueOf` returns the calling object itself by default, so then it's ignored; these functions may return a non-primitive value without causing an error but simply the result being ignored) is called; or, for `"number"`/`"default"` hint, `valueOf`/`toString` is called

Using `[Symbol.toPrimitive](hint)`:

```js
const obj = {
  a: 'Aaa',
  b: 100,
  Aaa: "!",
  
  [Symbol.toPrimitive](hint) {
    console.log(hint);
    return hint == "string" ? this.a : this.b;
  }
};

console.log(obj[obj]);
/*
"string"
"!"
*/

console.log(obj - 1);
/*
"number"
99
*/

console.log(obj + " USD");
/*
"default"
"100 USD"
*/
```

Using `toString`/`valueOf`:

```js
const obj = {
  a: 'Aaa',
  b: 100,
  Aaa: "!",
  
  toString() {
    return this.a;
  },
  
  valueOf() {
    return this.b;
  }
};

console.log(obj[obj]); // "!"
console.log(obj - 1); // 99
console.log(obj + " USD"); // "100 USD"
```

Using `toString` only (to handle all object-to-primitive conversions at once):

```js
const obj = {
  a: 'Aaa',
  b: 100,
  Aaa: "!",
  
  toString() {
    return this.a;
  }
};

console.log(obj[obj]); // "!"
console.log(obj - 1); // NaN
console.log(obj + " USD"); // "Aaa USD"
```

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

Accessing an array element at a non-found index results in getting an `undefined` value

```js
for (el of [1, 2, 3]) {
  console.log(el); // 1 2 3
}
```

An array may be truncated by decreasing `length` property (or cleared by assigning `0` to it)

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

#### Array-Like Object

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/iterable#array-like)

An array-like object has numeric indices and `length` property

```js
const arrayLike = {
  0: 'a',
  1: 'b',
  2: 'c',
  length: 3
};
```

#### Iterable Object

> 📖 [The Modern JavaScript Tutorial: Iterables](https://javascript.info/iterable)
>
> 📖 [The Modern JavaScript Tutorial: Generators](https://javascript.info/generators#using-generators-for-iterables)

Iterables can be looped over using `for...of` and work with spread `...` syntax (while array-likes cannot)

Arrays and strings are iterable

To make an object iterable:
- Add `Symbol.iterator` method
- `Symbol.iterator` method must return an iterator object with the `next` method
- `next` method must return an object in the following form: `{done: Boolean, value: nextValue}`

```js
const iterable = {
  start: 100,
  finish: 110,
  
  [Symbol.iterator]() {
    return {
      nextValue: this.start,
      endValue: this.finish,
      
      next() {
        if (this.nextValue > this.endValue) {
          return {
            done: true
          }
        } else {
          return {
            done: false,
            value: this.nextValue++
          }
        }
      }
    }
  }
};

for (let el of iterable) {
  console.log(el)
}

// 100 101 102 103 104 105 106 107 108 109 110
```

To make the same iterable object as above, but using a generator:

```js
const iterable = {
  start: 100,
  finish: 110,

  *[Symbol.iterator]() {
    for (let value = this.start; value <= this.finish; value++) {
      yield value;
    }
  }
};

for (let el of iterable) {
  console.log(el)
}

// 100 101 102 103 104 105 106 107 108 109 110
```

Iterator can be used explicitly:

```js
const string = "abc";

const iterator = string[Symbol.iterator]();

while (true) {
  let result = iterator.next();
  
  if (result.done) break;
  console.log(result.value);
}

// "a" "b" "c"
```

#### Map

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/map-set)

Is a keyed collection that allows keys of any type

Preserves entry insertion order

Creation syntax and iteration using `for...of`:

```js
const map1 = new Map()
  .set(1, 'a')
  .set(2, 'b');
const map2 = new Map([
  [1, 'a'],
  [2, 'b']
]);
const map3 = new Map(Object.entries({
  '1': 'a',
  '2': 'b'
}));

for (let entry of map1) console.log(`map1: ${entry}`);
/*
"map1: 1,a"
"map1: 2,b"
*/
for (let entry of map2) console.log(`map2: ${entry}`);
/*
"map2: 1,a"
"map2: 2,b"
*/
for (let entry of map3) console.log(`map3: ${entry}`);
/*
"map2: 1,a"
"map2: 2,b"
*/
```

Available methods and properties:

```js
const obj = {
  a: 1,
  b: 2
};

const map = new Map();

map.set(obj, 3)
  .set(NaN, 4)
  .set(obj, 5);
console.log(map.size); // 2
console.log(map.has(obj)); // true
console.log(map.get(obj)); // 5
console.log(map[obj]); // undefined

map.delete(obj);
console.log(map.has(obj)); // false

map.clear();
console.log(map.size); // 0
```

Destructuring a map:

```js
const map = new Map()
  .set(3, "Three")
  .set(1, "One")
  .set(2, "Two");

const [d, e, f] = map;

console.log(d, e, f); // [3, "Three"] [1, "One"] [2, "Two"]
```

#### WeakMap

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/weakmap-weakset)

Requires an object for a property:

```js
const weakMap = new WeakMap()
  .set({}, 1);
console.log(weakMap); // [object WeakMap] { ... }

// weakMap.set("b", 2); // TypeError: Invalid value used as weak map key
```

A key is removed from the WeakMap and memory when there's no reference to it

Doesn't support `clear`/`size` nor iteration nor `keys`/`values`/`entries` methods - it's not possible to list all its keys/values

Supports only `set`/`get`/`delete`/`has` methods

#### Set

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/map-set)

Is a collection of unique values

Preserves value insertion order

Creation syntax and iteration using `for...of`:

```js
const set1 = new Set()
  .add(1)
  .add(2)
  .add(2);
const set2 = new Set([1, 2, 2]);

console.log(...set1); // 1 2
console.log(...set2); // 1 2

for (let value of set1) console.log(value); // 1 2
```

Some methods and properties:

```js
const set = new Set([1, 2, 3]);

console.log(set.size); // 3
console.log(set.has(1)); // true

set.delete(1);
console.log(set.has(1)); // false
console.log(set.size); // 2

set.clear();
console.log(set.size); // 0
```

Working with objects:

```js
const obj = {b: 2};
const set = new Set()
  .add({a: 1})
  .add({a: 1})
  .add(obj)
  .add(obj);

console.log(...set);
/*
[object Object] {
  a: 1
}
[object Object] {
  a: 1
}
[object Object] {
  b: 2
}
*/
```

Destructuring a set:

```js
const set = new Set()
  .add(2)
  .add(3)
  .add(1);

const [a, b, c] = set;

console.log(a, b, c); // 2 3 1
```

#### WeakSet

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/weakmap-weakset#weakset)

Requires an object for a value:

```js
const weakSet = new WeakSet()
  .add({a: 1});
console.log(weakSet); // [object WeakSet] { ... }

// weakSet.add("b"); // TypeError: Invalid value used in weak set
```

A value is removed from the WeakMap and memory when there's no reference to it

Doesn't support `size` nor iteration or `keys`/`values`/`entries` methods - it's not possible to list all its values

Supports only `add`/`delete`/`has` methods

## Basic Operators

> 📖 [The Modern JavaScript Tutorial: Basic operators, maths](https://javascript.info/operators)
> 
> 📖 [The Modern JavaScript Tutorial: Comparisons](https://javascript.info/comparison)
> 
> 📖 [The Modern JavaScript Tutorial: Object references and copying](https://javascript.info/object-copy)
>
> 📖 [The Modern JavaScript Tutorial: Object to primitive conversion](https://javascript.info/object-toprimitive)
>
> 📖 [The Modern JavaScript Tutorial: Strings](https://javascript.info/string#comparing-strings)
>
> 📖 [The Modern JavaScript Tutorial: Arrays](https://javascript.info/array)

### 💠 Arithmetic Operators

When used with objects, these objects are converted to primitive values:

```js
const obj1 = {
  a: 1,
  b: 2
};
const obj2 = {
  c: 3,
  d: 4
};

console.log(obj1 + obj2); // "[object Object][object Object]"
console.log(+obj1 + +obj2); // NaN
```

### 💠 Comma

Each of the expressions separated with a comma is evaluated and the result of the last one is returned, e.g. `(1 + 2, 3 + 4)` returns `7`

`,` has lower precedence than `=` operator

### 💠 Assignment Operator

`=` operator returns the assigned value

Chained assignments are evaluated from right to left.

For each arithmetical and bitwise operator, there is a corresponding modify-and-assign operator, e.g. `*=`

### 💠 Increment/Decrement Operator

`++a` returns the new value, while `a++` returns the old value

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
- `NaN` does not equal `NaN` or any other value

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

`||` evaluates operands from left to right, converts each to a boolean, and returns the original value of the first truthy operand (returns the last one if all are false); used for:
- getting the first truthy value from a given list
- short-circuit evaluation, e.g. `false || console.log('Ok!')`

`&&` evaluates operands from left to right, converts each to a boolean, and returns the original value of the first falsy operand (returns the last one of all are true)

The precedence of `&&` is higher than `||`

It's not recommended to replace `if` statements with `||`/`&&`

#### NOT Operator

`!` converts its operand to a boolean and inverts the value

`!!` is used to convert a value to a boolean

#### Nullish Coalescing Operator

`??` is used to return the first value that isn't `null`/`undefined` (while in contrast to `||` operator, the value may be `0`, `NaN`, `''`, `false`)

`??` has the same precedence as `||`

It's forbidden to use `??` together with `&&`/`||` without parentheses

## Control Flow

### 💠 Conditionals

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/ifelse)

`if` statement: used when executing different branches of code

Conditional `?` operator (ternary operator): used when returning one of the two values

`switch` statement: used when comparing different value variants

The equality check in `switch` statement is strict

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

`break`/`continue` is not allowed to be used with the ternary operator (`?`)

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

### 💠 Handling Errors

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/try-catch)

#### Syntax

```js
try {
  console.log(1);
  error;
  console.log(2);
} catch (err) {
  console.log(err);
}
/*
1
[object Error] { ... }
*/
```

`try...catch` works for runtime errors (exceptions) but not for parse-time ones (wrong syntax)

The following syntax (optional `catch` binding) is a relatively recent addition:

```js
try {
  console.log(1);
  error;
  console.log(2);
} catch {
  console.log(3);
}
/*
1
3
*/
```

#### Handling Scheduled Functions

A scheduled function is executed after the engine has already left `try...catch` construct

```js
try {
  console.log(1);
  setTimeout(() => error);
  console.log(2);
} catch (err) {
  console.log(err);
}
/*
1
2
ReferenceError: error is not defined
*/
```

The above code should be fixed as follows:

```js
console.log(1);
setTimeout(() => {
  try {
    error;
  } catch (err) {
    console.log(err);
  }
});
console.log(2);
/*
1
2
[object Error] { ... }
*/
```

#### Throwing an Error

Although even a primitive value can be thrown as an error...

```js
try {
  throw 1;
} catch (err) {
  console.log(err); // 1
}

try {
  throw 1n;
} catch (err) {
  console.log(err); // [object BigInt] { ... }
}

try {
  throw "1";
} catch (err) {
  console.log(err); // "1"
}

try {
  throw true;
} catch (err) {
  console.log(err); // true
}

try {
  throw null;
} catch (err) {
  console.log(err); // null
}

try {
  throw undefined;
} catch (err) {
  console.log(err); // undefined
}

try {
  throw new Symbol();
} catch (err) {
  console.log(err); // [object Error] { ... }
}

try {
  throw {};
} catch (err) {
  console.log(err); // [object Object] { ... }
}

try {
  throw function(a) { alert(a); };
} catch (err) {
  console.log(err); // function(a) { alert(a); }
}
```

... it's recommended to be compatible with the built-in Error object (having `name` and `message` properties); built-in error constructors (Error, SyntaxError, ReferenceError, TypeError, etc.) may be used (error `name` is then derived from the constructor name while the error `message` is passed as an argument to the constructor):

```js
try {
  throw SyntaxError("Invalid data provided");
} catch (err) {
  console.log(err.name, err.message, err.stack);
}

/*
"SyntaxError"
"Invalid data provided"
"SyntaxError: Invalid data provided
    at bayorocida.js:2:9
    at https://static.jsbin.com/js/prod/runner-4.1.8.min.js:1:13924
    at https://static.jsbin.com/js/prod/runner-4.1.8.min.js:1:10866"
*/
```

#### Rethrowing an Error

Unexpected errors may be rethrown:

```js
try {
  try {
    if(error) {
      throw SyntaxError("Invalid data provided");
    }
  } catch (err) {
    if (err instanceof SyntaxError) {
      console.log("SyntaxError", err.message);
    } else {
      throw err;
    }
  }
} catch (err) {
  console.log(err.name);
}
/*
"ReferenceError"
*/
```

#### `finally` Clause

```js
try {
  console.log(1);
  error;
  console.log(2);
} catch (err) {
  console.log(err.name);
} finally {
  console.log(3);
}

/*
1
"ReferenceError"
3
*/
```

The clause works for any exit from `try...catch`:

```js
(function f() {
  try {
    console.log(1);
    return;
    console.log(2);
  } catch (err) {
    console.log(err.name);
  } finally {
    console.log(3);
  }
}())

/*
1
3
*/
```

```js
(function f() {
  try {
    console.log(1);
    error;
    console.log(2);
  } catch (err) {
    return;
    console.log(err.name);
  } finally {
    console.log(3);
  }
}())

/*
1
3
*/
```

Can be used even without `catch` to ensure execution of the code inside `finally`:

```js
try {
  console.log(1);
  error;
  console.log(2);
} finally {
  console.log(3);
}

/*
1
3
ReferenceError: error is not defined
*/
```

### 💠 Asynchronous Flow

#### Callback-Based Style

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/callbacks)

##### Basic Usage

A callback function is passed as an argument to the function that has asynchronous code:

```js
function asyncF(string, callback) {
  setTimeout(callback, 0, string);
}

function callbackF(val) {
  console.log(val);
}

asyncF("Test", callbackF); // "Test"
```

##### Handling Errors

The first argument of the callback functions is reserved for an error:

```js
function asyncF(string, callback) {
  const error = Math.random() > 0.5 ? new Error("Error message") : null;
  
  setTimeout(() => {
    if(error) {
      callback(error);
    } else {
      callback(null, string);
    }
  });
}

function callbackF(error, val) {
  if(error) {
    console.log(error.message);
  } else {
    console.log(val);
  }
}

asyncF("Test", callbackF); // "Test"
asyncF("Test", callbackF); // "Error message"
asyncF("Test", callbackF); // "Test"
```

##### Nested Callbacks

```js
function asyncF(string, callback) {
  const error = Math.random() > 0.85 ? new Error("Error message") : null;
  
  setTimeout(() => {
    if(error) {
      callback(error);
    } else {
      console.log(string);
      nextAsyncF("Step 2", callbackF);
    }
  });
}

function nextAsyncF(string, callback) {
  const error = Math.random() > 0.85 ? new Error("Error message") : null;
  
  setTimeout(() => {
    if(error) {
      callback(error);
    } else {
      callback(null, string);
    }
  });
}

function callbackF(error, val) {
  if(error) {
    console.log(error.message);
  } else {
    console.log(val);
  }
}

asyncF("Step 1", callbackF); // "Step 1" "Step 2" OR "Step 1" "Error message" OR "Error message"
```

#### Promises

##### Basic Usage

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/promise-basics)

The executor function is passed as an argument to the promise constructor and is executed automatically; two callbacks passed as the executor function arguments (`resolve` and `reject`) are provided by the language; the executor function calls one of the two callback functions (`resolve(value)` or `reject(error)`) after obtaining the result of its operation

The promise is either pending or settled; The object returned by the promise constructor has `state` (which value is `pending`/`fulfilled`/`rejected`) and `result` (which value is `undefined`/`value`/`error`) internal properties (cannot be accessed)

Consuming functions can be registered using `then` and `catch` methods

`then` receives two callbacks as its arguments - the first callback (success handler, `onFulfilled`) receives the result if the promise was resolved while the second callback (failure handler, `onRejected`) receives the error if the promise was rejected

```js
const promise = new Promise(function(resolve, reject) {
  setTimeout(() => {
    if (Math.random() > 0.5) {
      reject(new Error("Error happened..."));
    } else {
      resolve("Fulfilled value");
    }
  }, 1000);
});

promise.then(
  result => console.log(result), // "Fulfilled value"
  error => console.log(error.message) // "Error happened..."
);
```

It's possible to handle only resolved promises...

```js
const promise = new Promise(function(resolve, reject) {
  setTimeout(() => {
    if (Math.random() > 0.95) {
      reject(new Error("Error happened..."));
    } else {
      resolve("Fulfilled value");
    }
  }, 1000);
});

function logResult(result) {
  console.log(result);
}

promise.then(logResult); // "Fulfilled value"
```

... or to handle only rejected promises passing `null` as the first argument...

```js
const promise = new Promise(function(resolve, reject) {
  setTimeout(() => {
    if (Math.random() > 0.05) {
      reject(new Error("Error happened..."));
    } else {
      resolve("Fulfilled value");
    }
  }, 1000);
});

function logError(err) {
  console.log(err.message);
}

promise.then(null, logError); // "Error happened..."
```

... or to handle only rejected promises using `catch`:

```js
const promise = new Promise(function(resolve, reject) {
  setTimeout(() => {
    if (Math.random() > 0.05) {
      reject(new Error("Error happened..."));
    } else {
      resolve("Fulfilled value");
    }
  }, 1000);
});

function logError(err) {
  console.log(err.message);
}

promise.catch(logError); // "Error happened..."
```

`finally` handler (designed for executing finalizing procedures, e.g. turning the loading indicator off) is executed whether the promise was resolved or rejected; it doesn't return anything (any returns are ignored) except a possible thrown error (that's passed to the next handler instead of any previous result/error):

```js
function logResult(result) { console.log(result); }
function logError(err) { console.log(err.message); }

new Promise(function(resolve, reject) {
  setTimeout(() => {
    if (Math.random() > 0.5) {
      reject(new Error("Error happened..."));
    } else {
      resolve("Fulfilled value");
    }
  }, 1000);
})
  .finally(() => console.log("Finished"))
  .then(logResult, logError);
// "Finished" "Error happened..." OR "Finished" "Fulfilled value"

new Promise(function(resolve, reject) {
  resolve("Ok");
})
  .finally(() => console.log("Finally..."))
  .then(logResult, logError);
// "Finally..." "Ok"

new Promise(function(resolve, reject) {
  resolve("Ok");
})
  .finally(() => { throw new Error("Error message") })
  .then(logResult, logError);
// "Error message"

/*
ACTUAL LOG SEQUENCE:

"Finally..."
"Error message"
"Ok"
"Finished"
"Fulfilled value"
*/
```

If a handler (`then`/`catch`/`finally`) is added to an already settled promise, it will run immediately:

```js
const promise = new Promise(resolve => resolve("Resolved value"));

promise.finally(() => console.log("Finilizing..."));
promise.then(result => console.log(result));
/*
"Finilizing..."
"Resolved value"
*/
```

##### Promise Chaining

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/promise-chaining)

AKA promise composition

Handler used in `then` may create and return a promise:

```js
new Promise(function(resolve, reject) {
  reject(new Error("Error happened..."));
})
  .then(
    result => { return new Promise(resolve => resolve(result)) },
    error => { return new Promise(resolve => resolve("Error fixed")) }
  )
  .then(
    result => console.log(result),
    error => console.log(error.message)
  );

// "Error fixed"
```

Other scenarios:

```js
new Promise(resolve => resolve("Ok"))
  .then(result => { })
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

A "thenable" object (an object containing `then` method; doesn't need to inherit from Promise) may also be created and returned (which will be treated as a promise):

```js
class Thenable {
  constructor(val) {
    this.val = val;
  }
  
  then(resolve, reject) {
    console.log(typeof resolve); // "function"
    
    setTimeout(() => {
      if (Math.random() > 0.5) {
        reject(new Error("Error happened..."));
      } else {
        resolve("Fulfilled value");
      }
    });
  }
}

new Promise(function(resolve, reject) {
  resolve("Ok");
})
  .then(
    result => { return new Thenable(resolve => resolve(result)) }
  )
  .then(
    result => console.log(result),
    error => console.log(error.message)
  );

// "Error happened..." OR "Fulfilled value"
// OBSERVATION: Resolved promise result ("OK") does not make it to the second 'then' method

new Promise(function(resolve, reject) {
  reject(new Error("Error happened again..."));
})
  .then(
    result => console.log(1)
  )
  .then(
    result => console.log(result),
    error => console.log(error.message)
  );

// "Error happened again..."
// OBSERVATION: Rejected promise error passed through the first 'then' (which doesn't have an error handler)
```

##### Handling Errors

> 📖 [The Modern JavaScript Tutorial: Error handling with promises](https://javascript.info/promise-error-handling)
>
> 📖 [The Modern JavaScript Tutorial: Microtasks](https://javascript.info/microtask-queue#unhandled-rejection)

Errors coming from the code of the executor function or the promise handlers are automatically treated as a promise rejection:

```js
new Promise(resolve => error1)
  .then(
    null,
    (err) => console.log(err.message)
  );

// "error1 is not defined"

new Promise(resolve => resolve("Ok"))
  .then(
    result => { throw new Error("Another error happened...") }
  )
  .catch((err) => console.log(err.message));

// "Another error happened..."
```

If an error is successfully handled by a handler, the next success handler runs; if an error is not handled, the next failure handler runs:

```js
new Promise((resolve, reject) => reject(new Error()))
  .catch(err => { if (err instanceof Error) console.log("Error successfully handled...") })
  .then(() => console.log("Success!"));
/*
"Error successfully handled..."
"Success!"
*/

new Promise((resolve, reject) => reject(new Error()))
  .catch(err => {
    if (err instanceof TypeError)
      console.log("Error successfully handled...");
    else
      throw err;
  })
  .then(
    () => console.log("Success!"),
    (err) => console.log("Failure!", err.name)
  );
// "Failure!" "Error"
```

If a promise rejection is not handled, a global error occurs, which can be caught in the browser using the `unhandledrejection` event (which would fire when the microtask queue is empty):

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

Rules for handling errors:
- `catch` should be used where/when handling expected errors is possible; unknown errors should be rethrown
- `catch` may be omitted if errors cannot be handled
- `unhandledrejection` (in the browser runtime environment) event handler should be used to inform (users, server) about unhandled errors

##### Microtask Queue

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/microtask-queue)

Asynchronous tasks are placed in the internal `PromiseJobs' queue ("microtask queue" as called in V8) and are executed (in FIFO order) after the engine has already executed the current synchronous code

```js
Promise.resolve().then(() => console.log(1));
Promise.resolve().then(() => console.log(2));
Promise.resolve().then(() => console.log(3));
console.log(4);
console.log(5);
// 4 5 1 2 3

// FIXED ORDER:

Promise.resolve().then(() => console.log(1));
Promise.resolve().then(() => console.log(2));
Promise.resolve().then(() => console.log(3))
  .then(() => console.log(4))
  .then(() => console.log(5));
// 1 2 3 4 5
```

##### `async`/`await` Syntax

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/async-await)
>
> 📖 [Codecademy | Learn Intermediate JavaScript](https://www.codecademy.com/courses/learn-intermediate-javascript/lessons/async-await/exercises/multiple-awaits)

`async` function always returns a promise - values other than a promise are wrapped in a resolved promise:

```js
async function asyncF() {
  return "Ok";
}

asyncF().then(console.log); // "Ok"
```

`await` pauses the function execution until the promise is settled (whether resolved or rejected) and returns the result/error:

```js
async function asyncF() {
  let val = await new Promise((resolve, reject) => setTimeout(() => Math.random() > 0.5 ? reject(new Error()) : resolve("Ok!"), 1000));
  
  return val;
}

asyncF().then(console.log, console.log); // "Ok" OR [object Error] { ... }
```

To avoid `SyntaxError`, `await` must be either:
- placed in an `async` function
- used at a module top-level
- wrapped into an anonymous `async` function

```js
// let val = await new Promise(resolve => setTimeout(() => resolve("Ok!"), 1000));
// console.log(val);

// SyntaxError: await is only valid in async functions and the top level bodies of modules

(async () => {
  let val = await new Promise(resolve => setTimeout(() => resolve("Ok!"), 1000));
  console.log(val);
})();

// "Ok!"
```

The syntax also works with classes:

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

`await` can be also used with "thenables"

Errors need to be caught (either by `try...catch` or `catch` method)

```js
class Thenable {
  then(resolve, reject) {
    setTimeout(() => {
      if (Math.random() > 0.5) {
        reject(new Error("Thenable error"));
      } else {
        resolve("Ok!");
      }
    }, 100);
  }
}

(async () => {
  try {
    let val = await new Thenable();

    console.log(val);
  } catch (err) {
    console.log(err.message);
  }
})();

// "Ok!" OR "Thenable error"

async function f() {
  return await Promise.reject(new Error("Error happened..."));
}

f().catch(err => console.log(err.message));

// "Error happened..."
```

Chained promises look like this:

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

#### Asynchronous Iteration

##### Async Iterable Object

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/async-iterators-generators)

Async iterables can be looped over using `for await...of`, although don't work with spread `...` syntax (which requires `Symbol.iterator` method)

To make an object iterable:
- Add `Symbol.asyncIterator` method
- `Symbol.asyncIterator` method must return an iterator object with the `next` method
- `next` method (may be declared as `async` to be able to use `await` and wrap values other than a promise in a resolved promise) must return a promise to be fulfilled with the next value

```js
const iterable = {
  start: 100,
  finish: 110,

  [Symbol.asyncIterator]() {
    return {
      nextValue: this.start,
      endValue: this.finish,

      async next() {
        await new Promise(resolve => setTimeout(resolve, 200));

        if (this.nextValue > this.endValue) {
          return {
            done: true
          }
        } else {
          return {
            done: false,
            value: this.nextValue++
          }
        }
      }
    }
  }
};

(async () => {
  for await (let el of iterable) {
    console.log(el)
  }
})();

// 100 101 102 103 104 105 106 107 108 109 110
```

To make the same async iterable object as above, but using a generator:

```js
const iterable = {
  start: 100,
  finish: 110,

  async *[Symbol.asyncIterator]() {
    for (let value = this.start; value <= this.finish; value++) {
      await new Promise(resolve => setTimeout(resolve, 200));

      yield value;
    }
  }
};

(async () => {
  for await (let el of iterable) {
    console.log(el)
  }
})();

// 100 101 102 103 104 105 106 107 108 109 110
```

##### Async Generator

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/async-iterators-generators#async-generators-finally)

```js
async function* generateNumbers() {
  yield 1;
  yield 2;
  yield 3;
}

let generator = generateNumbers();

(async () => {
  console.log(await generator.next());
  console.log(await generator.next());
  console.log(await generator.next());
})();
/*
{ value: 1, done: false }
{ value: 2, done: false }
{ value: 3, done: false }
*/
```

```js
async function* generateNumbers() {
  for (let i = 0; i < 5; i++) {
    await new Promise(resolve => setTimeout(resolve, 200));
    yield i;
  }
}

let generator = generateNumbers();

(async () => {
  for await (let value of generator) console.log(value); // 0 1 2 3 4
})();
```

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

The first letter of the function name must be capital

Should be executed with the `new` operator

When executing with the `new` operator, parentheses may be omitted, but it's not a good practice

Does not have the `return` statement as it returns `this`

If there is a `return` statement then it returns:
- an object passed with the `return`
- `this`, if the `return` is not passing an object

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

If a constructor function has a `prototype` property which value is an object, then this object will be used as the prototype for the object created with the constructor function:

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
>
> 📖 [The Modern JavaScript Tutorial: Class inheritance](https://javascript.info/class-inheritance#homeobject)

A function is a value that can be printed:

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

For a function that is an object/class method, `[[HomeObject]]` internal property refers to that object; `[[HomeObject]]` is used only when using `super`; a copied method that uses `super`, will use `super` in reference to its original parent object/class:

```js
const parent1 = {
  f() {
    console.log('Parent 1 line');
  }
};

const child1 = {
  __proto__: parent1,

  f() {
    super.f();
  }
};

child1.f(); // "Parent 1 line"

const parent2 = {
  f() {
    console.log('Parent 2 line');
  }
}

const child2 = {
  __proto__: parent2,
  
  f: child1.f
};

child2.f(); // "Parent 1 line"
```

For object methods (but not for class methods), `[[HomeObject]]` internal property is set only when using `f()` (not `f: function()`) syntax for defining the method:

```js
const parent = {
  f: function() {
    console.log('Parent method');
  }
};

const child1 = {
  __proto__: parent,

  f() {
    super.f();
  }
};

child1.f();  // "Parent method"

const child2 = {
  __proto__: parent,

  f: function() {
    super.f();
  }
};

child2.f(); // SyntaxError: 'super' keyword unexpected here
```

### 💠 Generator

#### Basic Syntax

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/generators)

Generator function returns an iterable object (generator object) which `next` method returns an object in the format `{value: <the next yielded value>, done: <true/false>}`; both `function* f()` and `function *f()` syntaxes are correct but the first one is usually preferred:

```js
function* generateNumbers() {
  yield 1;
  yield 2;
  return 3;
}

const generator = generateNumbers();

console.log(generator); // Object [Generator] {}
console.log(generator.next()); // { value: 1, done: false }
console.log(generator.next()); // { value: 2, done: false }
console.log(generator.next()); // { value: 3, done: true }
console.log(generator.next()); // { value: undefined, done: true }
```

#### Using As an Iterable

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/generators#generators-are-iterable)

Iterations ignore the returned value when `done: true`:

```js
function* generateNumbers1() {
  yield 1;
  yield 2;
  return 3;
}

function* generateNumbers2() {
  yield 1;
  yield 2;
  yield 3;
}

let generator = generateNumbers1();
for (let value of generator) console.log(value); // 1 2

generator = generateNumbers2();
for (let value of generator) console.log(value); // 1 2 3
```

Using the spread syntax:

```js
function* generateNumbers1() {
  yield 1;
  yield 2;
  return 3;
}

function* generateNumbers2() {
  yield 1;
  yield 2;
  yield 3;
}

let generator = generateNumbers1();
console.log(...generator); // 1 2

generator = generateNumbers2();
console.log(...generator); // 1 2 3
```

#### Generator Composition

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/generators#generator-composition)

```js
function* generatePartialSequence(start, end) {
  for (let i = start; i <= end; i++) yield i;
}

console.log(...generatePartialSequence(0, 5)); // 0 1 2 3 4 5

function* generateFullSequence() {
  yield* generatePartialSequence(0, 5);
  yield* generatePartialSequence(100, 105);
  yield* generatePartialSequence(200, 205);
}

console.log(...generateFullSequence(0, 10));
// 0 1 2 3 4 5 100 101 102 103 104 105 200 201 202 203 204 205
```

#### Passing Values Into a Generator

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/generators#yield-is-a-two-way-street)

```js
function* generate() {
  let value1 = yield 1;
  yield 2;
  let value2 = yield 3;

  console.log(`Generate #1: ${value1}`);
  console.log(`Generate #2: ${value2}`);
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
Generate #1: undefined
Generate #2: undefined
{ value: undefined, done: true }
*/

generator = generate();
console.log(generator.next());
console.log(generator.next(4));
console.log(generator.next());
console.log(generator.next(5));
/*
{ value: 1, done: false }
{ value: 2, done: false }
{ value: 3, done: false }
Generate #1: 4
Generate #2: 5
{ value: undefined, done: true }
*/
```

#### Throwing an Error Into a Generator

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/generators#generator-throw)

```js
function* generate() {
  try {
    let value1 = yield 1;
    yield 2;
    let value2 = yield 3;

    console.log(`Generate #1: ${value1}`);
    console.log(`Generate #2: ${value2}`);
  } catch (error) {
    if (error.message === "Wrong!") {
      console.log("Error handled.");
    }
  }
}

let generator = generate();

console.log(generator.next());
console.log(generator.next(4));
console.log("!!!", generator.throw(new Error("Wrong!")));
console.log(generator.next());
console.log(generator.next(5));
/*
{ value: 1, done: false }
{ value: 2, done: false }
Error handled.
!!! { value: undefined, done: true }
{ value: undefined, done: true }
{ value: undefined, done: true }
*/
```

Errors may be also handled outside of the generator function (leading to a slightly different output - `!!!` is not printed to the console):

```js
function* generate() {
  let value1 = yield 1;
  yield 2;
  let value2 = yield 3;

  console.log(`Generate #1: ${value1}`);
  console.log(`Generate #2: ${value2}`);
}

let generator = generate();

console.log(generator.next());
console.log(generator.next(4));
try {
  console.log("!!!", generator.throw(new Error("Wrong!")));
} catch (error) {
  if (error.message === "Wrong!") {
    console.log("Error handled.");
  }
}
console.log(generator.next());
console.log(generator.next(5));
/*
{ value: 1, done: false }
{ value: 2, done: false }
Error handled.
{ value: undefined, done: true }
{ value: undefined, done: true }
*/
```

#### Returning From a Generator

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/generators#generator-return)

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

## Classes

### 💠 Definition

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/class)

There's no comma between class methods

`new` calls `constructor` method

`class` creates a function:
- the function name is taken from the class name
- the function code is taken from the `constructor` method
- the function stores class methods in the `prototype`

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
- a class uses the strict mode
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

This allows to define methods (using `f = () => {...}`) that will not lose `this` when passed as callbacks to another context:

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

When extending built-in classes, their methods (like `filter`, `map`, etc.) use the inherited class object constructor for creating the returned object:

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

#### Overriding/Extending Constructor

A default constructor is created when a class extending another class has none:

```js
constructor(...args) {
  super(...args);
}
```

Inheriting class constructor has an internal `[[ConstructorKind]]` property set to `"derived"`, so when it is executed with `new`, it doesn't assign an empty object to `this` (as is done with regular functions executed with `new`) but leaves this job to the base class constructor; that's why it must call `super` (to create the object for `this`) and do this before using `this`:

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

In the parent class, fields are initialized before the constructor; however, in inheriting classes, fields are initialized immediately after `super()`; that's why the parent class constructor uses its own fields (not the overriding ones) but still uses overriding methods:

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

#### Limitations of `super` and `this`

```js
class A {
  a = 1;

  constructor() {
    this.b = 2;
  }

  f() {
    console.log(this.a, this.b); // 1, 2
  }
};

class B extends A {
  f() {
    console.log(super.a); // undefined (not a [[Prototype]] property)
    console.log(super.b); // undefined (not a [[Prototype]] property)
    console.log(this.a); // 1 (an instance property)
    console.log(this.b); // 2 (an instance property)
  }
  
  static g() {
    console.log(super.a); // undefined (not a [[Prototype]] property)
    console.log(super.b); // undefined (not a [[Prototype]] property)
    console.log(this.a); // undefined (not accessible in a static context)
    console.log(this.b); // undefined (not accessible in a static context)
  }
};

const objA = new A();
const objB = new B();

objA.f(); 
objB.f();
B.g();
```

```js
const objA = {
    val: 'A',

    f() {
        console.log(this.val);
    }
};

const objB = {
    __proto__: objA,
    val: 'B',

    f() {
        this.__proto__.f();
    }
};
objB.f(); // A

const objC = {
    __proto__: objA,
    val: 'C',

    f() {
        this.__proto__.f.call(this); // (**)
    }
};
objC.f(); // C

const objD = {
    __proto__: objC,
    val: 'D',

    f() {
        this.__proto__.f.call(this); // (*)
    }
};
// objD.f(); // RangeError: Maximum call stack size exceeded
// "this" refers to objD both in line (*) and line (**) resulting in an endless reference loop

const objE = {
    __proto__: objC,
    val: 'E',

    f() {
        this.__proto__.__proto__.f.call(this);
    }
};
objE.f(); // E
```

#### Checking Class Instance

`instanceof` operator takes inheritance into account:

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

Checking rules may be modified using the `Symbol.hasInstance` static method:

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

Static methods are such that do not belong to particular class objects but rather to the whole class itself (are not available in particular instances of the class but rather are called from the class itself):

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
>
> 📖 [Felix Gerschau | JavaScript's Memory Management Explained](https://felixgerschau.com/javascript-memory-management/#global-variables)

### 💠 Global/Block/Function Scope

```js
{
  let a = 1;
  console.log(a); // 1
}

// console.log(a); // ReferenceError: a is not defined
```

`var` is not restricted by a code block (conditionals, loops), but is by a function:

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

Function declarations (i.e. using  `function` keyword) and variable declarations using `var` or no keyword will result in adding the function/variable to the global object:

```js
// Browser runtime environment

let a = 1;
console.log(window.a); // undefined

var b = 2;
c = 3;
console.log(window.b); // 2
console.log(window.c); // 3

function fAbc() {}
console.log(window.fAbc === fAbc); // true
```

```js
// Node.js runtime environment

let a = 1;
console.log(global.a); // undefined

var b = 2;
c = 3;
console.log(global.b); // 2
console.log(global.c); // 3

function fAbc() {}
console.log(global.fAbc === fAbc); // true
```

### 💠 Lexical Environment

Every running scope (global, block, function) has its associated Lexical Environment (theoretical object existing in the specification) which consists of:
- `Environment Record` object: stores local variables, `this`, and local function declarations as its properties
- Reference to the outer lexical environment

Lexical Environment is cleaned from memory by the garbage collector when it becomes unreachable

### 💠 Closure

Returned nested functions retain access to their outer variables because in a hidden `[[Environment]]` property they store a reference to the Lexical Environment in which these nested functions were created

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

### Global Scope Objects

#### 💠 Executing Code From a String

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/eval)

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
let a = 1;

{
  let a = 2;

  window.eval(`console.log(a);`); // 1
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

### Global Object

#### 💠 General

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/global-object)

`globalThis` is a standardized name for the global object (`window` in a browser or `global` in Node.js)

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

`isNaN(value)` tests if the value converted to a number is `NaN`:

```js
console.log(isNaN("a")); // true
```

`isFinite(value)` tests if the value converted to a number is not `NaN`/`Infinity`/`-Infinity`:

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

Property descriptor (an object containing the property value and its all flags) can be obtained using `Object.getOwnPropertyDescriptor()` while all descriptors can be obtained using `Object.getOwnPropertyDescriptors`

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

#### 💠 Object/Map Conversion

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/map-set)

`Object.entries` can be used to convert a plain object to a map:

```js
const map = new Map(Object.entries({
  '1': 'a',
  '2': 'b'
}));

for (let entry of map) console.log(`map: ${entry}`);
/*
"map: 1,a"
"map: 2,b"
*/
```

`Object.fromEntries` (with or without `Map.prototype.entries`) can be used to convert a map to a plain object:

```js
const map = new Map()
  .set(1, 'a')
  .set(2, 'b');

const obj1 = Object.fromEntries(map.entries());
const obj2 = Object.fromEntries(map);
      
for (let key in obj1) console.log(`${key}: ${obj1[key]}`);
/*
"1: a"
"2: b"
*/
for (let key in obj2) console.log(`${key}: ${obj2[key]}`);
/*
"1: a"
"2: b"
*/
```

#### 💠 Working With Object `[[Prototype]]` Property

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/prototype-methods)

`Object.setPrototypeOf`/`Object.getPrototypeOf` allows to set/get object `[[Prototype]]` in a modern way

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

`Object.prototype.toString` can display the type of primitives, objects with `Symbol.toStringTag`, and built-in objects:

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

Global symbol registry allows the creation and access of global symbols (accessible from anywhere in the code) with unique descriptions

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

#### 💠 Converting to Array

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/iterable#array-from)

`Array.from` allows to make an array (shallow copy) from an iterable or array-like object:

```js
const arrayLike = {
  0: 'a',
  1: {
    0: 'b1',
    1: 'b2'
  },
  2: 'c',
  length: 3
};

console.log(arrayLike);
/*
[object Object] {
  0: "a",
  1: [object Object] {
    0: "b1",
    1: "b2"
  },
  2: "c",
  length: 3
}
*/

console.log(Array.from(arrayLike));
/*
["a", [object Object] {
  0: "b1",
  1: "b2"
}, "c"]
*/
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

### Map

#### 💠 Map/Iterable Conversion

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/map-set#iteration-over-map)

`Map.prototype.keys`, `Map.prototype.values`, and `Map.prototype.entries` can be used to get an iterable object from a map (map insertion order is preserved):

```js
const map = new Map()
  .set(1, 'a')
  .set(2, 'b');

console.log(...map.keys()); // 1 2
console.log(...map.values()); // "a" "b"
console.log(...map.entries()); // [1, "a"] [2, "b"]
```

#### 💠 Iterating Over Map

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/map-set#iteration-over-map)

`Map.prototype.forEach` can be used to iterate over a map (map insertion order is preserved):

```js
const map1 = new Map()
  .set(1, 'a')
  .set(2, 'b');

map1.forEach((value, key, map) => console.log(`${key}: ${value}`));
/*
"1: a"
"2: b"
*/
```

### Set

#### 💠 Set/Iterable Conversion

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/map-set#iteration-over-set)

`Set.prototype.keys`, `Set.prototype.values`, and `Set.prototype.entries` can be used to get an iterable object from a set (set insertion order is preserved); they work in a way that preserves compatibility with the corresponding `Map.prototype` methods:

```js
const set = new Set()
  .add(2)
  .add(3)
  .add(1);

console.log(...set.keys()); // 2 3 1
console.log(...set.values()); // 2 3 1
console.log(...set.entries()); // [2, 2] [3, 3] [1, 1]
```

#### 💠 Iterating Over Set

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/map-set#iteration-over-set)

`Set.prototype.forEach` can be used to iterate over a set (set insertion order is preserved); it works in a way that preserves compatibility with the corresponding `Map.prototype` method:

```js
const set1 = new Set()
  .add(2)
  .add(3)
  .add(1);

set1.forEach((value, valueAgain, set) => console.log(value)); // 2 3 1
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

Arguments for `call()` are provided individually while for `apply()` as an array/array-like object

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

### Promise

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/promise-api)

#### 💠 `Promise.all`

`Promise.all` allows to execute many promises concurrently until all are resolved or any of them is rejected (if any is rejected, the resulting promise is immediately rejected while remaining source promises operations continue with their results being ignored); it takes an iterable (of promises; or values to be passed "as is" to the resulting promise) and returns a promise which resolves with an array of results from the resolved source promises (in the same order):

```js
Promise.all([
  new Promise(resolve => setTimeout(() => resolve(1), 1000)),
  new Promise(resolve => setTimeout(() => resolve(2), 100)),
  3,
  new Promise(resolve => setTimeout(() => resolve(4), 500))
])
  .then(resultArray => console.log("1: Resolved!", resultArray));
// "1: Resolved!" [1, 2, 3, 4]

Promise.all([
  new Promise(resolve => setTimeout(() => resolve(1), 1000)),
  new Promise(resolve => setTimeout(() => resolve(2), 100)),
  new Error(),
  new Promise(resolve => setTimeout(() => resolve(4), 500))
])
  .then(
    resultArray => console.log("2: Resolved!", resultArray),
    err => console.log("2: Rejected!", err)
  );
// "2: Resolved!" [1, 2, [object Error] { ... }, 4]

Promise.all([
  new Promise(resolve => setTimeout(() => resolve(1), 1000)),
  new Promise(resolve => setTimeout(() => resolve(2), 100)),
  new Promise((resolve, reject) => setTimeout(() => reject(new Error()), 200)),
  new Promise(resolve => setTimeout(() => resolve(4), 500))
])
  .then(
    resultArray => console.log("3: Resolved!", resultArray),
    err => console.log("3: Rejected!", err)
  );
// "3: Rejected!" [object Error] { ... }
```

#### 💠 `Promise.allSettled`

`Promise.allSettled` allows the execution of many promises concurrently until all are settled (whether resolved or rejected); it takes an iterable (of promises; or values to be passed "as is" to the resulting promise) and returns a promise that resolves with an array of results from the resolved source promises (in the same order); each result in the arrays is an object, `{ status: "fulfilled", value: result }` for each fulfilled promise, or `{ status: "rejected", reason: error }` for each rejected promise:

```js
Promise.allSettled([
  new Promise(resolve => resolve(1)),
  new Promise((resolve, reject) => reject(new Error())),
  new Promise(resolve => resolve(3))
])
  .then(result => console.log(result));
/*
[[object Object] {
  status: "fulfilled",
  value: 1
}, [object Object] {
  reason: [object Error] { ... },
  status: "rejected"
}, [object Object] {
  status: "fulfilled",
  value: 3
}]
*/
```

#### 💠 `Promise.race`

Differs from `Promise.all` in that it resolves with the first settled (whether resolved or rejected) promise while ignoring other results/errors:

```js
Promise.race([
  new Promise(resolve => setTimeout(() => resolve(1), Math.random()*1000)),
  new Promise((resolve, reject) => setTimeout(() => reject(new Error()), Math.random()*1000)),
  new Promise(resolve => setTimeout(() => resolve(3), Math.random()*1000))
])
  .then(
    result => console.log(result),
    error => console.log(error)
   );
// 1 OR [object Error] { ... } OR 3
```

#### 💠 `Promise.any`

Differs from `Promise.all` in that it either resolves with the first resolved promise while ignoring other results/errors or (if all source promises were rejected) it rejects with `AggregateError` object (stores an array of all the source promises errors in its `errors` property):

```js
Promise.any([
  new Promise(resolve => setTimeout(() => resolve(1), Math.random()*1000)),
  new Promise((resolve, reject) => setTimeout(() => reject(new Error()), Math.random()*1000)),
  new Promise(resolve => setTimeout(() => resolve(3), Math.random()*1000))
])
  .then(
    result => console.log(result),
    error => console.log(error)
   );
// 1 OR 3

Promise.any([
  new Promise((resolve, reject) => setTimeout(() => reject(new Error()), Math.random()*1000)),
  new Promise((resolve, reject) => setTimeout(() => reject(new Error()), Math.random()*1000)),
  new Promise((resolve, reject) => setTimeout(() => reject(new Error()), Math.random()*1000))
])
  .then(
    result => console.log(result),
    error => console.log(error.errors)
   );
// [[object Error] { ... }, [object Error] { ... }, [object Error] { ... }]
```

#### 💠 `Promise.resolve`

Returns a promise resolved with the given result:

```js
Promise.resolve("Ok")
  .then(result => console.log(result));
// "Ok"

new Promise(resolve => resolve("Ok"))
  .then(result => console.log(result));
// "Ok"
```

Used when `async`/`await` is not supported but a function must return a promise.

#### 💠 `Promise.reject`

Returns a promise rejected with the given error:

```js
Promise.reject(new Error())
  .catch(console.log);
// [object Error] { ... }

new Promise((resolve, reject) => reject(new Error))
  .catch(console.log);
// [object Error] { ... }
```

Almost never used.

### Date

#### 💠 Creation

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/date#creation)

```js
// The result is in GMT/UTC+0:

console.log(new Date()); // 2024-03-25T15:12:21.469Z

console.log(new Date(0)); // 1970-01-01T00:00:00.000Z
console.log(new Date(-1000 * 60 * 60 * 24)); // 1969-12-31T00:00:00.000Z

console.log(new Date('2024-03-25')); //2024-03-25T00:00:00.000Z
console.log(new Date('2024-03-25 16:00')); // 2024-03-25T15:00:00.000Z

// The result is in GTM/UTC+0 (but could be 1 hour less if during daylight saving time (DTS)):

// The month is provided as a 0-11 number
console.log(new Date(2024, 0)); // 2023-12-31T23:00:00.000Z
console.log(new Date(2024, 3, 25, 16, 10, 15, 900)); // 2024-04-25T14:10:15.900Z
```

#### 💠 Parsing Date from a String

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/date#date-parse-from-a-string)

To parse the date (number of milliseconds from 01.01.1970 UTC+0) from a string using `Date.parse`, the string must be in the `YYYY-MM-DDTHH:mm:ss.sssZ` format (or in its shorter variants, the shortest one being `YYYY`); `T` is the delimeter; `Z` accepts `+-hh:mm` format to denote time zone other than UTC+0

```js
console.log(Date.parse('1985-01-01T16:00:45.800Z')); // 473443245800
console.log(Date.parse('1985-01-01_16:00:45.800Z')); // NaN
```

#### 💠 Accessing Date Components

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/date#access-date-components)

```js
const date = new Date();

// The result is in GMT/UTC+0:
console.log(date); // 2024-03-25T15:38:46.686Z

//The result (if not in the UTC format) is in the local time zone:
console.log(date.getFullYear()); // 2024
console.log(date.getUTCFullYear()); // 2024
console.log(date.getMonth()); // 2 (counting from 0 to 11)
console.log(date.getUTCMonth()); // 2 (counting from 0 to 11)
console.log(date.getDate()); // 25 (day of the month)
console.log(date.getUTCDate()); // 25 (day of the month)
console.log(date.getHours()); // 16
console.log(date.getUTCHours()); // 15
console.log(date.getMinutes()); // 38
console.log(date.getUTCMinutes()); // 38
console.log(date.getSeconds()); // 46
console.log(date.getUTCSeconds()); // 46
console.log(date.getMilliseconds()); // 686
console.log(date.getUTCMilliseconds()); // 686

console.log(date.getDay()); // 1 (Tuesday; counting from Sunday as 0 to Saturday as 6)
console.log(date.getTime()); // 1711381126686 (a number of milliseconds from 01-01-1970 UTC+0)
console.log(date.getTimezoneOffset()); // -60 (the difference between UTC and the local time zone, in minutes)
```

#### 💠 Setting Date Components

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/date#setting-date-components)

```js
const date = new Date();

// The result is in GMT/UTC+0:

console.log(date); // 2024-03-25T16:03:15.146Z

date.setFullYear(1985); console.log(date); // 1985-03-25T16:03:15.146Z
date.setUTCFullYear(1985); console.log(date); //1985-03-25T16:03:15.146Z

date.setMonth(0, 10); console.log(date); // 1985-01-10T16:03:15.146Z
date.setUTCMonth(0, 10); console.log(date); // 1985-01-10T16:03:15.146Z

date.setDate(5); console.log(date); // 1985-01-05T16:03:15.146Z
date.setUTCDate(5); console.log(date); // 1985-01-05T16:03:15.146Z

date.setHours(0); console.log(date); // 1985-01-04T23:03:15.146Z (subtracted 1 hour from the UTC+1 to UTC+0)
date.setUTCHours(0); console.log(date); // 1985-01-04T00:03:15.146Z

date.setMinutes(10, 50, 800); console.log(date); // 1985-01-04T00:10:50.800Z
date.setUTCMinutes(10, 50, 800); console.log(date); // 1985-01-04T00:10:50.800Z

date.setSeconds(45, 750); console.log(date); // 1985-01-04T00:10:45.750Z
date.setUTCSeconds(45, 750); console.log(date); // 1985-01-04T00:10:45.750Z

date.setMilliseconds(700); console.log(date); // 1985-01-04T00:10:45.700Z
date.setUTCMilliseconds(700); console.log(date); // 1985-01-04T00:10:45.700Z

date.setTime(0); console.log(date); // 1970-01-01T00:00:00.000Z
```

#### 💠 Date Autocorrection

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/date#autocorrection)

```js
let date = new Date('1985-01-31');

console.log(date); // 1985-01-31T00:00:00.000Z

date.setDate(32);
console.log(date); // 1985-02-01T00:00:00.000Z

date.setDate(0); // The minimal day-of-the-month value is 1, so the last day of the previous month will be set
console.log(date); // 1985-01-31T00:00:00.000Z

date.setDate(date.getDate() + 1);
console.log(date); // 1985-02-01T00:00:00.000Z
```

#### 💠 Date-to-Primitive Conversions

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/date#date-to-number-date-diff)

To string:

```js
let date = new Date('1985-01-31');

console.log(date); // 1985-01-31T00:00:00.000Z
date += ' !!! ';
console.log(date); // Fri Feb 01 1985 01:00:00 GMT+0100 (czas środkowoeuropejski standardowy) !!!
```

To number (milliseconds):

```js
let date = new Date('1985-01-31');

console.log(date); // 1985-01-31T00:00:00.000Z
console.log(+date); // 475977600000
console.log((+date + 100) - date); // 100
```

#### 💠 Time Measurement

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/date#date-now)

`Date.now` static method doesn't create a new object so it's faster and more memory-efficient than its semantically equivalent `new Date().getTime()`

```js
let start = Date.now();

setTimeout(() => console.log(Date.now() - start), 1000); // 1008
```

### Error

#### 💠 Properties

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/try-catch#error-object)

```js
try {
  console.log(1);
  error;
  console.log(2);
} catch (err) {
  console.log(err.name);
  console.log(err.message);
  console.log(err.stack);
}
/*
1
"ReferenceError"
"error is not defined"
"ReferenceError: error is not defined
    at bayorocida.js:3:3
    at https://static.jsbin.com/js/prod/runner-4.1.8.min.js:1:13924
    at https://static.jsbin.com/js/prod/runner-4.1.8.min.js:1:10866"
*/
```

#### 💠 Extending Error Object

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/custom-errors)

```js
class MyError extends Error {
  constructor(message) {
    super(message);
    this.name = this.constructor.name;
  }
}

class MyParticularError extends MyError {
  constructor(message) {
    super(message);
  }
}

const err = new MyParticularError("Something went wrong...");

console.log(err.name, err.message); // "MyParticularError" "Something went wrong..."
```

#### 💠 Built-In `Error` Subclasses

```js
console.log(new SyntaxError() instanceof Error); // true
console.log(new TypeError() instanceof Error); // true
console.log(new ReferenceError() instanceof Error); // true
```

## Internal Mechanics

### 💠 Strict Mode

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
console.log(a); // 1
```

```js
"use strict";

a = 1;
console.log(a); // ReferenceError: a is not defined
```

Prevents accidental creation of global variables when assigning value without declaration inside a function that is called afterward:

```js
function f() {
  a = 1;
  var b = 2;
}

f();
console.log(a); // 1
// console.log(b); // ReferenceError: b is not defined
```

```js
"use strict";

function f() {
  a = 1;
  var b = 2;
}

f();
// console.log(a); // ReferenceError: a is not defined
// console.log(b); // ReferenceError: b is not defined
```

##### Function Declaration

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/function-expressions#function-expression-vs-function-declaration)

Makes the function visible only within the block scope in which it was declared

```js
if (true) {
  function f() {}
}

console.log(typeof f); // "function"
```

```js
"use strict";

if (true) {
  function f() {}
}

console.log(typeof f); // undefined
```

##### this Value

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/object-methods#this-is-not-bound)

When a function is called without an object, the value of `this` is:
- `undefined` when in the strict mode
- global object when not in the strict mode

##### Writing to a Non-Writible Property

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/property-descriptors#non-writable)

When not in strict mode, writing to a non-writable property will not result in an error, although the operation will not succeed

##### Code String Lexical Environment

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/eval)

Code executed from a string using `eval` has its own lexical environment in the strict mode:

```js
"use strict";

eval(`
  let a = 1;
`);

//console.log(a); // ReferenceError: a is not defined
```

When not in the strict mode (:warning: **Note: The following code should not result in a ReferenceError, but I could not get it to work in either a browser or Node.js**):

```js
eval(`
  let a = 1;
`);

// console.log(a); // ReferenceError: a is not defined
```

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

### 💠 Reference Record

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/reference-type)
>
> 📖 [ECMA-262](https://tc39.es/ecma262/#sec-reference-record-specification-type)

Is a specification type, a result of a property access

It passes information about the object (`this` value) and the property from the `.` to the calling parentheses `()`

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

### 💠 Hoisting

> 📖 [Codecademy | Learn Intermediate JavaScript](https://www.codecademy.com/courses/learn-intermediate-javascript/articles/javascript-hoisting)

At compile time the engine allocate memory by hoisting variable names and function declarations to the top of their corresponding scopes; functions are initialized immediately while variable initializations are done in-place:

```js
console.log(typeof f); // "function"
function f() {}

console.log(a); // undefined
var a = 1;

console.log(b); // ReferenceError: Cannot access 'b' before initialization
let b = 2;
```

Functions declared by function expressions follow the same rules as variables:

```js
console.log(typeof f1); // "function"
function f1() {}

// console.log(typeof f2); // ReferenceError: Cannot access 'f2' before initialization
const f2 = function() {};
console.log(typeof f2); // "function"

// console.log(typeof f3); // ReferenceError: Cannot access 'f3' before initialization
const f3 = () => {};
console.log(typeof f3); // "function"
```

### 💠 Execution Context

> 📖 [Codecademy | Learn Intermediate JavaScript](https://www.codecademy.com/courses/learn-intermediate-javascript/articles/javascript-concurrency-model-and-event-loop)
>
> 📖 [Felix Gerschau | JavaScript Event Loop And Call Stack Explained](https://felixgerschau.com/javascript-event-loop-call-stack/)
>
> 📖 [The Modern JavaScript Tutorial](https://javascript.info/recursion#the-execution-context-and-stack)

AKA execution context stack

Execution context data structure stores information about a given function call, including:
- current place in the control flow
- current variables, the value of `this`

Nested execution contexts are stored in the call stack (LIFO order) as frames

### 💠 Event Loop

> 📖 [Codecademy | Learn Intermediate JavaScript](https://www.codecademy.com/courses/learn-intermediate-javascript/articles/javascript-concurrency-model-and-event-loop)
>
> 📖 [Felix Gerschau | JavaScript Event Loop And Call Stack Explained](https://felixgerschau.com/javascript-event-loop-call-stack/)

JavaScript is single-threaded; the Event Loop (which is a code execution management system) allows to emulate concurrency:
1. Memory Heap and Call Stack (parts of JavaScript engine) interact with Node.js or Web APIs
2. Node.js or Web APIs send tasks to the Event Queue
3. Event Loop manages sending tasks from the Event Queue to the Call Stack in the FIFO order

`PromiseJobs` queue ("microtask queue" as called in V8) has higher priority than the callback queue:

```js
console.log(1);

setTimeout(() => console.log(2));

Promise.resolve(3).then(console.log);

console.log(4);

// 1 4 3 2
```

### 💠 Memory Data Structures

> 📖 [Codecademy | Learn Intermediate JavaScript](https://www.codecademy.com/courses/learn-intermediate-javascript/articles/javascript-intro-to-memory-management)
>
> 📖 [Codedamn | Memory Management in JavaScript – Complete guide](https://codedamn.com/news/javascript/memory-management-complete-guide)

#### The Stack

Used for static memory allocation - the size of the data type (primitive data types) is known at compile time and a fixed amount of memory is reserved for it

Stores (in the LIFO order) primitive values, references to non-primitive values, and function call frames

#### The Heap

Used for dynamic memory allocation at runtime

The size of the stored data is unknown at compile time or may change during runtime (e.g. objects, functions, arrays)

### 💠 Memory Life Cycle

> 📖 [Codecademy | Learn Intermediate JavaScript](https://www.codecademy.com/courses/learn-intermediate-javascript/articles/javascript-intro-to-memory-management)

#### Memory Allocation

Memory is allocated on:
- Variable declaration or assignment
- Object property declaration or assignment
- Function declaration
- Function call

#### Memory in Use

Memory is used when reading or writing the allocated memory:
- Variable reassignment
- Using variables
- Passing arguments to functions

#### Garbage Collection

JavaScript engines can use the following algorithms to release/clear memory:
- Reference counting (counts references stored in the stack; releases allocated memory when the count is zero)
- Mark-and-sweep (starts from the global object traversing all variables and marking the reachable ones; unmarked variables are garbage collected during the sweep phase)

### 💠 Memory Issues

> 📖 [Codecademy | Learn Intermediate JavaScript](https://www.codecademy.com/courses/learn-intermediate-javascript/articles/javascript-intro-to-memory-management)

#### Memory Leak

Occurs when unneeded memory persists

##### Improper Use of Closure

```js
function f() {
  const obj = {};
  objRef = obj;
  
  return (key, value) => obj[key] = value;
}

let objRef;
let fClient = f();

Array(5).fill(null).map((el, i) => fClient(Math.random(), el));
console.log(objRef);
/*
[object Object] {
  0.015052069172389881: null,
  0.13197042074765353: null,
  0.3760346483058761: null,
  0.7320972499204941: null,
  0.7908977615944583: null
}
*/

Array(5).fill(null).map((el, i) => fClient(Math.random(), el));
console.log(objRef);
/*
[object Object] {
  0.015052069172389881: null,
  0.13197042074765353: null,
  0.13960590007031048: null,
  0.3760346483058761: null,
  0.44942327222905365: null,
  0.4809711814293085: null,
  0.5490505986665013: null,
  0.5692808372579412: null,
  0.7320972499204941: null,
  0.7908977615944583: null
}
*/
```

##### Improper Use of Scheduling Functions

The callback function and its outer variables are kept in memory until the scheduling is cleared using `clearTimeout`/`clearInterval`

##### Improper Use of Event Listeners

Anonymous functions used in event listeners can be the cause of memory leaks in certain cases

##### Circular References

If a browser uses the reference counting algorithm for garbage collection, circular references can cause memory leaks

#### Global Scope Variables

```js
function f() {
  a = 1;
  this.b = 2;
}

f();

console.log(window.a, window.b); // 1 2
```

#### Frequent Garbage Collection

High object churn can slow down application execution due to frequent garbage collection; the object pool design pattern may be used to improve performance

## Programming Techniques

### 💠 Swapping the Values of Two Variables

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/destructuring-assignment)

The values of two variables can be swapped using a destructuring assignment:

```js
let a = 1;
let b = 2;

console.log(a, b); // 1 2
[a, b] = [b, a];
console.log(a, b); // 2 1
```

### 💠 Transforming Object Key/Value Pairs

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/keys-values-entries#transforming-objects)

Object keys or values can be transformed (using Array methods like `Array.prototype.map`, `Array.prototype.filter` etc.) by employing a combination of `Object.entries` and `Object.fromEntries`:

```js
const obj = {
    a: 1,
    b: 2
};

console.log(
    Object.fromEntries(Object.entries(obj)
        .map((entry, index, entries) => [entry[0].toUpperCase(), entry[1] * 10])
    )
); // { A: 10, B: 20 }

console.log(
    Object.fromEntries(Object.entries(obj)
        .filter((entry, index, entries) => entry[1] < 2)
    )
); // { a: 1 }
```

### 💠 Looping Over Object Key/Value Pairs

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/destructuring-assignment)

Object keys or values can be looped over using a combination of a destructuring assignment and `Object.entries`:

```js
const obj = {
    a: 1,
    b: 2
};

for (let [key, value] of Object.entries(obj)) {
    console.log(key, value);
}
/*
a 1
b 2
*/
```

### 💠 Immediately Invoked Function Expression (IIFE)

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

### 💠 Immediately Called Constructor Function

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/constructor-new#constructor-function)

```js
let abc = new function() {
  ...
}
```

Used when performing complex initialization for a single object to keep the code organized and to avoid polluting the global scope with temporary variables or functions

### 💠 Property Backward Compatibility

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

### 💠 Property-Based Encapsulation

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/property-accessors#smarter-getters-setters)

The convention is to treat the properties with names starting with `_` as internal properties

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

### 💠 Symbol-Based Encapsulation

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/symbol#hidden-properties)

Used for third-party code objects when it's unsafe to add properties to them in danger of affecting pre-defined behavior

### 💠 Private Members

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/symbol#hidden-properties)

Used when exposing an object to scripts that may add their own properties

### 💠 Call Forwarding

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

### 💠 Method Borrowing

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

### 💠 Passing a Method Without Losing `this`

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

### 💠 Partial Application

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

### 💠 'Very Plain'/'Pure Dictionary' Objects

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/prototype-methods#very-plain)

Used in associative arrays to avoid the default inheritance of built-in methods and `__proto__` getter/setter from `Object.prototype` which could cause side effects (hard-to-notice bugs or even vulnerabilities in the server-side JavaScript code)

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

### 💠 Mixin

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/mixins)

Mixin is a class with methods to be used by other classes (not using inheritance)

A simple example would be an object assigned to a class prototype:

```js
let mixin = {
  f() {
    console.log(this.val);
  }
};

class Cl {
  constructor(val) {
    this.val = val;
  }
}

Object.assign(Cl.prototype, mixin);

new Cl(1).f(1); // 1
```

Because mixins can override existing class methods, their naming must be carefully considered.

### 💠 Wrapping Exceptions

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/custom-errors#wrapping-exceptions)

It's a technique in which particular errors are wrapped into a more abstract one:

```js
class WrappingError extends Error {
  constructor(message, cause) {
    super(message);
    this.cause = cause;
    this.name = this.constructor.name;
  }
}

class ParticularError extends Error {
  constructor(message) {
    super(message);
    this.name = this.constructor.name;
  }
}

class AnotherParticularError extends Error {
  constructor(message) {
    super(message);
    this.name = this.constructor.name;
  }
}

function f() {
  try {
    console.log(1);
  } catch (err) {
    if (err instanceof ParticularError) {
      throw new WrappingError("Particular Error...", err)
    } else {
      throw err;
    }
  }
  
  try {
    throw new AnotherParticularError("Bad...");
    console.log(2);
  } catch (err) {
    if (err instanceof AnotherParticularError) {
      throw new WrappingError("Another Particular Error...", err)
    } else {
      throw err;
    }
  }
}

try {
  f();
} catch (err) {
  if (err instanceof WrappingError) {
    console.log(err);
  } else {
    throw err;
  }
}

/*
1
[object Error] {
  cause: [object Error] {
    name: "AnotherParticularError"
  },
  name: "WrappingError"
}
*/
```

### 💠 Mapping Data For Concurrent Asynchronous Execution

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/promise-api#promise-all)

It's a technique in which an array of data for the asynchronous operations is mapped into an array of promises passed to `Promise.all`:

```js
function asyncProcess(string) {
  return new Promise(resolve => setTimeout(() => console.log(string.toLowerCase(string)), 1000));
}

const data = ["A", "B", "C"];
const requests = data.map(el => asyncProcess(el));

Promise.all(requests);

/*
PRINTED ALL AT ONCE AFTER 1000ms:
"a"
"b"
"c"
*/
```

### 💠 Currying

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/currying-partials)
>
> 📖 [Codecademy | Learn Advanced JavaScript](https://www.codecademy.com/courses/learn-intermediate-javascript/articles/javascript-currying)

It's a technique in which a function in a form like `f(a, b, c)` is transformed (not called) into a form like `f(a)(b)(c)`

It allows easy generation of partial functions:

```js
function sum(a, b) {
  return a + b;
}

function curry(f) {
  return function (a) {
    return function (b) {
      return f(a, b);
    }
  }
}

console.log(sum(1)); // NaN

const curriedSum = curry(sum);
console.log(curriedSum(1)); // [Function (anonymous)]
console.log(curriedSum(1)(2)); // 3

const addTen = curriedSum(10);
console.log(addTen(1)); // 11
```

The `curry` function from the example above may be simplified using arrow functions:

```js
function sum(a, b) {
  return a + b;
}

function arrowCurry(f) {
  return a => b => f(a, b);
}

console.log(sum(1)); // NaN

const curriedSum = arrowCurry(sum);
console.log(curriedSum(1)); // [Function (anonymous)]
console.log(curriedSum(1)(2)); // 3

const addTen = curriedSum(10);
console.log(addTen(1)); // 11
```

It also allows modular function calls (handling one task per call so that the function is easier to read/debug/reuse):

```js
const databaseXYZ = [
  { id: "01", val1: 1, val2: "A", val3: true },
  { id: "02", val1: 2, val2: "A", val3: false },
  { id: "03", val1: 2, val2: "B", val3: false },
  { id: "04", val1: 2, val2: "B", val3: true }
];

function complexFilter(data, filterKey, filterValue) {
  return data.filter(item => item[filterKey] === filterValue);
}

console.log(complexFilter(databaseXYZ, 'val3', false));
/*
[
  { id: '02', val1: 2, val2: 'A', val3: false },
  { id: '03', val1: 2, val2: 'B', val3: false }
]
*/

function curryFilter(f) {
  return data => filterKey => filterValue => f(data, filterKey, filterValue);
}

const curriedFilter = curryFilter(complexFilter);
const filterDatabaseXYZ = curriedFilter(databaseXYZ);
const filterDatabaseXYZByVal3 = filterDatabaseXYZ('val3');
console.log(filterDatabaseXYZ); // [Function (anonymous)]
console.log(filterDatabaseXYZByVal3); // [Function (anonymous)]

const filterDatabaseXYZByFalseVal3 = filterDatabaseXYZByVal3(false);
console.log(filterDatabaseXYZByFalseVal3);
/*
[
  { id: '02', val1: 2, val2: 'A', val3: false },
  { id: '03', val1: 2, val2: 'B', val3: false }
]
*/
const filterDatabaseXYZByTrueVal3 = filterDatabaseXYZByVal3(true);
console.log(filterDatabaseXYZByTrueVal3);
/*
[
  { id: '01', val1: 1, val2: 'A', val3: true },
  { id: '04', val1: 2, val2: 'B', val3: true }
]
*/
```

Advanced currying (requires the function to be curried to have a fixed number of arguments, so currying `f(...args)` is not allowed) allows to call the curried function both normally and partially:

```js
function sum(a, b, c) {
  return a + b + c;
}

function curry(f) {
  return function curried(...args) {
    if (args.length < f.length) {
      return (...args2) => curried(...args.concat(args2));
      // OR: return (...args2) => curried.apply(this, args.concat(args2));
    } else {
      return f(...args);
      // OR: return f.apply(this, args);
    }
  }
}

const curriedSum = curry(sum);
console.log(curriedSum(1)); // [Function (anonymous)]
console.log(curriedSum(1, 2)); // [Function (anonymous)]
console.log(curriedSum(1, 2, 3)); // 6
console.log(curriedSum(1, 2, 3, 4)); // 6
console.log(curriedSum(1)(2)); // [Function (anonymous)]
console.log(curriedSum(1, 2)(3)); // 6
console.log(curriedSum(1)(2, 3)); // 6
console.log(curriedSum(1)(2)(3)); // 6
```
