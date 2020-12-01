# 通过在每个位置选择最大元素，从两个链表创建一个链表

> 原文：[https://www.geeksforgeeks.org/create-a-linked-list-from-two-linked-lists-by-choosing-max-element-at-each-position/](https://www.geeksforgeeks.org/create-a-linked-list-from-two-linked-lists-by-choosing-max-element-at-each-position/)

给定两个大小相等的链表，任务是使用这些链表创建新的链表，其中在每个步骤中，选择两个链表中两个元素的最大值，然后跳过另一个元素。

**示例**：

> **输入**：
> 
> ```
> list1 = 5 -> 2 -> 3 -> 8 -> NULL
> list2 = 1 -> 7 -> 4 -> 5 -> NULL
> ```
> 
> **输出**：`5 -> 7 -> 4 -> 8 ->NULL`
> 
> **输入**：
>
> ```
> list1 = 2 -> 8 -> 9 -> 3 -> NULL
> list2 = 5 -> 3 -> 6 -> 4 -> NULL
> ```
>
> **输出**：`5 -> 8 -> 9 -> 4 -> NULL`

**方法**：我们同时遍历两个链表，并比较两个链表中的节点。 其中更大的节点将被添加到新的链表中。 我们对每个节点执行此操作，然后打印生成的链表的节点。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation of the approach 
#include <iostream> 
using namespace std; 

// Representation of node 
struct Node { 
    int data; 
    Node* next; 
}; 

// Function to insert node in a linked list 
void insert(Node** root, int item) 
{ 
    Node *ptr, *temp; 
    temp = new Node; 
    temp->data = item; 
    temp->next = NULL; 

    if (*root == NULL) 
        *root = temp; 
    else { 
        ptr = *root; 
        while (ptr->next != NULL) 
            ptr = ptr->next; 

        ptr->next = temp; 
    } 
} 

// Function to print the 
// nodes of a linked list 
void display(Node* root) 
{ 
    while (root != NULL) { 
        cout << root->data << " -> "; 
        root = root->next; 
    } 
    cout << "NULL"; 
} 

// Function to generate the required 
// linked list and return its head 
Node* newList(Node* root1, Node* root2) 
{ 
    Node *ptr1 = root1, *ptr2 = root2; 
    Node* root = NULL; 

    // While there are nodes left 
    while (ptr1 != NULL) { 

        // Maximum node at current position 
        int currMax = ((ptr1->data < ptr2->data) 
                           ? ptr2->data 
                           : ptr1->data); 

        // If current node is the first node 
        // of the newly linked list being 
        // generated then assign it to the root 
        if (root == NULL) { 
            Node* temp = new Node; 
            temp->data = currMax; 
            temp->next = NULL; 
            root = temp; 
        } 

        // Else insert the newly 
        // created node in the end 
        else { 
            insert(&root, currMax); 
        } 

        // Get to the next nodes 
        ptr1 = ptr1->next; 
        ptr2 = ptr2->next; 
    } 

    // Return the head of the 
    // generated linked list 
    return root; 
} 

// Driver code 
int main() 
{ 
    Node *root1 = NULL, *root2 = NULL, *root = NULL; 

    // First linked list 
    insert(&root1, 5); 
    insert(&root1, 2); 
    insert(&root1, 3); 
    insert(&root1, 8); 

    // Second linked list 
    insert(&root2, 1); 
    insert(&root2, 7); 
    insert(&root2, 4); 
    insert(&root2, 5); 

    // Generate the new linked list 
    // and get its head 
    root = newList(root1, root2); 

    // Display the nodes of the generated list 
    display(root); 

    return 0; 
} 

```

## Java

```java

// Java implementation of the approach 
import java.util.*; 
class GFG 
{ 

// Representation of node 
static class Node  
{ 
    int data; 
    Node next; 
}; 

// Function to insert node in a linked list 
static Node insert(Node root, int item) 
{ 
    Node ptr, temp; 
    temp = new Node(); 
    temp.data = item; 
    temp.next = null; 

    if (root == null) 
        root = temp; 
    else 
    { 
        ptr = root; 
        while (ptr.next != null) 
            ptr = ptr.next; 

        ptr.next = temp; 
    } 
    return root; 
} 

// Function to print the 
// nodes of a linked list 
static void display(Node root) 
{ 
    while (root != null)  
    { 
        System.out.print( root.data + " - > "); 
        root = root.next; 
    } 
    System.out.print("null"); 
} 

// Function to generate the required 
// linked list and return its head 
static Node newList(Node root1, Node root2) 
{ 
    Node ptr1 = root1, ptr2 = root2; 
    Node root = null; 

    // While there are nodes left 
    while (ptr1 != null)  
    { 

        // Maximum node at current position 
        int currMax = ((ptr1.data < ptr2.data) 
                        ? ptr2.data 
                        : ptr1.data); 

        // If current node is the first node 
        // of the newly linked list being 
        // generated then assign it to the root 
        if (root == null)  
        { 
            Node temp = new Node(); 
            temp.data = currMax; 
            temp.next = null; 
            root = temp; 
        } 

        // Else insert the newly 
        // created node in the end 
        else 
        { 
            root = insert(root, currMax); 
        } 

        // Get to the next nodes 
        ptr1 = ptr1.next; 
        ptr2 = ptr2.next; 
    } 

    // Return the head of the 
    // generated linked list 
    return root; 
} 

// Driver code 
public static void main(String args[]) 
{ 
    Node root1 = null, root2 = null, root = null; 

    // First linked list 
    root1 = insert(root1, 5); 
    root1 = insert(root1, 2); 
    root1 = insert(root1, 3); 
    root1 = insert(root1, 8); 

    // Second linked list 
    root2 = insert(root2, 1); 
    root2 = insert(root2, 7); 
    root2 = insert(root2, 4); 
    root2 = insert(root2, 5); 

    // Generate the new linked list 
    // and get its head 
    root = newList(root1, root2); 

    // Display the nodes of the generated list 
    display(root); 

} 
} 

// This code is contributed by Arnab Kundu 

```

## Python3

```py

# Python3 implementation of the approach 
import math 

# Representation of node 
class Node:  
    def __init__(self, data):  
        self.data = data  
        self.next = None

# Function to insert node in a linked list 
def insert(root, item): 
    #ptr, *temp 
    temp = Node(item) 
    temp.data = item 
    temp.next = None

    if (root == None): 
        root = temp 
    else: 
        ptr = root 
        while (ptr.next != None): 
            ptr = ptr.next

        ptr.next = temp 

    return root 

# Function to print the 
# nodes of a linked list 
def display(root): 
    while (root != None) : 
        print(root.data, end = "->") 
        root = root.next

    print("NULL") 

# Function to generate the required 
# linked list and return its head 
def newList(root1, root2): 
    ptr1 = root1 
    ptr2 = root2 
    root = None

    # While there are nodes left 
    while (ptr1 != None) : 

        # Maximum node at current position 
        currMax = ((ptr1.data < ptr2.data) and  
                    ptr2.data or ptr1.data) 

        # If current node is the first node 
        # of the newly linked list being 
        # generated then assign it to the root 
        if (root == None): 
            temp = Node(currMax) 
            temp.data = currMax 
            temp.next = None
            root = temp 

        # Else insert the newly 
        # created node in the end 
        else : 
            root = insert(root, currMax) 

        # Get to the next nodes 
        ptr1 = ptr1.next
        ptr2 = ptr2.next

    # Return the head of the 
    # generated linked list 
    return root 

# Driver code 
if __name__=='__main__':  

    root1 = None
    root2 = None
    root = None

    # First linked list 
    root1 = insert(root1, 5) 
    root1 = insert(root1, 2) 
    root1 = insert(root1, 3) 
    root1 = insert(root1, 8) 

    # Second linked list 
    root2 = insert(root2, 1) 
    root2 = insert(root2, 7) 
    root2 = insert(root2, 4) 
    root2 = insert(root2, 5) 

    # Generate the new linked list 
    # and get its head 
    root = newList(root1, root2) 

    # Display the nodes of the generated list 
    display(root) 

# This code is contributed by Srathore 

```

## C#

```cs

// C# implementation of the approach 
using System;  

class GFG  
{  

// Representation of node  
public class Node  
{  
    public int data;  
    public Node next;  
};  

// Function to insert node in a linked list  
static Node insert(Node root, int item)  
{  
    Node ptr, temp;  
    temp = new Node();  
    temp.data = item;  
    temp.next = null;  

    if (root == null)  
        root = temp;  
    else
    {  
        ptr = root;  
        while (ptr.next != null)  
            ptr = ptr.next;  

        ptr.next = temp;  
    }  
    return root;  
}  

// Function to print the  
// nodes of a linked list  
static void display(Node root)  
{  
    while (root != null)  
    {  
        Console.Write( root.data + " - > ");  
        root = root.next;  
    }  
    Console.Write("null");  
}  

// Function to generate the required  
// linked list and return its head  
static Node newList(Node root1, Node root2)  
{  
    Node ptr1 = root1, ptr2 = root2;  
    Node root = null;  

    // While there are nodes left  
    while (ptr1 != null)  
    {  

        // Maximum node at current position  
        int currMax = ((ptr1.data < ptr2.data)  
                        ? ptr2.data  
                        : ptr1.data);  

        // If current node is the first node  
        // of the newly linked list being  
        // generated then assign it to the root  
        if (root == null)  
        {  
            Node temp = new Node();  
            temp.data = currMax;  
            temp.next = null;  
            root = temp;  
        }  

        // Else insert the newly  
        // created node in the end  
        else
        {  
            root = insert(root, currMax);  
        }  

        // Get to the next nodes  
        ptr1 = ptr1.next;  
        ptr2 = ptr2.next;  
    }  

    // Return the head of the  
    // generated linked list  
    return root;  
}  

// Driver code  
public static void Main(String []args)  
{  
    Node root1 = null, root2 = null, root = null;  

    // First linked list  
    root1 = insert(root1, 5);  
    root1 = insert(root1, 2);  
    root1 = insert(root1, 3);  
    root1 = insert(root1, 8);  

    // Second linked list  
    root2 = insert(root2, 1);  
    root2 = insert(root2, 7);  
    root2 = insert(root2, 4);  
    root2 = insert(root2, 5);  

    // Generate the new linked list  
    // and get its head  
    root = newList(root1, root2);  

    // Display the nodes of the generated list  
    display(root);  

}  
}  

/* This code contributed by PrinciRaj1992 */

```

**输出**：

```
5 -> 7 -> 4 -> 8 -> NULL

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。