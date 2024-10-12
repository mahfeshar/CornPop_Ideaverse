---
up:
  - "[[Programming MOC]]"
related: 
created: 2024-10-12
---
- هي فانكشن بتنادي على نفسها

![[Recursion.pdf]]

- زيها زي الـ Loops لازم حاجة توقف التكرار اللي بيحصل
### **Fibonacci Series**

The following example generates the Fibonacci series for a given number using a recursive function
```c
#include <stdio.h>

int fibonacci(int i) {

   if(i == 0) {
      return 0;
   }
	
   if(i == 1) {
      return 1;
   }
   return fibonacci(i-1) + fibonacci(i-2);
}

int  main() {

   int i;
	
   for (i = 0; i < 10; i++) {
      printf("%d\t\n", fibonacci(i));
   }
	
   return 0;
}
0	
1	
1	
2	
3	
5	
8	
13	
21	
34
```