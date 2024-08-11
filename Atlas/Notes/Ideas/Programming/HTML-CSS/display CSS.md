---
up:
  - "[[CSS]]"
related: 
created: 2024-06-13
---

## The display Property
The `display` property is used to specify how an element is shown on a web page.
Every HTML element has a default display value, depending on what type of element it is. The default display value for most elements is `block` or `inline`.

## Block-level Elements
A block-level element ALWAYS starts on a new line and takes up the full width available (stretches out to the left and right as far as it can).


<div style="border: 2px solid red;">The div element is a block-level element.</div>

Examples of block-level elements:

```
- <div>
- <h1> - <h6>
- <p>
- <form>
- <header>
- <footer>
- <section>
```

## Inline Elements
An inline element DOES NOT start on a new line and only takes up as much width as necessary.

This is <span style="border:2px solid red">an inline span element inside</span> a paragraph.

Examples of inline elements:

```
- <span>
- <a>
- <img>
```

## The display Property Values

![[Pasted image 20240613115658.png]]
### Display: none;

`display: none;` is commonly used with JavaScript to hide and show elements without deleting and recreating them. Take a look at our last example on this page if you want to know how this can be achieved.

The `<script>` element uses `display: none;` as default.

## Hide an Element - display:none or visibility:hidden?

الاتنين مش بيعملوا نفس الحاجة يعني لو حطيت ال display: none هيعتبر ان العنصر مش موجود أصلًا وهيخفيه
انما ال visibility: hidden دا هيسيب مكانها فاضي فهيأثر على ال layout

```css
h1.hidden {  display: none;}

h1.hidden {  visibility: hidden;}
```
وضحة هنا أكتر [CSS Layout - The display Property](https://www.w3schools.com/css/css_display_visibility.asp)
