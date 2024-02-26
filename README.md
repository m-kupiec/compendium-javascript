# JavaScript Reference

## TOC

- [Runtime Environments](#runtime-environments)

## Runtime Environments

### Browser

#### Execution

##### HTML <script> Tag

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
