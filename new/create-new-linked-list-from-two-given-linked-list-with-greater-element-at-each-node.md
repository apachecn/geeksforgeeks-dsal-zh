# 从两个给定的链表创建新的链表，每个链结在每个节点上都有更大的元素

> 原文：[https://www.geeksforgeeks.org/create-new-linked-list-from-two-given-linked-list-with-greater-element-at-each-node/](https://www.geeksforgeeks.org/create-new-linked-list-from-two-given-linked-list-with-greater-element-at-each-node/)

给定两个大小相同的链表，任务是使用这些链表创建一个新的链表。 条件是两个链接列表中的较大节点将被添加到新的喜欢列表中。

**示例**：

```
Input:  list1 = 5->2->3->8
list2 = 1->7->4->5
Output:  New list = 5->7->4->8

Input: list1 = 2->8->9->3
list2 = 5->3->6->4
Output:  New list = 5->8->9->4

```

**方法**：我们同时遍历两个链表，并比较两个链表的节点。 其中更大的节点将被添加到新的链表中。 我们为每个节点执行此操作。

## C++

```cpp

// C++ program to create a new linked list 
// from two given linked list 
// of the same size with 
// the greater element among the two at each node 

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

// Function which returns new linked list 
Node* newList(Node* root1, Node* root2) 
{ 
    Node *ptr1 = root1, *ptr2 = root2, *ptr; 
    Node *root = NULL, *temp; 

    while (ptr1 != NULL) { 
        temp = new Node; 
        temp->next = NULL; 

        // Compare for greater node 
        if (ptr1->data < ptr2->data) 
            temp->data = ptr2->data; 
        else
            temp->data = ptr1->data; 

        if (root == NULL) 
            root = temp; 
        else { 
            ptr = root; 
            while (ptr->next != NULL) 
                ptr = ptr->next; 

            ptr->next = temp; 
        } 
        ptr1 = ptr1->next; 
        ptr2 = ptr2->next; 
    } 
    return root; 
} 

void display(Node* root) 
{ 
    while (root != NULL) { 
        cout << root->data << "->"; 
        root = root->next; 
    } 

    cout << endl; 
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

    cout << "First List:  "; 
    display(root1); 

    // Second linked list 
    insert(&root2, 1); 
    insert(&root2, 7); 
    insert(&root2, 4); 
    insert(&root2, 5); 

    cout << "Second List: "; 
    display(root2); 

    root = newList(root1, root2); 
    cout << "New List:    "; 
    display(root); 
    return 0; 
} 

```

## Java

```java

// Java program to create a new linked list  
// from two given linked list  
// of the same size with  
// the greater element among the two at each node  
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
    else {  
        ptr = root;  
        while (ptr.next != null)  
            ptr = ptr.next;  

        ptr.next = temp;  
    }  
    return root; 
}  

// Function which returns new linked list  
static Node newList(Node root1, Node root2)  
{  
    Node ptr1 = root1, ptr2 = root2, ptr;  
    Node root = null, temp;  

    while (ptr1 != null) {  
        temp = new Node();  
        temp.next = null;  

        // Compare for greater node  
        if (ptr1.data < ptr2.data)  
            temp.data = ptr2.data;  
        else
            temp.data = ptr1.data;  

        if (root == null)  
            root = temp;  
        else {  
            ptr = root;  
            while (ptr.next != null)  
                ptr = ptr.next;  

            ptr.next = temp;  
        }  
        ptr1 = ptr1.next;  
        ptr2 = ptr2.next;  
    }  
    return root;  
}  

static void display(Node root)  
{  
    while (root != null)  
    {  
        System.out.print( root.data + "->");  
        root = root.next;  
    }  
    System.out.println(); 
}  

// Driver code  
public static void main(String args[]) 
{  
    Node root1 = null, root2 = null, root = null;  

    // First linked list  
    root1=insert(root1, 5);  
    root1=insert(root1, 2);  
    root1=insert(root1, 3);  
    root1=insert(root1, 8);  

    System.out.print("First List: ");  
    display(root1);  

    // Second linked list  
    root2=insert(root2, 1);  
    root2=insert(root2, 7);  
    root2=insert(root2, 4);  
    root2=insert(root2, 5);  

    System.out.print( "Second List: ");  
    display(root2);  

    root = newList(root1, root2);  
    System.out.print("New List: ");  
    display(root);  
}  
} 

// This code is contributed by Arnab Kundu 

```

## Python3

```py

# Python3 program to create a  
# new linked list from two given  
# linked list of the same size with 
# the greater element among the two 
# at each node 

# Node class  
class Node:  

    # Function to initialise the node object  
    def __init__(self, data):  
        self.data = data  
        self.next = None

# Function to insert node in a linked list 
def insert(root, item): 

    temp = Node(0) 
    temp.data = item 
    temp.next = None

    if (root == None): 
        root = temp 
    else : 
        ptr = root 
        while (ptr.next != None): 
            ptr = ptr.next

        ptr.next = temp 

    return root 

# Function which returns new linked list 
def newList(root1, root2): 

    ptr1 = root1 
    ptr2 = root2 

    root = None
    while (ptr1 != None) : 
        temp = Node(0) 
        temp.next = None

        # Compare for greater node 
        if (ptr1.data < ptr2.data): 
            temp.data = ptr2.data 
        else: 
            temp.data = ptr1.data 

        if (root == None): 
            root = temp 
        else : 
            ptr = root 
            while (ptr.next != None): 
                ptr = ptr.next

            ptr.next = temp 

        ptr1 = ptr1.next
        ptr2 = ptr2.next

    return root 

def display(root): 

    while (root != None) : 
        print(root.data, "->", end = " ") 
        root = root.next

    print(" "); 

# Driver Code  
if __name__=='__main__':  

    root1 = None
    root2 = None
    root = None

    # First linked list 
    root1 = insert(root1, 5) 
    root1 = insert(root1, 2) 
    root1 = insert(root1, 3) 
    root1 = insert(root1, 8) 

    print("First List: ", end = " ") 
    display(root1) 

    # Second linked list 
    root2 = insert(root2, 1) 
    root2 = insert(root2, 7) 
    root2 = insert(root2, 4) 
    root2 = insert(root2, 5) 

    print("Second List: ", end = " ") 
    display(root2) 

    root = newList(root1, root2) 
    print("New List: ", end = " ") 
    display(root) 

# This code is contributed by Arnab Kundu 

```

## C#

```cs

// C# program to create a new linked list  
// from two given linked list  
// of the same size with  
// the greater element among the two at each node  
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

// Function which returns new linked list  
static Node newList(Node root1, Node root2)  
{  
    Node ptr1 = root1, ptr2 = root2, ptr;  
    Node root = null, temp;  

    while (ptr1 != null) 
    {  
        temp = new Node();  
        temp.next = null;  

        // Compare for greater node  
        if (ptr1.data < ptr2.data)  
            temp.data = ptr2.data;  
        else
            temp.data = ptr1.data;  

        if (root == null)  
            root = temp;  
        else 
        {  
            ptr = root;  
            while (ptr.next != null)  
                ptr = ptr.next;  

            ptr.next = temp;  
        }  
        ptr1 = ptr1.next;  
        ptr2 = ptr2.next;  
    }  
    return root;  
}  

static void display(Node root)  
{  
    while (root != null)  
    {  
        Console.Write( root.data + "->");  
        root = root.next;  
    }  
    Console.WriteLine(); 
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

    Console.Write("First List: ");  
    display(root1);  

    // Second linked list  
    root2 = insert(root2, 1);  
    root2 = insert(root2, 7);  
    root2 = insert(root2, 4);  
    root2 = insert(root2, 5);  

    Console.Write( "Second List: ");  
    display(root2);  

    root = newList(root1, root2);  
    Console.Write("New List: ");  
    display(root);  
}  
} 

// This code has been contributed by 29AjayKumar 

```

**Output:**

```
First List:  5->2->3->8->
Second List: 1->7->4->5->
New List:    5->7->4->8->

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。