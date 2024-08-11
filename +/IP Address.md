## Intro to IP Address
- الجهاز بتاعك لازم يبقا له عنوان عشان يتواصل مع باقي الأجهزة في الانترنت
- It's the identity of each [[Host]]
- IP (Internet Protocol): Sets of rules اللي عايز يتواصل لازم يمشي عليها
- To know your IP (CMD -> ipconfig)
## IP Address Structure
- مكون من أربع خانات وبيفصل بينهم dot
- كل خانة اسمها **octet** وكل octet بيبقا 8bit وبيشيل رقم من 0 ل 255
- Length of IP = 8 * 4 = 32bit
- بيحتوي على Network Address and Host Address الرقم الخاص بالشبكة (عنوانه) والجهاز
![[Pasted image 20240508103722.png]]

## Subnet Mask
- بيكون ملازم لل IP ومكمل له وبستخدمه عشان أفرق بين ال Network and Host address
- الجزء اللي فوق 255 بيعبر عن ال Network Address والجزء اللي فوق 0 بيعبر عن ال Host Address
![[Pasted image 20240508103953.png]]
## IP classes
- تم تقسيم ال IP addresses لمجموعة من ال classes وكل class له استخدام معين
- بنقدر نعرف ال IP تبع أي class عن طريق أول octet
![[Pasted image 20240508104541.png]]
### Localhost
- It refers to the computer you're currently using.
- It's a way for your device to talk to itself, creating a loopback.
- This is useful for testing purposes, so you can access programs or services running on your machine without going out to the wider internet.

Here's a breakdown of how it works:

- **Local:** This refers to your own computer.
- **Host:** In networking terms, a host is a device that can communicate on a network. So, "localhost" literally means "local host" - your own computer as the host.
### Loopback address
- بيقدر يكلم نفسه عن طريق ال IP address دا `127.0.0.1`
- The local loopback mechanism may be used to run a network service on a host without requiring a physical network interface, or without making the service accessible from the networks the computer may be connected to.
- When you try to access something using localhost, the data goes out of your network interface and loops back in, all within your own machine.
![[Pasted image 20240508104605.png]]
**Hostname:** You can also use "localhost" as a hostname in a web address, like `http://localhost.` This tells your web browser to connect to the web server running on your own computer, rather than going out to the internet. This is commonly used by web developers to test websites they're creating.
## Giving IP
- لو جينا نوزع IPs على الأجهزة في الشبكة فهنبعد عن رقمين 0 و 255
	- 0 بيعبر عن Network Address يعني لو عايز أشاور على كل الأجهزة اللي في الشبكة بعبر عنها بIP address `192.168.1.0`
	- 255 بيعبر عن Broadcast Address يعني لو عايز ابعت حاجة لكل الأجهزة بستخدم `192.168.1.255`
![[Pasted image 20240508105239.png]]
## Types of IP
### Public IP address
- بناخده من ال Internet service provider ودا اللي بيبقا له الوصول الفعلي للإنترنت
  شركة We بتدي IP للراوتر بتاعك
- A public IP address is globally unique, and can only be assigned to a unique device.
### Private IP address
- فيه في الراوتر حاجة اسمها DHCP Service ودي اللي بتدي الأجهزة في البيت private IPs
- مبيبقاش ليها وصول فعلي للإنترنت وعشان تستخدم الانترنت لازم تستخدم ال Public 
- فلما بيحتاج يتوصل بالنت الprivate بيتترجم لل public واللي بيعمل العملية دي ال NAT (Network Address Translation)
![[Pasted image 20240508112014.png]]![[Pasted image 20240508112032.png]]

### IPv4 and IPv6
- IPv4: دا اللي بيستخدم في العادي ودا اللي هو حجمه 32 بت
- هيعملي مشكلة اني هوصل لمستوى معين مش هقدر أوزع IP لكل الأجهزة لأنه ممكن يعملي 4 مليار بس
- عملوا حل مؤقت وهو حوار ال Private IP دا بس زي ما قولت هو مؤقت وفكروا في حل تاني 
- ال IPv6: عبارة عن 128 bit وبيبقا عبارة عن 8 مجموعات
- ما زال معظم الشغل على ال IPv4
![[Pasted image 20240508112321.png]]