---
up:
  - "[[Asp DotNet Core Web API]]"
related: 
created: 2024-11-06
---
احنا هنعمل Product repository بس المفروض قبل يبقا عندي Generic Repository

## Interface
هنحتاج نعمل Interface اسمه `IGenericRepository` وزي ما اتفقنا الـ Interfaces بتتحط في الـ Core Layer
فأنا هعمل فولدر وممكن أسميه Repositories أو `Repositories.Contract` ودا الأحسن
وهعمل فولدر كمان لبعد كدا اسمه `Services.Contract` 

```cs
namspace Talabat.Core.Repositories.Contract;
public interface IGenericRepository<T> where T : BaseEntity
{
	// We will make now: 2 methods
	
}
```
- لازم تبقا `BaseEntity`
- المفروض بنعمل 5 Signatures لل 5 methods بتاعنا