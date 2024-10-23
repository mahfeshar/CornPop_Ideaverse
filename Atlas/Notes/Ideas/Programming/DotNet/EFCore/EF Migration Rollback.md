### 1. إنشاء قاعدة البيانات والجداول بعد أول Migration
- عند تنفيذ أول Migration باستخدام الأمر:
  ```bash
  update-database
  ```
  يتم **إنشاء قاعدة البيانات** تلقائيًا، بالإضافة إلى الجداول التي تم تعريفها في الـ **Domain Models** مثل `Employees`.

- الـ**EF Core** أيضًا ينشئ جدول إضافي باسم:
  ```sql
  __EFMigrationHistory
  ```
  هذا الجدول يحتفظ **بسجل لكل Migration** تم تنفيذها في قاعدة البيانات، بحيث يتمكن الـ EF من متابعة التعديلات التي تمت سابقًا.

---

### 2. محتويات `__EFMigrationHistory` وجدول Snapshots
- كل **Migration** تنفذها، يظهر لها **Row** في جدول `__EFMigrationHistory`، مع عمود `MigrationId` الذي يمثل **رقم أو اسم الـ Migration**.

![[Pasted image 20241024012150.png]]
- بالإضافة إلى ذلك، يتم إنشاء **كلاس في المشروع** باسم:
  ```cs
  ApplicationDbContextModelSnapshot
  ```

![[Pasted image 20241024012201.png]]
  - هذا الكلاس يحتوي على **نسخة Snapshot** من حالة قاعدة البيانات في كل مرحلة، بحيث يحتفظ المشروع بتاريخ **جميع الـ Migrations** التي تم تطبيقها على قاعدة البيانات.

---

### 3. إزالة Migrations والتحذيرات المتعلقة بذلك
- **لا يفضل حذف ملفات Migration يدويًا**، لأن هذا قد يؤدي إلى عدم التزامن بين الكود وقاعدة البيانات.  
- بدلاً من ذلك، استخدم أمر:
  ```bash
  remove-migration
  ```
  لكن يجب أن **تكون الـ Migration غير مطبقة على قاعدة البيانات**، وإلا سيظهر خطأ.

![[Pasted image 20241024012255.png]]

---

### 4. الرجوع إلى Migration سابقة باستخدام الأوامر
- يمكنك الرجوع إلى أي **Migration** سابقة باستخدام:
  ```bash
  update-database MigrationName
  ```
  - مثلاً: إذا كنت في **Migration رقم 10** وتريد الرجوع إلى **Migration 6**:
    ```bash
    update-database migration6
    // 10 -> 9 -> 8 -> 7 -> 6 بالتتابع
    ```

---

### 5. العودة إلى الحالة الأصلية (Migration 0)
- إذا أردت الرجوع إلى **ما قبل أي Migration** (قبل أول تعديل)، استخدم:
  ```bash
  update-database -migration:0
  ```
  - هذا الأمر يقوم بإزالة **الجداول** المرتبطة بهذه الـ Migrations من قاعدة البيانات، وكذلك حذف **الصف الخاص بها من جدول `__EFMigrationHistory`**، لكن:
    - **ملفات Migration** في المشروع لن تُحذف تلقائيًا.

![[Pasted image 20241024012330.png]]
![[Pasted image 20241024012406.png]]
![[Pasted image 20241024012759.png]]

---

### 6. حذف ملفات Migration القديمة
- إذا كنت تريد حذف ملف Migration قديم بعد الرجوع إلى **Migration 0**:
  ```bash
  remove-migration
  ```

![[Pasted image 20241024012428.png]]
![[Pasted image 20241024012439.png]]
  - ثم يمكنك إنشاء **Migration جديد** بنفس الأوامر السابقة:
    ```bash
    add-migration NewMigrationName
    update-database
    ```

---

### 7. الجديد في .NET 8* 
- في **.NET 8**، أصبحت **عمليات التراجع (Down)** والتعامل مع Snapshots محسّنة، مما يسهل متابعة التغييرات.  
- أيضًا، دعم **التعامل غير المتزامن (Async)** في عمليات الـ Migration يوفر أداءً أفضل عند العمل مع قواعد بيانات كبيرة.

---
