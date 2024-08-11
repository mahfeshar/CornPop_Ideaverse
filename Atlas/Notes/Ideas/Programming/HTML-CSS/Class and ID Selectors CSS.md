---
up:
  - "[[HTML-CSS]]"
related: 
created: 2024-05-24
---

### ID
- اني بدي لل element زي اسم ليها أعرفها بيه وممكن نستخدمها اننا نعمل Bookmark
```CSS
<p id="author">This is author</p>

#author {
	font-style: italic;
}
```
### class
- ممكن نستخدم برضو class attribute وهو يعتبر زي ال id
  بس الفرق الكبير بينهم ان ال id مينفعش تتكرر
```CSS
<p class="related">Related text</p>

.related {
	list-style: none;
}
```
- في الحياة العملية مش بنستخدم ال id وبنستخدم ال classes لأن دا بيخلينا مستعدين للمستقبل ان ممكن أعمل نفس الاستايل على حاجة تانية فأقدر استخدمها

- نقدر نضيف أكتر من class في نفس ال element بكل بساطة انك تضيف space
```html
<p class="copyright another">Copyright</p>
```
