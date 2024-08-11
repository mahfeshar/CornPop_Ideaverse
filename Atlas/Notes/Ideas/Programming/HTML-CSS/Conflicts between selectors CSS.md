---
up:
  - "[[CSS]]"
related: 
created: 2024-05-25
---
ايه اللي هيحصل لو اديت كذا rule لنفس الحاجة في أماكن مختلفة؟
كل الrules بتتنفذ على العنصر دا
آخر حاجة بتتشاف بتتنفذ لو ليهم نفس الأولوية

![[Pasted image 20240307080132.png]]

```css
footer p {
	color: green !important;
	/*Don't use it a lot, or use it just to debug*/
}
```
