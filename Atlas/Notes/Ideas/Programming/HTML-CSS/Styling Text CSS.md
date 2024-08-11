---
up:
  - "[[CSS]]"
related: 
created: 2024-05-24
---
```CSS
h1 {

    color: blue;

    font-size: 26px; /*for li, it's 16px by deafault*/

    font-family: sans-serif; /*The font we will use, and we cannot use it from our computer*/

    font-style: italic;

	font-weight: bold; /*To make text bold or light*/

	font-variant: small-caps; /* كل الحروف كابتل بس الأول بيبقا أكبر*/

	text-decoration: underline dashed; /*overline - line-through*/

    text-transform: uppercase;

    text-align: center;

    line-height: 1.5; /*it will multible for the text height*/

	list-style: none; /*It will remove bullets from list*/

	word-spacing: 100px; /*المسافة بين الكلمات*/

	letter-spacing: 10px; /*المسافة بين الحروف*/

	text-shodow: -25px -25px 5px gold; /* x y نسبة الظهور color*/
	/* 
		+x: right, -x: left
		+y: bottom, -y: top
	*/
}
```

## Font Family 
ممكن أستخدم حاجة موجودة بالفعل 

---
ممكن أستخدم حاجة مش موجودة فبستخدم API هو بيدهولي جاهز مجرد بس بعمله Link زي google fonts
Get font -> Get embed -> html -> put code in head
فيه مشكلة هنا ان ساعات فيه سيرفرات لما بترفع عليها الموقع مش بيبقا عليها نت فمش هيعرف يوصل للخط دا

---
لو مش هستخدمه من API فهعمل Download للخط نفسه من أي موقع زي da font
بتعمل Folder لFonts في المشروع بتاعك وتضيف الخط اللي انت نزلته بأي اسم والاسم دا اللي هتستخدمه 

بستخدم حاجة اسمها font face
### Font face
Specify a font named "Corn", and specify the URL where it can be found:

```css
@font-face {
	font-family: Corn;
	src: url(corn.woff);
}
```