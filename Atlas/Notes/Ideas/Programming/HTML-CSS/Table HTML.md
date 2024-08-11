---
up:
  - "[[HTML-CSS]]"
related: 
created: 2024-06-09
---

HTML tables allow web developers to arrange data into rows and columns.
## Tables
- We define it into tag `table`
- `<td>`: Each table cell, stands for table data
- `<tr>`: Each table row
- `<th>`: you want your cells to be table header cells
- You can have as many rows as you like in a table; just make sure that the number of cells are the same in each row.

```html
<table>
	<tr>
		<th>Name</th>
		<th>age</th>
	</tr>

	<tr>
		<td>Corn</td>
		<td>22</td>
	</tr>

	<tr>
		<td>Pop</td>
		<td>50</td>
	</tr>
</table>
```

> [!note]
> By default, the text in `<th>` elements are bold and centered, but you can change that with CSS.

## Borders Styling
We can make it with html attribute called `border` but the best is to use CSS border property on `table`, `th` and `td`

```html
<table border="1">
	<tr>
		<th>Name</th>
		<th>age</th>
	</tr>

	<tr>
		<td>Corn</td>
		<td>22</td>
	</tr>

	<tr>
		<td>Pop</td>
		<td>50</td>
	</tr>
</table>
```

```css
table, th, td {
	border: 1px solid black;
	border-collapse: collapse;
	border-radius: 10px;
}

th, td {  background-color: #96D4D4;}
```

- To avoid having double borders like in the example above, set the CSS `border-collapse` property to `collapse`.
- With the `border-radius` property, the borders get rounded corners

### Border styles
- `dotted`     
- `dashed`     
- `solid`     
- `double`     
- `groove`     
- `ridge`     
- `inset`     
- `outset`     
- `none`     
- `hidden`

```css
th, td {
	border-style: dotted;
	border-color: #96D4D4;
}
```

## Size
We can add `width` and `height` with values.
```html
<table border="1" width="300" height="200">
	<tr>
		<th>Name</th>
		<th>age</th>
	</tr>

	<tr>
		<td>Corn</td>
		<td>22</td>
	</tr>

	<tr>
		<td>Pop</td>
		<td>50</td>
	</tr>
</table>
```
And we can also make it with CSS
```html
<table style="width:100%">
<table style="width:100%">
```
Read more: [Site Unreachable](https://www.w3schools.com/html/html_table_sizes.asp)

## Colspan & Rowspan
HTML tables can have cells that span over multiple rows and/or columns.
![[Pasted image 20240609213747.png]]
### Colspan بالعرض
To make a cell span over multiple columns
```html
<table>
	<tr>
		<th Colspan="2">Name</th>
		<th>Age</th>
	</tr>
	<tr>  
		<td>Jill</td>  
		<td>Smith</td>  
		<td>43</td>
	</tr>  
	<tr>  
		<td>Eve</td>  
		<td>Jackson</td>  
		<td>57</td>  
	</tr>
</table>
```

<table>
	<tr>
		<th Colspan="2">Name</th>
		<th>Age</th>
	</tr>
	<tr>  
		<td>Jill</td>  
		<td>Smith</td>  
		<td>43</td>
	</tr>  
	<tr>  
		<td>Eve</td>  
		<td>Jackson</td>  
		<td>57</td>  
	</tr>
</table>

The value of the `colspan` attribute represents the number of columns to span.

### Rowspan بالطول
To make a cell span over multiple rows
```html
<table>  
  <tr>  
    <th>Name</th>  
    <td>Jill</td>  
  </tr>  
  <tr>  
    <th rowspan="2">Phone</th>  
    <td>555-1234</td>  
  </tr>  
  <tr>  
    <td>555-8745</td>  
</tr>  
</table>
```

![[Pasted image 20240609214203.png]]