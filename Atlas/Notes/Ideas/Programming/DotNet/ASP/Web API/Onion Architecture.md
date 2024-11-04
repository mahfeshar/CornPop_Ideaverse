---
up:
  - "[[Asp DotNet Core Web API]]"
related: 
created: 2024-11-04
---

قبل ما بنبدأ نشتغل بنحدد الـ **Architecture Pattern** اللي هنشتغل عليها وهنبني على أساسها الـ Application بتاعنا


هنا هنتكلم عن الـ **Onion Architecture Pattern** اللي بنبني عليه تطبيقاتنا، وده بيساعدنا نخلي التطبيق **Scalable** (قابل للتوسع) و **Modular** (سهل التعديل وإعادة الاستخدام). 
بيتميز بإن كل **Layer** موجودة فيه ممكن تتاخد وتتحط في مشروع تاني من غير ما يحصل مشاكل، وبيسهل علينا التغيير والـ **Testing**. 
وعشان كده بيشبه البصلة، عشان كل حاجة جوه طبقة مرتبة فوق بعض زي طبقات البصل.

## Onion Architecture Layers:
![[Pasted image 20241030085512.png]]
![[Pasted image 20241104160103.png]]
### 1. الـ **Domain Layer**:
الـ **Domain Layer** هي الطبقة اللي بتحتوي على **المكونات الأساسية للتطبيق** لكنها مش منفذة (Not Implemented) بالكامل. بتشمل:

- الـ**Domain Models**: ودي هي الكيانات الأساسية اللي بنشتغل بيها في التطبيق، زي **Product** أو **Order** مثلًا.
- الـ**Interfaces**: كل الـ **Interfaces** اللي هنحتاج نعملها Implement في طبقات تانية بتتكتب هنا.

بمعنى تاني، الطبقة دي زي "الكود الأساسي" اللي بيعرفلك إيه اللي التطبيق محتاج يعمله، لكن من غير تفاصيل التنفيذ نفسها.

### 2. الـ **Repository Layer**:
ودي عبارة عن **Class Library** اللي بنعمل فيها تعاملنا مع قواعد البيانات. هنا بنستخدم **Design Patterns** زي:

- الـ[[Generic Repository]]: ده بيسهل إعادة استخدام الأكواد، ويخليك تقدر تعمل أكواد عامة تقدر تتعامل مع أي **Entity** في قاعدة البيانات.
  
لو عندنا أكتر من **DbContext** أو أكتر من **Database**، ممكن يبقى عندنا أكتر من Repository عشان كل قاعدة بيانات يبقى ليها تعامل منفصل.

- الـ**Contracts في Domain Layer**: يعني الـ **Interfaces** بتاعة الـ Repositories بتكون موجودة في الـ Domain Layer. 
  مثلًا، لو عندنا Interface اسمه `IProductRepository`، ده هيتكتب في **Domain Layer**. 
  بعدين ممكن نعمل أكتر من Implementation ليه في الـ Repository Layer وكل واحدة تتعامل مع قاعدة بيانات مختلفة أو Context مختلف.

#### مثال
```cs
public interface IProductRepository
{
    Product GetProductById(int id);
}

public class ProductRepository : IProductRepository
{
    public Product GetProductById(int id)
    {
        // الكود اللي بيتعامل مع قاعدة البيانات عشان يجيب المنتج
    }
}
```
### 3. الـ **Service Layer**:
دي الطبقة اللي بتحط فيها كل الخدمات (Services) في مكان واحد، وده بيبقى مناسب لو احنا بنشتغل بنظام **[[Monolithic]] Architecture** (نظام متكامل في مشروع واحد) مش **[[Microservices]]** (تطبيق مقسم لخدمات صغيرة مستقلة). 
وعلشان احنا شغالين بـ .NET في مشروع واحد، فدي الطريقة الأنسب.

- هنا بيكون فيها كل حاجة ليها علاقة بالـ **Business Logic**، زي مثلًا مراحل معالجة (Order) من مرحلة الـ Draft لحد ما يتوافق عليه ويتبعت للشحن.
- الـ **Interfaces** بتاعتها بتبقى موجودة في الـ **Domain Layer** برضه.

#### مثال:
لو عندنا Service عشان نضيف طلب (Order):
```csharp
public interface IOrderService
{
    void CreateOrder(Order order);
}

public class OrderService : IOrderService
{
    public void CreateOrder(Order order)
    {
        // الكود اللي بينفذ منطق البيزنس الخاص بإنشاء الطلب
    }
}
```

## إزاي بنبدأ نعمل Solution منظم:
![[Pasted image 20241030111723.png]]
1. نعمل **Project جديد** كـ **Class Library** ونسميه `Talabat.Core` (ده للـ Domain Layer).
   - نحذف الملف الافتراضي (`Class1.cs`).

2. نعمل **Project تاني** للـ **Repository Layer** ونسميه `Talabat.Repository` ونخليه **Class Library** برضه.

3. نعمل **Project تالت** للـ **Service Layer** بنفس الطريقة، يعني نسميه `Talabat.Service` ونخليه Class Library.

4. ممكن نضيف مشاريع إضافية حسب احتياجاتنا، زي لو عايزين نضيف **API Layer** لواجهة الـ REST API مثلًا.

### مثال لمشروع متكامل:
- الـ`Talabat.Core`: فيه كل الـ **Domain Models** والـ **Interfaces** بتاعة الـ Repositories والـ Services.
- الـ`Talabat.Repository`: فيه Implementations للـ Repositories زي `ProductRepository` أو `OrderRepository`.
- الـ`Talabat.Service`: فيه Implementations للـ Services زي `OrderService`.

وبكده، يبقى عندك مشروع منظم وقابل للتوسع والتعديل، بحيث كل طبقة ممكن تشتغل منفصلة وتستفيد بيها في مشاريع تانية لو احتجت.