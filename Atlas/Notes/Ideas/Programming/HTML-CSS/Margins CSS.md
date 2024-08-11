---
up:
  - "[[Box Model CSS]]"
related: 
created: 2024-05-25
---

Margins are used to create space around elements, outside of any defined borders.
## Individual Sides
CSS has properties for specifying the margin for each side of an element:

- `margin-top`
- `margin-right`
- `margin-bottom`
- `margin-left`

All the margin properties can have the following values:

- auto - the browser calculates the margin
- _length_ - specifies a margin in px, pt, cm, etc.
- _%_ - specifies a margin in % of the width of the containing element
- inherit - specifies that the margin should be inherited from the parent element

```css
div {
  margin-top: 100px;
  margin-bottom: 100px;
  margin-right: 150px;
  margin-left: 80px;
}
```
## Shorthand Property
If the `margin` property has four values:

- **margin: 25px 50px 75px 100px;**
    - top margin is 25px
    - right margin is 50px
    - bottom margin is 75px
    - left margin is 100px

```css
p {
	margin: 25px 50px 75px 100px;
}
```

- **margin: 25px 50px 75px;**
    - top margin is 25px
    - right and left margins are 50px
    - bottom margin is 75px

```css
p {
	margin: 25px 50px 75px;
}
```

- **margin: 25px 50px;**
    - top and bottom margins are 25px
    - right and left margins are 50px

```css
p {
	margin: 25px 50px;
}
```

- **margin: 25px;**
    - all four margins are 25px

```css
p {
	margin: 25px;
}
```

## The auto Value
- بستخدمها عشان أعمل center للعنصر أفقي
- لو خصصت width معين فالعنصر هياخده والباقي من اليمين والشمال هيعمله هامش margin

```css
div {
  width: 300px;
  margin: auto;
  border: 1px solid red;
}
```
<p style="width: 300px; margin: auto; margin-top:5px; border: 1px solid red;">Text</p>

## The inherit Value
This example lets the left margin of the `<p class="ex1">` element be inherited from the parent element (`<div>`):
```css
div {
  border: 1px solid red;
  margin-left: 100px;
}

p.ex1 {
  margin-left: inherit;
}
```


## Margin Collapse
- باختصار لو العنصر اللي فوق عامل هامش تحت واللي تحته عامل هامش فوق فدا مش هيجمع القيمتين ويعمل الهامش بينهم لأ هو بيعمل الأكبر بينهم
- Top and bottom margins of elements are sometimes collapsed into a single margin that is equal to the largest of the two margins.
- This does not happen on left and right margins! _Only top and bottom_ margins!

```css
h1 {
  margin: 0 0 50px 0;
}

h2 {
  margin: 20px 0 0 0;
}
```

In the example above, the `<h1>` element has a bottom margin of 50px and the `<h2>` element has a top margin set to 20px.

Common sense would seem to suggest that the vertical margin between the `<h1>` and the `<h2>` would be a total of 70px (50px + 20px). But **due to margin** collapse, the actual margin ends up being 50px.