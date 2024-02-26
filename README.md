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

> The old HTML standard, HTML4, required a script to have a type. Usually it was `type="text/javascript"`. It’s not required anymore. . . .
> 
> `<script language=…>` This attribute was meant to show the language of the script. This attribute no longer makes sense because JavaScript is the default language. There is no need to use it.
> 
> — [The Modern JavaScript Tutorial](https://javascript.info/hello-world#the-script-tag)

References:
- [The Modern JavaScript Tutorial](https://javascript.info/hello-world#the-script-tag)
