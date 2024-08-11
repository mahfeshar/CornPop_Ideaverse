---
up:
  - "[[JavaScript MOC]]"
related: 
created: 2024-06-18
---

## In HTML (Internal)
the `<script>` tag
```html
<script>
	document.getElementById("demo").innerHtml = "My First JS";
</script>
```

We can put it in `head` or `body`.

### head
```html
<!DOCTYPE html>  
<html>  
<head>  
<script>  
function myFunction() {  
  document.getElementById("demo").innerHTML = "Paragraph changed.";  
}  
</script>  
</head>  
<body>

<h2>Demo JavaScript in Head</h2>  
  
<p id="demo">A Paragraph</p>  
<button type="button" onclick="myFunction()">Try it</button>

</body>  
</html>
```

### body
```html
<!DOCTYPE html>  
<html>  
<body>  
  
<h2>Demo JavaScript in Body</h2>  
  
<p id="demo">A Paragraph</p>  
  
<button type="button" onclick="myFunction()">Try it</button>  
  
<script>  
function myFunction() {  
  document.getElementById("demo").innerHTML = "Paragraph changed.";  
}  
</script>  
  
</body>  
</html>
```

> [!summary]
> أحسن حاجة انك تحطها جوا ال body تحت خالص ودا بيزود السرعة بتاع الظهور
> Placing scripts at the bottom of the \<body> element improves the display speed, because script interpretation slows down the display.


## External
We can write it at external JS file
```js
function myFunction() {  
  document.getElementById("demo").innerHTML = "Paragraph changed.";  
}
```
JavaScript files have the file extension **.js**.

To use an external script, put the name of the script file in the `src` (source) attribute of a `<script>` tag:
```html
<script src="myScript.js"></script>
```

You can place an external script reference in `<head>` or `<body>` as you like.


## External References
An external script can be referenced in 3 different ways:

- With a full URL (a full web address)
- With a file path (like /js/)
- Without any path

```html 
<script src="https://www.w3schools.com/js/myScript.js"></script>

<script src="/js/myScript.js"></script>

<script src="myScript.js"></script>
```
## Functions and Events JS
A JavaScript `function` is a block of JavaScript code, that can be executed when "called" for.

For example, a function can be called when an **event** occurs, like when the user clicks a button.