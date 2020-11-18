# 从末尾

的第n个节点后插入一个节点

在给定的单链列表中从末尾的**第n个**节点之后插入节点 **x** 。 确保列表从末尾包含第**个第**个节点。 另外1 < = n。

例子：

```
Input : list: 1->3->4->5
        n = 4, x = 2
Output : 1->2->3->4->5
4th node from the end is 1 and
insertion has been done after this node.

Input : list: 10->8->3->12->5->18
        n = 2, x = 11
Output : 10->8->3->12->5->11->18

```

**方法1（使用列表的长度）：**
查找链接列表的长度，即列表中的节点数。 设为**等于**。 现在从头开始遍历列表，从第一个节点到第**（len-n + 1）个**节点，然后在该节点之后插入新节点。 此方法需要两次遍历列表。

## C++

```cpp

// C++ implementation to insert a node after 
// the n-th node from the end 
#include <bits/stdc++.h> 
using namespace std; 

// structure of a node 
struct Node { 
    int data; 
    Node* next; 
}; 

// function to get a new node 
Node* getNode(int data) 
{ 
    // allocate memory for the node 
    Node* newNode = (Node*)malloc(sizeof(Node)); 

    // put in the data 
    newNode->data = data; 
    newNode->next = NULL; 
    return newNode; 
} 

// function to insert a node after the 
// nth node from the end 
void insertAfterNthNode(Node* head, int n, int x) 
{ 
    // if list is empty 
    if (head == NULL) 
        return; 

    // get a new node for the value 'x' 
    Node* newNode = getNode(x); 
    Node* ptr = head; 
    int len = 0, i; 

    // find length of the list, i.e, the 
    // number of nodes in the list 
    while (ptr != NULL) { 
        len++; 
        ptr = ptr->next; 
    } 

    // traverse up to the nth node from the end 
    ptr = head; 
    for (i = 1; i <= (len - n); i++) 
        ptr = ptr->next; 

    // insert the 'newNode' by making the 
    // necessary adjustment in the links 
    newNode->next = ptr->next; 
    ptr->next = newNode; 
} 

// function to print the list 
void printList(Node* head) 
{ 
    while (head != NULL) { 
        cout << head->data << " "; 
        head = head->next; 
    } 
} 

// Driver program to test above 
int main() 
{ 
    // Creating list 1->3->4->5 
    Node* head = getNode(1); 
    head->next = getNode(3); 
    head->next->next = getNode(4); 
    head->next->next->next = getNode(5); 

    int n = 4, x = 2; 

    cout << "Original Linked List: "; 
    printList(head); 

    insertAfterNthNode(head, n, x); 

    cout << "\nLinked List After Insertion: "; 
    printList(head); 

    return 0; 
} 

```

## Java

```java

// Java implementation to insert a node after  
// the n-th node from the end  
class GfG  
{ 

// structure of a node  
static class Node  
{  
    int data;  
    Node next;  
} 

// function to get a new node  
static Node getNode(int data)  
{  
    // allocate memory for the node  
    Node newNode = new Node();  

    // put in the data  
    newNode.data = data;  
    newNode.next = null;  
    return newNode;  
}  

// function to insert a node after the  
// nth node from the end  
static void insertAfterNthNode(Node head, int n, int x)  
{  
    // if list is empty  
    if (head == null)  
        return;  

    // get a new node for the value 'x'  
    Node newNode = getNode(x);  
    Node ptr = head;  
    int len = 0, i;  

    // find length of the list, i.e, the  
    // number of nodes in the list  
    while (ptr != null)  
    {  
        len++;  
        ptr = ptr.next;  
    }  

    // traverse up to the nth node from the end  
    ptr = head;  
    for (i = 1; i <= (len - n); i++)  
        ptr = ptr.next;  

    // insert the 'newNode' by making the  
    // necessary adjustment in the links  
    newNode.next = ptr.next;  
    ptr.next = newNode;  
}  

// function to print the list  
static void printList(Node head)  
{  
    while (head != null) 
    {  
        System.out.print(head.data + " ");  
        head = head.next;  
    }  
}  

// Driver code  
public static void main(String[] args)  
{  
    // Creating list 1->3->4->5  
    Node head = getNode(1);  
    head.next = getNode(3);  
    head.next.next = getNode(4);  
    head.next.next.next = getNode(5);  

    int n = 4, x = 2;  

    System.out.print("Original Linked List: ");  
    printList(head);  

    insertAfterNthNode(head, n, x);  
    System.out.println(); 
    System.out.print("Linked List After Insertion: ");  
    printList(head);  
} 
}  

// This code is contributed by prerna saini 

```

## 蟒蛇

```

# Python implementation to insert a node after  
# the n-th node from the end  

# Linked List node  
class Node:  
    def __init__(self, data):  
        self.data = data  
        self.next = None

# function to get a new node  
def getNode(data) : 

    # allocate memory for the node  
    newNode = Node(0)  

    # put in the data  
    newNode.data = data  
    newNode.next = None
    return newNode  

# function to insert a node after the  
# nth node from the end  
def insertAfterNthNode(head, n, x) : 

    # if list is empty  
    if (head == None) : 
        return

    # get a new node for the value 'x'  
    newNode = getNode(x)  
    ptr = head  
    len = 0
    i = 0

    # find length of the list, i.e, the  
    # number of nodes in the list  
    while (ptr != None) : 

        len = len + 1
        ptr = ptr.next

    # traverse up to the nth node from the end  
    ptr = head  
    i = 1
    while ( i <= (len - n) ) : 
        ptr = ptr.next
        i = i + 1

    # insert the 'newNode' by making the  
    # necessary adjustment in the links  
    newNode.next = ptr.next
    ptr.next = newNode  

# function to print the list  
def printList( head) : 

    while (head != None): 

        print(head.data ,end = " ")  
        head = head.next

# Driver code  

# Creating list 1->3->4->5  
head = getNode(1)  
head.next = getNode(3)  
head.next.next = getNode(4)  
head.next.next.next = getNode(5)  

n = 4
x = 2

print("Original Linked List: ")  
printList(head)  

insertAfterNthNode(head, n, x)  
print() 
print("Linked List After Insertion: ")  
printList(head)  

# This code is contributed by Arnab Kundu 

```

## C#

```cs

// C# implementation to insert a node after  
// the n-th node from the end  
using System; 

class GfG  
{ 

// structure of a node  
public class Node  
{  
    public int data;  
    public Node next;  
} 

// function to get a new node  
static Node getNode(int data)  
{  
    // allocate memory for the node  
    Node newNode = new Node();  

    // put in the data  
    newNode.data = data;  
    newNode.next = null;  
    return newNode;  
}  

// function to insert a node after the  
// nth node from the end  
static void insertAfterNthNode(Node head, int n, int x)  
{  
    // if list is empty  
    if (head == null)  
        return;  

    // get a new node for the value 'x'  
    Node newNode = getNode(x);  
    Node ptr = head;  
    int len = 0, i;  

    // find length of the list, i.e, the  
    // number of nodes in the list  
    while (ptr != null)  
    {  
        len++;  
        ptr = ptr.next;  
    }  

    // traverse up to the nth node from the end  
    ptr = head;  
    for (i = 1; i <= (len - n); i++)  
        ptr = ptr.next;  

    // insert the 'newNode' by making the  
    // necessary adjustment in the links  
    newNode.next = ptr.next;  
    ptr.next = newNode;  
}  

// function to print the list  
static void printList(Node head)  
{  
    while (head != null) 
    {  
        Console.Write(head.data + " ");  
        head = head.next;  
    }  
}  

// Driver code  
public static void Main(String[] args)  
{  
    // Creating list 1->3->4->5  
    Node head = getNode(1);  
    head.next = getNode(3);  
    head.next.next = getNode(4);  
    head.next.next.next = getNode(5);  

    int n = 4, x = 2;  

    Console.Write("Original Linked List: ");  
    printList(head);  

    insertAfterNthNode(head, n, x);  
    Console.WriteLine(); 
    Console.Write("Linked List After Insertion: ");  
    printList(head);  
} 
}  

// This code has been contributed by 29AjayKumar 

```

**Output:**

```
Original Linked List: 1 3 4 5
Linked List After Insertion: 1 2 3 4 5

```

**时间复杂度：** O（n），其中 **n** 是列表中节点的数量。

**方法2（单遍历）：**
该方法使用两个指针，一个是 **slow_ptr** ，另一个是 **fast_ptr** 。 首先从头开始将 **fast_ptr** 移到第**个第**个节点。 使 **slow_ptr** 指向列表的第一个节点。 现在，同时移动两个指针，直到 **fast_ptr** 指向最后一个节点。 此时， **slow_ptr** 将从末尾指向第**个第**个节点。 在该节点之后插入新节点。 此方法需要单遍遍列表。

## C++

```cpp

// C++ implementation to insert a node after the 
// nth node from the end 
#include <bits/stdc++.h> 

using namespace std; 

// structure of a node 
struct Node { 
    int data; 
    Node* next; 
}; 

// function to get a new node 
Node* getNode(int data) 
{ 
    // allocate memory for the node 
    Node* newNode = (Node*)malloc(sizeof(Node)); 

    // put in the data 
    newNode->data = data; 
    newNode->next = NULL; 
    return newNode; 
} 

// function to insert a node after the 
// nth node from the end 
void insertAfterNthNode(Node* head, int n, int x) 
{ 
    // if list is empty 
    if (head == NULL) 
        return; 

    // get a new node for the value 'x' 
    Node* newNode = getNode(x); 

    // Initializing the slow and fast pointers 
    Node* slow_ptr = head; 
    Node* fast_ptr = head; 

    // move 'fast_ptr' to point to the nth node 
    // from the beginning 
    for (int i = 1; i <= n - 1; i++) 
        fast_ptr = fast_ptr->next; 

    // iterate until 'fast_ptr' points to the 
    // last node 
    while (fast_ptr->next != NULL) { 

        // move both the pointers to the 
        // respective next nodes 
        slow_ptr = slow_ptr->next; 
        fast_ptr = fast_ptr->next; 
    } 

    // insert the 'newNode' by making the 
    // necessary adjustment in the links 
    newNode->next = slow_ptr->next; 
    slow_ptr->next = newNode; 
} 

// function to print the list 
void printList(Node* head) 
{ 
    while (head != NULL) { 
        cout << head->data << " "; 
        head = head->next; 
    } 
} 

// Driver program to test above 
int main() 
{ 
    // Creating list 1->3->4->5 
    Node* head = getNode(1); 
    head->next = getNode(3); 
    head->next->next = getNode(4); 
    head->next->next->next = getNode(5); 

    int n = 4, x = 2; 

    cout << "Original Linked List: "; 
    printList(head); 

    insertAfterNthNode(head, n, x); 

    cout << "\nLinked List After Insertion: "; 
    printList(head); 

    return 0; 
} 

```

## Java

```java

// Java implementation to  
// insert a node after the  
// nth node from the end  
class GfG 
{  

// structure of a node  
static class Node  
{  
    int data;  
    Node next;  
} 

// function to get a new node  
static Node getNode(int data)  
{  
    // allocate memory for the node  
    Node newNode = new Node();  

    // put in the data  
    newNode.data = data;  
    newNode.next = null;  
    return newNode;  
}  

// function to insert a node after  
// the nth node from the end  
static void insertAfterNthNode(Node head,  
                            int n, int x)  
{  
    // if list is empty  
    if (head == null)  
        return;  

    // get a new node for the value 'x'  
    Node newNode = getNode(x);  

    // Initializing the slow  
    // and fast pointers  
    Node slow_ptr = head;  
    Node fast_ptr = head;  

    // move 'fast_ptr' to point to the  
    // nth node from the beginning  
    for (int i = 1; i <= n - 1; i++)  
        fast_ptr = fast_ptr.next;  

    // iterate until 'fast_ptr' points   
    // to the last node  
    while (fast_ptr.next != null) 
    {  

        // move both the pointers to the  
        // respective next nodes  
        slow_ptr = slow_ptr.next;  
        fast_ptr = fast_ptr.next;  
    }  

    // insert the 'newNode' by making the  
    // necessary adjustment in the links  
    newNode.next = slow_ptr.next;  
    slow_ptr.next = newNode;  
}  

// function to print the list  
static void printList(Node head)  
{  
    while (head != null)  
    {  
        System.out.print(head.data + " ");  
        head = head.next;  
    }  
}  

// Driver code  
public static void main(String[] args)  
{  
    // Creating list 1->3->4->5  
    Node head = getNode(1);  
    head.next = getNode(3);  
    head.next.next = getNode(4);  
    head.next.next.next = getNode(5);  

    int n = 4, x = 2;  
    System.out.println("Original Linked List: ");  
    printList(head);  

    insertAfterNthNode(head, n, x);  
    System.out.println(); 
    System.out.println("Linked List After Insertion: ");  
    printList(head);  
} 
}  

// This code is contributed by 
// Prerna Saini. 

```

## C#

```cs

// C# implementation to  
// insert a node after the  
// nth node from the end  
using System; 

class GfG 
{  

    // structure of a node  
    public class Node  
    {  
        public int data;  
        public Node next;  
    } 

    // function to get a new node  
    static Node getNode(int data)  
    {  
        // allocate memory for the node  
        Node newNode = new Node();  

        // put in the data  
        newNode.data = data;  
        newNode.next = null;  
        return newNode;  
    }  

    // function to insert a node after  
    // the nth node from the end  
    static void insertAfterNthNode(Node head,  
                                int n, int x)  
    {  
        // if list is empty  
        if (head == null)  
            return;  

        // get a new node for the value 'x'  
        Node newNode = getNode(x);  

        // Initializing the slow  
        // and fast pointers  
        Node slow_ptr = head;  
        Node fast_ptr = head;  

        // move 'fast_ptr' to point to the  
        // nth node from the beginning  
        for (int i = 1; i <= n - 1; i++)  
            fast_ptr = fast_ptr.next;  

        // iterate until 'fast_ptr' points  
        // to the last node  
        while (fast_ptr.next != null) 
        {  

            // move both the pointers to the  
            // respective next nodes  
            slow_ptr = slow_ptr.next;  
            fast_ptr = fast_ptr.next;  
        }  

        // insert the 'newNode' by making the  
        // necessary adjustment in the links  
        newNode.next = slow_ptr.next;  
        slow_ptr.next = newNode;  
    }  

    // function to print the list  
    static void printList(Node head)  
    {  
        while (head != null)  
        {  
            Console.Write(head.data + " ");  
            head = head.next;  
        }  
    }  

    // Driver code  
    public static void Main()  
    {  
        // Creating list 1->3->4->5  
        Node head = getNode(1);  
        head.next = getNode(3);  
        head.next.next = getNode(4);  
        head.next.next.next = getNode(5);  

        int n = 4, x = 2;  
        Console.WriteLine("Original Linked List: ");  
        printList(head);  

        insertAfterNthNode(head, n, x);  
        Console.WriteLine(); 
        Console.WriteLine("Linked List After Insertion: ");  
        printList(head);  
    } 
} 

/* This code contributed by PrinciRaj1992 */

```

**Output:**

```
Original Linked List: 1 3 4 5
Linked List After Insertion: 1 2 3 4 5

```

**时间复杂度：** O（n），其中 **n** 是列表中节点的数量。

本文由 **Ayush Jauhari** 提供。 如果您喜欢GeeksforGeeks并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至tribution@geeksforgeeks.org。 查看您的文章出现在GeeksforGeeks主页上，并帮助其他Geeks。

如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请发表评论。

