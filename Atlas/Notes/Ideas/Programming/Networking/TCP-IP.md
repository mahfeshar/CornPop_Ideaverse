---
up:
  - "[[Networking Fundamentals]]"
related: 
created: 2024-11-14
---

نموذج **DoD** (اختصارًا لـ **Department of Defense** أو وزارة الدفاع الأمريكية) هو نفس نموذج **TCP/IP**، ويُعرف أحيانًا بنموذج **DoD** لأنه تم تطويره في الأصل من قبل وزارة الدفاع الأمريكية لأغراض الاتصال العسكري.

### الفرق بين DoD و TCP/IP:
- **نموذج DoD** هو الاسم الذي يُطلق على نموذج الشبكات الذي اعتمدته وزارة الدفاع الأمريكية، بينما **TCP/IP** يشير إلى بروتوكولات الشبكة الأساسية التي يعتمد عليها هذا النموذج.
### 1. TCP/IP vs OSI
   - مقارنة بين نموذج TCP/IP و[[OSI model]]. 
   - كلاهما متشابهان من حيث التصميم والوظائف، لكن يختلفان في عدد الطبقات وأسمائها.

![[Pasted image 20241114191740.png]]
### 2. طبقات نموذج TCP/IP
   - الـ**Process/Application Layer**: تتعامل مع التطبيقات والخدمات التي تُستخدم عادةً في شبكات IP، مثل **Telnet**، **FTP**، **TFTP**، **NFS**، **SMTP**، **SNMP**، **DNS**، و**DHCP**.
   - الـ**Host-to-Host Layer**: هدفها حماية التطبيقات في الطبقات العليا من تعقيدات الشبكة، وتحتوي على بروتوكولات مثل **TCP** و**UDP**.
     This layer says to the upper layer, “Just give me your data stream, with any instructions, and I’ll begin the process of getting your information ready to send.”
   - الـ**Internet Layer**: تتعامل مع عناوين **IP** وتوجيه البيانات عبر الشبكات.
   - الـ**Network Access**: تتعلق بالاتصال الفعلي مع الوسائط المادية لنقل البيانات.

![[Pasted image 20241114191950.png]]


### 3. Application Layer Protocols
   - الـ**Telnet**: بروتوكول للوصول الافتراضي للأجهزة وتوفير اتصال نصي تفاعلي بين جهازين.
   - الـ**FTP**: بروتوكول لنقل الملفات بين الأجهزة.
   - الـ**SMTP**: بروتوكول لإرسال البريد الإلكتروني.
   - الـ**DNS**: نظام لتسمية المجالات وترجمة أسماء النطاقات إلى عناوين IP.
   - الـ**DHCP**: بروتوكول لتوفير عناوين IP للأجهزة بشكل تلقائي.

![[Pasted image 20241114192046.png]]
![[Pasted image 20241114192117.png]]
![[Pasted image 20241114192137.png]]
### 4. Host-to-Host Protocols
   - الـ**TCP**: يوفر اتصالاً موثوقاً ويستخدم في التطبيقات التي تتطلب تأكيد استقبال البيانات.
   - الـ**UDP**: يستخدم في التطبيقات التي تتطلب سرعة عالية ولا تحتاج لتأكيد استقبال البيانات، مثل المكالمات الصوتية والفيديو.

### 5. Port Numbers
   - تخصيص أرقام منافذ محددة لبروتوكولات TCP وUDP مثل:

![[Pasted image 20241114192502.png]]
![[Pasted image 20241114192419.png]]
### 6. Internet Layer
   - تشمل استخدام **[[IP Address]]**، حيث يحدد بروتوكول **IP** العنوان الفريد لكل جهاز على الشبكة لتوجيه البيانات.
   - الـ**ICMP**: بروتوكول يستخدم للتحكم في الرسائل وتقديم معلومات حول مشاكل الشبكة.

![[Pasted image 20241114192627.png]]
### 7. التوجيه وحل عناوين IP
   - الـ**ARP**: يستخدم لتحويل عناوين IP إلى [[MAC Address]].

![[Pasted image 20241114192728.png]]
### 8. [[IP Address]]
   - عنوان IP هو معرّف رقمي يُخصص لكل جهاز على شبكة IP لتحديد موقعه.
   - **الطبقات**: عناوين Class A، Class B، Class C، والعناوين الخاصة المستخدمة داخل الشبكات المحلية.

![[Pasted image 20241114194054.png]]
### 9. مصطلحات عنوان IP
   - الـ**Bit**: وحدة واحدة من البيانات الثنائية (0 أو 1).
   - الـ**Byte**: مجموعة مكونة من 8 بتات.
   - الـ**Octet**: رقم ثنائي مكون من 8 بتات، ويمكن استخدامه بالتبادل مع البايت.
   - الـ**Network Address**: عنوان يستخدم لتوجيه البيانات إلى شبكة بعيدة.
   - الـ**Broadcast Address**: عنوان يستخدم لإرسال المعلومات إلى جميع الأجهزة على الشبكة.

### 10. عناوين IP المحجوزة
   - بعض عناوين IP مخصصة لأغراض خاصة مثل:
     - **127.0.0.1**: مخصص لاختبارات الاتصال الداخلي (Loopback).
     - **255.255.255.255**: بث لجميع العقد في الشبكة.

![[Pasted image 20241114194208.png]]