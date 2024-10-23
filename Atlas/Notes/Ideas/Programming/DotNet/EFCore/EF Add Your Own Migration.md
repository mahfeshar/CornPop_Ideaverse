---
up:
  - "[[Entity Framework Core]]"
related: 
created: 2024-10-24
---


### 1. إنشاء Migration لتعبئة البيانات (Populate Data)
- يمكن إضافة **بيانات أولية (Seed Data)** باستخدام Migrations، لتجنب إدخالها يدويًا.  
- لإنشاء Migration جديدة نستخدم:
  ```bash
  add-migration PopulateData
  ```
  - سيظهر هذا الملف فارغًا لأننا **لم نعدل شيئًا** في الكود بعد.

- نضيف بيانات إلى الجدول باستخدام SQL داخل الـ Migration كالتالي:
  ```cs
  protected override void Up(MigrationBuilder migrationBuilder)
  {
      migrationBuilder.Sql(
          "INSERT INTO Employees (Name) VALUES ('Employee 1'), ('Employee 2'), ('Employee 3');"
      );
  }

  protected override void Down(MigrationBuilder migrationBuilder)
  {
      migrationBuilder.Sql(
          "DELETE FROM Employees WHERE Name IN ('Employee 1', 'Employee 2', 'Employee 3');"
      );
  }
  ```
- الـ`Up`: يحتوي على الأوامر التي يتم تنفيذها عند تطبيق Migration (مثل إدخال البيانات).
- الـ`Down`: يحتوي على أوامر التراجع (مثل حذف البيانات)، حتى يسهل الرجوع إلى حالة سابقة.
- لازم تبقا عكسها تمامًا وهنا أنا معرفش الـ Id بتاعي فهعملهم Select عن طريق الإسم

---

### 2. الرجوع إلى Migration سابقة
- إذا كنت تريد العودة إلى Migration سابقة، استخدم الأمر:
  ```bash
  update-database MigrationName
  ```
  - مثلاً، للعودة إلى حالة قاعدة البيانات عند **Migration رقم 6**:
    ```bash
    update-database migration6
    ```

- للعودة إلى الحالة الأصلية (ما قبل أي Migration):
  ```bash
  update-database -migration:0
  ```
  - سيقوم هذا الأمر **بحذف كل الجداول المرتبطة بهذه الـ Migrations**، ولكن **ملفات Migration ستظل موجودة في المشروع**.
