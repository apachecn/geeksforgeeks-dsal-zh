# 用链接列表

> 原文：[https://www.geeksforgeeks.org/replace-each-node-with-its-surpasser-count-in-linked-list/](https://www.geeksforgeeks.org/replace-each-node-with-its-surpasser-count-in-linked-list/)

中的节点计数替换每个节点

给定 LinkedList，将每个节点的值替换为其超越者计数。 那是对它的权利更大的要素的数量。

**示例**：

> **输入**：10- > 12- > 5- > 40- > 21- > 70- > 1- > 49- > 37- >空
> **输出**：6- > 5- > 5- > 2- > 3- > 0- > 2- > 0- > 0- > NULL
> **说明**：
> 第一个节点中的元素为`10`，节点右侧的元素数为 大于`10`为`6`。 因此，将节点替换为`6`。
> 第一个节点中的元素是`12`，节点右侧大于`12`的元素数是`5`。 因此，将节点替换为`5`。
> 同样，替换列表中的所有元素。
> 
> **输入**：5- > 4- > 6- > 3- > 2- >空
> **输出**：1- > 1- > 0- > 0- > 0- > NULL

**简单方法**

1.  取两个指针 **p** 和 **x** 。 指针 **p** 用于遍历列表， **x** 用于遍历每个节点的列表的右半部分。

2.  初始化变量 *count* 以对大于当前节点的节点进行计数。

3.  使用指针 p 遍历列表中的所有节点。

    *   将计数初始化为 0。

    *   初始化指针 **x** 指向当前节点 **p** 。

    *   计算大于当前节点的节点数。

    *   用计数替换当前节点。

4.  重复步骤 4，直到列表完全遍历为止。

下面是上述方法的实现：

## C++

```cpp

// C++ program to replace the nodes 
// with their surpasser count 

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
    while (node != NULL) { 

        cout << node->data << " "; 

        node = node->next; 
    } 
} 

// Function to check Surpasser Count 
void replaceNodes(Node* head) 
{ 
    // Pointer used to traverse through 
    // all the nodes in the list 
    Node* p = head; 

    // Pointer used to traverse through the right 
    // elements to count the greater elements 
    Node* x = NULL; 

    // Variable to count the number of 
    // elements greater than the 
    // current element on right 
    int count = 0; 

    int i; 

    // Traverse through all the elements 
    // in the list 
    while (p != NULL) { 

        count = 0; 

        i = 0; 

        // Initialize x to current node 
        x = p; 

        // Check or count the number of nodes 
        // that are greater than the current 
        // node on right 
        while (x != NULL) { 

            if (x->data > p->data) 
                count++; 

            x = x->next; 
        } 

        // Replace the node data with the 
        // count of elements greater than 
        // the current element 
        p->data = count; 
        p = p->next; 
    } 
} 

// Driver code 
int main() 
{ 
    // Creating the linked list 
    Node* head = newNode(10); 
    head->next = newNode(12); 
    head->next->next = newNode(5); 
    head->next->next->next = newNode(40); 
    head->next->next->next->next = newNode(21); 
    head->next->next->next->next->next = newNode(70); 
    head->next->next->next->next->next->next = newNode(1); 
    head->next->next->next->next->next->next->next = newNode(49); 
    head->next->next->next->next->next->next->next->next = newNode(37); 

    replaceNodes(head); 

    printList(head); 

    return 0; 
} 

```

## Java

```java

// Java program to replace the nodes 
// with their surpasser count 

class GFG { 

// A linked list node 
static class Node { 
    int data; 
    Node next; 
}; 

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
    while (node != null) { 
        System.out.print(node.data+" "); 

        node = node.next; 
    } 
} 

// Function to check Surpasser Count 
static void replaceNodes(Node head) 
{ 
    // Pointer used to traverse through 
    // all the nodes in the list 
    Node p = head; 

    // Pointer used to traverse through the right 
    // elements to count the greater elements 
    Node x = null; 

    // Variable to count the number of 
    // elements greater than the 
    // current element on right 
    int count = 0; 

    int i; 

    // Traverse through all the elements 
    // in the list 
    while (p != null) { 

        count = 0; 

        i = 0; 

        // Initialize x to current node 
        x = p; 

        // Check or count the number of nodes 
        // that are greater than the current 
        // node on right 
        while (x != null) { 

            if (x.data > p.data) 
                count++; 

            x = x.next; 
        } 

        // Replace the node data with the 
        // count of elements greater than 
        // the current element 
        p.data = count; 
        p = p.next; 
    } 
} 

// Driver code 
public static void main(String[] args) { 
  // Creating the linked list 
    Node head = newNode(10); 
    head.next = newNode(12); 
    head.next.next = newNode(5); 
    head.next.next.next = newNode(40); 
    head.next.next.next.next = newNode(21); 
    head.next.next.next.next.next = newNode(70); 
    head.next.next.next.next.next.next = newNode(1); 
    head.next.next.next.next.next.next.next = newNode(49); 
    head.next.next.next.next.next.next.next.next = newNode(37); 

    replaceNodes(head); 

    printList(head); 
    } 
} 

// This code has been contributed by 29AjayKumar 

```

## Python3

```py

# Python3 program to replace the nodes  
# with their surpasser count  

# A linked list node  
class Node: 

    def __init__(self, data): 
        self.data = data  
        self.next = None

# Function to display the linked list  
def printList(node):  

    while node != None:  
        print(node.data, end = " ")  
        node = node.next

# Function to check Surpasser Count  
def replaceNodes(head):  

    # Pointer used to traverse through  
    # all the nodes in the list  
    p = head  

    # Pointer used to traverse through 
    # the right elements to count the  
    # greater elements  
    x = None

    # Variable to count the number of  
    # elements greater than the  
    # current element on right  
    count = 0

    # Traverse through all the elements  
    # in the list  
    while p != None:  

        count = 0

        # Initialize x to current node  
        x = p  

        # Check or count the number of nodes  
        # that are greater than the current  
        # node on right  
        while x != None:  

            if x.data > p.data:  
                count += 1

            x = x.next

        # Replace the node data with the  
        # count of elements greater than  
        # the current element  
        p.data = count  
        p = p.next

# Driver code  
if __name__ == "__main__": 

    # Creating the linked list  
    head = Node(10)  
    head.next = Node(12)  
    head.next.next = Node(5)  
    head.next.next.next = Node(40)  
    head.next.next.next.next = Node(21)  
    head.next.next.next.next.next = Node(70)  
    head.next.next.next.next.next.next = Node(1)  
    head.next.next.next.next.next.next.next = Node(49)  
    head.next.next.next.next.next.next.next.next = Node(37)  

    replaceNodes(head)  

    printList(head)  

# This code is contributed by Rituraj Jain 

```

## C#

```cs

// C# program to replace the nodes 
// with their surpasser count 
using System; 

class GFG  
{ 

// A linked list node 
public class Node 
{ 
    public int data; 
    public Node next; 
}; 

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
    while (node != null)  
    { 
        Console.Write(node.data + " "); 

        node = node.next; 
    } 
} 

// Function to check Surpasser Count 
static void replaceNodes(Node head) 
{ 
    // Pointer used to traverse through 
    // all the nodes in the list 
    Node p = head; 

    // Pointer used to traverse through the right 
    // elements to count the greater elements 
    Node x = null; 

    // Variable to count the number of 
    // elements greater than the 
    // current element on right 
    int count = 0; 

    int i; 

    // Traverse through all the elements 
    // in the list 
    while (p != null)  
    { 

        count = 0; 

        i = 0; 

        // Initialize x to current node 
        x = p; 

        // Check or count the number of nodes 
        // that are greater than the current 
        // node on right 
        while (x != null)  
        { 

            if (x.data > p.data) 
                count++; 

            x = x.next; 
        } 

        // Replace the node data with the 
        // count of elements greater than 
        // the current element 
        p.data = count; 
        p = p.next; 
    } 
} 

// Driver code 
public static void Main()  
{ 
    // Creating the linked list 
    Node head = newNode(10); 
    head.next = newNode(12); 
    head.next.next = newNode(5); 
    head.next.next.next = newNode(40); 
    head.next.next.next.next = newNode(21); 
    head.next.next.next.next.next = newNode(70); 
    head.next.next.next.next.next.next = newNode(1); 
    head.next.next.next.next.next.next.next = newNode(49); 
    head.next.next.next.next.next.next.next.next = newNode(37); 

    replaceNodes(head); 

    printList(head); 
} 
} 

/* This code contributed by PrinciRaj1992 */

```

**Output:**

```
6 5 5 2 3 0 2 0 0

```

**时间复杂度**：O（N <sup>2</sup> ）其中 N 是链​​表中节点的数量。

**辅助空间**：`O(1)`

被誉为业界最抢手的技能之一，拥有我们的 [**C++ STL**](https://practice.geeksforgeeks.org/courses/cpp-stl?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=GFG_Article_Bottom_CPP_STL) 课程的编码基础，并通过严格的问题解决方法掌握了这些概念。

* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。