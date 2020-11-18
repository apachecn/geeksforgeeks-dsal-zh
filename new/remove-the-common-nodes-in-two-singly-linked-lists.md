# 删除两个单链接列表中的公共节点

给定两个[链表](https://www.geeksforgeeks.org/data-structures/linked-list/) **L1** 和 **L2** ，任务是从给定的两个链表中生成一个没有公共元素的新链表。

**示例：**

> **输入：** L1 = 10-> 15-> 5-> 20，L2 = 8-> 5-> 20-> 10
> **输出：** 8-> 15
> **说明：**
> 由于两个链表都有5、10和20的共同点。 因此，删除了这些元素，结果列表为8-> 15。
> 
> **输入：** L1 = 0-> 5-> 52-> 21，L2 = 21-> 5-> 0-> 52
> **输出：** []
> **说明：**
> 由于两个给定链表的所有元素都是相同的。 因此，结果链接为空。

**方法：**

1.  对于第一个链表中的每个元素（例如 **X** ）：
    *   遍历第二个链接列表并检查链接列表中是否存在 **X** 。
    *   如果不存在 **X** ，则在结果链接列表中插入 **X** ，因为这在两个链接列表中都不常见。
2.  对于第二个链表中的每个元素（例如 **Y** ）：
    *   遍历第一个链表，并检查链表中是否存在 **Y** 。
    *   如果不存在 **Y** ，则在结果链接列表中插入 **Y** ，因为这在两个链接列表中都不常见。
3.  结果链表将是必需的链表，给定两个链表中没有公共节点。

下面是上述方法的实现：

## CPP

```

// C++ program for the above approach 

#include <bits/stdc++.h> 
using namespace std; 

// Link list node 
struct Node { 
    int data; 
    struct Node* next; 
}; 

// Function to print the element 
// of the Linked List 
void printList(struct Node* p) 
{ 
    if (p == NULL) { 
        cout << "[]"; 
    } 

    while (p != NULL) { 
        cout << p->data << " -> "; 
        p = p->next; 
    } 
} 

// Function to push the node at the 
// beginning of the linked list 
void push(struct Node** head_ref, 
          int new_data) 
{ 
    struct Node* new_node 
        = (struct Node*)malloc( 
            sizeof(struct Node)); 

    new_node->data = new_data; 
    new_node->next = (*head_ref); 
    (*head_ref) = new_node; 
} 

// Function to insert unique 
// elements in the new LL 
void traverse(struct Node** head3, 
              struct Node* temp1, 
              struct Node* temp2) 
{ 

    // Traverse the first linked list 
    while (temp1 != NULL) { 

        // Value of current node 
        int val = temp1->data; 
        struct Node* t = temp2; 
        int x = 0; 

        // Traverse the second list 
        while (t != NULL) { 
            if (t->data == val) { 
                x = 1; 
                break; 
            } 
            t = t->next; 
        } 

        // If element is not common 
        // then insert it in the 
        // resultant linked list 
        if (x == 0) { 
            push(head3, temp1->data); 
        } 

        temp1 = temp1->next; 
    } 
} 

// Function to remove the common nodes 
// in two Singly Linked Lists 
void removeCommonNodes(struct Node* head1, 
                       struct Node* head2) 
{ 

    // Head pointer for the resultant 
    // linked list 
    struct Node* head3 = NULL; 

    // Find the node common between 
    // linked list taking head1 as 
    // first linked list 
    traverse(&head3, head1, head2); 

    // Find the node common between 
    // linked list taking head2 as 
    // first linked list 
    traverse(&head3, head2, head1); 

    // Print the resultant linked list 
    printList(head3); 
} 

// Driver code 
int main() 
{ 
    // First list 
    struct Node* head1 = NULL; 
    push(&head1, 20); 
    push(&head1, 5); 
    push(&head1, 15); 
    push(&head1, 10); 

    // Second list 
    struct Node* head2 = NULL; 
    push(&head2, 10); 
    push(&head2, 20); 
    push(&head2, 15); 
    push(&head2, 8); 

    // Function call 
    removeCommonNodes(head1, head2); 

    return 0; 
} 

```

## Java

```java

// Java program for the above approach 
class GFG{ 

// Link list node 
static class Node { 
    int data; 
    Node next; 
}; 

// Function to print the element 
// of the Linked List 
static void printList(Node p) 
{ 
    if (p == null) { 
        System.out.print("[]"); 
    } 

    while (p != null) { 
        System.out.print(p.data+ "->"); 
        p = p.next; 
    } 
} 

// Function to push the node at the 
// beginning of the linked list 
static Node push(Node head_ref, 
          int new_data) 
{ 
    Node new_node = new Node(); 

    new_node.data = new_data; 
    new_node.next = head_ref; 
    head_ref = new_node; 
    return head_ref; 
} 

// Function to insert unique 
// elements in the new LL 
static Node traverse(Node head3, 
              Node temp1, 
              Node temp2) 
{ 

    // Traverse the first linked list 
    while (temp1 != null) { 

        // Value of current node 
        int val = temp1.data; 
        Node t = temp2; 
        int x = 0; 

        // Traverse the second list 
        while (t != null) { 
            if (t.data == val) { 
                x = 1; 
                break; 
            } 
            t = t.next; 
        } 

        // If element is not common 
        // then insert it in the 
        // resultant linked list 
        if (x == 0) { 
            head3 = push(head3, temp1.data); 
        } 

        temp1 = temp1.next; 
    } 
    return head3; 
} 

// Function to remove the common nodes 
// in two Singly Linked Lists 
static void removeCommonNodes(Node head1, 
                       Node head2) 
{ 

    // Head pointer for the resultant 
    // linked list 
    Node head3 = null; 

    // Find the node common between 
    // linked list taking head1 as 
    // first linked list 
    head3 = traverse(head3, head1, head2); 

    // Find the node common between 
    // linked list taking head2 as 
    // first linked list 
    head3 = traverse(head3, head2, head1); 

    // Print the resultant linked list 
    printList(head3); 
} 

// Driver code 
public static void main(String[] args) 
{ 
    // First list 
    Node head1 = new Node(); 
    head1 = push(head1, 20); 
    head1 = push(head1, 5); 
    head1 = push(head1, 15); 
    head1 = push(head1, 10); 

    // Second list 
    Node head2 = new Node(); 
    head2 = push(head2, 10); 
    head2 = push(head2, 20); 
    head2 = push(head2, 15); 
    head2 = push(head2, 8); 

    // Function call 
    removeCommonNodes(head1, head2); 
} 
} 

// This code is contributed by sapnasingh4991 

```

## C#

```cs

// C# program for the above approach 
using System; 

class GFG{ 

// Link list node 
class Node { 
    public int data; 
    public Node next; 
}; 

// Function to print the element 
// of the Linked List 
static void printList(Node p) 
{ 
    if (p == null) { 
        Console.Write("[]"); 
    } 

    while (p != null) { 
        Console.Write(p.data+ "->"); 
        p = p.next; 
    } 
} 

// Function to push the node at the 
// beginning of the linked list 
static Node push(Node head_ref, 
          int new_data) 
{ 
    Node new_node = new Node(); 

    new_node.data = new_data; 
    new_node.next = head_ref; 
    head_ref = new_node; 
    return head_ref; 
} 

// Function to insert unique 
// elements in the new LL 
static Node traverse(Node head3, 
              Node temp1, 
              Node temp2) 
{ 

    // Traverse the first linked list 
    while (temp1 != null) { 

        // Value of current node 
        int val = temp1.data; 
        Node t = temp2; 
        int x = 0; 

        // Traverse the second list 
        while (t != null) { 
            if (t.data == val) { 
                x = 1; 
                break; 
            } 
            t = t.next; 
        } 

        // If element is not common 
        // then insert it in the 
        // resultant linked list 
        if (x == 0) { 
            head3 = push(head3, temp1.data); 
        } 

        temp1 = temp1.next; 
    } 
    return head3; 
} 

// Function to remove the common nodes 
// in two Singly Linked Lists 
static void removeCommonNodes(Node head1, 
                       Node head2) 
{ 

    // Head pointer for the resultant 
    // linked list 
    Node head3 = null; 

    // Find the node common between 
    // linked list taking head1 as 
    // first linked list 
    head3 = traverse(head3, head1, head2); 

    // Find the node common between 
    // linked list taking head2 as 
    // first linked list 
    head3 = traverse(head3, head2, head1); 

    // Print the resultant linked list 
    printList(head3); 
} 

// Driver code 
public static void Main(String[] args) 
{ 
    // First list 
    Node head1 = new Node(); 
    head1 = push(head1, 20); 
    head1 = push(head1, 5); 
    head1 = push(head1, 15); 
    head1 = push(head1, 10); 

    // Second list 
    Node head2 = new Node(); 
    head2 = push(head2, 10); 
    head2 = push(head2, 20); 
    head2 = push(head2, 15); 
    head2 = push(head2, 8); 

    // Function call 
    removeCommonNodes(head1, head2); 
} 
} 

// This code is contributed by PrinciRaj1992 

```

**Output:**

```
8 -> 5 ->

```

**时间复杂度：** O（M * N），其中M和N是两个给定链表的长度。



* * *

* * *

如果您喜欢GeeksforGeeks并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至tribution@geeksforgeeks.org。 查看您的文章出现在GeeksforGeeks主页上，并帮助其他Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。