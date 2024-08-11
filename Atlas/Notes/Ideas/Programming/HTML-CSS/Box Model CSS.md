---
up:
  - "[[CSS]]"
related: 
created: 2024-05-25
---
- In CSS, the term "box model" is used when talking about design and layout.

- The CSS box model is essentially a box that wraps around every HTML element. It consists of: content, [[Padding CSS]], [[Border CSS]] and [[Margins CSS]].


![[vlcsnap-2024-05-25-12h28m43s755.png]]![[Pasted image 20240525123154.png]]

---
- We can first set [[Padding CSS]] and [[Margins CSS]] to zero to all elements by [[Understanding Common CSS Terms#Universal selector|Universal Selector]]

```css
* {
	margin: 0;
	padding: 0;
}
```