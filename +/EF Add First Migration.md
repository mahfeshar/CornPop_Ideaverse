---
up:
  - "[[Entity Framework Core]]"
related: 
created: 2024-10-23
---
هنغير اسم الـ Database ممكن يبقا لإسم البروجكت بتاعي أو الكلاس

## Table in Database
هعمل كلاس وهو دا اللي هيمثل Table في الـ Database
حاول تخلي اسم الكلاس دا يبقا فردي مثال: `Employee` عشان هي تلقائي بتعمل الـ Table في الـ Database بالجمع `Employees`

لحد دلوقتي معندناش Database اسمها `EFCore` فدا الدور اللي هتعمله الـ Entity Framework:
- هي هتحاول تشوف الـ Database بتاعتك موجودة ولا لا، لو موجودة بيبدأ يشوف ايه الإختلافات اللي حصلت بين الكلاسيز -اللي هي بتمثل الـ Tables الموجودة في الـ DB- ومبين الـ Tables اللي موجودة فعليًا (بتشوف ايه الإختلافات وتعمل Generate Migration للإختلافات اللي حصلت دي)
  ولو مش موجودة بيعملها Creation وبعد كدا يبدأ يضيف الـ Tables اللي انت عملتها

ازاي اعمل Migration بين الأبلكيشن بتاعي والـ DB 
هندخل على ال Package Manager Console
```bash

```