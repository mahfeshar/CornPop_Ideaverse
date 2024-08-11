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
- الأجهزة اللي هنربطها ببعض وبحد أدنى تكون جهازين ومش شرط يكون كمبيوتر بس
- Computers/ peripherals (Printers, Scanners, cams ..)
- هدفه إن الداتا بتنتهي أو بتبدأ عنده

![[Pasted image 20240507184501.png]]
#### Transmission media
- لازم الأجهزة دي تبقا متصلة ببعض بطريقة ما
- الوسط اللي الداتا بتنتقل فيه
- It should have physical connection (cables- wired, Radio frequency - wireless)
![[Pasted image 20240507184826.png]]
##### Cables
###### Coaxial cable
- معدش بيستخدم كتير ودا اللي بنستخدمه في الدش
![[Pasted image 20240507185217.png]]
###### Twisted pair cable
- اللي جاي من الكابينة وداخل الراوتر
- فيه منهم أكتر من نوع والفرق بينهم في ال transfer rate اللي هو معدل نقل ال data في الثانية الواحدة
![[Pasted image 20240507185814.png]]
![[Pasted image 20240507190148.png]]
##### Fibber optics
- شعاع ضوئي بيبقا bit وبيفضل يتعكس لحد ما يوصل
- بيستخدم في السرعات العالية
![[Pasted image 20240507190650.png]]
#### NICS (Network Interface card)
- We talked about it in [[MAC Address#NIC (Network Interface Card)|NICs]]
- الكابل مش بيفهم لغة الآلة فبالتالي دا بيبقا زي وسيط بيحول الإشارات الكهربية للغة الآلة والعكس
>[!multi-column]
> > ![[Pasted image 20240507191602.png]]
> 
> > ![[Pasted image 20240507191654.png]]

#### Networking Devices
- الأجهزة المسئولة عن إنها ت switch الداتا وبتوزع الداتا على دا وعلى دا(مش end device)
	- ماسدج الفيسبوك بتعدي على الحاجات دي لحد ما توصل لسيرفر الفيسبوك
- These devices interconnect various components within the network and manage data flow
##### Routers
- These intelligent devices direct data packets across different networks, determining the optimal path for data to reach its destination. 
- They are crucial for connecting multiple networks, like connecting your home network to the internet.
##### Switches
They provide dedicated connections between devices, improving network performance by reducing congestion.
##### Hubs
These are simpler devices that broadcast data to all connected devices, which can be less efficient for larger networks compared to switches.
##### Wireless Access Points (WAPs)
These devices create wireless networks using Wi-Fi technology, allowing devices to connect to the network without cables
### Software
#### Operating Systems (OS)
The operating system running on network devices like servers and routers manages network resources and communication protocols.
#### Network protocol
- مجموعة من القواعد اللي بيتفق عليها كل الأجهزة في الشبكة عشان يقدروا يفهموا بعض ويتبادلوا البيانات
- فنقدر نعتبرها هي اللغة اللي بيتكلموا بيها
- It's [[Protocol]]

![[Pasted image 20240507192243.png]]
- كل جهازين هيكلموا بعض لازم يبقا ليهم نفس اللغة (نفس ال network protocol)

![[Pasted image 20240507192352.png]]
- أشهر واحد هو ال IP (internet protocol)

![[Pasted image 20240507192441.png]]

#### Device Drivers
These are software programs that allow the operating system to communicate with specific hardware components like NICs.
#### Network Management Software
These tools assist network administrators in monitoring, configuring, and troubleshooting network performance and security.