# 仅使用 2 个指针迭代反向链接列表（一种有趣的方法）

给定指向链表头节点的指针，任务是反转链表。

例子：

```
Input : Head of following linked list  
       1->2->3->4->NULL
Output : Linked list should be changed to,
       4->3->2->1->NULL

Input : Head of following linked list  
       1->2->3->4->5->NULL
Output : Linked list should be changed to,
       5->4->3->2->1->NULL

```

在文章[反向链接列表](https://www.geeksforgeeks.org/write-a-function-to-reverse-the-nodes-of-a-linked-list/)中，我们已经看到了如何反向链接列表。 在**迭代方法**中，我们使用了 3 个指针 **prev，cur** 和 **next** 。 下面是一种仅使用两个指针的有趣方法。 这个想法是使用 XOR 交换指针。

## C / C++

```cpp

// C++ program to reverse a linked list using two pointers. 
#include <bits/stdc++.h> 
using namespace std; 
typedef uintptr_t ut; 

/* Link list node */
struct Node { 
    int data; 
    struct Node* next; 
}; 

/* Function to reverse the linked list using 2 pointers */
void reverse(struct Node** head_ref) 
{ 
    struct Node* prev = NULL; 
    struct Node* current = *head_ref; 

    // at last prev points to new head 
    while (current != NULL) { 
        // This expression evaluates from left to right 
        // current->next = prev, changes the link fron 
        // next to prev node 
        // prev = current, moves prev to current node for 
        // next reversal of node 
        // This example of list will clear it more 1->2->3->4 
        // initially prev = 1, current = 2 
        // Final expression will be current = 1^2^3^2^1, 
        // as we know that bitwise XOR of two same 
        // numbers will always be 0 i.e; 1^1 = 2^2 = 0 
        // After the evaluation of expression current = 3 that 
        // means it has been moved by one node from its 
        // previous position 
        current = (struct Node*)((ut)prev ^ (ut)current ^ (ut)(current->next) ^ (ut)(current->next = prev) ^ (ut)(prev = current)); 
    } 

    *head_ref = prev; 
} 

/* Function to push a node */
void push(struct Node** head_ref, int new_data) 
{ 
    /* allocate node */
    struct Node* new_node = (struct Node*)malloc(sizeof(struct Node)); 

    /* put in the data  */
    new_node->data = new_data; 

    /* link the old list off the new node */
    new_node->next = (*head_ref); 

    /* move the head to point to the new node */
    (*head_ref) = new_node; 
} 

/* Function to print linked list */
void printList(struct Node* head) 
{ 
    struct Node* temp = head; 
    while (temp != NULL) { 
        printf("%d  ", temp->data); 
        temp = temp->next; 
    } 
} 

/* Driver program to test above function*/
int main() 
{ 
    /* Start with the empty list */
    struct Node* head = NULL; 

    push(&head, 20); 
    push(&head, 4); 
    push(&head, 15); 
    push(&head, 85); 

    printf("Given linked list\n"); 
    printList(head); 
    reverse(&head); 
    printf("\nReversed Linked list \n"); 
    printList(head); 
    return 0; 
} 

```

## 蟒蛇

```

# Iteratively Reverse a linked list using only 2 pointers (An Interesting Method) 
# Python program to reverse a linked list  
# Link list node   
# node class  
class node: 

    # Constructor to initialize the node object 
    def __init__(self, data): 
        self.data = data 
        self.next = None

class LinkedList: 

    # Function to initialize head 
    def __init__(self): 
        self.head = None

    # Function to reverse the linked list 
    def reverse(self): 
        prev = None
        current = self.head 
    # Described here https://www.geeksforgeeks.org/ 
    # how-to-swap-two-variables-in-one-line / while(current is not None): 
            # This expression evaluates from left to right 
            # current->next = prev, changes the link fron 
            # next to prev node 
            # prev = current, moves prev to current node for 
            # next reversal of node 
            # This example of list will clear it more 1->2 
            # initially prev = 1, current = 2 
            # Final expression will be current = 1, prev = 2 
            next, current.next = current.next, prev 
            prev, current = current, next
        self.head = prev 

    # Function to push a new node  
    def push(self, new_data): 
        # allocate node and put in the data 
        new_node = node(new_data) 
        # link the old list off the new node 
        new_node.next = self.head 
        # move the head to point to the new node 
        self.head = new_node 

    # Function to print the linked list 
    def printList(self): 
        temp = self.head 
        while(temp): 
            print temp.data, 
            temp = temp.next

# Driver program to test above functions 
llist = LinkedList() 
llist.push(20) 
llist.push(4) 
llist.push(15) 
llist.push(85) 

print "Given Linked List"
llist.printList() 
llist.reverse() 
print "\nReversed Linked List"
llist.printList() 

# This code is contributed by Afzal Ansari 

```

**Output:**

```
Given linked list
85  15  4  20  
Reversed Linked list 
20  4  15  85

```

时间复杂度：O（n）

<u>**参考：**</u>

[http://discuss.joelonsoftware.com/default.asp?interview.11.564944.16](http://discuss.joelonsoftware.com/default.asp?interview.11.564944.16)

 **替代解决方案：**

## C++

```cpp

// C++ program to reverse a linked list using two pointers. 
#include <bits/stdc++.h> 
using namespace std; 
typedef uintptr_t ut; 

/* Link list node */
struct Node { 
    int data; 
    struct Node* next; 
}; 

/* Function to reverse the linked list using 2 pointers */
void reverse(struct Node** head_ref) 
{ 
    struct Node* current = *head_ref; 
    struct Node* next; 
    while (current->next != NULL) { 
        next = current->next; 
        current->next = next->next; 
        next->next = (*head_ref); 
        *head_ref = next; 
    } 
} 

/* Function to push a node */
void push(struct Node** head_ref, int new_data) 
{ 
    struct Node* new_node = new Node; 
    new_node->data = new_data; 
    new_node->next = (*head_ref); 
    (*head_ref) = new_node; 
} 

/* Function to print linked list */
void printList(struct Node* head) 
{ 
    struct Node* temp = head; 
    while (temp != NULL) { 
        printf("%d  ", temp->data); 
        temp = temp->next; 
    } 
} 

/* Driver program to test above function*/
int main() 
{ 
    /* Start with the empty list */
    struct Node* head = NULL; 

    push(&head, 20); 
    push(&head, 4); 
    push(&head, 15); 
    push(&head, 85); 

    printf("Given linked list\n"); 
    printList(head); 
    reverse(&head); 
    printf("\nReversed Linked list \n"); 
    printList(head); 
    return 0; 
} 

```

## Python3

```py

# Python3 program to reverse a linked list using two pointers. 

# A linked list node  
class Node : 
    def __init__(self): 
        self.data = 0
        self.next = None

# Function to reverse the linked list using 2 pointers  
def reverse(head_ref): 

    current = head_ref 
    next= None
    while (current.next != None) : 
        next = current.next
        current.next = next.next
        next.next = (head_ref) 
        head_ref = next

    return head_ref 

# Function to push a node  
def push( head_ref, new_data): 

    new_node = Node() 
    new_node.data = new_data 
    new_node.next = (head_ref) 
    (head_ref) = new_node 
    return head_ref 

# Function to print linked list  
def printList( head): 

    temp = head 
    while (temp != None) : 
        print( temp.data, end=" ") 
        temp = temp.next

# Driver code 

# Start with the empty list  
head = None

head = push(head, 20) 
head = push(head, 4) 
head = push(head, 15) 
head = push(head, 85) 

print("Given linked list") 
printList(head) 
head = reverse(head) 
print("\nReversed Linked list ") 
printList(head) 

# This code is contributed by Arnab Kundu 

```

**Output:**

```
Given linked list
85  15  4  20  
Reversed Linked list 
20  4  15  85

```

感谢 **Abhay Yadav** 提出了这种方法。

本文由 **[Shashank Mishra（Gullu）](https://www.facebook.com/shashank.mishra.92167)** 贡献。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请发表评论。

