---
up:
  - "[[Entity Framework Core]]"
related: 
created: 2024-10-23
---

### 1. **إنشاء كائن من `ApplicationDbContext`**  
- نبدأ بإنشاء **Object** من الـ `ApplicationDbContext` لربط الكود بقاعدة البيانات:
  ```cs
  var _context = new ApplicationDbContext();
  ```

### 2. **إنشاء كائن من نوع `Employee`**  
- نظرًا لأن `Employee` هو **Domain Model** يمثل **الجدول** في قاعدة البيانات، سنقوم بإنشاء Object منه.  
- لاحظ أننا لا نستطيع تعيين الـ `Id` يدويًا إذا كان يتم زيادته تلقائيًا (Auto Increment).

  ```cs
  var employee = new Employee()
  {
      Name = "Corn"
  };
  ```

### 3. **إضافة الكائن إلى DbContext**  
- يمكننا التعامل مع الـ `DbContext` كأننا نتعامل مع **List**.  
- نضيف الكائن إلى الجدول باستخدام `Add`:
  ```cs
  _context.Employees.Add(employee);
  ```

### 4. **حفظ التغييرات في قاعدة البيانات**  
- **حتى هذه اللحظة**، لم يتم حفظ التغييرات في قاعدة البيانات؛ التغييرات موجودة فقط في **الذاكرة (Memory)**.  
- يفضل تنفيذ **عدة تغييرات** (مثل إضافة أو تعديل أكثر من Object) مرة واحدة ثم حفظها، لتقليل عدد الاتصالات بقاعدة البيانات وتحسين الأداء.

  ```cs
  _context.SaveChanges();
  ```

### 5. **تنفيذ الحفظ بشكل غير متزامن (Async)**  
- في حال كنت تستخدم **[[Cs Task-Based Asynchronous Pattern]]**، يمكنك استخدام `SaveChangesAsync` مع `await` لتجنب حظر الـ Thread الرئيسي:

  ```cs
  await _context.SaveChangesAsync();
  ```

### 6. **الفرق بين `null` و String فارغ**  
- إذا أنشأت **كائن Employee بدون اسم**، سيعتمد الحفظ على إعدادات **الـ Name**.  
  - **لو الحقل قابل للـ null**، سيتم تخزين قيمة `null`.
  - **لو الحقل غير قابل للـ null**، سيحدث **خطأ** عند محاولة الحفظ.
  - هناك فرق بين **String فارغ ("")** وبين `null`. 
    - الـ**null** تعني عدم وجود قيمة نهائيًا.  
    - الـ**String فارغ** يعني وجود قيمة، لكنها لا تحتوي على نص.