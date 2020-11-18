# 使用递归

删除链接列表

使用递归删除给定的链表

**方法**
1）如果head等于NULL，则链表为空，我们简单地返回。
2）递归删除头节点之后的链表。
3）删除头节点。

## C++

```cpp

// C++ program to recursively delete a linked list 
#include <bits/stdc++.h> 

/* Link list node */
struct Node { 
    int data; 
    struct Node* next; 
}; 

/* Recursive Function to delete the entire linked list */
void deleteList(struct Node* head) 
{ 
    if (head == NULL) 
        return; 
    deleteList(head->next);  
    free(head); 
} 

/* Given a reference (pointer to pointer) to  
   the head of a list and an int, push a new 
   node on the front of the list. */
void push(struct Node** head_ref, int new_data) 
{ 
    struct Node* new_node = new Node; 
    new_node->data = new_data; 
    new_node->next = (*head_ref); 
    (*head_ref) = new_node; 
} 

/* Driver program to test count function*/
int main() 
{ 
    /* Start with the empty list */
    struct Node* head = NULL; 

    /* Use push() to construct below list 
    1->12->1->4->1 */
    push(&head, 1); 
    push(&head, 4); 
    push(&head, 1); 
    push(&head, 12); 
    push(&head, 1); 
    printf("\n Deleting linked list"); 
    deleteList(head); 
    printf("\nLinked list deleted"); 
    return 0; 
} 

```

## Java

```java

// Java program to recursively delete a linked list 
class GFG  
{ 

/* Link list node */
static class Node  
{ 
    int data; 
    Node next; 
}; 

/* Recursive Function to delete 
the entire linked list */
static void deleteList(Node head) 
{ 
    if (head == null) 
        return; 
    deleteList(head.next);  
    System.gc(); 
} 

/* Given a reference (pointer to pointer) to  
the head of a list and an int, push a new 
node on the front of the list. */
static void push(Node head_ref, int new_data) 
{ 
    Node new_node = new Node(); 
    new_node.data = new_data; 
    new_node.next = head_ref; 
    head_ref = new_node; 
} 

/* Driver code*/
public static void main(String[] args)  
{ 
    /* Start with the empty list */
    Node head = new Node(); 

    /* Use push() to conbelow list 
    1->12->1->4->1 */
    push(head, 1); 
    push(head, 4); 
    push(head, 1); 
    push(head, 12); 
    push(head, 1); 
    System.out.print("\nDeleting linked list"); 
    deleteList(head); 
    System.out.print("\nLinked list deleted"); 
} 
} 

/* This code contributed by PrinciRaj1992 */

```

## Python3

```py

# Python3 program to recursively delete  
# a linked list 
import math 

# Link list node  
class Node:  
    def __init__(self, data):  
        self.data = data  
        self.next = None

# Recursive Function to delete 
# the entire linked list  
def deleteList(head): 
    if (head == None): 
        return
    deleteList(head.next)  
    # free(head) 

# Given a reference (pointer to pointer) to the head  
# of a list and an int, head=push a new node  
# on the front of the list.  
def push(head_ref, new_data): 
    new_node = Node(new_data) 
    new_node.data = new_data 
    new_node.next = head_ref 
    head_ref = new_node 
    return head_ref 

# Driver Code 
if __name__=='__main__': 

    # Start with the empty list  
    head = None

    # Use head=push() to construct below list 1.12.1.4.1  
    head = push(head, 1) 
    head = push(head, 4) 
    head = push(head, 1) 
    head = push(head, 12) 
    head = push(head, 1) 
    print("Deleting linked list") 
    deleteList(head) 
    print("Linked list deleted") 

# This code is contributed by Srathore 

```

## C#

```cs

// C# program to recursively delete a linked list 
using System; 

class GFG  
{ 

/* Link list node */
public class Node  
{ 
    public int data; 
    public Node next; 
}; 

/* Recursive Function to delete 
the entire linked list */
static void deleteList(Node head) 
{ 
    if (head == null) 
        return; 
    deleteList(head.next);  
} 

/* Given a reference (pointer to pointer) to  
the head of a list and an int, push a new 
node on the front of the list. */
static void push(Node head_ref, int new_data) 
{ 
    Node new_node = new Node(); 
    new_node.data = new_data; 
    new_node.next = head_ref; 
    head_ref = new_node; 
} 

/* Driver code*/
public static void Main(String[] args)  
{ 
    /* Start with the empty list */
    Node head = new Node(); 

    /* Use push() to conbelow list 
    1->12->1->4->1 */
    push(head, 1); 
    push(head, 4); 
    push(head, 1); 
    push(head, 12); 
    push(head, 1); 
    Console.Write("\nDeleting linked list"); 
    deleteList(head); 
    Console.Write("\nLinked list deleted"); 
} 
} 

// This code contributed by Rajput-Ji 

```

**输出：**

```
Deleting linked list
Linked list deleted

```



* * *

* * *

如果您喜欢GeeksforGeeks并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至tribution@geeksforgeeks.org。 查看您的文章出现在GeeksforGeeks主页上，并帮助其他Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。