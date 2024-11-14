---
up:
  - "[[Networking Fundamentals]]"
related: 
created: 2024-11-14
---
## Intro to IP Address
- جهازك لازم يكون له **عنوان IP** عشان يتواصل مع باقي الأجهزة على الإنترنت.
- It's the identity of each [[Host]]
- الـ**Internet Protocol (IP)** هو مجموعة قواعد لازم يتبعها الجهاز عشان يقدر يتواصل على الشبكة.
- لمعرفة عنوان IP الخاص بك: (افتح CMD -> اكتب `ipconfig`).
## IP Address Structure
- عنوان IP مكون من أربع خانات (octets) مفصولة بنقطة.
- كل خانة (octet) تحتوي على 8 بت، وتقدر تحمل قيمة من 0 إلى 255.
- طول عنوان IP هو 32 بت (8 بت * 4 خانات).
- يحتوي على **Network Address** (عنوان الشبكة) و**Host Address** (عنوان الجهاز).

![[Pasted image 20240508103722.png]]

## Subnet Mask
- بيكون مرافق لعنوان IP ويكمله، ويستخدم للتفريق بين **Network Address** و**Host Address**.
- الجزء اللي يحتوي على 255 يمثل **Network Address**، بينما الجزء اللي يحتوي على 0 يمثل **Host Address**.

![[Pasted image 20240508103953.png]]
## IP classes
- تم تقسيم عناوين IP إلى عدة **Classes**، وكل Class له استخدام معين.
- نقدر نعرف عنوان IP تابع لأي Class من خلال قيمة أول octet.

![[Pasted image 20240508104541.png]]
## Localhost
- يشير إلى الجهاز اللي بتستخدمه حاليًا.
- بيمكن جهازك إنه يتكلم مع نفسه عن طريق **loopback**.
- دا بيساعد في أغراض الاختبار، بحيث تقدر تشغل برامج أو خدمات على جهازك بدون الحاجة للاتصال بالإنترنت الخارجي.

Here's a breakdown of how it works:
- **Local:** This refers to your own computer.
- **Host:** In networking terms, a host is a device that can communicate on a network. So, "localhost" literally means "local host" - your own computer as the host.
## Loopback address
- عنوان يمكن الجهاز من التواصل مع نفسه عبر IP `127.0.0.1`.
- دا بيسمح بتشغيل خدمة شبكة على الجهاز بدون الحاجة لاتصال فعلي بالشبكة، أو بدون جعل الخدمة متاحة من الشبكات الأخرى.
- عندما تستخدم "localhost"، البيانات بتخرج من الـ network interface وترجع تاني لجهازك.

![[Pasted image 20240508104605.png]]
**Hostname:** You can also use "localhost" as a hostname in a web address, like `http://localhost.` This tells your web browser to connect to the web server running on your own computer, rather than going out to the internet. 
This is commonly used by web developers to test websites they're creating.
## توزيع عناوين IP
عند توزيع IPs على الأجهزة في الشبكة، بنتجنب استخدام الرقمين 0 و255.
	- 0 بيعبر عن Network Address يعني لو عايز أشاور على كل الأجهزة اللي في الشبكة بعبر عنها بIP address `192.168.1.0`
	- 255 بيعبر عن Broadcast Address يعني لو عايز ابعت حاجة لكل الأجهزة بستخدم `192.168.1.255`

![[Pasted image 20240508105239.png]]
## Types of IP
### Public IP address
- يتم تعيينه من قبل مزود خدمة الإنترنت Internet service provider (مثل شركة We)، ويكون له وصول فعلي للإنترنت.
- عنوان IP عام يكون فريدًا عالميًا، ولا يمكن تكراره لجهازين مختلفين.
### Private IP address
- يتم تعيينه من الراوتر عبر خدمة DHCP، ويستخدم داخل الشبكة المنزلية أو المحلية.
- مبيبقاش ليها وصول فعلي للإنترنت وعشان تستخدم الانترنت لازم تستخدم ال Public 
- ليس له وصول فعلي للإنترنت، وللتواصل مع الإنترنت يتم تحويله إلى Public IP بواسطة تقنية **NAT (Network Address Translation)**.

![[Pasted image 20240508112014.png]]![[Pasted image 20240508112032.png]]

### IPv4 and IPv6
- الـ**IPv4**: يتكون من 32 بت ويستخدم بشكل شائع حاليًا، لكنه قد يواجه مشكلة في توزيع العناوين على مستوى العالم بسبب الحد الأقصى للعناوين المتاحة (حوالي 4 مليار).
- عملوا حل مؤقت وهو حوار ال Private IP دا بس زي ما قولت هو مؤقت وفكروا في حل تاني 
- الـ**IPv6**: تم تصميمه ليكون بديلًا لـ IPv4 ويتكون من 128 بت، مما يوفر عددًا ضخمًا من العناوين (يستخدم 8 مجموعات).
- بالرغم من ذلك، ما زال معظم الشغل يعتمد على IPv4.

![[Pasted image 20240508112321.png]]