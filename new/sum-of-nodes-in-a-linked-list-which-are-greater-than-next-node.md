# 链表中大于下一节点的节点总数

> 原文：[https://www.geeksforgeeks.org/sum-of-nodes-in-a-linked-list-which-are-greater-than-next-node/](https://www.geeksforgeeks.org/sum-of-nodes-in-a-linked-list-which-are-greater-than-next-node/)

给定一个链表，任务是找到所有大于其旁边节点的节点之和。 **请注意**，对于链表的最后一个节点，该节点的旁边没有任何节点，它必须大于第一个节点，以使它有助于总和。

**示例**：

> **输入**：`9 -> 2 -> 3 -> 5 -> 4 -> 6 -> 8`
>
> **输出**：14
>
> `9 + 5 = 14`
> 
> **输入**：`2 -> 1 -> 5 -> 7`
>
> **输出**：9
>
> `2 + 7 = 9`

**方法**：遍历整个链表，对于每个节点，如果该节点大于下一个节点，则将其添加到总和中。 对于最后一个节点，将其与链表的开头进行比较，如果最后一个节点大于开头，则将其添加到总和中。 最后打印总和。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation of the approach 
#include <iostream> 
using namespace std; 

// Represents node of the linked list 
struct Node { 
    int data; 
    Node* next; 
}; 

// Function to insert a node at the 
// end of the linked list 
void insert(Node** root, int item) 
{ 
    Node *ptr = *root, *temp = new Node; 
    temp->data = item; 
    temp->next = NULL; 

    if (*root == NULL) 
        *root = temp; 
    else { 
        while (ptr->next != NULL) 
            ptr = ptr->next; 
        ptr->next = temp; 
    } 
} 

// Function to return the sum of the nodes 
// which are greater than the node next to them 
int sum(Node* root) 
{ 

    // If there are no nodes 
    if (root == NULL) 
        return 0; 

    int sm = 0; 
    Node* ptr = root; 
    while (ptr->next != NULL) { 

        // If the node is greater than the next node 
        if (ptr->data > ptr->next->data) 
            sm += ptr->data; 
        ptr = ptr->next; 
    } 

    // For the last node 
    if (ptr->data > root->data) 
        sm += ptr->data; 

    // Return the sum 
    return sm; 
} 

// Driver code 
int main() 
{ 
    Node* root = NULL; 

    insert(&root, 9); 
    insert(&root, 2); 
    insert(&root, 3); 
    insert(&root, 5); 
    insert(&root, 4); 
    insert(&root, 6); 
    insert(&root, 8); 

    cout << sum(root) << endl; 
    return 0; 
} 

```

## Java

```java

// Java implementation of the approach  
class GFG 
{ 

// Represents node of the linked list  
static class Node  
{  
    int data;  
    Node next;  
};  

// Function to insert a node at the  
// end of the linked list  
static Node insert(Node root, int item)  
{  
    Node ptr = root, temp = new Node();  
    temp.data = item;  
    temp.next = null;  

    if (root == null)  
        root = temp;  
    else 
    {  
        while (ptr.next != null)  
            ptr = ptr.next;  
        ptr.next = temp;  
    }  
    return root; 
}  

// Function to return the sum of the nodes  
// which are greater than the node next to them  
static int sum(Node root)  
{  

    // If there are no nodes  
    if (root == null)  
        return 0;  

    int sm = 0;  
    Node ptr = root;  
    while (ptr.next != null)  
    {  

        // If the node is greater than the next node  
        if (ptr.data > ptr.next.data)  
            sm += ptr.data;  
        ptr = ptr.next;  
    }  

    // For the last node  
    if (ptr.data > root.data)  
        sm += ptr.data;  

    // Return the sum  
    return sm;  
}  

// Driver code  
public static void main(String args[]) 
{  
    Node root = null;  

    root=insert(root, 9);  
    root=insert(root, 2);  
    root=insert(root, 3);  
    root=insert(root, 5);  
    root=insert(root, 4);  
    root=insert(root, 6);  
    root=insert(root, 8);  

    System.out.print( sum(root) ); 
} 
}  

// This code is contributed by Arnab Kundu 

```

## Python3

```py

# Python3 implementation of the approach 
import math 

# Represents node of the linked list 
class Node:  
    def __init__(self, data):  
        self.data = data  
        self.next = None

# Function to root=insert a node at the 
# end of the linked list 
def insert(root, item): 

    ptr = root 
    temp = Node(item); 
    temp.data = item; 
    temp.next = None; 

    if (root == None): 
        root = temp; 
    else: 
        while (ptr.next != None): 
            ptr = ptr.next; 
        ptr.next = temp; 

    return root 

# Function to return the sum of the nodes 
# which are greater than the node next to them 
def sum(root): 

    # If there are no nodes 
    if (root == None): 
        return 0; 

    sm = 0; 
    ptr = root; 
    while (ptr.next != None): 

        # If the node is greater than the next node 
        if (ptr.data > ptr.next.data): 
            sm += ptr.data; 
        ptr = ptr.next; 

    # For the last node 
    if (ptr.data > root.data): 
        sm += ptr.data; 

    # Return the sum 
    return sm; 

# Driver code 
if __name__=='__main__':  
    root = None; 
    root = insert(root, 9); 
    root = insert(root, 2); 
    root = insert(root, 3); 
    root = insert(root, 5); 
    root = insert(root, 4); 
    root = insert(root, 6); 
    root = insert(root, 8); 

    print(sum(root)) 

# This code is contributed by Srathore 

```

## C#

```cs

// C# implementation of the approach 
using System; 

class GFG 
{ 

// Represents node of the linked list  
public class Node  
{  
    public int data;  
    public Node next;  
};  

// Function to insert a node at the  
// end of the linked list  
static Node insert(Node root, int item)  
{  
    Node ptr = root, temp = new Node();  
    temp.data = item;  
    temp.next = null;  

    if (root == null)  
        root = temp;  
    else
    {  
        while (ptr.next != null)  
            ptr = ptr.next;  
        ptr.next = temp;  
    }  
    return root; 
}  

// Function to return the sum of the nodes  
// which are greater than the node next to them  
static int sum(Node root)  
{  

    // If there are no nodes  
    if (root == null)  
        return 0;  

    int sm = 0;  
    Node ptr = root;  
    while (ptr.next != null)  
    {  

        // If the node is greater than the next node  
        if (ptr.data > ptr.next.data)  
            sm += ptr.data;  
        ptr = ptr.next;  
    }  

    // For the last node  
    if (ptr.data > root.data)  
        sm += ptr.data;  

    // Return the sum  
    return sm;  
}  

// Driver code  
public static void Main(String []args) 
{  
    Node root = null;  

    root = insert(root, 9);  
    root = insert(root, 2);  
    root = insert(root, 3);  
    root = insert(root, 5);  
    root = insert(root, 4);  
    root = insert(root, 6);  
    root = insert(root, 8);  

    Console.Write( sum(root) ); 
} 
} 

// This code contributed by Rajput-Ji 

```

**输出**：

```
14

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。