# 提取双链表

中的二叉树的叶子

给定一棵二叉树，将其所有叶子提取到 **L** ist（DLL）的 **D** 整体 **L** 中。 请注意，需要就地创建 DLL。 假设 DLL 和 Binary Tree 的节点结构相同，只是左右指针的含义不同。 在 DLL 中，左表示上一个指针，右表示下一个指针。

```
Let the following be input binary tree
        1
     /     \
    2       3
   / \       \
  4   5       6
 / \         / \
7   8       9   10

Output:
Doubly Linked List
785910

Modified Tree:
        1
     /     \
    2       3
   /         \
  4           6
```

我们需要遍历所有叶子，并通过更改它们的左右指针来连接它们。 我们还需要通过更改父节点中的左或右指针将它们从二叉树中删除。 有很多方法可以解决此问题。 在以下实现中，我们在当前链接列表的开头添加叶子，并使用指向 head 的指针更新列表的 head。 由于我们在开始时插入，因此我们需要以相反的顺序处理叶子。 对于逆序，我们先遍历右侧子树，然后遍历左侧子树。 我们使用返回值来更新父节点中的左或右指针。

## C++

```cpp

// C++ program to extract leaves of  
// a Binary Tree in a Doubly Linked List  
#include <bits/stdc++.h> 
using namespace std; 

// Structure for tree and linked list  
class Node  
{  
    public: 
    int data;  
    Node *left, *right;  
};  

// Main function which extracts all  
// leaves from given Binary Tree.  
// The function returns new root of  
// Binary Tree (Note that root may change  
// if Binary Tree has only one node). 
// The function also sets *head_ref as  
// head of doubly linked list. left pointer  
// of tree is used as prev in DLL  
// and right pointer is used as next  
Node* extractLeafList(Node *root, Node **head_ref)  
{  
// Base cases  
if (root == NULL) return NULL;  

if (root->left == NULL && root->right == NULL)  
{  
    // This node is going to be added  
    // to doubly linked list of leaves, 
    // set right pointer of this node  
    // as previous head of DLL. We  
    // don't need to set left pointer   
    // as left is already NULL  
    root->right = *head_ref;  

    // Change left pointer of previous head  
    if (*head_ref != NULL) (*head_ref)->left = root;  

    // Change head of linked list  
    *head_ref = root;  

    return NULL; // Return new root  
}  

// Recur for right and left subtrees  
root->right = extractLeafList(root->right, head_ref);  
root->left = extractLeafList(root->left, head_ref);  

return root;  
}  

// Utility function for allocating node for Binary Tree.  
Node* newNode(int data)  
{  
    Node* node = new Node(); 
    node->data = data;  
    node->left = node->right = NULL;  
    return node;  
}  

// Utility function for printing tree in In-Order.  
void print(Node *root)  
{  
    if (root != NULL)  
    {  
        print(root->left);  
        cout<<root->data<<" ";  
        print(root->right);  
    }  
}  

// Utility function for printing double linked list.  
void printList(Node *head)  
{  
    while (head)  
    {  
        cout<<head->data<<" ";  
        head = head->right;  
    }  
}  

// Driver code  
int main()  
{  
    Node *head = NULL;  
    Node *root = newNode(1);  
    root->left = newNode(2);  
    root->right = newNode(3);  
    root->left->left = newNode(4);  
    root->left->right = newNode(5);  
    root->right->right = newNode(6);  
    root->left->left->left = newNode(7);  
    root->left->left->right = newNode(8);  
    root->right->right->left = newNode(9);  
    root->right->right->right = newNode(10);  

    cout << "Inorder Trvaersal of given Tree is:\n";  
    print(root);  

    root = extractLeafList(root, &head);  

    cout << "\nExtracted Double Linked list is:\n";  
    printList(head);  

    cout << "\nInorder traversal of modified tree is:\n";  
    print(root);  
    return 0;  
}  

// This code is contributed by rathbhupendra 

```

## C

```c

// C program to extract leaves of a Binary Tree in a Doubly Linked List 
#include <stdio.h> 
#include <stdlib.h> 

// Structure for tree and linked list 
struct Node 
{ 
    int data; 
    struct Node *left, *right; 
}; 

// Main function which extracts all leaves from given Binary Tree. 
// The function returns new root of Binary Tree (Note that root may change 
// if Binary Tree has only one node).  The function also sets *head_ref as 
// head of doubly linked list.  left pointer of tree is used as prev in DLL 
// and right pointer is used as next 
struct Node* extractLeafList(struct Node *root, struct Node **head_ref) 
{ 
   // Base cases 
   if (root == NULL)  return NULL; 

   if (root->left == NULL && root->right == NULL) 
   { 
       // This node is going to be added to doubly linked list 
       // of leaves, set right pointer of this node as previous 
       // head of DLL. We don't need to set left pointer as left 
       // is already NULL 
       root->right = *head_ref; 

       // Change left pointer of previous head 
       if (*head_ref != NULL) (*head_ref)->left = root; 

       // Change head of linked list 
       *head_ref = root; 

       return NULL;  // Return new root 
   } 

   // Recur for right and left subtrees 
   root->right = extractLeafList(root->right, head_ref); 
   root->left  = extractLeafList(root->left, head_ref); 

   return root; 
} 

// Utility function for allocating node for Binary Tree. 
struct Node* newNode(int data) 
{ 
    struct Node* node = (struct Node*)malloc(sizeof(struct Node)); 
    node->data = data; 
    node->left = node->right = NULL; 
    return node; 
} 

// Utility function for printing tree in In-Order. 
void print(struct Node *root) 
{ 
    if (root != NULL) 
    { 
         print(root->left); 
         printf("%d ",root->data); 
         print(root->right); 
    } 
} 

// Utility function for printing double linked list. 
void printList(struct Node *head) 
{ 
     while (head) 
     { 
         printf("%d ", head->data); 
         head = head->right; 
     } 
} 

// Driver program to test above function 
int main() 
{ 
     struct Node *head = NULL; 
     struct Node *root = newNode(1); 
     root->left = newNode(2); 
     root->right = newNode(3); 
     root->left->left = newNode(4); 
     root->left->right = newNode(5); 
     root->right->right = newNode(6); 
     root->left->left->left = newNode(7); 
     root->left->left->right = newNode(8); 
     root->right->right->left = newNode(9); 
     root->right->right->right = newNode(10); 

     printf("Inorder Trvaersal of given Tree is:\n"); 
     print(root); 

     root = extractLeafList(root, &head); 

     printf("\nExtracted Double Linked list is:\n"); 
     printList(head); 

     printf("\nInorder traversal of modified tree is:\n"); 
     print(root); 
     return 0; 
} 

```

## Java

```java

// Java program to extract leaf nodes from binary tree 
// using double linked list 

// A binay tree node 
class Node  
{ 
    int data; 
    Node left, right; 

    Node(int item)  
    { 
        data = item; 
        right = left = null; 
    } 
} 

public class BinaryTree  
{ 
    Node root; 
    Node head; // will point to head of DLL   
    Node prev; // temporary pointer  

    // The main function that links the list list to be traversed 
    public Node extractLeafList(Node root)  
    { 
        if (root == null) 
            return null; 
        if (root.left == null && root.right == null)  
        { 
            if (head == null)  
            { 
                head = root; 
                prev = root; 
            }  
            else 
            { 
                prev.right = root; 
                root.left = prev; 
                prev = root; 
            } 
            return null; 
        } 
        root.left = extractLeafList(root.left); 
        root.right = extractLeafList(root.right); 
        return root; 
    } 

    //Prints the DLL in both forward and reverse directions. 
    public void printDLL(Node head)  
    { 
        Node last = null; 
        while (head != null)  
        { 
            System.out.print(head.data + " "); 
            last = head; 
            head = head.right; 
        } 
    } 

    void inorder(Node node)  
    { 
        if (node == null) 
            return; 
        inorder(node.left); 
        System.out.print(node.data + " "); 
        inorder(node.right); 
    } 

    // Driver program to test above functions 
    public static void main(String args[])  
    { 
        BinaryTree tree = new BinaryTree(); 
        tree.root = new Node(1); 
        tree.root.left = new Node(2); 
        tree.root.right = new Node(3); 

        tree.root.left.left = new Node(4); 
        tree.root.left.right = new Node(5); 
        tree.root.right.right = new Node(6); 
        tree.root.left.left.left = new Node(7); 
        tree.root.left.left.right = new Node(8); 
        tree.root.right.right.left = new Node(9); 
        tree.root.right.right.right = new Node(10); 

        System.out.println("Inorder traversal of given tree is : "); 
        tree.inorder(tree.root); 
        tree.extractLeafList(tree.root); 
        System.out.println(""); 
        System.out.println("Extracted double link list is : "); 
        tree.printDLL(tree.head); 
        System.out.println(""); 
        System.out.println("Inorder traversal of modified tree is : "); 
        tree.inorder(tree.root); 
    } 
} 

// This code has been contributed by Mayank Jaiswal(mayank_24) 

```

## Python

```py

# Python program to extract leaf nodes from binary tree 
# using double linked list 

# A binary tree node 
class Node: 

    # Constructor to create a new node 
    def __init__(self, data): 
        self.data = data 
        self.left = None
        self.right = None

# Main function which extracts all leaves from given Binary Tree. 
# The function returns new root of Binary Tree (Note that  
# root may change if Binary Tree has only one node). 
# The function also sets *head_ref as head of doubly linked list. 
# left pointer of tree is used as prev in DLL 
# and right pointer is used as next 
def extractLeafList(root): 

    # Base Case 
    if root is None: 
        return None

    if root.left is None and root.right is None: 
        # This node is going to be added to doubly linked 
        # list of leaves, set pointer of this node as 
        # previous head of DLL. We don't need to set left 
        # pointer as left is already None 
        root.right = extractLeafList.head 

        # Change the left pointer of previous head 
        if extractLeafList.head is not None: 
            extractLeafList.head.left = root 

        # Change head of linked list 
        extractLeafList.head = root 

        return None # Return new root 

    # Recur for right and left subtrees 
    root.right = extractLeafList(root.right) 
    root.left = extractLeafList(root.left) 

    return root  

# Utility function for printing tree in InOrder 
def printInorder(root): 
    if root is not None: 
        printInorder(root.left) 
        print root.data, 
        printInorder(root.right) 

def printList(head): 
    while(head): 
        if head.data is not None: 
            print head.data, 
        head = head.right 

# Driver program to test above function 
extractLeafList.head = Node(None) 
root = Node(1) 
root.left = Node(2) 
root.right = Node(3) 
root.left.left = Node(4) 
root.left.right = Node(5) 
root.right.right = Node(6) 
root.left.left.left = Node(7) 
root.left.left.right = Node(8) 
root.right.right.left = Node(9) 
root.right.right.right = Node(10) 

print "Inorder traversal of given tree is:"
printInorder(root) 

root = extractLeafList(root) 

print "\nExtract Double Linked List is:"
printList(extractLeafList.head) 

print "\nInorder traversal of modified tree is:"
printInorder(root) 

```

## C#

```cs

// C# program to extract leaf  
// nodes from binary tree 
// using double linked list 
using System; 

// A binay tree node 
public class Node  
{ 
    public int data; 
    public Node left, right; 

    public Node(int item)  
    { 
        data = item; 
        right = left = null; 
    } 
} 

public class BinaryTree  
{ 
    Node root; 
    Node head; // will point to head of DLL  
    Node prev; // temporary pointer  

    // The main function that links  
    // the list list to be traversed 
    public Node extractLeafList(Node root)  
    { 
        if (root == null) 
            return null; 
        if (root.left == null && root.right == null)  
        { 
            if (head == null)  
            { 
                head = root; 
                prev = root; 
            }  
            else
            { 
                prev.right = root; 
                root.left = prev; 
                prev = root; 
            } 
            return null; 
        } 
        root.left = extractLeafList(root.left); 
        root.right = extractLeafList(root.right); 
        return root; 
    } 

    // Prints the DLL in both forward 
    // and reverse directions. 
    public void printDLL(Node head)  
    { 
        Node last = null; 
        while (head != null)  
        { 
            Console.Write(head.data + " "); 
            last = head; 
            head = head.right; 
        } 
    } 

    void inorder(Node node)  
    { 
        if (node == null) 
            return; 
        inorder(node.left); 
        Console.Write(node.data + " "); 
        inorder(node.right); 
    } 

    // Driver code 
    public static void Main(String []args)  
    { 
        BinaryTree tree = new BinaryTree(); 
        tree.root = new Node(1); 
        tree.root.left = new Node(2); 
        tree.root.right = new Node(3); 

        tree.root.left.left = new Node(4); 
        tree.root.left.right = new Node(5); 
        tree.root.right.right = new Node(6); 
        tree.root.left.left.left = new Node(7); 
        tree.root.left.left.right = new Node(8); 
        tree.root.right.right.left = new Node(9); 
        tree.root.right.right.right = new Node(10); 

        Console.WriteLine("Inorder traversal of given tree is : "); 
        tree.inorder(tree.root); 
        tree.extractLeafList(tree.root); 
        Console.WriteLine(""); 
        Console.WriteLine("Extracted double link list is : "); 
        tree.printDLL(tree.head); 
        Console.WriteLine(""); 
        Console.WriteLine("Inorder traversal of modified tree is : "); 
        tree.inorder(tree.root); 
    } 
} 

// This code has been contributed by 29AjayKumar 

```

**Output:**

```
Inorder Trvaersal of given Tree is:
7 4 8 2 5 1 3 9 6 10
Extracted Double Linked list is:
7 8 5 9 10
Inorder traversal of modified tree is:
4 2 1 3 6
```

**时间复杂度**：`O(n)`，该解决方案对给定的二叉树进行单个遍历。

本文由 [**Chandra Prakash**](https://www.facebook.com/chandra.prakash.52643?fref=ts) 贡献。 如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请发表评论。

