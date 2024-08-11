---
up:
  - "[[HTML-CSS]]"
related: 
created: 2024-05-28
---
- HTML colors are specified with predefined color names, or with RGB, HEX, HSL, RGBA, or HSLA values.
## Color Names
* In HTML, a color can be specified by using a color name:
<h3 style="background-color:Tomato;">Tomato</h3>
<h3 style="background-color:yellow;">Yellow</h3>

```HTML
<!DOCTYPE html>
<html>
<body>

<h1 style="background-color:Tomato;">Tomato</h1>
<h1 style="background-color:Orange;">Orange</h1>
<h1 style="background-color:DodgerBlue;">DodgerBlue</h1>
<h1 style="background-color:MediumSeaGreen;">MediumSeaGreen</h1>
<h1 style="background-color:Gray;">Gray</h1>
<h1 style="background-color:SlateBlue;">SlateBlue</h1>
<h1 style="background-color:Violet;">Violet</h1>
<h1 style="background-color:LightGray;">LightGray</h1>

</body>
</html>
```
HTML supports [140 standard color names](https://www.w3schools.com/colors/colors_names.asp).

## Background color
You can set the background color for HTML elements:
```HTML
<h1 style="background-color:DodgerBlue;">Hello World</h1>  
<p style="background-color:Tomato;">Lorem ipsum...</p>
```

we can add opacity for it 
```css
div {  
	background-color: green;  
	opacity: 0.3;
}
```
or use RGBA to make this.
## Text Color
You can set the color of text:
```HTML
<h1 style="color:Tomato;">Hello World</h1>  
<p style="color:DodgerBlue;">Lorem ipsum...</p>  
<p style="color:MediumSeaGreen;">Ut wisi enim...</p>
```
## Border Color
You can set the color of borders:

```HTML
<h1 style="border:2px solid Tomato;">Hello World</h1>  
<h1 style="border:2px dashed DodgerBlue;">Hello World</h1>  
<h1 style="border:2px dotted Violet;">Hello World</h1>
```
we can use special variants for border like top and bottom
```CSS
border-top: 5px solid #1098ad;
border-bottom: 5px solid #1098ad;
border-left: 5px solid #1098ad;
border-right: 5px solid #1098ad;
```
## Color Values
In HTML, colors can also be specified using ==RGB== values, ==HEX== values, ==HSL== values, ==RGBA== values, and ==HSLA== values.
rgb(255, 99, 71) = \#ff6347 = hsl(9, 100%, 64%)
RGB, HEX, and HSL
rgba(255, 99, 71, 0.5) = hsla(9, 100%, 64%, 0.5)
RGBA and HSLA, which add an Alpha channel to the color (here we have 50% transparency)

```HTML
<h1 style="background-color:rgb(255, 99, 71);">...</h1>  
<h1 style="background-color:#ff6347;">...</h1>  
<h1 style="background-color:hsl(9, 100%, 64%);">...</h1>  
  
<h1 style="background-color:rgba(255, 99, 71, 0.5);">...</h1>  
<h1 style="background-color:hsla(9, 100%, 64%, 0.5);">...</h1>
```

### RGB and RGBA Colors

An RGB color value represents RED, GREEN, and BLUE light sources.
An RGBA color value is an extension of RGB with an Alpha channel (opacity).

rgb(_red,_ _green_, _blue_)
Each parameter (red, green, and blue) defines the intensity of the color with a value between 0 and 255.

rgba(_red,_ _green_, _blue, alpha_)
The alpha parameter is a number between 0.0 (fully transparent) and 1.0 (not transparent at all)

You can use this to try all colors [HTML RGB and RGBA Colors (w3schools.com)](https://www.w3schools.com/html/html_colors_rgb.asp)

### HEX Colors

In HTML, a color can be specified using a hexadecimal value in the form:
`#_rrggbb_`
Where rr (red), gg (green) and bb (blue) are hexadecimal values between 00 and ff (same as decimal 0-255).

### HSL colors
In HTML, a color can be specified using hue, saturation, and lightness (HSL) in the form:
hsl(_hue_, _saturation_, _lightness_)
* Hue is a degree on the color wheel from 0 to 360. 0 is red, 120 is green, and 240 is blue.
* Saturation is a percentage value. 0% means a shade of gray, and 100% is the full color.
* Lightness is also a percentage value. 0% is black, and 100% is white.

hsla(_hue,_ _saturation_, _lightness, alpha_)
* The alpha parameter is a number between 0.0 (fully transparent) and 1.0 (not transparent at all)
