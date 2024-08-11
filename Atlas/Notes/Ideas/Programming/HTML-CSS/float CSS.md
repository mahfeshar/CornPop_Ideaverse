---
up:
  - "[[HTML-CSS]]"
related: 
created: 2024-06-13
---

The CSS `float` property specifies how an element should float.
The CSS `clear` property specifies what elements can float beside the cleared element and on which side.

# float
The `float` property is used for positioning and formatting content e.g. let an image float left to the text in a container.

The `float` property can have one of the following values:

- `left` - The element floats to the left of its container
- `right` - The element floats to the right of its container
- `none` - The element does not float (will be displayed just where it occurs in the text). This is default
- `inherit` - The element inherits the float value of its parent
In its simplest use, the `float` property can be used to wrap text around images.
### Example
```html
<img src="pineapple.jpg" alt="Pineapple" style="width:170px;height:170px;float:right;margin-left:15px;margin-bottom:10px;">
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Phasellus imperdiet, nulla et dictum interdum, nisi lorem egestas odio, vitae scelerisque enim ligula venenatis dolor. Maecenas nisl est, ultrices nec congue eget, auctor vitae massa. 
```

## Example - Float Next To Each Other
Normally div elements will be displayed on top of each other. However, if we use `float: left` we can let elements float next to each other:

```css
div {  
	float: left;  
	padding: 15px;
}
```
![[Pasted image 20240613122205.png]]

# clear
When we use the `float` property, and we want the next element below (not on right or left), we will have to use the `clear` property.
The `clear` property specifies what should happen with the element that is next to a floating element.
The `clear` property can have one of the following values:

- `none` - The element is not pushed below left or right floated elements. This is default
- `left` - The element is pushed below left floated elements
- `right` - The element is pushed below right floated elements
- `both` - The element is pushed below both left and right floated elements
- `inherit` - The element inherits the clear value from its parent

When clearing floats, you should match the clear to the float: If an element is floated to the left, then you should clear to the left. Your floated element will continue to float, but the cleared element will appear below it on the web page.

```css
div1 {  float: left;}  

div2 {  clear: left;}
```

![[Pasted image 20240613122436.png]]
## The clearfix Hack

If a floated element is taller than the containing element, it will "overflow" outside of its container. We can then add a clearfix hack to solve this problem:

![[Pasted image 20240613122532.png]]

```css
.clearfix {  overflow: auto;}

<div class="clearfix">
  <img class="img2" src="pineapple.jpg" alt="Pineapple" width="170" height="170">
  Lorem ipsum dolor sit amet, consectetur adipiscing elit. Phasellus imperdiet...
</div>
```

The `overflow: auto` clearfix works well as long as you are able to keep control of your margins and padding (else you might see scrollbars). The **new, modern clearfix hack** however, is safer to use, and the following code is used for most webpages:

```css
.clearfix::after {  
	content: "";  
	clear: both;  
	display: table;
}
```