# 以给定大小的组反向链接列表（迭代方法）

给定一个链表和一个整数 **K** ，任务是反转给定链表的每个 **K** 个节点。

**示例：**

> **输入：** 1-> 2-> 3-> 4-> 5-> 6-> 7-> 8-> NULL， K = 3
> **输出：** 3 2 1 6 5 4 8 7
> 
> **输入：** 1-> 2-> 3-> 4-> 5-> 6-> 7-> 8-> NULL， K = 5
> **输出：** 5 4 3 2 1 8 7 6

**方法：**我们已经在帖子 [Set 1](https://www.geeksforgeeks.org/reverse-a-list-in-groups-of-given-size/) 和 [Set 2](https://www.geeksforgeeks.org/reverse-linked-list-groups-given-size-set-2/) 中讨论了递归解决方案。 在这篇文章中，我们将讨论上述问题的迭代解决方案。 与上述解决方案不同，我们不使用任何形式的堆栈来实现我们的解决方案。 我们反转链表的前k个节点。 反转时，我们使用join和tail指针跟踪k反转链表的第一个和最后一个节点。 反转链表的k个节点后，我们连接由尾指针指向的节点，并连接并更新它们。 我们重复此过程，直到所有节点组都被反转为止。

下面是上述方法的实现：

## C ++

```

// C++ implementation of the approach 
#include <bits/stdc++.h> 
using namespace std; 

// Link list node 
struct Node { 
    int data; 
    struct Node* next; 
}; 

/* Function to reverse the linked list in groups of  
size k and return the pointer to the new head node. */
Node* reverse(struct Node* head, int k) 
{ 
    Node* prev = NULL; 
    Node* curr = head; 
    Node* temp = NULL; 
    Node* tail = NULL; 
    Node* newHead = NULL; 
    Node* join = NULL; 
    int t = 0; 

    // Traverse till the end of the linked list 
    while (curr) { 
        t = k; 
        join = curr; 
        prev = NULL; 

        // Reverse group of k nodes of the linked list 
        while (curr && t--) { 
            temp = curr->next; 
            curr->next = prev; 
            prev = curr; 
            curr = temp; 
        } 

        // Sets the new head of the input list 
        if (!newHead) 
            newHead = prev; 

        /* Tail pointer keeps track of the last node  
        of the k-reversed linked list. We join the  
        tail pointer with the head of the next  
        k-reversed linked list's head */
        if (tail) 
            tail->next = prev; 

        /* The tail is then updated to the last node  
        of the next k-reverse linked list */
        tail = join; 
    } 

    /* newHead is new head of the input list */
    return newHead; 
} 

// Function to insert a node at 
// the head of the linked list 
void push(Node** head_ref, int new_data) 
{ 
    /* allocate node */
    Node* new_node = new Node(); 

    /* put in the data */
    new_node->data = new_data; 

    /* link the old list off the new node */
    new_node->next = (*head_ref); 

    /* move the head to point to the new node */
    (*head_ref) = new_node; 
} 

// Function to print the linked list 
void printList(Node* node) 
{ 
    while (node != NULL) { 
        cout << node->data << " "; 
        node = node->next; 
    } 
} 

// Driver code 
int main() 
{ 

    // Start with the empty list 
    Node* head = NULL; 

    // Created Linked list is 
    // 1->2->3->4->5->6->7->8->9 
    push(&head, 9); 
    push(&head, 8); 
    push(&head, 7); 
    push(&head, 6); 
    push(&head, 5); 
    push(&head, 4); 
    push(&head, 3); 
    push(&head, 2); 
    push(&head, 1); 

    int k = 3; 

    cout << "Given linked list \n"; 
    printList(head); 
    head = reverse(head, k); 

    cout << "\nReversed Linked list \n"; 
    printList(head); 

    return (0); 
} 

```

## 爪哇

```

// Java implementation of the approach  
class GFG 
{ 

// Link list node  
static class Node  
{  
    int data;  
    Node next;  
};  

// Function to reverse the linked list in groups of  
//size k and return the pointer to the new head node. / 
static Node reverse( Node head, int k)  
{  
    Node prev = null;  
    Node curr = head;  
    Node temp = null;  
    Node tail = null;  
    Node newHead = null;  
    Node join = null;  
    int t = 0;  

    // Traverse till the end of the linked list  
    while (curr != null)  
    {  
        t = k;  
        join = curr;  
        prev = null;  

        // Reverse group of k nodes of the linked list  
        while (curr != null && t-- != 0) 
        {  
            temp = curr.next;  
            curr.next = prev;  
            prev = curr;  
            curr = temp;  
        }  

        // Sets the new head of the input list  
        if ((newHead == null))  
            newHead = prev;  

        /* Tail pointer keeps track of the last node  
        of the k-reversed linked list. We join the  
        tail pointer with the head of the next  
        k-reversed linked list's head */
        if (tail != null)  
            tail.next = prev;  

        /* The tail is then updated to the last node  
        of the next k-reverse linked list */
        tail = join;  
    }  

    // newHead is new head of the input list / 
    return newHead;  
}  

// Function to insert a node at  
// the head of the linked list  
static Node push(Node head_ref, int new_data)  
{  
    // allocate node / 
    Node new_node = new Node();  

    // put in the data / 
    new_node.data = new_data;  

    // link the old list off the new node / 
    new_node.next = (head_ref);  

    // move the head to point to the new node / 
    (head_ref) = new_node; 
    return head_ref; 
}  

// Function to print the linked list  
static void printList(Node node)  
{  
    while (node != null)  
    {  
        System.out.print( node.data + " ");  
        node = node.next;  
    }  
}  

// Driver code  
public static void main(String args[]) 
{  

    // Start with the empty list  
    Node head = null;  

    // Created Linked list is  
    // 1.2.3.4.5.6.7.8.9  
    head = push(head, 9);  
    head = push(head, 8);  
    head = push(head, 7);  
    head = push(head, 6);  
    head = push(head, 5);  
    head = push(head, 4);  
    head = push(head, 3);  
    head = push(head, 2);  
    head = push(head, 1);  

    int k = 3;  

    System.out.print( "Given linked list \n");  
    printList(head);  
    head = reverse(head, k);  

    System.out.print( "\nReversed Linked list \n");  
    printList(head);  
} 
}  

// This code is contributed by Arnab Kundu 

```

## Python3

```

# Python3 implementation of the approach  
import math 

# Link list node  
class Node:  
    def __init__(self, data):  
        self.data = data  
        self.next = None

# Function to reverse the linked list in groups of  
#size k and return the poer to the new head node.  
def reverse(head, k) :  
    prev = None
    curr = head  
    temp = None
    tail = None
    newHead = None
    join = None
    t = 0

    # Traverse till the end of the linked list  
    while (curr) :  
        t = k  
        join = curr  
        prev = None

        # Reverse group of k nodes of the linked list  
        while (curr and t > 0): 
            temp = curr.next
            curr.next = prev 
            prev = curr 
            curr = temp 
            t = t - 1

        # Sets the new head of the input list  
        if (newHead == None):  
            newHead = prev  

        # Tail pointer keeps track of the last node  
        # of the k-reversed linked list. We join the  
        # tail poer with the head of the next  
        # k-reversed linked list's head  
        if (tail != None):  
            tail.next = prev  

        # The tail is then updated to the last node  
        # of the next k-reverse linked list  
        tail = join  

    # newHead is new head of the input list */ 
    return newHead  

# Function to insert a node at  
# the head of the linked list  
def push(head_ref, new_data) :  

    # allocate node */ 
    new_node =Node(new_data)  

    # put in the data */ 
    new_node.data = new_data  

    # link the old list off the new node */ 
    new_node.next = head_ref 

    # move the head to po to the new node */ 
    head_ref = new_node 
    return head_ref 

# Function to print the linked list  
def prList(node):  
    while (node != None) :  
        print(node.data, end = " ")  
        node = node.next

# Driver code  
if __name__=='__main__': 

    # Start with the empty list  
    head = None

    # Created Linked list is  
    # 1.2.3.4.5.6.7.8.9  
    head = push(head, 9) 
    head = push(head, 8) 
    head = push(head, 7) 
    head = push(head, 6) 
    head = push(head, 5) 
    head = push(head, 4) 
    head = push(head, 3) 
    head = push(head, 2) 
    head = push(head, 1)  

    k = 3

    print("Given linked list ")  
    prList(head)  
    head = reverse(head, k)  

    print("\nReversed Linked list ")  
    prList(head)  

# This code is contributed by Srathore 

```

## C＃

```

// C# implementation of the approach  
using System; 

class GFG 
{ 

// Link list node  
public class Node  
{  
    public int data;  
    public Node next;  
};  

// Function to reverse the linked list in groups of  
//size k and return the pointer to the new head node. / 
static Node reverse( Node head, int k)  
{  
    Node prev = null;  
    Node curr = head;  
    Node temp = null;  
    Node tail = null;  
    Node newHead = null;  
    Node join = null;  
    int t = 0;  

    // Traverse till the end of the linked list  
    while (curr != null)  
    {  
        t = k;  
        join = curr;  
        prev = null;  

        // Reverse group of k nodes of the linked list  
        while (curr != null && t-- != 0) 
        {  
            temp = curr.next;  
            curr.next = prev;  
            prev = curr;  
            curr = temp;  
        }  

        // Sets the new head of the input list  
        if ((newHead == null))  
            newHead = prev;  

        /* Tail pointer keeps track of the last node  
        of the k-reversed linked list. We join the  
        tail pointer with the head of the next  
        k-reversed linked list's head */
        if (tail != null)  
            tail.next = prev;  

        /* The tail is then updated to the last node  
        of the next k-reverse linked list */
        tail = join;  
    }  

    // newHead is new head of the input list / 
    return newHead;  
}  

// Function to insert a node at  
// the head of the linked list  
static Node push(Node head_ref, int new_data)  
{  
    // allocate node / 
    Node new_node = new Node();  

    // put in the data / 
    new_node.data = new_data;  

    // link the old list off the new node / 
    new_node.next = (head_ref);  

    // move the head to point to the new node / 
    (head_ref) = new_node; 
    return head_ref; 
}  

// Function to print the linked list  
static void printList(Node node)  
{  
    while (node != null)  
    {  
        Console.Write( node.data + " ");  
        node = node.next;  
    }  
}  

// Driver code  
public static void Main(String []args) 
{  

    // Start with the empty list  
    Node head = null;  

    // Created Linked list is  
    // 1.2.3.4.5.6.7.8.9  
    head = push(head, 9);  
    head = push(head, 8);  
    head = push(head, 7);  
    head = push(head, 6);  
    head = push(head, 5);  
    head = push(head, 4);  
    head = push(head, 3);  
    head = push(head, 2);  
    head = push(head, 1);  

    int k = 3;  

    Console.Write( "Given linked list \n");  
    printList(head);  
    head = reverse(head, k);  

    Console.Write( "\nReversed Linked list \n");  
    printList(head);  
} 
}  

// This code is contributed by 29AjayKumar 

```

**Output:**

```
Given linked list 
1 2 3 4 5 6 7 8 9 
Reversed Linked list 
3 2 1 6 5 4 9 8 7

```

**时间复杂度：** O（n），其中n是给定列表中的节点数。
**空间复杂度：** O（1）

注意读者！ 现在不要停止学习。 通过 [**DSA自学课程**](https://practice.geeksforgeeks.org/courses/dsa-self-paced?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_dsa_content_bottom) 以对学生方便的价格掌握所有重要的DSA概念，并为行业做好准备。

* * *

* * *

如果您喜欢GeeksforGeeks并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至tribution@geeksforgeeks.org。 查看您的文章出现在GeeksforGeeks主页上，并帮助其他Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。