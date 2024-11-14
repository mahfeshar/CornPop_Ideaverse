### 1. Subnetting Basics
   - الفوائد الرئيسية لتقسيم الشبكة باستخدام الـ Subnetting تشمل:
     - تقليل الازدحام في الشبكة.
     - تحسين أداء الشبكة.
     - تسهيل إدارة الشبكة.
     - تسهيل الربط عبر مسافات جغرافية كبيرة.

### 2. How to create Subnets
   - يتم ذلك عن طريق أخذ بعض البتات من جزء الـ Host في عنوان IP وتخصيصها لتحديد عنوان الشبكة الفرعية (**Subnet Address**).

### 3. Subnet Masks
   - تستخدم الـ Subnet Mask لتعريف الجزء من عنوان الـ IP الذي يمثل الشبكة والجزء الذي يمثل الجهاز.
   - تتكون من قيمة 32 بت تسمح للمستقبل بتمييز جزء network ID portion عن host ID protionمعرف الجهاز.

![[Pasted image 20241114195016.png]]
### 4. Classless Inter-Domain Routing (CIDR)
   - يُستخدم لتخصيص مساحة عناوين IP لكيان معين (مثل شركة، منزل، عميل).
   - يتم استخدام ترميز Slash (`/`) لتحديد عدد البتات المفتوحة (1s)، والتي تحدد الـ Subnet Mask.

### 5. Subnetting Class C Addresses
   - في عناوين Class C، يوجد 8 بتات فقط لتحديد الأجهزة.
   - يمكن تحديد Subnet Masks ثابتة لعناوين Class C مثل:
     - `/25` : 128 - 10000000
     - `/26` : 192 - 11000000
     - `/27` : 224 - 11100000
     - `/28` : 240 - 11110000
     - `/29` : 248 -  11111000
     - `/30` : 252 - 11111100

### 6. الطريقة السريعة لتقسيم Class C
![[Pasted image 20241114200052.png]]
   - حساب عدد subnets وHosts المتاحة لكل شبكة فرعية:
     - عدد subnets يعتمد على عدد البتات المحجوزة للشبكة masked bits (1s).
       11000000 => $2^2$ *number of ones* = 4 subnets
     - عدد Valid Hosts لكل شبكة يعتمد على عدد البتات المحجوزة للجهاز (0s).
       $2^y - 2$ = number of hosts per subnet (y => the number of unmasked bits)
       11000000 (/26) => $2^6 - 2 = 62$ 

- **Valid Subnets**: $256 - subnetMask = blockSize (baseNumber)$
  $256 - 192 = 64$ (64 => the first subnet)
  The next subnet would be the base number + itself ($64 + 64 = 128$)
- Broadcast Address for each Subnet (All hosts bits turned on)
  آخر رقم عندي اللي بيسبق الـ Subnet اللي بعدها
- Valid Hosts (The number between the subnets omitting all 0s and all 1s)
  هنشيل أول واحد وآخر واحد والباقي كله Valid

---


### 7. Variable Length Subnet Masks (VLSM)
- يسمح بتطبيق **Subnet Mask** بأطوال مختلفة داخل نفس الشبكة.
- يساعد في استغلال عناوين IP بشكل أكثر كفاءة عبر تقسيم الشبكة حسب الحاجة بدلاً من استخدام قناع شبكة موحد.

![[Pasted image 20241114201406.png]]
![[Pasted image 20241114201415.png]]
![[Pasted image 20241114201926.png]]

---

### Problem 1
الـ IP كان 192.168.10.0/27

عنوان IP هو `192.168.10.0` مع **Subnet Mask** `/27`.

#### خطوات حساب الـ Subnet Mask لـ /27:

1. **فهم التدوين (/27)**:
   - الـ `/27` يعني أن أول 27 بت في عنوان IP مخصصة للشبكة، والباقي للأجهزة.
   - عدد البتات في عنوان IP هو 32، وبتالي **32 - 27 = 5 بتات** مخصصة للأجهزة.

2. **تحويل Subnet Mask لـ /27 إلى صيغة عشرية**:
   - أول 27 بت تكون 1، والباقي 0.
   - بالتالي، Subnet Mask في صيغة البتات:
     ```
     11111111.11111111.11111111.11100000
     ```

3. **تحويل الـ Subnet Mask من الصيغة الثنائية إلى عشرية**:
   - كل ثمانية بتات (octet) نحولها لعدد عشري:
     - `11111111` = 255
     - `11111111` = 255
     - `11111111` = 255
     - `11100000` = 224
   - إذن، Subnet Mask هو: `255.255.255.224`.

#### ملخص
- الـ**Subnet Mask** لـ `/27` هو `255.255.255.224`.

### Problem 2
![[Pasted image 20241114204506.png]]
![[Pasted image 20241114200604.png]]
![[Pasted image 20241114200619.png]]