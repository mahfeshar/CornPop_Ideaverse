---
up:
  - "[[Box Model CSS]]"
related: 
created: 2024-05-25
---

Padding is used to create space around an element's content, inside of any defined borders.

## Individual Sides
- `padding-top`
- `padding-right`
- `padding-bottom`
- `padding-left`

All the padding properties can have the following values:

- _length_ - specifies a padding in px, pt, cm, etc.
- _%_ - specifies a padding in % of the width of the containing element
- inherit - specifies that the padding should be inherited from the parent element

```css
div {
	padding-top: 50px;
	padding-right: 30px;
	padding-bottom: 50px;
	padding-left: 80px;
}
```

## Shorthand Property
If the `padding` property has four values:

- **padding: 25px 50px 75px 100px;**
    - top padding is 25px
    - right padding is 50px
    - bottom padding is 75px
    - left padding is 100px

- **padding: 25px 50px 75px;**
    - top padding is 25px
    - right and left paddings are 50px
    - bottom padding is 75px

- **padding: 25px 50px;**
    - top and bottom paddings are 25px
    - right and left paddings are 50px

- **padding: 25px;**
    - all four paddings are 25px

```css
pading: 25px 50px 75px 100px;
padding: 25px 50px 75px;
padding: 25px 50px;
padding: 25px;
```

## Padding and Element Width

The CSS `width` property specifies the width of the element's content area. The content area is the portion inside the padding, border, and margin of an element [[Box Model CSS]]

So, if an element has a specified width, the padding added to that element will be added to the total width of the element.

### Example

Here, the `<div>` element is given a width of 300px. However, the actual width of the `<div>` element will be 350px (300px + 25px of left padding + 25px of right padding):

```css
div {
	width: 300px;
	padding: 25px;
}
```

To keep the width at 300px, no matter the amount of padding, you can use the `box-sizing` property. This causes the element to maintain its actual width; if you increase the padding, the available content space will decrease.

```css
div {
	width: 300px;
	padding: 25px;
	box-sizing: border-box;
}
```