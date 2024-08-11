---
up:
  - "[[CSS]]"
related: 
created: 2024-05-25
---

- لنفترض دلوقتي اني عايز اخلي كل أول عنصر في ال list يبقا bold فالطريقة الأولى اني استخدم الكلاس 
- بس انا دلوقتي عايز أخلي ال code يعمله automatic وهنا دي وظيفة ال pseudo classes
```CSS
li:first-child {
	font-weight: bold;
}

li:last-child {
	font-style: italic;
}

li:nth-child(2) { /*If I want any oreder of list*/
	color: red;
}

li:nth-child(odd) { /*even*/
	color: red;
}

article p:first-child { /* Misconception: this won't work*/
	color: red;
}
```

المفروض الكود اللي فوق دا يخلي أول p يقابلك يبقا أحمر
بس لأ هو بيشوف أول ابن في ال article ولو هو p بيعمل كدا ولو مش p فكدا الشرط مش صح أصلا لانه مش first-child

الطريقة دي هتبقا مفيدة جدًا لو عايز مثلًا أظبط جدول 
مفيدة أكتر لو العناصر شبه بعض أو من نفس النوع زي ال list عناصرها `li`