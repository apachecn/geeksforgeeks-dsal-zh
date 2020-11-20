# 从给定的二叉树

> 原文：[https://www.geeksforgeeks.org/create-a-sorted-linked-list-from-the-given-binary-tree/](https://www.geeksforgeeks.org/create-a-sorted-linked-list-from-the-given-binary-tree/)

创建排序的链表

给定一个二叉树，任务是将其转换为排序的链表。

**示例**：

```
Input:
     1   
   /  \  
  2    3 
Output: 1 2 3

Input:
        2
      /   \
     4     8
   /  \   / \
  7   3  5   1
Output: 1 2 3 4 5 7 8

Input:
        3   
       /  
      4 
     / 
    1
   /
  9
Output: 1 3 4 9

```

**方法**：递归地迭代给定的二叉树，并使用[插入排序](http://www.geeksforgeeks.org/insertion-sort/)将每个节点添加到结果链表中其正确位置（最初为空）。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation of the approach 
#include <iostream> 
using namespace std; 

// A linked list node 
class Node { 
public: 
    int data; 
    Node* next; 
    Node(int data) 
    { 
        this->data = data; 
        this->next = NULL; 
    } 
}; 

// A binary tree node 
class treeNode { 
public: 
    int data; 
    treeNode* left; 
    treeNode* right; 
    treeNode(int data) 
    { 
        this->data = data; 
        this->left = NULL; 
        this->right = NULL; 
    } 
}; 

// Function to print the linked list 
void print(Node* head) 
{ 
    if (head == NULL) { 
        return; 
    } 
    Node* temp = head; 
    while (temp != NULL) { 
        cout << temp->data << " "; 
        temp = temp->next; 
    } 
} 

// Function to create Linked list from given binary tree 
Node* sortedList(Node* head, treeNode* root) 
{ 
    // return head if root is null 
    if (root == NULL) { 
        return head; 
    } 

    // First make the sorted linked list 
    // of the left sub-tree 
    head = sortedList(head, root->left); 
    Node* newNode = new Node(root->data); 
    Node* temp = head; 
    Node* prev = NULL; 

    // If linked list is empty add the 
    // node to the head 
    if (temp == NULL) { 
        head = newNode; 
    } 
    else { 

        // Find the correct position of the node 
        // in the given linked list 
        while (temp != NULL) { 
            if (temp->data > root->data) { 
                break; 
            } 
            else { 
                prev = temp; 
                temp = temp->next; 
            } 
        } 

        // Given node is to be attached 
        // at the end of the list 
        if (temp == NULL) { 
            prev->next = newNode; 
        } 
        else { 

            // Given node is to be attached 
            // at the head of the list 
            if (prev == NULL) { 
                newNode->next = temp; 
                head = newNode; 
            } 
            else { 

                // Insertion in between the list 
                newNode->next = temp; 
                prev->next = newNode; 
            } 
        } 
    } 

    // Now add the nodes of the right sub-tree 
    // to the sorted linked list 
    head = sortedList(head, root->right); 
    return head; 
} 

// Driver code 
int main() 
{ 
    /* Tree: 
         10 
        /  \ 
      15    2 
     /  \ 
    1    5 
*/
    treeNode* root = new treeNode(10); 
    root->left = new treeNode(15); 
    root->right = new treeNode(2); 
    root->left->left = new treeNode(1); 
    root->left->right = new treeNode(5); 

    Node* head = sortedList(NULL, root); 
    print(head); 

    return 0; 
} 

```

## Java

```java

// Java implementation of the approach 
import java.util.*; 

class GFG 
{ 

// A linked list node 
static class Node 
{ 
    int data; 
    Node next; 
    Node(int data) 
    { 
        this.data = data; 
        this.next = null; 
    } 
}; 

// A binary tree node 
static class treeNode 
{ 
    int data; 
    treeNode left; 
    treeNode right; 
    treeNode(int data) 
    { 
        this.data = data; 
        this.left = null; 
        this.right = null; 
    } 
}; 

// Function to print the linked list 
static void print(Node head) 
{ 
    if (head == null)  
    { 
        return; 
    } 
    Node temp = head; 
    while (temp != null) 
    { 
        System.out.print(temp.data + " "); 
        temp = temp.next; 
    } 
} 

// Function to create Linked list from given binary tree 
static Node sortedList(Node head, treeNode root) 
{ 
    // return head if root is null 
    if (root == null)  
    { 
        return head; 
    } 

    // First make the sorted linked list 
    // of the left sub-tree 
    head = sortedList(head, root.left); 
    Node newNode = new Node(root.data); 
    Node temp = head; 
    Node prev = null; 

    // If linked list is empty add the 
    // node to the head 
    if (temp == null)  
    { 
        head = newNode; 
    } 
    else
    { 

        // Find the correct position of the node 
        // in the given linked list 
        while (temp != null) 
        { 
            if (temp.data > root.data)  
            { 
                break; 
            } 
            else 
            { 
                prev = temp; 
                temp = temp.next; 
            } 
        } 

        // Given node is to be attached 
        // at the end of the list 
        if (temp == null) 
        { 
            prev.next = newNode; 
        } 
        else 
        { 

            // Given node is to be attached 
            // at the head of the list 
            if (prev == null)  
            { 
                newNode.next = temp; 
                head = newNode; 
            } 
            else
            { 

                // Insertion in between the list 
                newNode.next = temp; 
                prev.next = newNode; 
            } 
        } 
    } 

    // Now add the nodes of the right sub-tree 
    // to the sorted linked list 
    head = sortedList(head, root.right); 
    return head; 
} 

// Driver code 
public static void main(String[] args) 
{ 
    /* Tree: 
        10 
        / \ 
    15 2 
    / \ 
    1 5 
*/
    treeNode root = new treeNode(10); 
    root.left = new treeNode(15); 
    root.right = new treeNode(2); 
    root.left.left = new treeNode(1); 
    root.left.right = new treeNode(5); 

    Node head = sortedList(null, root); 
    print(head); 
} 
} 

// This code is contributed by 29AjayKumar 

```

## C#

```cs

// C# implementation of the approach 
using System; 

class GFG 
{ 

// A linked list node 
class Node 
{ 
    public int data; 
    public Node next; 
    public Node(int data) 
    { 
        this.data = data; 
        this.next = null; 
    } 
}; 

// A binary tree node 
class treeNode 
{ 
    public int data; 
    public treeNode left; 
    public treeNode right; 
    public treeNode(int data) 
    { 
        this.data = data; 
        this.left = null; 
        this.right = null; 
    } 
}; 

// Function to print the linked list 
static void print(Node head) 
{ 
    if (head == null)  
    { 
        return; 
    } 
    Node temp = head; 
    while (temp != null) 
    { 
        Console.Write(temp.data + " "); 
        temp = temp.next; 
    } 
} 

// Function to create Linked list  
// from given binary tree 
static Node sortedList(Node head, treeNode root) 
{ 
    // return head if root is null 
    if (root == null)  
    { 
        return head; 
    } 

    // First make the sorted linked list 
    // of the left sub-tree 
    head = sortedList(head, root.left); 
    Node newNode = new Node(root.data); 
    Node temp = head; 
    Node prev = null; 

    // If linked list is empty add the 
    // node to the head 
    if (temp == null)  
    { 
        head = newNode; 
    } 
    else
    { 

        // Find the correct position of the node 
        // in the given linked list 
        while (temp != null) 
        { 
            if (temp.data > root.data)  
            { 
                break; 
            } 
            else
            { 
                prev = temp; 
                temp = temp.next; 
            } 
        } 

        // Given node is to be attached 
        // at the end of the list 
        if (temp == null) 
        { 
            prev.next = newNode; 
        } 
        else
        { 

            // Given node is to be attached 
            // at the head of the list 
            if (prev == null)  
            { 
                newNode.next = temp; 
                head = newNode; 
            } 
            else
            { 

                // Insertion in between the list 
                newNode.next = temp; 
                prev.next = newNode; 
            } 
        } 
    } 

    // Now add the nodes of the right sub-tree 
    // to the sorted linked list 
    head = sortedList(head, root.right); 
    return head; 
} 

// Driver code 
public static void Main(String[] args) 
{ 
    /* Tree: 
        10 
        / \ 
    15 2 
    / \ 
    1 5 
    */
    treeNode root = new treeNode(10); 
    root.left = new treeNode(15); 
    root.right = new treeNode(2); 
    root.left.left = new treeNode(1); 
    root.left.right = new treeNode(5); 

    Node head = sortedList(null, root); 
    print(head); 
} 
} 

// This code is contributed by PrinciRaj1992 

```

## Python3

```py

# Python3 implementation of the approach 

# A linked list node 
class Node: 
    def __init__(self, data = 0): 
        self.data = data 
        self.next = None

# A binary tree node 
class treeNode: 
    def __init__(self, data): 
        self.data = data 
        self.left = None
        self.right = None

# Function to print the linked list 
def print_(head): 

    if (head == None):  
        return

    temp = head 
    while (temp != None): 
        print ( temp.data, end = " " ) 
        temp = temp.next

# Function to create Linked list from given binary tree 
def sortedList( head, root): 

    # return head if root is None 
    if (root == None) : 

        return head 

    # First make the sorted linked list 
    # of the left sub-tree 
    head = sortedList(head, root.left) 
    newNode = Node(root.data) 
    temp = head 
    prev = None

    # If linked list is empty add the 
    # node to the head 
    if (temp == None) : 
        head = newNode 

    else: 

        # Find the correct position of the node 
        # in the given linked list 
        while (temp != None): 

            if (temp.data > root.data) : 
                break

            else: 
                prev = temp 
                temp = temp.next

        # Given node is to be attached 
        # at the end of the list 
        if (temp == None): 
            prev.next = newNode 

        else: 

            # Given node is to be attached 
            # at the head of the list 
            if (prev == None) : 
                newNode.next = temp 
                head = newNode 

            else: 

                # Insertion in between the list 
                newNode.next = temp 
                prev.next = newNode 

    # Now add the nodes of the right sub-tree 
    # to the sorted linked list 
    head = sortedList(head, root.right) 
    return head 

# Driver code 

# Tree: 
# 10 
# / \ 
# 15 2 
# / \ 
#1 5 

root = treeNode(10) 
root.left = treeNode(15) 
root.right = treeNode(2) 
root.left.left = treeNode(1) 
root.left.right = treeNode(5) 

head = sortedList(None, root) 

print_(head) 

# This code is contributed by Arnab Kundu 

```

**Output:**

```
1 2 5 10 15

```

**时间复杂度**：`O(N ^ 2)`



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。