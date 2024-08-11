---
up:
  - "[[HTML-CSS]]"
related: 
created: 2024-05-28
---
The CSS `height` and `width` properties are used to set the height and width of an element.
The CSS `max-width` property is used to set the maximum width of an element.

---
The `height` and `width` properties may have the following values:


- `auto` - This is default. The browser calculates the height and width
- `length` - Defines the height/width in px, cm, etc.
- `%` - Defines the height/width in percent of the containing block
- `initial` - Sets the height/width to its default value
- `inherit` - The height/width will be inherited from its parent value

```css
div {
	height: 200px;
	width: 50%; /* نص الصفحة */
	/* 100% is كل الصفحة */
	background-color: powderblue;
}
```
<p style="height: 200px; width: 50%; background-color: powderblue;">This is text</p>
## Setting max-width
- The `max-width` property is used to set the maximum width of an element.
- The `max-width` can be specified in _length values_, like px, cm, etc., or in percent (%) of the containing block, or set to none (this is default. Means that there is no maximum width).
- من غير ما استخدمها هيظهرلي تحت scroll bar لو قل عن المساحة اللي انا مديهاله
- انما بيها مش هينفع أقلل أصلًا البراوزر أقل منها

```css
div {
  height: 100px;
  max-width: 500px;
  background-color: powderblue;
}

div {
  height: 100px;
  width: 500px;
  background-color: powderblue;
}
```