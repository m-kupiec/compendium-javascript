# JavaScript Reference

## TOC

- [Runtime Environments](#runtime-environments)
- [Miscellaneous](#miscellaneous)

## Runtime Environments

### Browser

#### 💠 Execution

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

References:
- [The Modern JavaScript Tutorial](https://javascript.info/hello-world#the-script-tag)

## Miscellaneous

### 💠 ES5 & 'use strict'

`'use strict'` enables modifications introduced in ES5

Must be placed at the beginning of a script or a function

Used in classes and modules by default

Not used in the browser console by default

References:
- [The Modern JavaScript Tutorial](https://javascript.info/strict-mode)

### 💠 Automatic semicolon insertion

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

References:
- [The Modern JavaScript Tutorial](https://javascript.info/structure#semicolon)
- [ECMA-262](https://tc39.es/ecma262/#sec-automatic-semicolon-insertion)
