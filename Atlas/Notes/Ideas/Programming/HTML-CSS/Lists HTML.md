---
up:
  - "[[HTML-CSS]]"
related: 
created: 2024-05-24
---
We will use it to make a nav bar.
### Numbered List (ordered)
`ol` element: stands for ordered list

And for each element in list, we should create `<li>` for it and it stands for list item

```HTML
<ol>
	<li>First</li>
	<li>Second</li>
</ol>
```

We can change `type` of it from numbers to anything like characters. 
```html
<ol type="I"> <!-- roman numbers -->
</ol>
```

We can make it `start` with any number or character

```html
<ol start="3" type="a"> <!-- Will start with c -->
</ol>
```
### Bullet point
`<ul>`: stands for unordered list
We also here should use `li` element for every list item

```HTML
<ul>
	<li>First</li>
	<li>Second</li>
</ul>
```

We can change type also to circle or square or more.

```html
<ul type="square">
        <li>Item 1</li>
        <li>Item 2</li>
        <li>Item 3</li>
        <li>Item 4</li>
        <li>Item 5</li>
</ul>
```
### Definition list

![[Pasted image 20240609155728.png]]

`<dt>`: stands for definition term
`<dd>`: stands for definition description
`<dl>`: stands for definition list

```html
<dl>
	<dt>C#</dt>
	<dd>Description for language</dd>
</dl>
```
<dl>
	<dt>C#</dt>
	<dd>Description for language</dd>
</dl>

### Nested list
اني أعمل ليست جوا ليست وهكذا
```html
<ul>
	<li>
		Products
		<ul>
			<li>P1</li>
			<li>P2></li>
		</ul>
	</li>
	<li>Home</li>
</ul>
```