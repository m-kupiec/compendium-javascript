# JavaScript Reference

## TOC

- [Data](#data)
- [Runtime Environments](#runtime-environments)
- [Miscellaneous](#miscellaneous)

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

### Data Types

#### Primitives

##### 💠 Number

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/types)

May have the following values:
- integer
- floating point
- `Infinity`
- `-Infinity`
- `NaN` (represents a computational error)

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

##### 💠 null

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/types)

Represents empty or unknown value

##### 💠 undefined

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/types)

Represent not assigned value

It's recommended to assing `null` instead of `undefined` to a variable

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

## Miscellaneous

### 💠 ES5 & 'use strict'

#### Usage

> 📖 [The Modern JavaScript Tutorial: The modern mode, "use strict"](https://javascript.info/strict-mode)

`'use strict'` enables modifications introduced in ES5

Must be placed at the beginning of a script or a function

Used in classes and modules by default

Not used in the browser console by default

#### Effects

##### Variable declaration

> 📖 [The Modern JavaScript Tutorial: Variables](https://javascript.info/variables#variable-naming)

Forces variable declaration, as it's possible to simply assign a value without a declaration when not using `'use strict'`:

```js
a = 1;
```

### 💠 Automatic semicolon insertion

> 📖 [The Modern JavaScript Tutorial](https://javascript.info/structure#semicolon)
> 
> 📖 [ECMA-262](https://tc39.es/ecma262/#sec-automatic-semicolon-insertion)

Occurs an a line break in most cases

**Example exception #1**

```js
a = b + c
(d + e).f()
```

is transformed into:

```js
a = b + c(d + e).f()
```

**Example exception #2**

```js
a()
[b, c].d()
```

is transformed into:

```js
a()[b, c].d()
```
