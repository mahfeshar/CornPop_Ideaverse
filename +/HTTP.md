---
up:
  - "[[Networking Fundamentals]]"
related: 
created: 2024-10-16
---


الـ **HTTP** أو **Hypertext Transfer Protocol** هو البروتوكول الأساسي اللي بنستخدمه علشان نبادل البيانات بين الكلاينت (زي المتصفح) والسيرفر على الإنترنت. 
هو اللي بيخلينا نقدر نفتح مواقع ويب، نرسل طلبات (Requests) زي طلب صفحة HTML، والسيرفر يرد علينا ببيانات (Response) زي الصفحة اللي بتظهر قدامك.

في منه إصدارين مشهورين:
- **HTTP**: العادي، بدون تشفير.
- **HTTPS**: نفس البروتوكول، بس فيه تشفير للبيانات علشان يحميها خلال الإرسال.

---
## HTTP Methods
لما تيجي تتعامل مع الـ APIs هتلاقي إن في شوية طرق للتواصل زي:
- **GET**: بتستخدمها علشان تجيب بيانات.
- **POST**: بتستخدمها علشان تضيف بيانات جديدة.
- **PUT**: علشان تحدث بيانات موجودة.
- **DELETE**: علشان تمسح بيانات.