---
up:
  - "[[Entity Framework Core]]"
related: 
created: 2024-10-23
---
![[Pasted image 20241023082733.png]]
الـ EF هو **[[ORM]] (Object-Relational Mapping)**، وده معناه إنه بيسمح للمبرمجين يتعاملوا مع **الـ Database** بطريقة سهلة من غير ما يحتاجوا يكتبوا SQL معقد. 
كأنك بتتعامل مع **Classes** في الكود بتاعك مباشرة، وكأن كل **جدول** في الـ Database هو Class موجود في المشروع.

---

### إيه الفرق بين الطريقة القديمة و Entity Framework؟  
قبل ما نستخدم EF، كنا بنحتاج نعمل كل حاجة يدوي، زي:

- نكتب **Queries** باستخدام SQL.
- نستخدم **Stored Procedures** لو الكود بتاعنا محتاج أداء أعلى أو أمان إضافي.
- نحط الـ SQL Queries دي جوه الكود، وده كان صعب في التعديل والصيانة.

لكن مع EF، بقى الموضوع أبسط بكتير. تقدر:

- تتعامل مع الـ **Database** كأنها مجموعة من **[[Cs Class]]**.
- تكتب **LINQ Queries** بدلاً من SQL.
- تقلل الأخطاء اللي ممكن تحصل لما تكتب SQL يدوي.

---

### ليه Entity Framework أفضل؟  
الـ **Entity Framework** بيسهل التعامل مع الـ **Database**، خصوصاً لو كنت بتشتغل على **Projects معقدة** أو فيها **Tables كتير**. 
مش بس كده، لكن الأداء نفسه بيكون عالي مقارنة بالطريقة اليدوية في بعض الحالات. وده لأنه:

- بيعتمد على **Lazy Loading**، يعني مش بيجيب الداتا كلها مرة واحدة، وده بيحسن الأداء.
- سهل في **Maintenance**؛ لو غيرت حاجة في الـ Database، التعديل بينعكس بسرعة في الكود.
- بيدعم أنواع كتير من الـ Databases زي **SQL Server** و**SQLite** و**MySQL**.

---
### الفرق بين **ADO.NET** و **Entity Framework**

#### 1. **كتابة الكود:**
- **ADO.NET**:  
  لازم تكتب SQL بنفسك لكل عملية (Select, Insert, Update, Delete).

  مثال:
  ```csharp
  using System.Data;
  using System.Data.SqlClient;

  var connection = new SqlConnection("Server=.;Database=MyDatabase;Trusted_Connection=True;");
  connection.Open();

  var command = new SqlCommand("SELECT * FROM Products", connection);
  var reader = command.ExecuteReader();

  while (reader.Read())
  {
      Console.WriteLine(reader["Name"]);
  }
  connection.Close();
  ```
  
- **Entity Framework**:  
  تقدر تستخدم LINQ Queries بدل SQL مباشر.

  مثال:
  ```csharp
  using (var context = new ApplicationDbContext())
  {
      var products = context.Products.ToList();
      foreach (var product in products)
      {
          Console.WriteLine(product.Name);
      }
  }
  ```

#### 2. **الأداء**:
- **ADO.NET**:  
  أسرع من Entity Framework في بعض الحالات، خصوصًا لما تشتغل مع كمية كبيرة من البيانات لأنك بتكتب SQL **Optimized**.

- **Entity Framework**:  
  أبطأ نسبيًا في بعض السيناريوهات، لكنه بيعتمد على **Lazy Loading** وبيكون أسرع في التطوير والصيانة.

#### 3. **سهولة الاستخدام**:
- **ADO.NET**:  
  صعب شوية، وبيحتاج تفاصيل كتير في كتابة الأكواد، زي فتح وغلق الاتصالات يدويًا، والتعامل مع الأخطاء.

- **Entity Framework**:  
  أسهل بكتير. كل حاجة بتحصل في الخلفية (الاتصال، التحقق من الأخطاء، إلخ). وبيخليك تركز على المنطق بدل كتابة استعلامات.

#### 4. **المرونة**:
- **ADO.NET**:  
  أكتر مرونة في كتابة Queries معقدة جدًا أو استخدام **Stored Procedures**.

- **Entity Framework**:  
  مناسب للـ CRUD Operations العادية، لكن لو فيه استعلامات معقدة جدًا، ممكن تحتاج تستخدم SQL مع EF.

#### 5. **الصيانة والتحديث**:
- **ADO.NET**:  
  الصيانة بتكون أصعب لأن أي تعديل في الـ SQL يتطلب تعديل الكود كله.

- **Entity Framework**:  
  التعديلات أسهل لأن كل حاجة مرتبطة بالـ Models والـ DbContext، وأي تغيير بينعكس تلقائي في الكود.

---

#### أيهم الأفضل؟
- **ADO.NET**:  
  مناسب لما تكون محتاج **أداء عالي جدًا** أو بتتعامل مع **مشاريع معقدة** تعتمد على **Stored Procedures** أو **Queries معقدة**.

- **Entity Framework**:  
  الأفضل في **التطوير السريع** (Rapid Development) والمشاريع اللي مش محتاجة SQL معقد. بيوفر وقت وجهد كبير وبيخلي الكود أنظف وأسهل في الصيانة.

---

#### ملخص  
ببساطة، **ADO.NET** هو خيارك لما الأداء يكون أولوية أو لما تحتاج تحكم كامل في الـ SQL. 
أما **Entity Framework** فهو الأنسب لو عايز تركز على **المنطق البرمجي** بدون الدخول في تفاصيل قواعد البيانات. 
كل واحد فيهم ليه استخداماته، وقرار اختيار الأنسب بيختلف حسب احتياجات المشروع.

### Entity Framework vs. SQL العادي  
الـ EF مش بس بيبسط الشغل، لكنه كمان بيخليك:

- **تركز على المنطق** بدل ما تضيع وقتك في SQL.
- **تجنب الأخطاء** اللي بتحصل بسبب الـ SQL Injection، لأن EF بيهتم بالأمان.
- **تتعلم بسرعة**، لأنك بتتعامل مع كود C# عادي بدل ما تحفظ Queries معقدة.

---

### الخاتمة  
ببساطة، **Entity Framework** هو طبقة بتسهل الاتصال بين الكود بتاعك والـ **Database**. بدل ما تكتب SQL بشكل يدوي، تقدر تتعامل مع **Classes** في الكود وتخلي EF يعمل كل الشغل التقيل. 
الموضوع بيساعدك تبدأ بسرعة، وبيوفر وقت ومجهود كبير خصوصاً لو المشروع بتاعك معقد أو فيه جداول كتير.

