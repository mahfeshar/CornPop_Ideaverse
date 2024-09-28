---
up:
  - "[[CSharp MOC]]"
related: 
created: 2024-09-28
---
- شرحنا الـ [[Polymorphism]] قبل كدا
- هو مرتبط بصورة كبيرة بالـ [[Cs Inheritance]] لأن فيه مبدأ من المبادئ اللي هنا مينفعش تتحقق غير لما يحصل وراثة وهو مبدأ الـ **Overriding**

### Overriding
- في نفس المثال اللي قولناه في الـ Inheritance

#### Hide and make new version
- الطريقة دي زي ما قولنا إنها بتعمل function جديدة وبتخفي اللي في الأب نهائي
```cs
// Parent
puplic int Product()
{
	return X * Y;
}

// Child

/// Hide and make a new version
/// The VS will tell you to add new, It will hide product from the parent
public int Product() 
{
    return X * Y * Z;
}

/// TRUE
public new int Product()
{
    return X * Y * Z;
    // return base.Product() * Z;
}
```

#### Override
- دي بتعيد كتابة الحاجة تاني
- شرط: إن الفانكشن الأساسية تبقا **Public virtual**
```cs
//Parent
public virtual int Product()
{
    return X * Y;
}

// Child
public override int Product()
{
    return base.Product() * Z;
}

public override string ToString()
{
    return $"X: {X}, Y: {Y}, Z: {Z}";
}
```