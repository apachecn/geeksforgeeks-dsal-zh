# 重新排列链接列表以替换第一个和最后一个元素

给定一个链表。 以交替的第一个和最后一个元素的方式排列链接列表。

例子：

```
Input : 1->2->3->4->5->6->7->8
Output :1->8->2->7->3->6->4->5

Input :10->11->15->13
Output :10->13->11->15

```

我们在[中讨论了三种不同的解决方案，就地重新排列给定的链表。](https://www.geeksforgeeks.org/rearrange-a-given-linked-list-in-place/)

在这篇文章中，讨论了一个不同的基于 [Deque](https://www.geeksforgeeks.org/deque-set-1-introduction-applications/) 的解决方案。

**方法**

1）创建一个空双端队列

2）将链接列表中的所有元素插入到双端队列

3）将元素从双端队列重新插入到链表中 首先，然后最后，依此类推

## C++

```cpp

// CPP program to rearrange a linked list in given manner 
#include <bits/stdc++.h> 
using namespace std; 

/* Link list node */
struct Node { 
    int data; 
    struct Node* next; 
}; 

/* Function to reverse the linked list */
void arrange(struct Node* head) 
{ 
    struct Node* temp = head; 
    deque<int> d; // defining a deque 

    // push all the elements of linked list in to deque 
    while (temp != NULL) { 
        d.push_back(temp->data); 
        temp = temp->next; 
    } 

    // Alternatively push the first and last elements 
    // from deque to back to the linked list and pop 
    int i = 0; 
    temp = head; 
    while (!d.empty()) { 
        if (i % 2 == 0) { 
            temp->data = d.front(); 
            d.pop_front(); 
        } 
        else { 
            temp->data = d.back();  
            d.pop_back();  
        } 
        i++; 
        temp = temp->next; // increase temp 
    } 
} 

/*UTILITY FUNCTIONS*/
/* Push a node to linked list. Note that this function 
changes the head */
void push(struct Node** head_ref, char new_data) 
{ 
    /* allocate node */
    struct Node* new_node = (struct Node*)malloc(sizeof(struct Node)); 

    /* put in the data */
    new_node->data = new_data; 

    /* link the old list off the new node */
    new_node->next = (*head_ref); 

    /* move the head to pochar to the new node */
    (*head_ref) = new_node; 
} 

// printing the linked list 
void printList(struct Node* head) 
{ 
    struct Node* temp = head; 
    while (temp != NULL) { 
        printf("%d  ", temp->data); 
        temp = temp->next; 
    } 
} 

/* Drier program to test above function*/
int main() 
{ 
    // Let us create linked list 1->2->3->4 
    struct Node* head = NULL; 

    push(&head, 5); 
    push(&head, 4); 
    push(&head, 3); 
    push(&head, 2); 
    push(&head, 1); 
    cout << "Given linked list\t"; 
    printList(head); 
    arrange(head); 
    cout << "\nAfter rearrangement\t"; 
    printList(head); 
    return 0; 
} 

```

## Java

```java

// Java program to rearrange a linked list in given manner 
import java.util.*; 
import java.lang.*; 
import java.io.*; 

class GFG 
{ 
    /* Link list node */
    static class Node  
    {  
        int data;  
        Node next; 
        Node(int data) 
        { 
            this.data = data; 
            next = null; 
        } 
    } 

    // printing the linked list  
    static void printList(Node head)  
    {  
        Node temp = head;  
        while (temp != null)  
        {  
            System.out.print(temp.data + " ");  
            temp = temp.next;  
        }  
    } 

    /* Function to reverse the linked list */
    static void arrange(Node head) 
    { 
        // defining a deque 
        Deque<Integer> deque = new ArrayDeque<>(); 
        Node temp = head; 

        // push all the elements of linked list in to deque 
        while(temp != null) 
        { 
            deque.addLast(temp.data); 
            temp = temp.next; 
        } 
        temp = head; 
        int i = 0; 

        // Alternatively push the first and last elements 
        // from deque to back to the linked list and pop 
        while(!deque.isEmpty()) 
        { 
            if(i % 2 == 0) 
            { 
                temp.data = deque.removeFirst(); 
            } 
            else
            { 
                temp.data = deque.removeLast(); 
            } 
            i++; 
            temp = temp.next; 
        } 
    } 

    // Driver code 
    public static void main (String[] args) 
    { 
        // Let us create linked list 1->2->3->4->5 
        Node head = null;  

        head = new Node(1); 
        head.next = new Node(2); 
        head.next.next = new Node(3); 
        head.next.next.next = new Node(4); 
        head.next.next.next.next = new Node(5); 

        System.out.println("Given linked list");  
        printList(head);  
        arrange(head);  
        System.out.println("\nAfter rearrangement"); 
        printList(head); 
    } 
} 

// This code is contributed by nobody_cares. 

```

## 蟒蛇

```

# Python program to rearrange  
# a linked list in given manner 

# Link list node  
class Node:  

    def __init__(self, data):  
        self.data = data  
        self.next = None

# Function to reverse the linked list  
def arrange( head): 

    temp = head 

    # defining a deque 
    d = [] 

    # push all the elements of linked list in to deque 
    while (temp != None) : 
        d.append(temp.data) 
        temp = temp.next

    # Alternatively push the first and last elements 
    # from deque to back to the linked list and pop 
    i = 0
    temp = head 
    while (len(d) > 0) : 
        if (i % 2 == 0) : 
            temp.data = d[0] 
            d.pop(0) 

        else : 
            temp.data = d[-1]  
            d.pop()  

        i = i + 1

        # increase temp 
        temp = temp.next

    return head 

# UTILITY FUNCTIONS 
# Push a node to linked list. Note that this function 
# changes the head  
def push( head_ref, new_data): 

    # allocate node  
    new_node = Node(0) 

    # put in the data  
    new_node.data = new_data 

    # link the old list off the new node  
    new_node.next = (head_ref) 

    # move the head to pochar to the new node  
    (head_ref) = new_node 
    return head_ref 

# printing the linked list 
def printList( head): 

    temp = head 
    while (temp != None) : 
        print( temp.data,end=" ") 
        temp = temp.next

# Driver program to test above function 

# Let us create linked list 1.2.3.4 
head = None

head = push(head, 5) 
head = push(head, 4) 
head = push(head, 3) 
head = push(head, 2) 
head = push(head, 1) 
print("Given linked list\t") 
printList(head) 
head = arrange(head) 
print( "\nAfter rearrangement\t") 
printList(head) 

# This code is contributed by Arnab Kundu 

```

**输出**：

```
Given linked list    1 2 3 4 5 
After rearrangement    1 5 2 4 3

```

**时间复杂度**：`O(n)`



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。