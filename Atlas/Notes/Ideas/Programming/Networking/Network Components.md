---
up:
  - "[[Networking Fundamentals]]"
related: 
created: 2024-07-21
---
## Network Components
![[Pasted image 20240721115816.png]]
### Hardware
#### End devices
- الأجهزة النهائية اللي بنوصلها ببعض، مثل **الحواسيب والطابعات**. الهدف منها إن الداتا تبدأ أو تنتهي عندها.

![[Pasted image 20240507184501.png]]
#### Transmission media
الوسط اللي بينقل البيانات بين الأجهزة، وبيشمل:
- **الكابلات (wired)** مثل الأسلاك النحاسية.
- **الترددات اللاسلكية (wireless)** مثل الـ Wi-Fi.

![[Pasted image 20240507184826.png]]
##### Cables
###### Coaxial cable
- الكابل المستخدم في الدش، ولكنه قليل الاستخدام في الشبكات حالياً.

![[Pasted image 20240507185217.png]]
###### Twisted pair cable
- الكابل اللي بيجي من الكابينة للراوتر. يتميز بتعدد أنواعه بناءً على سرعة نقل البيانات transfer rate.

![[Pasted image 20240507185814.png]]
![[Pasted image 20240507190148.png]]
##### Fibber optics
- بيستخدم في السرعات العالية، حيث ينقل البيانات كإشارات ضوئية.

![[Pasted image 20240507190650.png]]
#### NICS (Network Interface card)
- We talked about it in [[MAC Address#NIC (Network Interface Card)|NICs]]
- الكارت المسئول عن تحويل الإشارات الكهربائية للغة الآلة والعكس، ويعمل كوسيط بين الجهاز والشبكة.
- الكابل مبيفهمش لغة الآلة

>[!multi-column]
> > ![[Pasted image 20240507191602.png]]
> 
> > ![[Pasted image 20240507191654.png]]

#### Networking Devices
- الأجهزة التي تنقل وتوزع البيانات عبر الشبكة، وليست **End Devices**.
##### Routers
- الأجهزة الذكية التي توجه حزم البيانات عبر الشبكات المختلفة وتختار أفضل مسار optimal path للوصول للوجهة المطلوبة.
- They are crucial for connecting multiple networks, like connecting your home network to the internet.
##### Switches
توفر اتصالات مخصصة بين الأجهزة، مما يحسن من أداء الشبكة عن طريق تقليل الازدحام congestion.

![[Pasted image 20241114190152.png]]
##### Hubs
- أجهزة بسيطة تبث البيانات لكل الأجهزة المتصلة، لكنها أقل كفاءة مقارنةً بالسويتشات.

![[Pasted image 20241114190230.png]]
##### Wireless Access Points (WAPs)
تتيح الاتصال بالشبكة لاسلكياً عبر تقنية Wi-Fi، مما يسمح للأجهزة بالاتصال بالشبكة بدون كابلات.
### Software
#### Operating Systems (OS)
نظام التشغيل اللي بيشتغل على الأجهزة الشبكية زي السيرفرات والرواتر ويدير موارد الشبكة وبروتوكولات الاتصال.
#### Network [[Protocol]]
- مجموعة من القواعد اللي بيتفق عليها كل الأجهزة في الشبكة عشان يقدروا يفهموا بعض ويتبادلوا البيانات
- فنقدر نعتبرها هي اللغة اللي بيتكلموا بيها

![[Pasted image 20240507192243.png]]
- كل جهازين هيكلموا بعض لازم يبقا ليهم نفس اللغة (نفس ال network protocol)

![[Pasted image 20240507192352.png]]
- أشهر واحد هو ال IP (internet protocol)

![[Pasted image 20240507192441.png]]

#### Device Drivers
- برامج بتتيح لنظام التشغيل التواصل مع المكونات المادية المعينة زي NICs.
#### Network Management Software
- أدوات تساعد مسؤولي الشبكة في مراقبة وتكوين وإصلاح أداء الشبكة والأمان فيها.