# 两个链表中的第一个公共元素

> 原文：[https://www.geeksforgeeks.org/first-common-element-two-linked-lists/](https://www.geeksforgeeks.org/first-common-element-two-linked-lists/)

给定两个链表，找到给定链表之间的第一个公共元素，即我们需要找到第一个链表的第一个节点，该节点也存在于第二个链表中。

**范例**：

```
Input :  
   List1: 10->15->4->20
   Lsit2:  8->4->2->10
Output : 10

Input : 
   List1: 1->2->3->4
   Lsit2:  5->6->3->8
Output : 3

```

我们遍历第一个列表，对于每个节点，我们在第二个列表中搜索它。 一旦在第二个列表中找到一个元素，就将其返回。

## C++

```cpp

// C++ program to find first common element in 
// two unsorted linked list 
#include <bits/stdc++.h> 
using namespace std; 

/* Link list node */
struct Node { 
    int data; 
    struct Node* next; 
}; 

/* A utility function to insert a node at the  
   beginning of a linked list*/
void push(struct Node** head_ref, int new_data) 
{ 
    struct Node* new_node =  
          (struct Node*)malloc(sizeof(struct Node)); 
    new_node->data = new_data; 
    new_node->next = (*head_ref); 
    (*head_ref) = new_node; 
} 

/* Returns the first repeating element in linked list*/
int firstCommon(struct Node* head1, struct Node* head2) 
{ 
    // Traverse through every node of first list 
    for (; head1 != NULL; head1=head1->next) 

       // If current node is present in second list 
       for (Node *p = head2; p != NULL; p = p->next) 
            if (p->data == head1->data) 
                return head1->data; 

    // If no common node 
    return 0; 
} 

// Driver code 
int main() 
{ 
    struct Node* head1 = NULL; 
    push(&head1, 20); 
    push(&head1, 5); 
    push(&head1, 15); 
    push(&head1, 10); 

    struct Node* head2 = NULL; 
    push(&head2, 10); 
    push(&head2, 2); 
    push(&head2, 15); 
    push(&head2, 8); 

    cout << firstCommon(head1, head2); 
    return 0; 
} 

```

## Java

```java

// Java program to find first common element  
// in two unsorted linked list 
import java.util.*; 

class GFG  
{ 

/* Link list node */
static class Node  
{ 
    int data; 
    Node next; 
}; 

/* A utility function to insert a node at the  
beginning of a linked list*/
static Node push(Node head_ref, int new_data) 
{ 
    Node new_node = new Node(); 
    new_node.data = new_data; 
    new_node.next = head_ref; 
    head_ref = new_node; 
    return head_ref; 
} 

/* Returns the first repeating element 
   in linked list*/
static int firstCommon(Node head1, Node head2) 
{ 
    // Traverse through every node of first list 
    for (; head1 != null; head1 = head1.next) 

    // If current node is present in second list 
    for (Node p = head2; p != null; p = p.next) 
            if (p.data == head1.data) 
                return head1.data; 

    // If no common node 
    return 0; 
} 

// Driver code 
public static void main(String[] args) 
{ 
    Node head1 = null; 
    head1 = push(head1, 20); 
    head1 = push(head1, 5); 
    head1 = push(head1, 15); 
    head1 = push(head1, 10); 

    Node head2 = null; 
    head2 = push(head2, 10); 
    head2 = push(head2, 2); 
    head2 = push(head2, 15); 
    head2 = push(head2, 8); 

    System.out.println(firstCommon(head1, head2)); 
} 
}  

// This code is contributed by 29AjayKumar 

```

## Python3

```py

# Python3 program to find first common element  
# in two unsorted linked list 
import math 

# Link list node  
class Node:  
    def __init__(self, data):  
        self.data = data  
        self.next = None

# A utility function to insert a node at the  
#beginning of a linked list 
def push(head_ref, new_data): 
    new_node = Node(new_data) 
    new_node.data = new_data 
    new_node.next = head_ref 
    head_ref = new_node 
    return head_ref 

# Returns the first repeating element 
# in linked list*/ 
def firstCommon(head1, head2): 

    # Traverse through every node of first list 
    while(head1 != None): 
        p = head2 

    # If current node is present in second list 
        while(p != None): 
            if (p.data == head1.data): 
                return head1.data 
            p = p.next
        head1 = head1.next

    # If no common node 
    return 0

# Driver code 
if __name__=='__main__':  
    head1 = None
    head1 = push(head1, 20) 
    head1 = push(head1, 5) 
    head1 = push(head1, 15) 
    head1 = push(head1, 10) 

    head2 = None
    head2 = push(head2, 10) 
    head2 = push(head2, 2) 
    head2 = push(head2, 15) 
    head2 = push(head2, 8) 

    print(firstCommon(head1, head2)) 

# This code is contributed by Srathore 

```

## C#

```cs

// C# program to find first common element  
// in two unsorted linked list 
using System; 
using System.Collections.Generic; 

class GFG  
{ 

/* Link list node */
class Node  
{ 
    public int data; 
    public Node next; 
}; 

/* A utility function to insert a node at the  
beginning of a linked list*/
static Node push(Node head_ref, int new_data) 
{ 
    Node new_node = new Node(); 
    new_node.data = new_data; 
    new_node.next = head_ref; 
    head_ref = new_node; 
    return head_ref; 
} 

/* Returns the first repeating element 
in linked list*/
static int firstCommon(Node head1, Node head2) 
{ 
    // Traverse through every node of first list 
    for (; head1 != null; head1 = head1.next) 

    // If current node is present in second list 
    for (Node p = head2; p != null; p = p.next) 
            if (p.data == head1.data) 
                return head1.data; 

    // If no common node 
    return 0; 
} 

// Driver code 
public static void Main(String[] args) 
{ 
    Node head1 = null; 
    head1 = push(head1, 20); 
    head1 = push(head1, 5); 
    head1 = push(head1, 15); 
    head1 = push(head1, 10); 

    Node head2 = null; 
    head2 = push(head2, 10); 
    head2 = push(head2, 2); 
    head2 = push(head2, 15); 
    head2 = push(head2, 8); 

    Console.WriteLine(firstCommon(head1, head2)); 
} 
}  

// This code is contributed by PrinciRaj1992 

```

**输出**：

```
10

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。