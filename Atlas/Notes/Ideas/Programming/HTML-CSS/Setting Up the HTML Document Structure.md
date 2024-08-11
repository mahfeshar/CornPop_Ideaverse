---
up:
  - "[[HTML-CSS]]"
related: 
created: 2024-05-24
---

- All HTML documents have a required structure that includes the following declaration and elements: `<!DOCTYPE html>`, `<html>`, `<head>`, and `<body>`.
### DOCTYPE html
- The document type declaration, or `<!DOCTYPE html>`, informs web browsers which version of HTML is being used and is placed at the very beginning of the HTML document.
### html
- Following the document type declaration, the `<html>` element signifies the beginning of the document.
#### lang
- `lang` is a [[Attributes HTML]]
- we use it to specify the language that we use for a webpage
```html
<html lang="en">
<!-- we have codes for any language -->
```
### head
- Inside the `<html>` element, the `<head>` element identifies the top of the document, including any metadata (accompanying information about the page).
- The content inside the `<head>` element is not displayed on the web page itself.
  Instead, it may include the document title (which is displayed on the title bar in the browser window), links to any external files, or any other beneficial metadata.
#### charset
- `charset` is a [[Attributes HTML]]
- We use it to describe the character set
- We use it at `meta` element, that is mean data about the data.
- `meta` is element without a closing tag [[Self-Closing Elements HTML]]
```html
<head>
	<meta charset="UTF-8"/>
	<!-- UTF-8 have all characters that we use at English -->
</head>
```

### body
- All of the visible content within the web page will fall within the `<body>` element.
### Start Code
```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <title>Hello World</title>
  </head>
  <body>
    <h1>Hello World</h1>
    <p>This is a web page.</p>
  </body>
</html>
```