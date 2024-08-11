---
up:
  - "[[SQL Server MOC]]"
related: 
created: 2024-06-07
---
## Numbers
![[DataTypeNumeric.png]]
```sql
-- Numbers

   -- Integer ( tinyINT , SmallINT , INT, BIGINT)


   declare @a1 int = 10;
   declare @a2 tinyint = 255;
   print @a2;

   declare @a3 bigint = 10;
   declare @a4 smallint = 10;

   -- Fraction (Float , Decimal)

   declare @b1 float = 56.365569; -- Only first 4 numbers after .
   print @b1;



-- (5 --All number ,2 -- قبل آخر رقمين عاليمين)
   declare @b2 decimal(5,2) = 23.4;
   print @b2;

--------------------------------


-- Boolean (True/False)  -  (bit)
  declare @d1 bit = 1;
  declare @d1 bit = NULL;
```

- الأكثر استخدام هو ال INT
## Text
- ال N في الأول عشان تظبطلك موضوع اللغة، يعني لو عايز أكتب بالعربي مثلًا
- ال CHAR بيحجز كل اللي انت اديتهوله يعني لو اديتله 10 أماكن وكتبت 5 بس هيحجز ال 10 كلهم برضو 
- ال VARCHAR بيحجز على قد الكلمة اللي بتكتبها يعني لو اديتله 10 أماكن وكتبت 5 بس هيحجز 5
- ال max عشان ياخد الرقم اللي هو عايزه براحته ملوش حد معين
- لو محددتش عدد الحروف فال default حرف واحد بس `nvarchar(1) = nvarchar`
![[dataTypestring.png]]
```sql
-- Text

   -- Charachters
   -- One Charachter

   -- ( CHAR(N) , NCHAR(N))
   -- ( VARCHAR(N) , NVARCHAR(N))
   -- ( VARCHAR(MAX) , NVARCHAR(MAX))

   declare @c1 nvarchar(20) = N'ÇÍãÏ'; -- Single
   print @c1;

   declare @c2 nvarchar = 'ahmed';
   print @c2; -- a
```

- الأكثر استخدام هو ال NVARCHAR من غير max

## Date and Time

![[DataTypeDate.png]]
```sql
-- Data and Time (DATE , TIME , DATETIME , DATETIME2 , 
-- SMALLDATETIME , DATETIMEOFFSET -- التوقيت الدولي)
   
   declare @d2 date = '2022-10-15'; 
   print @d2
```