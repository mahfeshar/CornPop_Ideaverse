We will try to styling [[Hyperlinks HTML]] and [[Buttons HTML]]

## Styling Hyperlinks
عشان أشيل الخط اللي تحت اللينك 
```css
a {
	text-decoration: none;
}
```

### pseudo classes for links
*LVHA*
[[Pseudo Classes CSS]]
#### link
عشان تعمل كدا هتستخدم ال a وهنا هنستخدم كمان pseudo class عشان انظم الشغل ويبقا أحسن

```CSS
a {
	color: red;
}

a:link {
	color: blue;
}
```
الفرق بين الاتنين اني لما استخدم pseudo class عرفته ان أي حاجة متعتبرش لينك متعملهاش style يعني ممكن أعمل a من غير ال `href` فدا مش هيتطبق عليه
#### visited
دا بنستخدمه مع اللينكات اللي تم زيارتها قبل كدا زي مثلًا جوجل بتغير اللون للون مختلف
```CSS
a:visited {
	color: #777;
}
```
#### hover
دا عشان لما تقف على اللينك تخلي الstyle بتاعه مختلف
```CSS
a:hover {
	color: orangered;
	text-decoration: underline dotted orangered; /*بتاخد أكتر من قيمة زي البوردر*/
	font-weight: bold;
}
```
#### active
دي في الحالة اللي هي بتبقا ضاغط على الماوس قبل ما تروح للصفحة التانية
```CSS
a:active {
	background-color: black;
	font-style: italic;
}
```

## Buttons
انك تعمل style لزرار نفس فكرة اللينك لأن يعتبروا زي بعض
فعندنا شوية pseudo classes زي hover 
```css
button {
	background-color: black;
	color: white;
	border: none;
	font-size: 20px;
	cursor: pointer; /*To make hand appear when you on it*/
}
button:hover {
	background-color: white;
	color: black;
}
```