---
up:
  - "[[Networking Fundamentals]]"
related: 
created: 2024-07-06
Output: "[[OSI model - Article]]"
---

> Open Systems Interconnection model

## Why do we need a communication model?
- بدون الـ Standard model:
	- التطبيق مش هيعرف طبيعة الـ [[Network Components#Network media|media]] أو الوسيلة اللي هيتواصل من خلالها (زي السلوك).
	  - السيرفر مش هيعرف يتواصل مع الـ Client.
	  - مش هتعرف تحول الإشارات من signal لـ analog والعكس.
- على حسب طبيعة الـ media وطريقة التواصل لازم تحدد طريقة التواصل لكل واحدة منهم زي: WIFI، Ethernet، LTE، Fiber.
  - لازم تعمل لكل واحدة منهم version مخصصة.
  - لكن دلوقتي الوضع مختلف، يعني لو بتبني تطبيق Node.js وبتبعت أو تستقبل طلبات، مش بيفرق البرنامج بيشتغل على ايه.
---
- بدون الـ Standard model، تحديث معدات الشبكة هيكون صعب upgrade for network equipment. 
---
- تقدر تطور وتبتكر في كل layer بشكل منفصل من غير ما تأثر على باقي الـ models.
- تقدر تطور الـ Physical layer، يعني لو شغال على تقنية قديمة زي radio، تقدر تحولها لـ fiber لأنها أسرع، وكده من غير ما تأثر على باقي الـ models.

---
![[Pasted image 20240721121818.png]]
## Intro
- قامت منظمة ال iso بعمل نظام موحد لكي يستخدم على مختلف انظمة التشغيل المختلفة (ويندوز – لينكس – یونکس ….. و غيرها ) 
- لكي يسهل على انظمة التشغل أن تتخاطب معا بلغة موحدة، وهذا النظام هو OSI Layers 
- هو يمثل مراحل سبع تمر من خلالها البيانات من جهاز المرسل مرورا بالشبكة حتى تصل إلى الجهاز المستقبل والعكس
- The OSI Model, also known as the Open Systems Interconnection Model, is a conceptual framework that defines how network communication should occur. 
- It's a foundational concept in understanding how data travels across networks.
- كل مرحلة بتمثل specific networking component
![[Pasted image 20240508082553.png]]
## OSI Layers

مراحل OSI السبع :- (وهذا الترتيب من 7 إلى 1 حسب جهاز المستقبل وليس المرسل)

7- Application Layer  (HTTP/FTP/gRPC)
6- Presentation Layer (Encoding - Serialization)
5- Session Layer (Connection establishment - TLS)
4- Transport Layer (UDP/TCP) - **Segments**
3- Network Layer (IP) - **Packets**
2- Data Link Layer (Frames - Mac address Ethernet) - **Frames**
1- Physical Layer (Electric signals - fibber - radio waves)
### 7- Application layer (*Worry*) 
- دي المرحلة اللي بيتعامل فيها الuser مع واجهات البرامج زي المتصفح، البريد الإلكتروني، والألعاب الإلكترونية.
- الطبقة دي بتوفر network services للـ applications وبتضمن تواصلها مع بعضها على الشبكة.
- بيحدد البروتوكول اللي هيدعم ال action اللي انت بتعمله ويوفره
	- البروتوكولات زي HTTP (تصفح الويب)، SMTP (البريد الإلكتروني)، وFTP (نقل الملفات) بتشتغل في الطبقة دي.
- مثال: في مطعم، Application layer زي منطقة الانتظار والقائمة. 
  المستخدم بيتفاعل مع القائمة (Application) عشان يختار اللي عايزه (Service)، ومنطقة الانتظار (Application layer) بتسهل التواصل مع المطبخ (Network) لتوصيل الطلب (data).

![[Pasted image 20240508082847.png]]
#### Application Layer Protocols
- We talked about [[Protocol]]
##### English
Some common application layer protocols and how they function:
- **`HTTP` (Hypertext Transfer Protocol):** The cornerstone of web browsing. 
  HTTP establishes the rules for how web browsers and servers communicate. 
  When you enter a website address, HTTP works behind the scenes, fetching the requested web pages and data from the server and presenting them on your screen.
- **`HTTPS` (Hypertext Transfer Protocol Secure):** HTTPS is the secure version of HTTP. 
  It encrypts communication between web browsers and servers, safeguarding sensitive data like credit card information or login credentials during transmission. 
  Imagine HTTPS as a secure vault that protects important information while it travels across the network.
- **`SMTP` (Simple Mail Transfer Protocol):** This protocol is the workhorse behind email functionality. 
  When you compose an email and hit send, SMTP takes charge, transferring the email message from your computer to the recipient's mail server.
- **`FTP` (File Transfer Protocol):** FTP allows users to transfer files between computers on a network. It provides a mechanism for uploading and downloading files to and from remote servers, similar to moving photos from your phone to your computer.
- **`SSH` (Secure Shell):** This protocol enables secure remote access to computer systems. SSH encrypts communication between a local computer and a remote server, allowing authorized users to log in and manage these remote systems securely. Imagine SSH as a secure tunnel that grants authorized access and control over a remote computer.

##### عربي
بعض البروتوكولات الشهيرة في طبقة التطبيقات ووظيفتها:
-  الـ **`HTTP` (Hypertext Transfer Protocol):** دا الأساس في تصفح الويب وبيحدد إزاي المتصفحات والسيرفرات تتواصل. 
  لما تدخل عنوان موقع، HTTP بيشتغل في الخلفية ويجيب لك صفحات الويب والبيانات المطلوبة من السيرفر.
  
- الـ **`HTTPS` (Hypertext Transfer Protocol Secure):** النسخة الآمنة من HTTP. 
  بيشفر الاتصال بين المتصفحات والسيرفرات، وبيحمي البيانات الحساسة زي معلومات بطاقات الائتمان أو بيانات تسجيل الدخول أثناء النقل.
  
- الـ **`SMTP` (Simple Mail Transfer Protocol):** البروتوكول المسؤول عن البريد الإلكتروني. 
  لما تكتب إيميل وتضغط إرسال، SMTP بيتولى نقل الرسالة من جهازك لسيرفر بريد المستلم.
  
- الـ **`FTP` (File Transfer Protocol):** بيسمح بنقل الملفات بين الأجهزة على الشبكة. 
  زي لما ترفع أو تنزل ملفات من سيرفر بعيد، زي ما بتنقل صور من تليفونك للكمبيوتر.
  
- الـ **`SSH` (Secure Shell):** بيمكنك من الوصول الآمن عن بُعد للأنظمةوبيشفر الاتصال بين الكمبيوتر المحلي والسيرفر البعيد، وبيسمح للمستخدمين المصرح لهم بالدخول وإدارة الأنظمة البعيدة بشكل آمن.
### 6- Presentation Layer 
This layer focuses on how data is presented for exchange between different systems. 
It handles **data formatting**, **encryption**, and **compression** to ensure compatibility between sender and receiver, regardless of their underlying hardware or software. 
(Note: While some references mention this layer, it's not always implemented in real-world protocols.)
1. Translation (Formatting)
	- بياخد الداتا اللي جاية من الـ application layer (حروف، أرقام، صور..) اللي هي human language ويحوله لـ machine language.
2. Data Compression
	- بيضغط الملفات عشان يقلل حجمها ويسهل عملية النقل.
3. Encryption
	- بيشفر الداتا ولما الـ receiver بتجيله الداتا بيفك الشفرة دي عن طريق بروتوكول SSL

![[Pasted image 20240508083432.png]]
### 5- Session Layer  
This layer **establishes, manages, and terminates sessions** between communicating applications. 
It ensures data exchange occurs in an orderly manner, allowing applications to exchange control information and synchronize communication.
هي اللي بتبدأ ال session الفعلية ومن هنا بيبدأ يبعت

---
بيعمل أربع عمليات مختلفة:
1. Transmission mode

في المرحلة دي، بيتحدد وضع النقل وعندنا 3 أنواع:
	- **Simplex:** زي التليفزيون، بتستقبل بس ومبتبعتش.
	- **Half-duplex:** إرسال واستقبال لكن مش في نفس الوقت، زي اللاسلكي.
	- **Full-duplex:** زي التليفون، إرسال واستقبال في نفس الوقت.


2. Authentication

إثبات الهوية، لما تحاول تدخل على سيرفر، يطلب منك إيميل وباسوورد عشان تدخل.

3. Authorization

تحديد صلاحياتك كـ user على السيرفر، زي إذا كان لك access على فايل معين أو لأ

4. Session Management

لما تدخل على فيسبوك والنت مش شغال، بياخد معلومات من الجلسة السابقة ويخزنها مؤقتًا، وعند العودة بيعمل ريستور للبيانات حتى لو مش متصل بالنت

![[Pasted image 20240508084953.png]]

### التلاتة اللي فوق بيتلخصوا في Layer واحدة في الـ TCP/IP
### 4- Transport Layer  (**Segment** | *worry*)
دي الطبقة مسؤولة عن النقل الموثوق للبيانات بين التطبيقات على أجهزة مختلفة. 
بتقسم البيانات إلى **segments**، وتضمن توصيلها الصحيح بالترتيب، وبتتعامل مع فحص الأخطاء وإعادة الإرسال إذا لزم الأمر. 
البروتوكولات زي TCP (Transmission Control Protocol) وUDP (User Datagram Protocol) بتتحدد في الطبقة دي.

الطبقة دي بتعمل عمليتين مهمتين:

1. **Segmentation:**
   - بتقسم البيانات إلى مجموعة من الـ segments، وكل واحد منهم بيبقى له port number وsequence number، عشان لما تتجمع البيانات تاني ما تحصلش لخبطة.

2. **Flow Control:**
   - بتتحكم في معدل النقل لضمان أن المرسل والمستقبل يشتغلوا بنفس السرعة، عشان نتجنب فقد البيانات ونوصل لأفضل أداء.

3. **Protocol Selection:**
   - بتحدد البروتوكول المناسب لنقل البيانات:
     - **TCP:** دقيق جداً لكن بطيء، مناسب للتحميل أو إرسال الإيميلات.
     - **UDP:** سريع جداً لكن أقل دقة، مناسب للألعاب الأونلاين أو المكالمات. 
   - البروتوكول المناسب يُختار حسب الحاجة لسرعة أكبر أو دقة أعلى.
 ![[Pasted image 20240508090538.png]]

- كل دا بيتحدد في ال transport layer **automatically**

![[Pasted image 20240508090626.png]]
![[Pasted image 20240727190303.png]]
### 3- Network Layer  (**Packet**)
- This layer is the **heart of internetworking**. 
- It handles addressing and routing **data packets** across networks. 
- It determines the most efficient path for data to travel from source to destination, using IP addresses (Internet Protocol) to uniquely identify devices on a network.
- الـ [[Network Components#Routers|Routers]] بتشتغل في الـ Layer دي، هي اللي بتعمل العملية دي أصلًا

![[Pasted image 20240727190730.png]]

---
بتعمل عمليتين مهمين جدًا:
#### 1. Logical Addressing (End-to-end Addressing)
- في المرحلة اللي فاتت نقلنا الداتا على شكل segments
- هنا بيكون ال packet وهي ال data unit بتاع ال network layer
- بيكون في ال packet عبارة عن data segment + Source IP (IPs) + destination IP (IPr)
- بنضيف [[IP Address]] ليها للمرسل والمستقبل
#### 2. Routing (أهم فايدة ليها)
- عملية اختيار أفضل مسار ممكن الداتا تمشي فيه عشان توصل من ال source لل destination
- بيساعدني في دا مجموعة من ال Protocols 
  زي RIP (Routing Information protocol) أو OSPF (Open Shortest Path First)

![[Pasted image 20240508092357.png]]
### 2- Data Link Layer
This layer manages how data gets transmitted on the **physical network media**, such as cables or wireless signals. 
It ensures reliable data transfer between devices on the same network segment (e.g., devices connected to the same switch). 
Protocols like Ethernet and Wi-Fi operate at this layer.
#### Framing
- عرفنا اننا بنعمل Logical addressing في المرحلة اللي فاتت ودلوقتي هنعملPhysical Addressing
- هنعمل دا عن طريق ال [[MAC Address]]
- بيستقبل ال data packet اللي جاية من ال network layer ويزود عليها MAC للمرسل والمستقبل
- بيكون Frame اللي هو ال Data unit في المرحلة دي
- العملية دي اسمها Frame Encapsulation بتحصل للجهاز اللي بيبعت الداتا والجهاز اللي بيستقبل بعد ما بيستلم ال frame بيقرأ الMAC وبعدين يعمل Frame Decapsulation 
- عشان ياخد ال packet وبعدها يطلع على transport layer وهكذا لحد ما يوصل لل application layer
![[Pasted image 20240508114705.png]]
- Upper layers access the media 
- وهو ال transmission media اللي هو ال physical link بين جهازين سواء كابل او اشارات راديو او غيره
![[Pasted image 20240508123141.png]]
#### Error Detection & Correction
- ممكن خلال النقل الداتا تتعرض لعوامل خارجية تسبب مشاكل زي وجود مجال مغناطيسي قريب من السلك
- في ال data link layer هي اللي بتتأكد ان ال data وصلت سليمة ومتأثرتش بأي عوامل خارجية ولو فيه أي error هيكتشف عن طريق عدة طرق وبعدين بيعمل correction عن طريق انه بيعمل discard للفريم اللي فيه مشكلة ويرجع يطلبه تاني

عندنا 3 طرق نكتشف بيهم ال error:

1. Parity Checking:
الداتا بتبقا عبارة عن مجموعة bits فهنا بيعد عدد الوحايد لو زوجي يبقا ال parity bit = 0 ولو فردي يبقا 1
بيقارن قيمة ال parity اللي موجودة في ال sender واللي موجودة في ال receiver ولازم يبقوا بيساووا بعض
بس الطريقة دي هتنفع لو عندي مشكلة في bit واحد بس أكتر من كدا مش هتنفع
![[Pasted image 20240508124017.png]]
2. Check Sum
بياخد ال bits وبيجمع عليها ال complements المفروض كله يطلع واحد ولو عكسه المفروض يطلع zero 
فلو طلع الناتج كله اصفار يبقا كدا العملية نجحت غير كدا يبقا فشلت 
![[Pasted image 20240508124221.png]]
3. CRC (Cyclic redundancy check):
نفس الفكرة مع اختلاف تفاصيل بسيطة 
بينفذ معادلة رياضية على الداتا الموجودة في الباكت بتاع المرسل وبعدين يحطها في ال trailer بتاع الفريم ولما توصل للمستقبل هينفذ نفس المعادلة
وبيقارن قيمة المعادلة هنا وهنا
![[Pasted image 20240508124430.png]]
#### CSMA (carrier sense multiple access)
- بيمنع ان يحصل collision بين ال signals في الشبكة بتاعتي
- لما الجهاز بيبدأ يبعت أي رسالة بيدور ويشوف هل في الmedia فيه أي signal تانية  في نفس اللينك ولا لا
- أول ما يلاقيه idle بيبعت الماسدج بتاعنا
![[Pasted image 20240508124744.png]]
### 1- Physical layers
The most basic layer, dealing with the physical transmission of raw data bits over the network cabling or wireless signals. 
It defines the electrical or optical specifications for transmitting data, like voltage levels, signal encoding, and connector types.
- بيحول الbits اللي وصلت لحد هنا لإشارات على حسب نوع ال media المستخدمه
- بعدين الإشارات دي بتتنقل عن طريق ال media لحد ما توصل لل physical layer بتاع الجهاز ال receiver وتمشي نفس الlayers بس بالعكس
![[Pasted image 20240508125044.png]]
### Why layered model
![[Pasted image 20240721122650.png]]
## Example
![[Pasted image 20240709070041.png]]
![[Pasted image 20240709070048.png]]
![[Pasted image 20240709070114.png]]
![[Pasted image 20240709070127.png]]
![[Pasted image 20240715052921.png]]
- لاحظ الفرق بين الراوتر والاسويتش وان router عبارة عن 3 layers وال switch اتنين بس واللي يفرقهم ان الراوتر بيهتم بال Network فمهتم بال [[IP Address]] انما ال Switch مجرد physical address اللي هو ال [[MAC Address]] والراوتر بيهتم به برضو 
## مثال شعبولي
- سمير عايز يبعت رسالة لصاحبة مدحت 
- سمير هيفتح الbrowser ويكتب facebook.com فهيلاقي ظهر http 
  ودا ال protocol المسئول عن التصفح وكل دا هيتم في application layer 
- بعدين في presentation layer بتحصل عملية ال encryption التشفير 
  وعملية تحويل لل html, JS files ل xml file عشان الbrowser يقدر يفهمها ويعرضها
- في ال session layer هيتحدد ملامح ال connection  اذا كان simplex, half-duplex or full-duplex 
  وفي الحالة دي هيبقا full-duplex
- بعدين في ال Transport layer هياخد ال data اللي جاتله من المرحلة اللي فاتت ويقطعها ل segments 
  وهيحدد هيستخدم أنهي بروتوكول في النقل سواء TCP or UDP وفي الحالة دي هيستخدم TCP
- في ال Network layer هتاخد ال segment وتحطلها source IP and destination IP عشان يكون ال packet 
- وبعدين في ال Data link layer هياخد ال packet ويحطلها source MAC and destination MAC عشان يكون ال Frame
- الفريم في ال physical layer هيكون عبارة عن مجموعة من ال bits اللي هتتحول ل signals بعد كدا 
  عشان تمشي في الmedia لحد ما توصل لل physical layer في ال destination device 
- بعدين الداتا بتطلع لdata link layer وهيعمل encapsulation لل frame
  ويبدأ يبص على ال MAC address ويقارن ال destination بالماك بتاع الجهاز لو هو هو يبقا الداتا دي بتاعته فيعملها accept ولو لا فهيعملها discard 
- بعدين هتطلع على network layer ويشوف ال IP وهكذا هتعدي على كل layers لحد ما توصل لل Application layer
  وساعتها هتظهر على الشاشة بتاع مدحت عن طريق ال application layer protocols 

![[Pasted image 20240508130431.png]]