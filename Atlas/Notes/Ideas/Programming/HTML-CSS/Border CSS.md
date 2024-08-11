---
up:
  - "[[Box Model CSS]]"
related: 
created: 2024-05-25
---
## Borders Style

- `dotted` - Defines a dotted border
- `dashed` - Defines a dashed border
- `solid` - Defines a solid border
- `double` - Defines a double border
- `groove` - Defines a 3D grooved border. The effect depends on the border-color value
- `ridge` - Defines a 3D ridged border. The effect depends on the border-color value
- `inset` - Defines a 3D inset border. The effect depends on the border-color value
- `outset` - Defines a 3D outset border. The effect depends on the border-color value
- `none` - Defines no border
- `hidden` - Defines a hidden border

The `border-style` property can have from one to four values (for the top border, right border, bottom border, and the left border).

```css
p.dotted {border-style: dotted;}
```
<p style="border-style: dotted;">Paragraph dotted</p>
>[!Note]
>None of the OTHER CSS border properties (which you will learn more about in the next chapters) will have ANY effect unless the `border-style` property is set!

### Border Sides
```css
p {  border-top-style: dotted;  
  border-right-style: solid;  
  border-bottom-style: dotted;  
  border-left-style: solid;}

p {  border-style: dotted solid;} /*Same*/
```

If the `border-style` property has four values:

- **border-style: dotted solid double dashed;**
    - top border is dotted
    - right border is solid
    - bottom border is double
    - left border is dashed

If the `border-style` property has three values:

- **border-style: dotted solid double;**
    - top border is dotted
    - right and left borders are solid
    - bottom border is double

If the `border-style` property has two values:

- **border-style: dotted solid;**
    - top and bottom borders are dotted
    - right and left borders are solid

If the `border-style` property has one value:

- **border-style: dotted;**
    - all four borders are dotted

```css
/* Four values */
p.four {
  border-style: dotted solid double dashed;
}

/* Three values */
p.three {
  border-style: dotted solid double;
}

/* Two values */
p.two {
  border-style: dotted solid;
}

/* One value */
p.one {
  border-style: dotted;
}
```


## Border Width
The `border-width` property specifies the width of the four borders.
The width can be set as a specific size (in px, pt, cm, em, etc) or by using one of the three pre-defined values: thin, medium, or thick:
```css
p.one {
	border-style: solid;
	border-width: 5px;
}

p.two {  
	border-style: solid;
	border-width: medium;
}
```

<p style="border-style: solid; border-width: 5px;">5px border-width</p>

### Specific Side Widths
```css
p.one {
  border-style: solid;
  border-width: 5px 20px; /* 5px top and bottom, 20px on the sides */
}

p.two {
  border-style: solid;
  border-width: 20px 5px; /* 20px top and bottom, 5px on the sides */
}

p.three {
  border-style: solid;
  border-width: 25px 10px 4px 35px; /* 25px top, 10px right, 4px bottom and 35px left */
}
```
## Border Color
We talked before about [[Colors CSS and HTML]]
The `border-color` property is used to set the color of the four borders.

- name - specify a color name, like "red"
- HEX - specify a HEX value, like "#ff0000"
- RGB - specify a RGB value, like "rgb(255,0,0)"
- HSL - specify a HSL value, like "hsl(0, 100%, 50%)"
- transparent

```css
p.one {  
	border-style: solid;  
	border-color: red;
}  
  
p.two {
	border-style: solid;  
	border-color: green;
}  
  
p.three {
	border-style: dotted;
	border-color: blue;
}
```
<p style="border-style: solid; border-color: red;">red text</p>
### Specific Side Colors
```css
p.one {  
	border-style: solid;  
	border-color: red green blue yellow; 
	/* red top, green right, blue bottom and yellow left */}
```
## Shorthand Border
To shorten the code, it is also possible to specify all the individual border properties in one property.

The `border` property is a shorthand property for the following individual border properties:

- `border-width`
- `border-style` (required)
- `border-color`

```css
p {
  border: 5px solid red;
}
```

You can also specify all the individual border properties for just one side:

```css
p {
  border-left: 6px solid red;
  border-right: 6px solid red;
  border-top: 6px solid red;
  border-bottom: 6px solid red;
  background-color: lightgrey;
}
```

## Rounded Borders
The `border-radius` property is used to add rounded borders to an element:
```css
p {  
	border: 2px solid red;  
	border-radius: 5px;
}
```

<p style="border: 2px solid red; border-radius: 5px;">Test Text</p>

> [!todo]
> لو خليت ال width قد ال height قد ال rounded هيعملهالك دايرة


<p style="border: 2px solid red; border-radius: 50px; width:50px; height:50px;"></p>

## outline
هو عبارة عن border فوق ال border بتاعي

```css
div {
	border: blue solid 3px;
	outline: 3px solid red;
}
```

<p style="border: blue solid 3px; outline: 3px solid red;">Test Text</p>
وهو زي ال border فيه color و style و width 

بس فيه واحدة زيادة اللي هي `outline-offset` وهي المسافة بين ال outline و ال offset

```css
div {
	border: blue solid 3px;
	outline: 3px solid red;
	outline-offset: 5px;
}
```
<p style="border: blue solid 3px; outline: 3px solid red; outline-offset:5px">Test Text</p>
وملوش radius 