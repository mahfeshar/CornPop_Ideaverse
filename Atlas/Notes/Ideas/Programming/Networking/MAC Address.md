---
up:
  - "[[Networking Fundamentals]]"
related: 
created: 2024-07-21
---

## NIC (Network Interface Card)
- Hardware component (internal - external)
- We use it to make network between devices (بيخلي الجهاز يتوصل بالنتورك)
- It's move us from data link layer to physical layer because it's translate machine languages to signals
![[Pasted image 20240508115215.png]]
- It can be wired and wireless.
- أمثلة: زي البلوتوث أو الوايفاي أو يبقا وايرد
## MAC Address
- It's a physical address written by hexadecimal
- It have 6 octet and every octet = 8bit so it's length is 48bit
- First 3 octet for vendor or company that made this NIC
- Second 3 octet is unique numbers
![[Pasted image 20240508121626.png]]
## How to know my MAC address
### Windows
network and sharing center -> your connection -> details -> physical address
CMD -> getmac