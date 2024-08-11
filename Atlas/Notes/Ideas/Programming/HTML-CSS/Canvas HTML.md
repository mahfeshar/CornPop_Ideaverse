---
up:
  - "[[HTML]]"
related: 
created: 2024-06-22
---

The `<canvas>` element is used to draw graphics via scripting. 
JavaScript is one way to utilize scripting to draw these graphics, as shown in the example below.

```html
<canvas>
    Your browser does not support the canvas tag.
</canvas>

<script>
    var canvas = document.getElementsByTagName("canvas")[0];
    var context = canvas.getContext("2d");
    context.fillRect(0, 0, 100, 100);
</script>
```