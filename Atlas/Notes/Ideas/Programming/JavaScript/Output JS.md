---
up:
  - "[[JavaScript MOC]]"
related: 
created: 2024-06-18
---

JavaScript can "display" data in different ways:

- Writing into an HTML element, using `innerHTML`.
- Writing into the HTML output using `document.write()`.
- Writing into an alert box, using `window.alert()`.
- Writing into the browser console, using `console.log()`.

## innerHTML
To access an HTML element, JavaScript can use the `document.getElementById(id)` method.

The `id` attribute defines the HTML element. The `innerHTML` property defines the HTML content:

```html
<!DOCTYPE html>  
<html>  
<body>  
  
<h1>My First Web Page</h1>  
<p>My First Paragraph</p>  
  
<p id="demo"></p>

<script>
	document.getElmenetById("demo").innerHTML = 5 + 6;
</script>

</body>  
</html>
```

## write
```html
<!DOCTYPE html>  
<html>  
<body>  
  
<h1>My First Web Page</h1>  
<p>My first paragraph.</p>  
  
<script>  
document.write(5 + 6);  
</script>  
  
</body>  
</html>
```
> [!danger]
> Using document.write() after an HTML document is loaded, will **delete all existing HTML**:

```html
<!DOCTYPE html>  
<html>  
<body>  
  
<h1>My First Web Page</h1>  
<p>My first paragraph.</p>  
  
<button type="button" onclick="document.write(5 + 6)">Try it</button>  
  
</body>  
</html>
```

The `document.write()` method should only be used for testing.

## alert
You can use an alert box to display data:
```html
<!DOCTYPE html>  
<html>  
<body>  
  
<h1>My First Web Page</h1>  
<p>My first paragraph.</p>

<script>
	window.alert(5 + 6);
</script>

</body>  
</html>
```

You can skip the `window` keyword.

## log
For debugging purposes, you can call the `console.log()` method in the browser to display data.

```js
console.log(5 + 6);
```

## Print
JavaScript does not have any print object or print methods.
The only exception is that you can call the `window.print()` method in the browser to print the content of the current window.
بالطابعة

```js
window.print();
```