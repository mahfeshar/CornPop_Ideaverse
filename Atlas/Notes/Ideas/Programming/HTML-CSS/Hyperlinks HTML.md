---
up:
  - "[[HTML-CSS]]"
related: 
created: 2024-05-24
---

We use `<a>` stands for anchor.

```html
<a href="link here" target="_blank">Text of the link</a> outside

<a href="Name of html file">Blog</a> internal

<a>Text</a> 
This will be normal text not link

<a href="#">Challenges</a> 
Not point to anywhere and will go back to the top of the page
```
*  To internal pages
	Links that points to other pages within our own website 
* To outside
	Links take you to another website outside our own website
### Attributes
> `a` has a lot of [[Attributes HTML]]

`href="Link"` : To put a URL
`target="_blank"`: To make site open in another tab
`alt`: description for photo if it damaged

### Make image as link
```HTML
<a href="default.html">
	<img src="smiley.gif">
</a>
```
### Add a "tooltip"
- It will appear when you go up the text
```HTML
<a href="default.html" title="Home">Back to Home</a>
```
### Bookmark
First, use the [[Class and ID Selectors CSS#ID|ID]] to create a bookmark:
```HTML
<h2 id="C4">Chapter 4</h2>
```
Second, add a link to a bookmark
```HTML
<a href="#C4">Jump to Chapter 4</a>
```
You can also add a link to a bookmark on another page:
```HTML
<a href="html_demo.html#C4">Jump to Chapter 4</a>
```

### Remove underline 
We can use [[Styling Text CSS]]
```HTML
<a href="html_images.asp" style="text-decoration:none;">HTML Images</a>
```