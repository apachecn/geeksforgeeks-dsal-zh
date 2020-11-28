# 删除链表

> 原文：[https://www.geeksforgeeks.org/remove-last-node-of-the-linked-list/](https://www.geeksforgeeks.org/remove-last-node-of-the-linked-list/)

的最后一个节点

给定一个链表，任务是删除链表的最后一个节点并更新链表的头指针。

**示例**：

```
Input: 1 -> 2 -> 3 -> 4 -> 5 -> NULL
Output: 1 -> 2 -> 3 -> 4 -> NULL

Explanation: The last node of the linked list
is 5, so 5 is deleted.

Input: 2 -> 4 -> 6 -> 8 -> 33 -> 67 -> NULL
Output: 2 -> 4 -> 6 -> 8 -> 33 -> NULL

Explanation: The last node of the linked list
is 67, so 67 is deleted.

```

**方法**：要删除链表的最后一个节点，请找到倒数第二个节点，并使该节点的下一个指针为空。

![](img/70ab2350756844a2a95b30cdcb391368.png)

**算法**：

1.  如果第一个节点为 *null* 或只有一个节点，则返回 *null*

    ```
    if *headNode* == null then return null
    if *headNode*.nextNode == null then free 
    head and return null

    ```

2.  创建一个额外的空间 *secondLast* ，并遍历链表，直到倒数第二个节点。

    ```
    while *secondLast*.nextNode.nextNode != null 
          *secondLast* = *secondLast*.nextNode 

    ```

3.  删除最后一个节点，即倒数第二个节点的下一个节点`delete(secondLast.nextNode)`，并将倒数第二个节点的`next`值设置为`null`。

**实现**：

## C++

```cpp

// CPP program to remove last node of 
// linked list. 
#include <iostream> 
using namespace std; 

/* Link list node */
struct Node { 
    int data; 
    struct Node* next; 
}; 

/* Function to remove the last node   
   of the linked list */
Node* removeLastNode(struct Node* head) 
{ 
    if (head == NULL) 
        return NULL; 

    if (head->next == NULL) { 
        delete head; 
        return NULL; 
    } 

    // Find the second last node 
    Node* second_last = head; 
    while (second_last->next->next != NULL) 
        second_last = second_last->next; 

    // Delete last node 
    delete (second_last->next); 

    // Change next of second last 
    second_last->next = NULL; 

    return head; 
} 

// Function to push node at head 
void push(struct Node** head_ref, int new_data) 
{ 
    struct Node* new_node = new Node; 
    new_node->data = new_data; 
    new_node->next = (*head_ref); 
    (*head_ref) = new_node; 
} 

// Driver code 
int main() 
{ 
    /* Start with the empty list */
    Node* head = NULL; 

    /* Use push() function to construct    
       the below list 8 -> 23 -> 11 -> 29 -> 12 */
    push(&head, 12); 
    push(&head, 29); 
    push(&head, 11); 
    push(&head, 23); 
    push(&head, 8); 

    head = removeLastNode(head); 
    for (Node* temp = head; temp != NULL; temp = temp->next) 
        cout << temp->data << " "; 

    return 0; 
} 

```

## Java

```java

// Java program to remove last node of 
// linked list. 
class GFG { 

    // Link list node / 
    static class Node { 
        int data; 
        Node next; 
    }; 

    // Function to remove the last node 
    // of the linked list / 
    static Node removeLastNode(Node head) 
    { 
        if (head == null) 
            return null; 

        if (head.next == null) { 
            return null; 
        } 

        // Find the second last node 
        Node second_last = head; 
        while (second_last.next.next != null) 
            second_last = second_last.next; 

        // Change next of second last 
        second_last.next = null; 

        return head; 
    } 

    // Function to push node at head 
    static Node push(Node head_ref, int new_data) 
    { 
        Node new_node = new Node(); 
        new_node.data = new_data; 
        new_node.next = (head_ref); 
        (head_ref) = new_node; 
        return head_ref; 
    } 

    // Driver code 
    public static void main(String args[]) 
    { 
        // Start with the empty list / 
        Node head = null; 

        // Use push() function to con 
        // the below list 8 . 23 . 11 . 29 . 12 / 
        head = push(head, 12); 
        head = push(head, 29); 
        head = push(head, 11); 
        head = push(head, 23); 
        head = push(head, 8); 

        head = removeLastNode(head); 
        for (Node temp = head; temp != null; temp = temp.next) 
            System.out.print(temp.data + " "); 
    } 
} 

// This code is contributed by Arnab Kundu 

```

## Python3

```py

# Python3 program to remove the last node of  
# linked list. 
import sys 
import math 

# Link list node 
class Node: 
    def __init__(self, data): 
        self.data = data 
        self.next = None

# Function to push node at head  
def push(head, data): 
    if not head: 
        return Node(data) 
    temp = Node(data) 
    temp.next = head 
    head = temp 
    return head 

# Function to remove the last node  
# of the linked list 
def removeLastNode(head): 
    if head == None: 
        return None
    if head.next == None: 
        head = None
        return None
    second_last = head 
    while(second_last.next.next): 
        second_last = second_last.next
    second_last.next = None
    return head 

# Driver code 
if __name__=='__main__': 

    # Start with the empty list 
    head = None
    # Use push() function to con  
    # the below list 8 . 23 . 11 . 29 . 12  
    head = push(head, 12) 
    head = push(head, 29) 
    head = push(head, 11) 
    head = push(head, 23) 
    head = push(head, 8) 

    head = removeLastNode(head) 
    while(head): 
        print("{} ".format(head.data), end ="") 
        head = head.next

# This code is contributed by Vikash kumar 37 

```

## C#

```cs

// C# program to remove last node of 
// linked list. 
using System; 

class GFG { 

    // Link list node / 
    public class Node { 
        public int data; 
        public Node next; 
    }; 

    // Function to remove the last node 
    // of the linked list / 
    static Node removeLastNode(Node head) 
    { 
        if (head == null) 
            return null; 

        if (head.next == null) { 
            return null; 
        } 

        // Find the second last node 
        Node second_last = head; 
        while (second_last.next.next != null) 
            second_last = second_last.next; 

        // Change next of second last 
        second_last.next = null; 

        return head; 
    } 

    // Function to push node at head 
    static Node push(Node head_ref, int new_data) 
    { 
        Node new_node = new Node(); 
        new_node.data = new_data; 
        new_node.next = (head_ref); 
        (head_ref) = new_node; 
        return head_ref; 
    } 

    // Driver code 
    public static void Main(String[] args) 
    { 
        // Start with the empty list / 
        Node head = null; 

        // Use push() function to con 
        // the below list 8 . 23 . 11 . 29 . 12 / 
        head = push(head, 12); 
        head = push(head, 29); 
        head = push(head, 11); 
        head = push(head, 23); 
        head = push(head, 8); 

        head = removeLastNode(head); 
        for (Node temp = head; temp != null; temp = temp.next) 
            Console.Write(temp.data + " "); 
    } 
} 

/* This code contributed by PrinciRaj1992 */

```

**输出**：

```
8 23 11 29

```

**复杂度分析**：

*   **时间复杂度**：`O(n)`。

    该算法涉及遍历链表直到其结束，因此所需的时间复杂度为 *`O(n)`*。

*   **空间复杂度**：`O(1)`。

    不需要额外的空间，因此空间复杂度是恒定的



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。