---
up:
  - "[[HTML-CSS]]"
related: 
created: 2024-05-24
---

### Heading
Every page should only have one H1 heading
```HTML
	<h1>The basic Language of the web: HTML</h1>
    <h2>The basic Language of the web: HTML</h2>
    <h3>The basic Language of the web: HTML</h3>
    <h4>The basic Language of the web: HTML</h4>
    <h5>The basic Language of the web: HTML</h5>
    <h6>The basic Language of the web: HTML</h6>
```

### Paragraph

```HTML
<p>Hello, World</p>
```

### Comments
It doesn't appear

```HTML
<!-- This is comment -->
```
### Bold Text
`<b>` : not good practice, It's old HTML because `<b>` doesn't have semantic meaning, It's without a specific meaning

`<strong>` It's same as bold but have a meaning that is really an important element

And this is the idea of [[Semantic HMTL]]

```HTML
<b>This text is bold</b>
<strong>This text is strong</strong>
```

### Italic text
`<i>` stands for italic, but it's have no meaning again

`<em>` stands for emphasize, do same thing as italic but have semantic meaning

And this is the idea of [[Semantic HMTL]]

```HTML
<i>This text is italic</i>

<em>This text is emphasized</em>
```

### under line
`<u>` stands for underline, but it's have no meaning again
`<ins>` stands for insert, but have semantic meaning

```html
<u>ccccccc</u>
<ins>ccccccc</ins>
```
<u>ccccccc</u>
<ins>ccccccc</ins>

### Highlights 
We will use `mark`
```html
<mark>Hello</mark>
```
<mark>Hello</mark>

### quotation
```html
<q>Hello</q>
```
<q>Hello</q>
### Super and sub
```html
<p>X<sup>3</sup></p>
<p>H<sub>2</sub></p>
```

<p>X<sup>3</sup></p>
<p>H<sub>2</sub></p>
### marquee
لو عايز الtext يفضل يتحرك كدا فأي اتجاه بقول عليه
```html
<marquee behavior="alternate" direction="right">
	 <h1>Corn Pop</h1>
</marquee>
```
بقوله الاتجاه وكمان لو عايز أغير بيتصرف ازاي يعني ال alternate معناها لو خبطت في طرف الصفحة ارجع تاني
### br
بيعمل  line break وبينزل الكلام لسطر تاني أو بيعمل فرق
```html
<br>
<p>
	Hello <br>
	World <br>
</p>

<p>
	Hello
	World
</p>
```
<br>
<p>
	Hello <br>
	World <br>
</p>
<b>
	Hello
	World
</b>
### pre 
بيخلي الكلام يظهر زي ما هيتكتب جواه بالظبط ومش هيغير حاجة
```html 
<pre>
	Hel   lo
	World
</pre>
```

<pre>
	Hel   lo
	World
</pre>

