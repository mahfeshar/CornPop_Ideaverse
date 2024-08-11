---
up:
  - "[[Networking Fundamentals]]"
related: 
created: 2024-07-21
---
## Types of Networks (Networks Classifications)
### Geographical Area (Covered Area)
![[Pasted image 20240721062804.png]]
#### PAN (personal Area Network)
- هي شبكة شخصية وتعتبر أصغر شبكة كمدى جغرافي لأنها تقدري تغطي لحوالي 10 - 15 متر
- بنستخدمها لما نيجي نوصل الأجهزة بتاعنا ببعض زي ما بوصل الموبايل بالكمبيوتر
  سواء Wireless زي (Bluetooth - Infrared - NFC Near field communication)
  أو Wired عن طريق USB
- بنستخدمها عشان ننقل فايلات صغيرة زي الصور والأغاني والفيديوهات
![[Pasted image 20240508074636.png]]
#### LAN (Local Area Network)
- أشهر الأنواع
- شبكة متكونة من مجموعة من الأجهزة متوصلين ببعض وموجودين في نفس المكان
- زي في السايبرات وكدا
- النوع الأكثر استخدام منه اسمه Ethernet LAN وهو ان كل الأجهزة متوصلة مع بعض عن طريق switch بال Ethernet cable
![[Pasted image 20240508074711.png]]
#### WLAN (Wireless Local Area Network)
- نفس اللي فوق بس بتبقا متوصلة من غير كابلات
- الأجهزة بتبقا متوصلة ببعض عن طريق الراوتر
![[Pasted image 20240508074749.png]]
#### CAN (Campus Area Network)
- شبكة مكونة من شبكتين LAN أو أكتر في مكان واحد أو نطاق جغرافي محدود
- زي الجامعة، كل كلية ليها شبكة LAN خاصة بيها وفالآخر كلهم متوصلين ببعض
![[Pasted image 20240508074914.png]]
#### MAN (Metropolitan Area Network)
- تعتبر أكبر من ال CAN
- بيمتد النطاق الجغرافي لمدينة صغيرة
![[Pasted image 20240508075157.png]]
#### SAN (Storage Area Network)
- High Speed network
- مهتمة بالداتا سواء التخزين او الوصول ليها
- فيها Disk arrays اللي بيبقا جواها هاردات سواء HDD او SSD
- وفيه مجموعة من الservers اللي بيتم ربط بينهم وبين ال disc array عن طريق Switches
![[Pasted image 20240508075518.png]]
##### Why SAN?
1. بتحسن أداء تخزين الداتا والوصول ليها ودا هيحسن عمليات ال Backup and restore 
2. Scalability: أقدر أزود ديسك اراي لو محتاج مساحة زيادة أو أزود سيرفرات لو محتاج أداء أحسن
3. Not affected by traffic
#### WAN (Wide area network)
- أكبر نوع من حيث النطاق الجغرافي Wide area coverage
![[Pasted image 20240508075925.png]]
- بتربط مجموغة كبيرة من الشبكات بأنواعها المختلفة اللي فوق دي في بلاد مختلفة (بتوصل العالم ببعضه)
- أكبر مثال هو الانترنت
![[Pasted image 20240508080107.png]]

### Network Topology
- الشكل التخطيطي لل network

![[Pasted image 20240507193959.png]]

![[Pasted image 20240721063516.png]]
**Types of Network Topology**:
#### Bus Topology
- بيبقا عندي central cable(bus) وبيطلع منه مجموعة من ال dropped cables ومتوصلة بالأجهزة 
- عندنا ال T- terminator ودي بتمنع ان الداتا يحصلها reflection وترجع تلف تاني في الكابل

![[Pasted image 20240507194847.png]]
- دلوقتي لو عايز أبعت ماسدج في شكل Frame من جهاز A إلى جهاز B 
- في الحالة دي الفريم هيطلع من جهاز A على ال central cable 
- كل الأجهزة في الشبكة هتستقبل نفس الفريم بس جهاز B بس اللي هيقبل الفريم وباقي الأجهزة هترفضه
- لأنه هيشوف ال destination MAC address وهيلاقيه مختلف فهيرفضه

![[Pasted image 20240507200450.png]]
نفس الفكرة لو مدرس سال سؤال لسمير فكله هيسمعه بس سمير بس اللي هيرد

![[Pasted image 20240507200619.png]]
>[!multi-column]
> > ##### Advantages
> > 1. Inexpensive
> >    مش مكلف لأنه مش بيحتاج كابلات كتير
> > 2. Easy to install
> >    سهل انك تنفذه بالمقارنة بالباقي
> 
> > ##### Disadvantages
> > 1. Low performance 
> >    لما بيتبعت ماسدج الشبكة كلها بتبقا مشغولة لأن السنترال كابل بيبقا مشغول ولازم الأجهزة التانية تستنى الماسدج دي توصل
> > 2. Limited computers 
> >    مع زيادة عدد الأجهزة الإشارة هتضعف واحتمال حدوث ال كوليجن اكبر
> > 3. Low fault tolerance
> >    مصطلح بنستخدمه عشان نعبر عن ان السيستم يقدر يشتغل حتى في حالة المشاكل
> >    Depend on central cable
> >    لو وقع أو حصله حاجة الشبكة هتقف لأن كل الأجهزة معتمدة عليه
> > 4. Less secure
> >    كل الأجهزة بتطلع على الرسالة اللي بتتبعت دي

![[Pasted image 20240507201924.png]]

#### Ring Topology
- كل جهاز متوصل بجهاز تاني في الشبكة 
- لو جهاز عايز يبعت رسالة لجهاز تاني فالرسالة لازم تعدي على كل الأجهزة اللي بينهم

![[Pasted image 20240507202158.png]]
>[!multi-column]
>> ##### Advantages
>> 1. Easy to install
>> 2. No data collision
>>    لأن الداتا بتمشي في اتجاه واحد
>
>> ##### Disadvantages
>> 1. Slower transmission
>>    لأن لازم الماسدج تعدي على كل الأجهزة اللي بين الجهازين الأول
>>2. Low fault tolerance
>>   لو كابل باظ او جهاز فصل فكل الشبكة هتقف
>>3. Difficult to reconfigure
>>   صعب اني أضيف جهاز جديد لأني هحطه بين جهازين تانيين وأقطع الوصلة وهكذا

![[Pasted image 20240507202718.png]]
#### Mesh topology
- بوصل كل جهاز بكل الأجهزة اللي موجودة في الشبكة 
- حللي مشكلة الlow fault tolerance لان لو كابل باظ فالوصلة بين الجهازين دول هتبوظ بس انما باقي الشبكة هتفضل شغالة

![[Pasted image 20240507203001.png]]
- مش بيستخدم اوي للربط بين الأجهزة بس بيكون جيد جدًا في الربط بين الراوترات
#### Star topology
- الأكثر استخدامًا
- بربط كل الأجهزة ببعض عن طريق central device (Switch or Hub) ومن خلاله كل الأجهزة تقدر تكلم بعض

![[Pasted image 20240507203218.png]]
![[Pasted image 20240507203412.png]]
### Network Model
![[Pasted image 20240721064437.png]]
![[Pasted image 20240721064500.png]]
#### Client/Server Networks
- بيبقا عندي شوية أجهزة بتتعامل انها Server وشوية بيبقوا Clients 
- ال Server بيبقا أقوى
- اتكلمنا قبل كدا عنها [[Client-Server Architecture]]
#### Peer to Peer Networks
- نفس فكرة ال Torrent ان بيبقا عندك أكتر من جهاز بقدر أنزل منهم مش جهاز واحد اسمه server