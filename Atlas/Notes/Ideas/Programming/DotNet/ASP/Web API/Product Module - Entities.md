---
up:
  - "[[Asp DotNet Core Web API]]"
related: 
created: 2024-11-06
---

هنقسم البروجكت لـ Versions وهنبدأ بـ Version الـ Product

هنشتغل على الـ **Core** الأول عشان نعمل الـ Domain Models وكمان الـ Interfaces
هنعمل أول حاجة Folder هنسميه Entities

![[Pasted image 20241106072316.png]]
### Base Entity
أول حاجة هنعملها هي الـ Base Entity اللي لازم كله يورث منها 
هعمل كل الحاجات اللي جاية Public عشان هحتاج أستخدمه برا في بروجكت تاني
واتكلمنا عن الحوار دا في الـ [[Cs Access Modifiers]]

```cs
public class BaseEntity
{
	public int Id {get; set;} // Property for Primary key
}
```

### Domain Models in Product
عندنا 3 Entities وهما الـ Product و Product brand و Product category
كلهم هيورثوا من الـ Base Entity
 
```cs
public class ProductBrand : BaseEntity
{
	public string Name {get; set;}
}
```

```cs
public class ProductCategory : BaseEntity
{
	public string Name {get; set;}
}
```

نيجي للأساسي
```cs
public class Product : BaseEntity
{
	public string Name {get; set;}
	public string Description {get; set;}
	public string PuctureUrl {get; set;}
	public decimal Price {get; set;}
}
```
ولازم نكتب الـ Properties  بالشكل دا عشان لما نيجي نعمل Data Seeding من الـ Json Files
```json
{
	"Name": "Double Caramel Frappuccino",
	"Description": "Lorem ipsum dolor sit amet, consectetuer adipiscing elit. Maecenas porttitor congue massa. Fusce posuere, magna sed pulvinar ultricies, purus lectus malesuada libero, sit amet commodo magna eros quis urna.",
	"Price": 200,
	"PictureUrl": "images/products/sb-ang1.png",
	"CategoryId": 1,
	"BrandId": 1
    }
```

### Relationships between Domain Models
لازم نعرف العلاقات اللي بينهم وبين بعض 
وعندنا فيه اتنين Relationship بين الـ Product و الـ Brand وبين الـ Product و الـ Category

بين الـ Product والـ Brand إن كل Brand واحد جواه أكتر من Product إنما الـ Product هو تابع لـ Brand واحد بس

فلازم أعمل Mapping للـ Relationship من خلال الـ [[Navigational Property]] 

```cs
public class Product : BaseEntity
{
	public string Name {get; set;}
	public string Description {get; set;}
	public string PuctureUrl {get; set;}
	public decimal Price {get; set;}
	public ProductBrand Brand {get; set;} 
	// Navigational Property [One]
}
```
المفروض برضو أعمل Mapping ليها في الـ `ProductBrand` عشان يعرف انه هيبقا Many

```cs
public class ProductCategory : BaseEntity
{
	public string Name {get; set;}
	
	public ICollection<Product> Products {get; set;} = new HashSet<Product>();
}
```
ولازم أعملها Initialization عشان متعملش Null exception 
بس برضو الحل دا مش صح لأني مش هحتاج من الـ Brand اني أوصل للـ Products بتاعته فكدا الـ Property التانية ملهاش لازمة فالمفروض أشليها
```cs
public class ProductCategory : BaseEntity
{
	public string Name {get; set;}
	// Removed navigational Property
	// One-to-One
}
```
بس كدا هيفهم ان العلاقة One to One وهي One to Many
فكدا هحتاج أعمل Configure للـ Relationship من خلال الـ Fluent API وأقوله انها هتبقا One-to-Many

### Foreign Key
فكدا لما نعملها لما نضيف Product هيروح يعمله Add في Table الـ Product هيمثل الـ Foreign Key الخاص بالـ Brand فلازم أعمله Property بتمثله
عشان كدا بنعملها باسم الـ Entity متبوع بالـ Primary Key بتاع الـ Entity
```cs
public int ProductBrandId {get; set;} 
// Foregin Key Column : ProductBrand
```
ممكن أستخدم Data Annotation اسمها ForeignKey
```cs
[ForeignKey(nameof(Product.Brand))]
// Writing the Navigitional Property
public int ProductBrandId {get; set;} 
```
بس مش محتاج أعمل حاجة زي كدا عادي إلا لو استخدمت اسم مختلف عن اللي فوق يعني مثلًا
```cs
[ForeignKey(nameof(Product.Brand))]
public int ProductBrandId {get; set;} 
```
وممكن نظبطها Fluent API 

### Inverse Property
وممكن أستخدم في الـ Navigational Property بتاعتي حاجة اسمها `InverseProperty` عشان أقوله ايه في الـ Class التاني بيمثل الـ Navigational Property
```cs
[InverseProperty(nameof(ProducBrand.Products))] 
// لو موجود
public ProductBrand Brand {get; set;} 
```
بس لو معملتهاش في الناحية التانية مش هينفع استخدمها زي المثال بتاعنا هنا

ومش هحتاج أستخدمها في العموم إلا لو عندي أكتر من Relationship مبين اتنين Entity نفسهم
يعني لو عندي أكتر من Relationship بين الـ Product و Brand هنا نستخدمها

### كرر نفس الحوار في الـ Relation بين Product و Category
#### الحل
- كل Category عنده Many Product والـ Product تابع لـ Category واحد
- هنعمل Navigational Property في الـ Product نوعه `ProductCategory`
- ونروح نعمل واحد في الـ Category (لو محتاجه) 
  ولو مش محتاجه هتحتاج تظبطها في الـ Fluent API
- هنعمل الـ Fluent دي في الـ Product الطرف اللي فيه Navigational Property
- نعمل الـ Foreign Key وهيبقا اسمه `ProductCategoryId`
- لو محتاج أي Data Annotation زي الـ `ForeignKey` أو `InverseProperty` أو ممكن أظبطها Fluent API
- كدا هي هتبقا Cascade لأن كل الـ Foreign Keys مش بتسمح بالـ null