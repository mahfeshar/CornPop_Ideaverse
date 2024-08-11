---
up:
  - "[[Data Structure and Algorithms MOC]]"
related: 
created: 2024-08-04
---

- هي قريبة من الـ Arrays بس مع اختلافات كتير بس هي نفس الفكرة
- أول حاجة لازم تعرفها إنها بتتكون من List of Nodes
- الـ node عبارة عن Object بيبقا جواه حاجتين (عالأقل) وهما الـ Value (ودي ممكن تبقا أي حاجة حرفيًا) والحاجة التانية اللي هي Next ودي عبارة عن Pointer بتشاور على العنصر اللي جاي في الـ linked list
- مش بيفرق ترتيب الـ Linked list في الـ Memory (ممكن حرفيًا تبقا مترتبة بالعكس)
  ودا الفرق بين الـ linked list والـ [[Array]] لأن الـ Array لازم تبقا مترتبة في الـ Memory

## شرح الفكرة
1. نفترض إني عندي مثلًا 3 Nodes بيعبروا عن الألوان
2. هنحط القيم بتاع الألوان في أي مكان في الـ Memory حرفيًا ومهم أبقا عارف الـ Address بتاعه
3. هنحط قيمة كل Next بالقيمة التالية في الـ List بتاعي (Pointer بيشاور على عنوان الـ Node الجاية) وهكذا
   لما بنتكلم عن الـ Pointers بنتكلم عن الـ reference بتاع الحاجة دي في الـ Memory

![[Pasted image 20240804221542.png]]

## Iterate through
- بكل بساطة هبدأ بالـ Node الأولى وأفضل أتحرك لحد ما يبقا الـ current بتاعي بيساوي Null
- هتاخد **O(n)** ودا زي الـ Array

![[Pasted image 20240805233758.png]]

## Add to the end
- في الغالب بيبقا عندي اتنين Pointer واحد اسمه Tail (بيشاور على آخر عنصر) والـ Head (بيشاور على الأول)
	- لو الإتنين على أول عنصر او بيساووا بعض دا معناه ان الـ list بتاعي عنصر واحد
- لو عايز أضيف عنصر في الآخر بعمل الآتي:
	- أحط الـ next بتاع الـ tail (آخر عنصر) بالـ Node الجديدة 
	  بس كدا لسا الـ Tail بيشاور على العنصر القديم وأنا عايزة يشاور على آخر عنصر
	- أخلي الـ Tail بيشاور على الـ Node الجديدة
- دا بيخلي الإضافة دي تاخد **O(1)** ودا أحسن بكتير من إني أعدي على كل عنصر من الأول
  ودا زي الـ Array بالظبط

![[Pasted image 20240805234507.png]]

## Remove a node
- سواء في الأول أو في الأخر
- بتبقا **O(1)**
  ودي ميزة عن الـ [[Array]] لأني لو عايز أمسح فالـ Array لازم أعمل shift لكل اللي قبله
  هتبقا **O(n)** لو اضطريت ادور على العنصر عشان أمسحه (يعني لو مش فالأول أو فالآخر)
- لازم يبقا معايا pointer على الـ Node اللي قبل العنصر اللي بمسحه
- بدل ما بخلي العنصر اللي قبله يبص عليه بخلي العنصر اللي قبله يشاور على العنصر اللي بعده 
- بمعنى إن العنصر بتاعي بيبقا مبتعرفش توصله بأي طريقة فيعتبر مش موجود ومع الوقت الـ Garbage collector بيلمه

![[Pasted image 20240805235243.png]]

## Code
### Python
```python
class ListNode:
    def __init__(self, val):
        self.val = val
        self.next = None

# Implementation for Singly Linked List
class LinkedList:
    def __init__(self):
        # Init the list with a 'dummy' node which makes 
        # removing a node from the beginning of list easier.
        self.head = ListNode(-1)
        self.tail = self.head
    
    def insertEnd(self, val):
        self.tail.next = ListNode(val)
        self.tail = self.tail.next

    def remove(self, index):
        i = 0
        curr = self.head
        while i < index and curr:
            i += 1
            curr = curr.next
        
        # Remove the node ahead of curr
        if curr:
            curr.next = curr.next.next

    def print(self):
        curr = self.head.next
        while curr:
            print(curr.val, ' -> ')
            curr = curr.next
        print()
```

### C++
```cpp
#include <iostream>

using std::cout;
using std::endl;

class ListNode {
public:
    int val_;
    ListNode* next = nullptr;

    ListNode(int val) {
        val_ = val;
    }
};

// Implementation for Singly Linked List
class LinkedList {
public:
    ListNode* head;
    ListNode* tail;

    LinkedList() {
        // Init the list with a 'dummy' node which makes 
        // removing a node from the beginning of list easier.
        head = new ListNode(-1);
        tail = head;
    }

    void insertEnd(int val) {
        tail->next = new ListNode(val);
        tail = tail->next;
    }

    void remove(int index) {
        int i = 0;
        ListNode* curr = head;
        while (i < index && curr) {
            i++;
            curr = curr->next;
        }
        
        // Remove the node ahead of curr
        if (curr) {
            curr->next = curr->next->next;
        }
    }

    void print() {
        ListNode* curr = head->next;
        while (curr) {
            cout << curr->val_ << " -> ";
            curr = curr->next;
        }
        cout << endl;
    }
};   
```