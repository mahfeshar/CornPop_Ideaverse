---
up:
  - "[[Data Structure and Algorithms MOC]]"
related: 
created: 2024-07-15
---

# Using Dynamic Array
- We can use [[Array#Dynamic Arrays|Dynamic Arrays]] to make a stack
- هدفها إن عمليات زي دي تبقا سريعة جدًا

![[Pasted image 20240715144619.png]]

## python
```python
# Implementing a stack is trivial using a dynamic array
# (which we implemented earlier).
class Stack:
    def __init__(self):
        self.stack = []

    def push(self, n):
        self.stack.append(n)

    def pop(self):
        return self.stack.pop()
```
# With C

1. **Statically:** Array implementation of stacks allows the static memory allocation of its data elements. It is important to note that in this method, the stack acquires all the features of an array.
2. **Dynamically:** Linked list implementation of stacks follow the dynamic memory allocation of its data elements. It is important to note that in this method, the stack inherits all the characteristics of a **_[linked list in C](https://data-flair.training/blogs/linked-list-in-c-tutorial/)_.**

## Array Implementation of Stack in C

### Insertion

Operation of insertion an element into the stack is pushing. The elements are inserted from the top.

```c
#define LIMIT 100
void push()
{
	int stack[LIMIT], top, element;
	if (top == LIMIT - 1)
	{
		printf("Stack Overflow\\n");
	}
	else 
	{
		printf("Enter the element: ");
		scanf("%d", &element);
		top++;
		stack[top] = element;
	}
}
```

![[Pasted image 20240201155159.png]]
### Deletion

Operation of deletion is referred to as popping. The deletion is done from the top.

```c
#define LIMIT 100
void pop()
{
	int stack[LIMIT], top, element;
	if(top == -1)
		printf("Stack underflow");
	else
	{
		element = stack[top];
		printf("The deleted item is %d\\n", stack[top]);
		top--;
	}
}
```

![[Pasted image 20240201155234.png]]
### Display

```c
#define LIMIT 100
void display()
{
	int stack[LIMIT], top, i;
	if (top == -1)
	{
		printf("Stack underflow");
	}
	else if (top > 0)
	{
		printf("The elements of the stack are:\\n");
		for (i = top; i >=0; i--)
		{
			printf("%d\\n", stack[i]);
		}
	}
}
```

### Stack overflow

we are talking about the static memory allocation of data elements of a stack. Therefore, if the stack is filled completely, that is, no more elements can be inserted in the stack, then the condition would be called STACK-FULL condition. It is also referred to as stack overflow.

### Stack Underflow

In case we wish to display the data elements of the stack or perform the deletion operation, but no elements have been inserted into the stack yet, this condition is called STACK-EMPTY. It is also referred to as stack underflow.

### Stack with array (Full program)

- Full code
    
    ```c
    #include <stdio.h>
    #include <stdlib.h>
    #define LIMIT 100
    
    /*Global Variables for Stack*/
    int stack[LIMIT]; //ARRAY IMPLEMENTATION of stack
    int top; // To insert and delete data
    int i; //To traverse the loop in displaying
    int choice; // to choose each operation I want to make
    
    void push(); //function to push data
    void pop(); //function to delete data
    void display(); //Function to display all elements
    
    int main()
    {
    	printf ("ARRAY IMPLEMENTATION USING STACKS\\n\\n");
    	top = -1; // Initializing top to -1 indicates that it is empty
    	do
    	{
    		printf("1. Insert\\n2. Delete\\n3. Display\\n4. Exit\\n\\n");
    		printf("Enter your choice:");
    		scanf("%d",&choice);
    		switch(choice)
    		{
    			case 1:
    				push();
    				break;
    			case 2:
    				pop();
    				break;
    			case 3:
    				display();
    				break;
    			case 4:
    				exit(0);
    				break;
    			default:
    				printf("Sorry, invalid choice!\\n");
    				break;
    		}
    	} while(choice!=4);
    	return 0;
    }
    
    void push()
    {
    	int emlement;
    	if (top == LIMIT - 1)
    	{
    		printf("Stack underflow\\n")
    	}
    	else
    	{
    		printf("Enter the element to be inserted:");
    		scanf("%d", &element);
    		top++;
    		stack[top] = element;
    	}
    }
    
    void pop()
    {
    	int element;
    	if(top == -1)
    	{
    		printf("Stack underflow\\n");
    	}
    	else
    	{
    		element=stack[top];
    		printf("The deleted item is %d\\n",stack[top]);
    		top--; // The element below the topmost element is deleted
    	}
    }
    
    void display()
    {
    	if(top == -1)
    	{
    		printf("Stack underflow\\n"); // Stack is empty
    	}
    	else if(top > 0)
    	{
    		printf("The elements of the stack are:\\n");
    		for(i = top; i >= 0; i--) // top to bottom traversal
    		{
    			printf("%d\\n",stack[i]);
    		}
    	}
    }
    ```
    
- Output
    ![[Pasted image 20240202151705.png]]
    ![[Pasted image 20240202151713.png]]
    

---

## Linked List Implementation of Stack in C

### Insertion

```c
void push()
{
	int data;
	struct node *pointer = (struct node*) malloc(sizeof(struct node));
	if (pointer == NULL)
	{
		printf("Stack overflow");
	}
	else
	{
		printf("Enter the element: ");
		scanf("%d", &data);
		if (temp == NULL)
		{
			pointer->data = data;
			pointer->next = NULL;
			temp = pointer;
		}
		else
		{
			pointer->data = data;
			pointer->next = temp;
			temp = pointer;
		}
	}
}
```

### Deletion

```c
void pop()
{
	int item; 
	struct node *pointer;
	if (temp == NULL)
	{
		printf("Stack Underflow");
	}
	else
	{
		item = temp->data;
		pointer = temp;
		temp = temp->next;
		free(pointer);
		printf("The deleted item is %d\\n", item);
	}
}
```

### Display

```c
void display()
{
	int item;
	struct node *pointer;
	pointer = temp;
	if(pointer == NULL)
	{
		printf("Stack underflow\\n");
	}
	else
	{
		printf("The elements: ")
		while (pointer != NULL)
		{
			printf("%d\\n", pointer->data;
			pointer = pointer->next;
		}
	}
}
```

### Stack with Linked List (Full program)

- Full code
    
    ```c
    #include <stdio.h>
    #include <stdlib.h>
    void push(); // Function used to insert the element into the stack
    void pop(); // Function used to delete the elememt from the stack
    void display(); // Function used to display all the elements in the stack according to LIFO rule
    struct node
    {
        int data;
        struct node *next;
    };
    struct node *temp;
    int main()
    {
        printf("Welcome to DataFlair tutorials!\\n\\n");
        int choice;
        printf ("LINKED LIST IMPLEMENTATION USING STACKS\\n\\n");
        do
        {
            printf("1. Insert\\n2. Delete\\n3. Display\\n4. Exit\\n\\n");
            printf("Enter your choice:");
            scanf("%d",&choice);
            switch(choice)
            {
                case 1:
                    push();
                    break;
                case 2:
                    pop();
                    break;
                case 3:
                    display();
                    break;
                case 4:
                    exit(0);
                    break;
                default:
                    printf("Sorry, invalid choice!\\n");
                    break;
            }
        } while(choice!=4);
        return 0;
    }
    void push ()
    {
        int data;
        struct node *pointer = (struct node*)malloc(sizeof(struct node));
        if(pointer == NULL)
        {
            printf("Stack overflow");
        }
        else
        {
            printf("Enter the element to be inserted: ");
            scanf("%d",&data);
            if(temp == NULL)
            {
                pointer -> data = data;
                pointer -> next = NULL;
                temp = pointer;
            }
            else
            {
                pointer -> data = data;
                pointer -> next = temp;
                temp = pointer;
            }
        }
    }
    void pop()
    {
        int item;
        struct node *pointer;
        if (temp == NULL)
        {
            printf("Stack Underflow\\n");
        }
        else
        {
            item = temp -> data;
            pointer = temp;
            temp = temp -> next;
            free(pointer);
            printf("The deleted item is %d\\n",item);
        }
    }
    void display()
    {
        int i;
        struct node *pointer;
        pointer = temp;
        if(pointer == NULL)
        {
            printf("Stack underflow\\n");
        }
        else {
            printf("The elements of the stack are:\\n");
            while (pointer != NULL) {
                printf("%d\\n", pointer->data);
                pointer = pointer->next;
            }
        }
    }
    ```
    
- Output
    ![[Pasted image 20240201155320.png]]
    ![[Pasted image 20240201155338.png]]
    
---

## Application of Stack in C

- **Number reversal:** A stack helps you reverse a number or a word entered as a sequence of digits or characters respectively.
- **Undo operation:** Implementation of a stack helps you perform the “undo” operation in text editors or word processors. Here, all the changes done in the text editor are stored in a stack.
- **Infix to postfix conversion:** Using stacks, you can perform the conversion of an infix expression to a postfix expression.
- **Backtracking:** Stacks are finding applications in puzzle or maze problem-solving.
- **Depth-first search (DFS):** Stacks allow you to perform a searching algorithm called the depth-first search.