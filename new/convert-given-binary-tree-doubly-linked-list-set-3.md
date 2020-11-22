# 将给定的二叉树转换为双链表 | 系列 3

> 原文：[https://www.geeksforgeeks.org/convert-given-binary-tree-doubly-linked-list-set-3/](https://www.geeksforgeeks.org/convert-given-binary-tree-doubly-linked-list-set-3/)

给定二叉树（BT），将其转换为原地双链表（DLL）。 节点中的左指针和右指针分别用作转换后的双链表中的上一个指针和下一个指针。 双链表中节点的顺序必须与给定二叉树的顺序相同。 有序遍历的第一个节点（BT 中最左边的节点）必须是双链表的头节点。

![TreeToList](img/1e6723c342ed8e5706a1c58b68241a4c.png)

针对此问题讨论了以下两种不同的解决方案。

[将给定的二叉树转换为双链表 | 系列 1](https://www.geeksforgeeks.org/in-place-convert-a-given-binary-tree-to-doubly-linked-list/)

[将给定的二叉树转换为双链表| 组合 2](https://www.geeksforgeeks.org/convert-a-given-binary-tree-to-doubly-linked-list-set-2/)

在这篇文章中，讨论了第三个解决方案，这似乎是最简单的。 这个想法是对二叉树进行有序遍历。 在进行有序遍历时，请在变量`prev`中跟踪先前访问的节点。 对于每个访问的节点，将其变为`prev`的下一个，并将该节点的前一个变为`prev`。

感谢 rahul，wishall 和所有其他读者对以上两个帖子的有用评论。

以下是此解决方案的实现。

## C++

```cpp

// A C++ program for in-place conversion of Binary Tree to DLL 
#include <iostream> 
using namespace std; 

/* A binary tree node has data, and left and right pointers */
struct node 
{ 
    int data; 
    node* left; 
    node* right; 
}; 

// A simple recursive function to convert a given Binary tree to Doubly 
// Linked List 
// root --> Root of Binary Tree 
// head --> Pointer to head node of created doubly linked list 
void BinaryTree2DoubleLinkedList(node *root, node **head) 
{ 
    // Base case 
    if (root == NULL) return; 

    // Initialize previously visited node as NULL. This is 
    // static so that the same value is accessible in all recursive 
    // calls 
    static node* prev = NULL; 

    // Recursively convert left subtree 
    BinaryTree2DoubleLinkedList(root->left, head); 

    // Now convert this node 
    if (prev == NULL) 
        *head = root; 
    else
    { 
        root->left = prev; 
        prev->right = root; 
    } 
    prev = root; 

    // Finally convert right subtree 
    BinaryTree2DoubleLinkedList(root->right, head); 
} 

/* Helper function that allocates a new node with the 
   given data and NULL left and right pointers. */
node* newNode(int data) 
{ 
    node* new_node = new node; 
    new_node->data = data; 
    new_node->left = new_node->right = NULL; 
    return (new_node); 
} 

/* Function to print nodes in a given doubly linked list */
void printList(node *node) 
{ 
    while (node!=NULL) 
    { 
        cout << node->data << " "; 
        node = node->right; 
    } 
} 

/* Driver program to test above functions*/
int main() 
{ 
    // Let us create the tree shown in above diagram 
    node *root        = newNode(10); 
    root->left        = newNode(12); 
    root->right       = newNode(15); 
    root->left->left  = newNode(25); 
    root->left->right = newNode(30); 
    root->right->left = newNode(36); 

    // Convert to DLL 
    node *head = NULL; 
    BinaryTree2DoubleLinkedList(root, &head); 

    // Print the converted list 
    printList(head); 

    return 0; 
} 

```

## Java

```java

// A Java program for in-place conversion of Binary Tree to DLL 

// A binary tree node has data, left pointers and right pointers 
class Node  
{ 
    int data; 
    Node left, right; 

    public Node(int data)  
    { 
        this.data = data; 
        left = right = null; 
    } 
} 

class BinaryTree  
{ 
    Node root; 

    // head --> Pointer to head node of created doubly linked list 
    Node head; 

    // Initialize previously visited node as NULL. This is 
    // static so that the same value is accessible in all recursive 
    // calls 
    static Node prev = null; 

    // A simple recursive function to convert a given Binary tree  
    // to Doubly Linked List 
    // root --> Root of Binary Tree 
    void BinaryTree2DoubleLinkedList(Node root)  
    { 
        // Base case 
        if (root == null) 
            return; 

        // Recursively convert left subtree 
        BinaryTree2DoubleLinkedList(root.left); 

        // Now convert this node 
        if (prev == null)  
            head = root; 
        else
        { 
            root.left = prev; 
            prev.right = root; 
        } 
        prev = root; 

        // Finally convert right subtree 
        BinaryTree2DoubleLinkedList(root.right); 
    } 

    /* Function to print nodes in a given doubly linked list */
    void printList(Node node) 
    { 
        while (node != null)  
        { 
            System.out.print(node.data + " "); 
            node = node.right; 
        } 
    } 

    // Driver program to test above functions 
    public static void main(String[] args)  
    { 
        // Let us create the tree as shown in above diagram 
        BinaryTree tree = new BinaryTree(); 
        tree.root = new Node(10); 
        tree.root.left = new Node(12); 
        tree.root.right = new Node(15); 
        tree.root.left.left = new Node(25); 
        tree.root.left.right = new Node(30); 
        tree.root.right.left = new Node(36); 

        // convert to DLL 
        tree.BinaryTree2DoubleLinkedList(tree.root); 

        // Print the converted List 
        tree.printList(tree.head); 

    } 
} 
// This code has been contributed by Mayank Jaiswal(mayank_24) 

```

## C#

```cs

// A C# program for in-place conversion 
// of Binary Tree to DLL  
using System; 

// A binary tree node has data, left  
// pointers and right pointers  
public class Node 
{ 
    public int data; 
    public Node left, right; 

    public Node(int data) 
    { 
        this.data = data; 
        left = right = null; 
    } 
} 

class GFG 
{ 
public Node root; 

// head --> Pointer to head node of  
// created doubly linked list  
public Node head; 

// Initialize previously visited node  
// as NULL. This is static so that the 
// same value is accessible in all  
// recursive calls  
public static Node prev = null; 

// A simple recursive function to  
// convert a given Binary tree  
// to Doubly Linked List  
// root --> Root of Binary Tree  
public virtual void BinaryTree2DoubleLinkedList(Node root) 
{ 
    // Base case  
    if (root == null) 
    { 
        return; 
    } 

    // Recursively convert left subtree  
    BinaryTree2DoubleLinkedList(root.left); 

    // Now convert this node  
    if (prev == null) 
    { 
        head = root; 
    } 
    else
    { 
        root.left = prev; 
        prev.right = root; 
    } 
    prev = root; 

    // Finally convert right subtree  
    BinaryTree2DoubleLinkedList(root.right); 
} 

/* Function to print nodes in a  
   given doubly linked list */
public virtual void printList(Node node) 
{ 
    while (node != null) 
    { 
        Console.Write(node.data + " "); 
        node = node.right; 
    } 
} 

// Driver Code 
public static void Main(string[] args) 
{ 
    // Let us create the tree as  
    // shown in above diagram  
    GFG tree = new GFG(); 
    tree.root = new Node(10); 
    tree.root.left = new Node(12); 
    tree.root.right = new Node(15); 
    tree.root.left.left = new Node(25); 
    tree.root.left.right = new Node(30); 
    tree.root.right.left = new Node(36); 

    // convert to DLL  
    tree.BinaryTree2DoubleLinkedList(tree.root); 

    // Print the converted List  
    tree.printList(tree.head); 

} 
} 

// This code is contributed by Shrikant13 

```

**输出**：

```
25 12 30 10 36 15
```

请注意，不建议您像上面那样使用静态变量（为简单起见，我们使用了静态变量）。 想象一下，对于两棵或更多棵树调用相同功能的情况， *prev* 的旧值将在下一次对另一棵树的调用中使用。 为避免此类问题，我们可以使用双指针或引用指针。

**时间复杂度**：上面的程序执行简单的有序遍历，因此时间复杂度为`O(n)`，其中 n 是给定二叉树中的节点数。

如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请发表评论

