# 通过更改链接对 0、1、2 和 2 的链接列表进行排序

给定一个链接列表 0、1 和 2，对其进行排序。

**示例：**

```
Input  : 2->1->2->1->1->2->0->1->0
Output : 0->0->1->1->1->1->2->2->2
The sorted Array is 0, 0, 1, 1, 1, 1, 2, 2, 2.

Input : 2->1->0
Output : 0->1->2
The sorted Array is 0, 1, 2

```

<u>**方法 1：**</u> 在下面的文章中讨论了一种解决方案，该解决方案通过更改节点的数据来工作。
[对 0、1、2 和 2 的链接列表进行排序](https://www.geeksforgeeks.org/sort-a-linked-list-of-0s-1s-or-2s/)

当这些值与它们相关联的数据时，上述解决方案不起作用。
*例如，*这三个代表三种颜色以及与该颜色关联的不同类型的对象，并根据颜色对这些对象（与链接列表相连）进行排序。

**<u>方法 2</u> ：**在本文中，将讨论通过更改链接来工作的新解决方案。

**方法：**迭代链接列表。 维护 3 个名为零的指针，一个和两个指针分别指向链接列表的当前结尾节点，该链接列表分别包含 0、1 和 2。 对于每个遍历的节点，我们将其附加到其对应列表的末尾。 最后，我们链接所有三个列表。 为了避免许多空检查，我们使用三个伪指针 zeroD，oneD 和 twoD 作为三个列表的伪头。

## C++

```cpp

// CPP Program to sort a linked list 0s, 1s 
// or 2s by changing links 
#include <bits/stdc++.h> 

/* Link list node */
struct Node { 
    int data; 
    struct Node* next; 
}; 

Node* newNode(int data); 

// Sort a linked list of 0s, 1s and 2s 
// by changing pointers. 
Node* sortList(Node* head) 
{ 
    if (!head || !(head->next)) 
        return head; 

    // Create three dummy nodes to point to 
    // beginning of three linked lists. These 
    // dummy nodes are created to avoid many 
    // null checks. 
    Node* zeroD = newNode(0); 
    Node* oneD = newNode(0); 
    Node* twoD = newNode(0); 

    // Initialize current pointers for three 
    // lists and whole list. 
    Node* zero = zeroD, *one = oneD, *two = twoD; 

    // Traverse list 
    Node* curr = head; 
    while (curr) { 
        if (curr->data == 0) { 
            zero->next = curr; 
            zero = zero->next; 
            curr = curr->next; 
        } else if (curr->data == 1) { 
            one->next = curr; 
            one = one->next; 
            curr = curr->next; 
        } else { 
            two->next = curr; 
            two = two->next; 
            curr = curr->next; 
        } 
    } 

    // Attach three lists 
    zero->next = (oneD->next)  
? (oneD->next) : (twoD->next); 
    one->next = twoD->next; 
    two->next = NULL; 

    // Updated head 
    head = zeroD->next; 

    // Delete dummy nodes 
    delete zeroD; 
    delete oneD; 
    delete twoD; 

    return head; 
} 

// Function to create and return a node 
Node* newNode(int data) 
{ 
    // allocating space 
    Node* newNode = new Node; 

    // inserting the required data 
    newNode->data = data; 
    newNode->next = NULL; 
} 

/* Function to print linked list */
void printList(struct Node* node) 
{ 
    while (node != NULL) { 
        printf("%d  ", node->data); 
        node = node->next; 
    } 
    printf("\n"); 
} 

/* Driver program to test above function*/
int main(void) 
{ 
    // Creating the list 1->2->4->5 
    Node* head = newNode(1); 
    head->next = newNode(2); 
    head->next->next = newNode(0); 
    head->next->next->next = newNode(1); 

    printf("Linked List Before Sorting\n"); 
    printList(head); 

    head = sortList(head); 

    printf("Linked List After Sorting\n"); 
    printList(head); 

    return 0; 
} 

```

## Java

```java

// Java Program to sort a linked list 0s, 1s  
// or 2s by changing links  
public class Sort012 { 

    // Sort a linked list of 0s, 1s and 2s  
    // by changing pointers. 
    public static Node sortList(Node head) 
    { 
        if(head==null || head.next==null) 
        { 
            return head; 
        } 
        // Create three dummy nodes to point to  
        // beginning of three linked lists. These  
        // dummy nodes are created to avoid many  
        // null checks.  
        Node zeroD = new Node(0);  
        Node oneD = new Node(0);  
        Node twoD = new Node(0);  

        // Initialize current pointers for three  
        // lists and whole list.  
        Node zero = zeroD, one = oneD, two = twoD;  
        // Traverse list  
        Node curr = head;  
        while (curr!=null)  
        {  
            if (curr.data == 0)  
            {  
                zero.next = curr;  
                zero = zero.next;  
                curr = curr.next;  
            } 
            else if (curr.data == 1)  
            {  
                one.next = curr;  
                one = one.next;  
                curr = curr.next;  
            }  
            else 
            {  
                two.next = curr;  
                two = two.next;  
                curr = curr.next;  
            }  
        } 
        // Attach three lists  
        zero.next = (oneD.next!=null)  
? (oneD.next) : (twoD.next);  
        one.next = twoD.next;  
        two.next = null; 
        // Updated head  
        head = zeroD.next; 
        return head; 
    } 

    // function to create and return a node  
    public static Node newNode(int data)  
    {  
        // allocating space  
        Node newNode = new Node(data); 
        newNode.next = null;  
        return newNode; 
    }  

    /* Function to print linked list */
    public static void printList(Node node)  
    {  
        while (node != null)  
        {  
            System.out.print(node.data+" "); 
            node = node.next;  
        }  
    } 

    public static void main(String args[]) { 
        Node head = new Node(1);  
        head.next = new Node(2);  
        head.next.next = new Node(0);  
        head.next.next.next = new Node(1); 
        System.out.println(" 
Linked List Before Sorting"); 
        printList(head);  
        head = sortList(head);   
        System.out.println(" 
\nLinked List After Sorting"); 
        printList(head);  
    } 
} 

class Node 
{ 
    int data; 
    Node next; 
    Node(int data) 
    { 
        this.data=data; 
    } 
} 
//This code is contributed by Gaurav Tiwari 

```

## Python3

```py

# Python3 Program to sort a linked list  
# 0s, 1s or 2s by changing links 
import math 

# Link list node  
class Node:  
    def __init__(self, data):  
        self.data = data  
        self.next = None

#Node* newNode( data) 

# Sort a linked list of 0s, 1s and 2s 
# by changing poers. 
def sortList(head): 
    if (head == None or 
        head.next == None): 
        return head 

    # Create three dummy nodes to point to 
    # beginning of three linked lists.  
    # These dummy nodes are created to  
    # avoid many None checks. 
    zeroD = Node(0) 
    oneD = Node(0) 
    twoD = Node(0) 

    # Initialize current pointers for three 
    # lists and whole list. 
    zero = zeroD  
    one = oneD  
    two = twoD 

    # Traverse list 
    curr = head 
    while (curr): 
        if (curr.data == 0): 
            zero.next = curr 
            zero = zero.next
            curr = curr.next
        elif(curr.data == 1): 
            one.next = curr 
            one = one.next
            curr = curr.next
        else: 
            two.next = curr 
            two = two.next
            curr = curr.next

    # Attach three lists 
    zero.next = (oneD.next) if (oneD.next ) \ 
                            else (twoD.next) 
    one.next = twoD.next
    two.next = None

    # Updated head 
    head = zeroD.next

    # Delete dummy nodes 
    return head 

# function to create and return a node 
def newNode(data): 

    # allocating space 
    newNode = Node(data) 

    # inserting the required data 
    newNode.data = data 
    newNode.next = None
    return newNode 

# Function to print linked list  
def prList(node): 
    while (node != None): 
        print(node.data, end = " ") 
        node = node.next

# Driver Code 
if __name__=='__main__': 

    # Creating the list 1.2.4.5 
    head = newNode(1) 
    head.next = newNode(2) 
    head.next.next = newNode(0) 
    head.next.next.next = newNode(1) 

    print("Linked List Before Sorting") 
    prList(head) 

    head = sortList(head) 

    print("\nLinked List After Sorting") 
    prList(head) 

# This code is contributed by Srathore 

```

## C#

```cs

// C# Program to sort a linked list 0s, 1s  
// or 2s by changing links  
using System; 

public class Sort012 
{ 

    // Sort a linked list of 0s, 1s and 2s  
    // by changing pointers. 
    public static Node sortList(Node head) 
    { 
        if(head == null || head.next == null) 
        { 
            return head; 
        } 
        // Create three dummy nodes to point to  
        // beginning of three linked lists. These  
        // dummy nodes are created to avoid many  
        // null checks.  
        Node zeroD = new Node(0);  
        Node oneD = new Node(0);  
        Node twoD = new Node(0);  

        // Initialize current pointers for three  
        // lists and whole list.  
        Node zero = zeroD, one = oneD, two = twoD;  
        // Traverse list  
        Node curr = head;  
        while (curr != null)  
        {  
            if (curr.data == 0)  
            {  
                zero.next = curr;  
                zero = zero.next;  
                curr = curr.next;  
            } 
            else if (curr.data == 1)  
            {  
                one.next = curr;  
                one = one.next;  
                curr = curr.next;  
            }  
            else
            {  
                two.next = curr;  
                two = two.next;  
                curr = curr.next;  
            }  
        } 

        // Attach three lists  
        zero.next = (oneD.next != null)  
? (oneD.next) : (twoD.next);  
        one.next = twoD.next;  
        two.next = null; 

        // Updated head  
        head = zeroD.next; 
        return head; 
    } 

    // function to create and return a node  
    public static Node newNode(int data)  
    {  
        // allocating space  
        Node newNode = new Node(data); 
        newNode.next = null;  
        return newNode; 
    }  

    /* Function to print linked list */
    public static void printList(Node node)  
    {  
        while (node != null)  
        {  
            Console.Write(node.data + " "); 
            node = node.next;  
        }  
    } 

    // Driver code 
    public static void Main() 
    { 
        Node head = new Node(1);  
        head.next = new Node(2);  
        head.next.next = new Node(0);  
        head.next.next.next = new Node(1); 
        Console.WriteLine("Linked List Before Sorting"); 
        printList(head);  
        head = sortList(head);  
        Console.WriteLine("\nLinked List After Sorting"); 
        printList(head);  
    } 
} 

public class Node 
{ 
    public int data; 
    public Node next; 
    public Node(int data) 
    { 
        this.data = data; 
    } 
} 

// This code is contributed by PrinciRaj1992 

```

**Output :**

```
Linked List Before Sorting
1  2  0  1  
Linked List After Sorting
0  1  1  2  
```

**复杂度分析：**

*   **时间复杂度：** O（n），其中 n 是链表中的节点数。
    只需遍历链接列表。
*   **辅助空间：** O（1）。
    由于不需要额外的空间。

感谢 Musarrat_123 在此处的评论[中建议上述解决方案。](https://www.geeksforgeeks.org/sort-a-linked-list-of-0s-1s-or-2s/)

本文由 **Bhaskar Kumar Mishra** 提供。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请发表评论。

