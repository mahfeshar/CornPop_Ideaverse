---
up:
  - "[[Networking Fundamentals]]"
related: 
created: 2024-07-05
---
- الثورة الحقيقية في ال Networking
- إني بقسم البرنامج بتاعي ال SW لجزئين أو Two Components 
	- الجزء اللي بيتكلف أكتر وبيبقا expensive workload نشغله على جزء ال server
	- وال client كل اللي بيعمله إنه ينادي على ال server عشان يعمله العملية دي
- ال Remote Procedure Call *RPC* اتعملت: إنه بقا remote call
## Benefits
- ال Servers عبارة عن hardware تقيل
- ال Clients عكسها وهي Hardware خفيف
	- بس لسا ال client يقدر يعمل Lightweight tasks عليه من غير سيرفر مفيش مشاكل
- بس ال Clients معدوش محتاجين dependencies على حاجات تانية عشان يشغل البرنامج
- محتاجين standard لطريقة التواصل دي، We need a communication model