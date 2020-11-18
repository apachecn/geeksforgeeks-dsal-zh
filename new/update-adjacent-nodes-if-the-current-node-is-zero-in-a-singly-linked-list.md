# 如果单链接列表

> 原文：[https://www.geeksforgeeks.org/update-adjacent-nodes-if-the-current-node-is-zero-in-a-singly-linked-list/](https://www.geeksforgeeks.org/update-adjacent-nodes-if-the-current-node-is-zero-in-a-singly-linked-list/)

中的当前节点为零，则更新相邻节点。

给定一个链表。 如果当前节点为 0，则任务是将节点的上一个和下一个节点的值更改为 0。

**示例**：

```
Input :  2->3->4->5->0->9->0->9->NULL
Output : 2->3->4->0->0->0->0->0->NULL

Input : 0->2->3->4->0->0->NULL
Output : 0->0->3->0->0->0->NULL

```

**算法**：

1.  第一步是创建两个指针 **prev** 和 **curr** 。

    上一个**指向**的前一个节点**，**指向**到**当前节点**。 使用 **prev** 的原因是我们无法在单个链接列表中回溯。**

2.  **如果**第一个节点是`0`，则检查下一个节点是否是`0`

    *   如果是，请先跳过**，然后再跳过**

    *   **否则**将下一个节点更改为 **-1** 。

3.  开始遍历列表中的节点。

    *   **如果**当前节点为`0`，变量 **temp** 为`0`，则

        *   将前一个节点设置为 **-1** 。

        *   将 temp 变量设置为`1`。

    *   **如果**的**温度**的值为`1`，并且当前节点数据不是`1`，则将当前节点设置为 **-1**

4.  重复步骤 3，直到到达列表的末尾。

5.  浏览列表，并将值 **-1** 更改为`0`的节点。

使用**临时**和 **-1** 的原因是，如果我们直接将下一个节点更改为`0`，则可能导致将下一个节点后的节点更改为`0`结果，整个列表可能会更改为`0`。

下面是上述方法的实现：

## C++

```cpp

// C++ program to update the adjacent 
// nodes in a linked list 

#include <bits/stdc++.h> 
using namespace std; 

// A linked list node 
struct Node { 
    int data; 
    struct Node* next; 
}; 

// Utility function to create a new Node 
Node* newNode(int data) 
{ 
    Node* temp = new Node; 
    temp->data = data; 
    temp->next = NULL; 

    return temp; 
} 

// Function to display the linked list 
void printList(Node* node) 
{ 
    // iterate until end of the list is reached 
    while (node != NULL) { 
        cout << node->data << " "; 

        node = node->next; 
    } 
} 

// Function to udate the adjacent 
// nodes to zero 
void updateAdjacent(Node* head) 
{ 
    // Pointer to point to 
    // the previous node 
    Node* prev = head; 

    // Pointer to the 
    // current node 
    Node* curr = head->next; 

    // If the first node is zero and the 
    // second node is not zero then change  
    // the value to -1 
    if (prev->data == 0 && curr->data != 0) 
        curr->data = -1; 

    // Temp variable to denote if the  
    // current node is zero then the next 
    // node will be changed to zero 
    int temp = 0; 

    while (curr != NULL) { 

        // if the temp variable is 1 and 
        // current data is not zero 
        if (temp == 1 && curr->data != 0) { 

            // change the data to -1 
            curr->data = -1; 
            temp = 0; 
        } 

        // if the data is zero 
        if (curr->data == 0) { 

            // set the temp variable to 1 
            temp = 1; 

            // set the previous node data to -1 
            prev->data = -1; 
        } 

        curr = curr->next; 
        prev = prev->next; 
    } 

    curr = head; 

    // change all the nodes with -1 to 0 
    while (curr != NULL) { 
        if (curr->data == -1) 
            curr->data = 0; 

        curr = curr->next; 
    } 
} 

// Driver code 
int main() 
{ 
    // creating the linked list 
    Node* head = newNode(2); 
    head->next = newNode(3); 
    head->next->next = newNode(4); 
    head->next->next->next = newNode(5); 
    head->next->next->next->next = newNode(0); 
    head->next->next->next->next->next = newNode(9); 
    head->next->next->next->next->next->next = newNode(0); 
    head->next->next->next->next->next->next->next = newNode(9); 

    updateAdjacent(head); 

    printList(head); 

    return 0; 
} 

```

## Java

```java

// Java program to update the adjacent 
// nodes in a linked list 
class GFG  
{ 

// A linked list node 
static class Node 
{ 
    int data; 
    Node next; 
} 

// Utility function to create a new Node 
static Node newNode(int data) 
{ 
    Node temp = new Node(); 
    temp.data = data; 
    temp.next = null; 

    return temp; 
} 

// Function to display the linked list 
static void printList(Node node) 
{ 
    // iterate until end of the list is reached 
    while (node != null)  
    { 
        System.out.print(node.data + " "); 

        node = node.next; 
    } 
} 

// Function to udate the adjacent 
// nodes to zero 
static void updateAdjacent(Node head) 
{ 
    // Pointer to point to 
    // the previous node 
    Node prev = head; 

    // Pointer to the 
    // current node 
    Node curr = head.next; 

    // If the first node is zero and the 
    // second node is not zero then change  
    // the value to -1 
    if (prev.data == 0 && curr.data != 0) 
        curr.data = -1; 

    // Temp variable to denote if the  
    // current node is zero then the next 
    // node will be changed to zero 
    int temp = 0; 

    while (curr != null)  
    { 

        // if the temp variable is 1 and 
        // current data is not zero 
        if (temp == 1 && curr.data != 0) 
        { 

            // change the data to -1 
            curr.data = -1; 
            temp = 0; 
        } 

        // if the data is zero 
        if (curr.data == 0)  
        { 

            // set the temp variable to 1 
            temp = 1; 

            // set the previous node data to -1 
            prev.data = -1; 
        } 

        curr = curr.next; 
        prev = prev.next; 
    } 

    curr = head; 

    // change all the nodes with -1 to 0 
    while (curr != null)  
    { 
        if (curr.data == -1) 
            curr.data = 0; 

        curr = curr.next; 
    } 
} 

// Driver code 
public static void main(String[] args)  
{ 
    // creating the linked list 
    Node head = newNode(2); 
    head.next = newNode(3); 
    head.next.next = newNode(4); 
    head.next.next.next = newNode(5); 
    head.next.next.next.next = newNode(0); 
    head.next.next.next.next.next = newNode(9); 
    head.next.next.next.next.next.next = newNode(0); 
    head.next.next.next.next.next.next.next = newNode(9); 

    updateAdjacent(head); 

    printList(head); 
} 
} 

/* This code contributed by PrinciRaj1992 */

```

## Python3

```py

# Python3 program to update the adjacent  
# nodes in a linked list  

# A linked list node  
class Node: 

    def __init__(self, data): 
        self.data = data 
        self.next = None

# Function to display the linked list  
def printList(node):  

    # iterate until end of the  
    # list is reached  
    while node != None:  
        print(node.data, end = " ")  

        node = node.next

# Function to udate the adjacent  
# nodes to zero  
def updateAdjacent(head):  

    # Pointer to point to  
    # the previous node  
    prev = head  

    # Pointer to the  
    # current node  
    curr = head.next

    # If the first node is zero and the  
    # second node is not zero then change  
    # the value to -1  
    if prev.data == 0 and curr.data != 0:  
        curr.data = -1

    # Temp variable to denote if the  
    # current node is zero then the next  
    # node will be changed to zero  
    temp = 0

    while curr != None:  

        # if the temp variable is 1 and  
        # current data is not zero  
        if temp == 1 and curr.data != 0:  

            # change the data to -1  
            curr.data = -1
            temp = 0

        # if the data is zero  
        if curr.data == 0:  

            # set the temp variable to 1  
            temp = 1

            # set the previous node data to -1  
            prev.data = -1

        curr = curr.next
        prev = prev.next

    curr = head  

    # change all the nodes with -1 to 0  
    while curr != None:  
        if curr.data == -1:  
            curr.data = 0

        curr = curr.next

# Driver Code 
if __name__ == "__main__":  

    # creating the linked list  
    head = Node(2)  
    head.next = Node(3)  
    head.next.next = Node(4)  
    head.next.next.next = Node(5)  
    head.next.next.next.next = Node(0)  
    head.next.next.next.next.next = Node(9)  
    head.next.next.next.next.next.next = Node(0)  
    head.next.next.next.next.next.next.next = Node(9)  

    updateAdjacent(head)  

    printList(head)  

# This code is contributed by Rituraj Jain 

```

## C#

```cs

// C# program to update the adjacent 
// nodes in a linked list 
using System; 

class GFG  
{ 

// A linked list node 
public class Node 
{ 
    public int data; 
    public Node next; 
} 

// Utility function to create a new Node 
static Node newNode(int data) 
{ 
    Node temp = new Node(); 
    temp.data = data; 
    temp.next = null; 

    return temp; 
} 

// Function to display the linked list 
static void printList(Node node) 
{ 
    // iterate until end of the list is reached 
    while (node != null)  
    { 
        Console.Write(node.data + " "); 

        node = node.next; 
    } 
} 

// Function to udate the adjacent 
// nodes to zero 
static void updateAdjacent(Node head) 
{ 
    // Pointer to point to 
    // the previous node 
    Node prev = head; 

    // Pointer to the 
    // current node 
    Node curr = head.next; 

    // If the first node is zero and the 
    // second node is not zero then change  
    // the value to -1 
    if (prev.data == 0 && curr.data != 0) 
        curr.data = -1; 

    // Temp variable to denote if the  
    // current node is zero then the next 
    // node will be changed to zero 
    int temp = 0; 

    while (curr != null)  
    { 

        // if the temp variable is 1 and 
        // current data is not zero 
        if (temp == 1 && curr.data != 0) 
        { 

            // change the data to -1 
            curr.data = -1; 
            temp = 0; 
        } 

        // if the data is zero 
        if (curr.data == 0)  
        { 

            // set the temp variable to 1 
            temp = 1; 

            // set the previous node data to -1 
            prev.data = -1; 
        } 

        curr = curr.next; 
        prev = prev.next; 
    } 

    curr = head; 

    // change all the nodes with -1 to 0 
    while (curr != null)  
    { 
        if (curr.data == -1) 
            curr.data = 0; 

        curr = curr.next; 
    } 
} 

// Driver code 
public static void Main(String[] args)  
{ 
    // creating the linked list 
    Node head = newNode(2); 
    head.next = newNode(3); 
    head.next.next = newNode(4); 
    head.next.next.next = newNode(5); 
    head.next.next.next.next = newNode(0); 
    head.next.next.next.next.next = newNode(9); 
    head.next.next.next.next.next.next = newNode(0); 
    head.next.next.next.next.next.next.next = newNode(9); 

    updateAdjacent(head); 

    printList(head); 
} 
} 

// This code contributed by Rajput-Ji 

```

**Output:**

```
2 3 4 0 0 0 0 0

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。