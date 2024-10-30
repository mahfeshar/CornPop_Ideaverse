هنقسم البروجكت لـ Versions وهنبدأ بـ Version الـ Product

هنشتغل على الـ Core الأول عشان نعمل الـ Domain Models وكمان الـ Interfaces
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