---
up:
  - "[[CSS]]"
related: 
created: 2024-06-10
---

We talked before about [[Colors CSS and HTML#Background color|Background color]]

## Background image
We can add image as background of an element
By default, the image is repeated so it covers the entire element.

```css
body {
	background-image: url("paper.gif");
}
```

The background image can also be set for specific elements, like the `<p>` element.

## Background repeat
By default, the `background-image` property repeats an image both horizontally and vertically.

To make image only repeated horizontally
```css
body {
	background-image: url("gradient_bg.png");
	background-repeat: repeat-x;
}
```

**Tip:** To repeat an image vertically, set `background-repeat: repeat-y;`

To make no-repeat
```css
background-repeat: no-repeat;
```

## background-position
The `background-position` property is used to specify the position of the background image.
```css
background-position: right top;
```

## background-attachment
The `background-attachment` property specifies whether the background image should scroll or be fixed (will not scroll with the rest of the page):

```css
background-attachment: fixed; /*fixed*/
background-attachment: scroll;
```

## background - Shorthand
```css
background: #ffffff url("img_tree.png") no-repeat right top;
```

When using the shorthand property the order of the property values is:

- `background-color`
- `background-image`
- `background-repeat`
- `background-attachment`
- `background-position`
## Other
| Property                                                                               | Description                                                                   |
| -------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------- |
| [background](https://www.w3schools.com/cssref/css3_pr_background.asp)                  | Sets all the background properties in one declaration                         |
| [background-attachment](https://www.w3schools.com/cssref/pr_background-attachment.asp) | Sets whether a background image is fixed or scrolls with the rest of the page |
| [background-clip](https://www.w3schools.com/cssref/css3_pr_background-clip.asp)        | Specifies the painting area of the background                                 |
| [background-color](https://www.w3schools.com/cssref/pr_background-color.asp)           | Sets the background color of an element                                       |
| [background-image](https://www.w3schools.com/cssref/pr_background-image.asp)           | Sets the background image for an element                                      |
| [background-origin](https://www.w3schools.com/cssref/css3_pr_background-origin.asp)    | Specifies where the background image(s) is/are positioned                     |
| [background-position](https://www.w3schools.com/cssref/pr_background-position.asp)     | Sets the starting position of a background image                              |
| [background-repeat](https://www.w3schools.com/cssref/pr_background-repeat.asp)         | Sets how a background image will be repeated                                  |
| [background-size](https://www.w3schools.com/cssref/css3_pr_background-size.asp)        | Specifies the size of the background image(s)                                 |
