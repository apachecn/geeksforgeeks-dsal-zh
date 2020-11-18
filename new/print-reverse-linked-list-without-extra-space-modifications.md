# 无需额外的空间和修改即可反向打印链接列表

给定[链接列表](https://www.geeksforgeeks.org/data-structures/linked-list/)，以反向方式显示链接列表，而无需使用递归，堆栈或对给定列表的修改。

**示例：**

```
Input : 1->2->3->4->5->NULL
Output :5->4->3->2->1->NULL

Input :10->5->15->20->24->NULL
Output :24->20->15->5->10->NULL

```

下面是现在允许在此处使用的不同解决方案，因为我们不能使用额外的空间并修改列表。

1）[递归解决方案，以打印反向链接列表](https://www.geeksforgeeks.org/write-a-recursive-function-to-print-reverse-of-a-linked-list/)。 需要额外的空间。

2）[反向链接列表](https://www.geeksforgeeks.org/reverse-a-linked-list/)，然后打印。 这需要修改原始列表。

3）[基于堆栈的解决方案，用于打印反向链接列表](https://www.geeksforgeeks.org/print-reverse-linked-list-using-stack/)。 将所有节点一个一个地推入堆栈。 然后从堆栈中逐一弹出元素并进行打印。 这也需要额外的空间。

算法：

```
1) Find n = count nodes in linked list.
2) For i = n to 1, do following.
    Print i-th node using get n-th node function
```

## C++

```cpp

// C/C++ program to print reverse of linked list 
// without extra space and without modifications. 
#include<stdio.h> 
#include<stdlib.h> 

/* Link list node */
struct Node 
{ 
    int data; 
    struct Node* next; 
}; 

/* Given a reference (pointer to pointer) to the head 
  of a list and an int, push a new node on the front 
  of the list. */
void push(struct Node** head_ref, int new_data) 
{ 
    struct Node* new_node = 
            (struct Node*) malloc(sizeof(struct Node)); 
    new_node->data  = new_data; 
    new_node->next = (*head_ref); 
    (*head_ref)    = new_node; 
} 

/* Counts no. of nodes in linked list */
int getCount(struct Node* head) 
{ 
    int count = 0;  // Initialize count 
    struct Node* current = head;  // Initialize current 
    while (current != NULL) 
    { 
        count++; 
        current = current->next; 
    } 
    return count; 
} 

/* Takes head pointer of the linked list and index 
    as arguments and return data at index*/
int getNth(struct Node* head, int n) 
{ 
    struct Node* curr = head; 
    for (int i=0; i<n-1 && curr != NULL; i++) 
       curr = curr->next; 
    return curr->data; 
} 

void printReverse(Node *head) 
{ 
    // Count nodes 
    int n = getCount(head); 

    for (int i=n; i>=1; i--) 
        printf("%d ", getNth(head, i)); 
} 

/* Driver program to test count function*/
int main() 
{ 
    /* Start with the empty list */
    struct Node* head = NULL; 

    /* Use push() to construct below list 
     1->2->3->4->5 */
    push(&head, 5); 
    push(&head, 4); 
    push(&head, 3); 
    push(&head, 2); 
    push(&head, 1); 

    printReverse(head); 

    return 0; 
} 

```

## Java

```java

// Java program to print reverse of linked list 
// without extra space and without modifications. 
class GFG  
{ 

/* Link list node */
static class Node 
{ 
    int data; 
    Node next; 
}; 
static Node head; 

/* Given a reference (pointer to pointer) to  
the head of a list and an int, push a new node  
on the front of the list. */
static void push(Node head_ref, int new_data) 
{ 
    Node new_node = new Node(); 
    new_node.data = new_data; 
    new_node.next = (head_ref); 
    (head_ref) = new_node; 
    head = head_ref; 
} 

/* Counts no. of nodes in linked list */
static int getCount(Node head) 
{ 
    int count = 0; // Initialize count 
    Node current = head; // Initialize current 
    while (current != null) 
    { 
        count++; 
        current = current.next; 
    } 
    return count; 
} 

/* Takes head pointer of the linked list and  
index as arguments and return data at index*/
static int getNth(Node head, int n) 
{ 
    Node curr = head; 
    for (int i = 0; i < n - 1 && curr != null; i++) 
    curr = curr.next; 
    return curr.data; 
} 

static void printReverse() 
{ 
    // Count nodes 
    int n = getCount(head); 

    for (int i = n; i >= 1; i--) 
        System.out.printf("%d ", getNth(head, i)); 
} 

// Driver Code 
public static void main(String[] args) 
{ 
    /* Start with the empty list */
    head = null; 

    /* Use push() to conbelow list 
    1->2->3->4->5 */
    push(head, 5); 
    push(head, 4); 
    push(head, 3); 
    push(head, 2); 
    push(head, 1); 

    printReverse(); 
} 
} 

// This code is contributed by PrinciRaj1992  

```

## C#

```cs

// C# program to print reverse of  
// linked list without extra space 
// and without modifications. 
using System; 

class GFG  
{ 

/* Link list node */
public class Node 
{ 
    public int data; 
    public Node next; 
}; 
static Node head; 

/* Given a reference (pointer to pointer)  
to the head of a list and an int, push a  
new node on the front of the list. */
static void push(Node head_ref,  
                 int new_data) 
{ 
    Node new_node = new Node(); 
    new_node.data = new_data; 
    new_node.next = (head_ref); 
    (head_ref) = new_node; 
    head = head_ref; 
} 

/* Counts no. of nodes in linked list */
static int getCount(Node head) 
{ 
    int count = 0; // Initialize count 
    Node current = head; // Initialize current 
    while (current != null) 
    { 
        count++; 
        current = current.next; 
    } 
    return count; 
} 

/* Takes head pointer of the linked list and  
index as arguments and return data at index*/
static int getNth(Node head, int n) 
{ 
    Node curr = head; 
    for (int i = 0;  
             i < n - 1 && curr != null; i++) 
    curr = curr.next; 
    return curr.data; 
} 

static void printReverse() 
{ 
    // Count nodes 
    int n = getCount(head); 

    for (int i = n; i >= 1; i--) 
        Console.Write("{0} ", getNth(head, i)); 
} 

// Driver Code 
public static void Main(String[] args) 
{ 
    /* Start with the empty list */
    head = null; 

    /* Use push() to conbelow list 
    1->2->3->4->5 */
    push(head, 5); 
    push(head, 4); 
    push(head, 3); 
    push(head, 2); 
    push(head, 1); 

    printReverse(); 
} 
} 

// This code is contributed by Princi Singh 

```

**Output:**

```
5 4 3 2 1
```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。