# 排序的链表包含从 1 到 N 的值

> 原文：[https://www.geeksforgeeks.org/sort-linked-list-containing-values-from-1-to-n/](https://www.geeksforgeeks.org/sort-linked-list-containing-values-from-1-to-n/)

给定大小为 N 的链接列表，其中包含从 1 到 N 的所有值。任务是按递增顺序对链接列表进行排序。

**示例**：

```
Input : List = 3 -> 5 -> 4 -> 6 -> 1 -> 2
Output : 1 -> 2 -> 3 -> 4 -> 5 -> 6

Input : List = 5 -> 4 -> 3 -> 2 -> 1
Output : 1 -> 2 -> 3 -> 4 -> 5

```

**天真的方法**：最简单的方法是使用任何类型的[排序方法](https://www.geeksforgeeks.org/merge-sort-for-linked-list/)对该链表进行排序。 最少需要 O（N * logN）个时间。

**有效方法**：一种有效方法是观察链表包含总共 N 个元素，并且元素从 1 到 N 进行编号。遍历链表并将每个元素替换为其位置。

以下是此方法的实现：

## C++

```cpp

// C++ program to sort linked list containing 
// values from 1 to N 
#include <iostream> 

using namespace std; 

// A linked list node 
struct Node { 
    int data; 
    struct Node* next; 
}; 

// Function to sort linked list 
bool sortList(struct Node* head) 
{ 
    int startVal = 1; 

    while (head != NULL) { 
        head->data = startVal; 

        startVal++; 

        head = head->next; 
    } 
} 

// Function to add a node at the 
// beginning of Linked List 
void push(struct Node** head_ref, int new_data) 
{ 
    /* allocate node */
    struct Node* new_node = (struct Node*)malloc(sizeof(struct Node)); 

    /* put in the data */
    new_node->data = new_data; 

    /* link the old list off the new node */
    new_node->next = (*head_ref); 

    /* move the head to point to the new node */
    (*head_ref) = new_node; 
} 

// This function prints contents of 
// linked list starting from 
// the given node 
void printList(struct Node* node) 
{ 
    while (node != NULL) { 
        cout << node->data << " "; 

        node = node->next; 
    } 
} 

// Driver program to test above function 
int main() 
{ 
    struct Node* start = NULL; 

    /* The constructed linked list is:  
    3->5->4->6->1->2 */
    push(&start, 2); 
    push(&start, 1); 
    push(&start, 6); 
    push(&start, 4); 
    push(&start, 5); 
    push(&start, 3); 

    sortList(start); 

    printList(start); 

    return 0; 
} 

```

## Java

```java

// Java program to sort linked list containing 
// values from 1 to N 
import java.util.*; 
class GFG  
{ 

/* Link list node */
static class Node 
{ 
    int data; 
    Node next; 
}; 
static Node start; 

// Function to sort linked list 
static void sortList(Node head) 
{ 
    int startVal = 1; 

    while (head != null) 
    { 
        head.data = startVal; 

        startVal++; 

        head = head.next; 
    } 
} 

// Function to add a node at the 
// beginning of Linked List 
static void push(Node head_ref,  
                 int new_data) 
{ 
    /* allocate node */
    Node new_node = new Node(); 

    /* put in the data */
    new_node.data = new_data; 

    /* link the old list off the new node */
    new_node.next = head_ref; 

    /* move the head to point to the new node */
    head_ref = new_node; 
    start = head_ref; 
} 

// This function prints contents of 
// linked list starting from 
// the given node 
static void printList(Node node) 
{ 
    while (node != null) 
    { 
        System.out.print(node.data + " "); 

        node = node.next; 
    } 
} 

// Driver Code 
public static void main(String[] args)  
{ 
    start = null; 

    /* The constructed linked list is:  
    3->5->4->6->1->2 */
    push(start, 2); 
    push(start, 1); 
    push(start, 6); 
    push(start, 4); 
    push(start, 5); 
    push(start, 3); 

    sortList(start); 

    printList(start); 
} 
} 

// This code is contributed by PrinciRaj1992  

```

## Python3

```py

# Python3 program to sort linked list  
# containing values from 1 to N 
import math 

# A linked list node 
class Node:  
    def __init__(self, data):  
        self.data = data  
        self.next = None

# Function to sort linked list 
def sortList(head): 
    startVal = 1

    while (head != None): 
        head.data = startVal 

        startVal = startVal + 1

        head = head.next

# Function to add a node at the 
# beginning of Linked List 
def push(head_ref, new_data): 

    # allocate node  
    new_node = Node(new_data) 

    # put in the data  
    new_node.data = new_data 

    # link the old list off the new node  
    new_node.next = head_ref 

    # move the head to po to the new node  
    head_ref = new_node 
    return head_ref 

# This function prs contents of 
# linked list starting from 
# the given node 
def prList(node): 
    while (node != None): 
        print(node.data, end = " ") 

        node = node.next

# Driver Code 
if __name__=='__main__': 
    head = None

    # The constructed linked list is:  
    #3.5.4.6.1.2  
    head = push(head, 2) 
    head = push(head, 1) 
    head = push(head, 6) 
    head = push(head, 4) 
    head = push(head, 5) 
    head = push(head, 3) 

    sortList(head) 

    prList(head) 

# This code is contributed by Srathore 

```

## C#

```cs

// C# program to sort linked list  
// containing values from 1 to N 
using System; 

class GFG  
{ 

/* Link list node */
public class Node 
{ 
    public int data; 
    public Node next; 
}; 
static Node start; 

// Function to sort linked list 
static void sortList(Node head) 
{ 
    int startVal = 1; 

    while (head != null) 
    { 
        head.data = startVal; 

        startVal++; 

        head = head.next; 
    } 
} 

// Function to add a node at the 
// beginning of Linked List 
static void push(Node head_ref,  
                 int new_data) 
{ 
    /* allocate node */
    Node new_node = new Node(); 

    /* put in the data */
    new_node.data = new_data; 

    /* link the old list  
     off the new node */
    new_node.next = head_ref; 

    /* move the head to point  
       to the new node */
    head_ref = new_node; 
    start = head_ref; 
} 

// This function prints contents of 
// linked list starting from 
// the given node 
static void printList(Node node) 
{ 
    while (node != null) 
    { 
        Console.Write(node.data + " "); 

        node = node.next; 
    } 
} 

// Driver Code 
public static void Main(String[] args)  
{ 
    start = null; 

    /* The constructed linked list is:  
    3->5->4->6->1->2 */
    push(start, 2); 
    push(start, 1); 
    push(start, 6); 
    push(start, 4); 
    push(start, 5); 
    push(start, 3); 

    sortList(start); 

    printList(start); 
} 
} 

// This code is contributed  
// by Princi Singh 

```

**Output:**

```
1 2 3 4 5 6

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。