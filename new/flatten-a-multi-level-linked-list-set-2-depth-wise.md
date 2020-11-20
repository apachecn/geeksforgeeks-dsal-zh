# 展平多级链表 | 系列 2（深度方式）

> 原文：[https://www.geeksforgeeks.org/flatten-a-multi-level-linked-list-set-2-depth-wise/](https://www.geeksforgeeks.org/flatten-a-multi-level-linked-list-set-2-depth-wise/)

我们已经讨论了多级链表的[扁平化，其中节点具有向下和向后两个指针。 在上一篇文章中，我们明智地扁平化了链表。 当我们总是需要在每个节点上的下一个指针之前处理指针时，如何展平链表。](https://www.geeksforgeeks.org/flatten-a-linked-list-with-next-and-child-pointers/)

```
Input:  
1 - 2 - 3 - 4
    |
    7 -  8 - 10 - 12
    |    |    |
    9    16   11
    |    |
    14   17 - 18 - 19 - 20
    |                    |
    15 - 23             21
         |
         24

Output:        
Linked List to be flattened to
1 - 2 - 7 - 9 - 14 - 15 - 23 - 24 - 8
 - 16 - 17 - 18 - 19 - 20 - 21 - 10 - 
11 - 12 - 3 - 4
Note : 9 appears before 8 (When we are 
at a node, we process down pointer before 
right pointer)    

```

资料来源：Oracle 专访

如果仔细观察，我们会发现此问题类似于[树到链表的转换](https://www.geeksforgeeks.org/convert-given-binary-tree-doubly-linked-list-set-3/)。 我们通过以下步骤递归地展平链表。

**1）**如果节点为 NULL，则返回 NULL。

**2）**存储当前节点的下一个节点（在步骤 4 中使用）。

**3）**递归拉平列表。 展平时，请跟踪上一个访问的节点，以便可以在其后链接下一个列表。

**4）**递归展平下一个列表（我们从步骤 2 中存储的指针中获取下一个列表），并将其附加在上次访问的节点之后。

以下是上述想法的实现。

## C++

```cpp

// C++ program to flatten a multilevel linked list 
#include <bits/stdc++.h> 
using namespace std; 

// A Linked List Node 
struct Node 
{ 
    int data; 
    struct Node *next; 
    struct Node *down; 
}; 

// Flattens a multi-level linked list depth wise 
Node* flattenList(Node* node) 
{ 
    // Base case 
    if (node == NULL) 
        return NULL; 

    // To keep track of last visited node 
    // (NOTE: This is static) 
    static Node *last; 
    last = node; 

    // Store next pointer 
    Node *next = node->next; 

    // If down list exists, process it first 
    // Add down list as next of current node 
    if (node->down) 
       node->next = flattenList(node->down); 

    // If next exists, add it after the next 
    // of last added node 
    if (next) 
       last->next = flattenList(next); 

    return node; 
} 

// Utility method to print a linked list 
void printFlattenNodes(Node* head) 
{ 
    while (head)  
    {  
    printf("%d ", head->data);  
    head = head->next;  
    }  

} 

// Utility function to create a new node 
Node* newNode(int new_data) 
{ 
    Node* new_node = new Node; 
    new_node->data = new_data; 
    new_node->next = new_node->down = NULL; 
    return new_node; 
} 

// Driver code 
int main() 
{ 
    // Creating above example list 
    Node* head = newNode(1); 
    head->next = newNode(2); 
    head->next->next = newNode(3); 
    head->next->next->next = newNode(4); 
    head->next->down = newNode(7); 
    head->next->down->down = newNode(9); 
    head->next->down->down->down = newNode(14); 
    head->next->down->down->down->down 
                                     = newNode(15); 
    head->next->down->down->down->down->next 
                                     = newNode(23); 
    head->next->down->down->down->down->next->down 
                                      = newNode(24); 
    head->next->down->next = newNode(8); 
    head->next->down->next->down = newNode(16); 
    head->next->down->next->down->down = newNode(17); 
    head->next->down->next->down->down->next 
                                      = newNode(18); 
    head->next->down->next->down->down->next->next 
                                      = newNode(19); 
    head->next->down->next->down->down->next->next->next 
                                      = newNode(20); 
    head->next->down->next->down->down->next->next->next->down 
                                      = newNode(21); 
    head->next->down->next->next = newNode(10); 
    head->next->down->next->next->down = newNode(11); 

    head->next->down->next->next->next = newNode(12); 

    // Flatten list and print modified list 
    head = flattenList(head); 
    printFlattenNodes(head); 

    return 0; 
} 

```

## Java

```java

// Java program to flatten a multilevel linked list 
public class FlattenList { 

    static Node last; 

    // Flattens a multi-level linked list depth wise  
    public static Node flattenList(Node node) 
    { 
        if(node==null)  
            return null;  

        // To keep track of last visited node  
        // (NOTE: This is static)   
        last = node;  

        // Store next pointer  
        Node next = node.next;  

        // If down list exists, process it first  
        // Add down list as next of current node  
        if(node.down!=null)  
            node.next = flattenList(node.down);  

        // If next exists, add it after the next  
        // of last added node  
        if(next!=null)  
            last.next = flattenList(next);  

        return node;  
    } 

    // Utility method to print a linked list 
    public static void printFlattenNodes(Node head)  
    {  
        Node curr=head; 
        while(curr!=null)  
        {  
            System.out.print(curr.data+" "); 
            curr = curr.next; 
        }  

    }  

    // Utility function to create a new node  
    public static Node push(int newData)  
    {  
        Node newNode = new Node(newData);  
        newNode.next =null;  
        newNode.down = null;  
        return newNode;  
    }  

    public static void main(String args[]) { 
        Node head=new Node(1); 
        head.next = new Node(2);  
        head.next.next = new Node(3);  
        head.next.next.next = new Node(4);  
        head.next.down = new Node(7);  
        head.next.down.down = new Node(9);  
        head.next.down.down.down = new Node(14);  
        head.next.down.down.down.down= new Node(15);  
        head.next.down.down.down.down.next= new Node(23);  
        head.next.down.down.down.down.next.down = new Node(24);  
        head.next.down.next = new Node(8);  
        head.next.down.next.down = new Node(16);  
        head.next.down.next.down.down= new Node(17);  
        head.next.down.next.down.down.next= new Node(18);  
        head.next.down.next.down.down.next.next= new Node(19);  
        head.next.down.next.down.down.next.next.next  
                                            = new Node(20);  
        head.next.down.next.down.down.next.next.next.down  
                                            = new Node(21);  
        head.next.down.next.next = new Node(10);  
        head.next.down.next.next.down = new Node(11);  
        head.next.down.next.next.next = new Node(12);  

        head = flattenList(head);  
        printFlattenNodes(head); 
    } 
} 

//Node of Multi-level Linked List 
class Node 
{ 
    int data; 
    Node next,down; 
    Node(int data) 
    { 
        this.data=data; 
        next=null; 
        down=null; 
    } 
} 
//This code is contributed by Gaurav Tiwari 

```

## C#

```cs

// C# program to flatten a multilevel linked list 
using System; 

class FlattenList  
{ 

    static Node last; 

    // Flattens a multi-level linked list depth wise  
    public static Node flattenList(Node node) 
    { 
        if(node == null)  
            return null;  

        // To keep track of last visited node  
        // (NOTE: This is static)  
        last = node;  

        // Store next pointer  
        Node next = node.next;  

        // If down list exists, process it first  
        // Add down list as next of current node  
        if(node.down != null)  
            node.next = flattenList(node.down);  

        // If next exists, add it after the next  
        // of last added node  
        if(next != null)  
            last.next = flattenList(next);  

        return node;  
    } 

    // Utility method to print a linked list 
    public static void printFlattenNodes(Node head)  
    {  
        Node curr = head; 
        while(curr != null)  
        {  
            Console.Write(curr.data + " "); 
            curr = curr.next; 
        }  

    }  

    // Utility function to create a new node  
    public static Node push(int newData)  
    {  
        Node newNode = new Node(newData);  
        newNode.next =null;  
        newNode.down = null;  
        return newNode;  
    }  

    // Driver code 
    public static void Main() 
    { 
        Node head = new Node(1); 
        head.next = new Node(2);  
        head.next.next = new Node(3);  
        head.next.next.next = new Node(4);  
        head.next.down = new Node(7);  
        head.next.down.down = new Node(9);  
        head.next.down.down.down = new Node(14);  
        head.next.down.down.down.down= new Node(15);  
        head.next.down.down.down.down.next= new Node(23);  
        head.next.down.down.down.down.next.down = new Node(24);  
        head.next.down.next = new Node(8);  
        head.next.down.next.down = new Node(16);  
        head.next.down.next.down.down= new Node(17);  
        head.next.down.next.down.down.next= new Node(18);  
        head.next.down.next.down.down.next.next= new Node(19);  
        head.next.down.next.down.down.next.next.next  
                                            = new Node(20);  
        head.next.down.next.down.down.next.next.next.down  
                                            = new Node(21);  
        head.next.down.next.next = new Node(10);  
        head.next.down.next.next.down = new Node(11);  
        head.next.down.next.next.next = new Node(12);  

        head = flattenList(head);  
        printFlattenNodes(head); 
    } 
} 

// Node of Multi-level Linked List 
public class Node 
{ 
    public int data; 
    public Node next,down; 
    public Node(int data) 
    { 
        this.data = data; 
        next = null; 
        down = null; 
    } 
} 

/* This code is contributed PrinciRaj1992 */

```

**Output:**

```
1 2 7 9 14 15 23 24 8 16 17 18 19 20 21 10 11 12 3 4  

```

 **使用堆栈数据结构**的替代实现

## C++

```cpp

Node* flattenList2(Node* head) 
{ 
    Node* headcop = head; 
    stack<Node*> save; 
    save.push(head); 
    Node* prev = NULL; 

    while (!save.empty()) { 
        Node* temp = save.top(); 
        save.pop(); 

        if (temp->next) 
            save.push(temp->next); 
        if (temp->down) 
            save.push(temp->down); 

        if (prev != NULL) 
            prev->next = temp; 

        prev = temp; 
    } 
    return headcop; 
}

```

本文由 **Mu Ven** 提供。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请发表评论。

