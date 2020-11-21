# 将二叉树展平为链表 | 系列 3

> 原文：[https://www.geeksforgeeks.org/flatten-a-binary-tree-into-linked-list-set-3/](https://www.geeksforgeeks.org/flatten-a-binary-tree-into-linked-list-set-3/)

给定一棵二叉树，将其平整就位到链表中。 不允许使用辅助数据结构。 展平后，每个节点的左侧应指向 NULL，右侧应按级别顺序包含下一个节点。

**示例**：

```
Input: 
          1
        /   \
       2     5
      / \     \
     3   4     6

Output:
    1
     \
      2
       \
        3
         \
          4
           \
            5
             \
              6

Input:
        1
       / \
      3   4
         /
        2
         \
          5
Output:
     1
      \
       3
        \
         4
          \
           2
            \ 
             5

```

**方法**：以有序格式递归二叉树，在函数调用的每个阶段传递平展链表中最后一个节点的地址，以便当前节点可以使自己成为最后一个节点的右节点。

对于左孩子，其父节点是拼合列表中的最后一个节点。

对于右孩子，有两个条件：

*   如果父节点没有左子节点，则父节点是展平列表中的最后一个节点。

*   如果 left child 不为 null，则左子树中的叶节点是扁平化列表中的最后一个节点。

下面是上述方法的实现：

## C++

```cpp

// C++ program to flatten the binary tree 
// using previous node approach 
using namespace std; 
#include <iostream> 
#include <stdlib.h> 

// Structure to represent a node of the tree 
struct Node { 
    int data; 
    struct Node* left; 
    struct Node* right; 
}; 

Node* AllocNode(int data) 
{ 
    Node* temp = new Node; 
    temp->left = NULL; 
    temp->right = NULL; 
    temp->data = data; 
    return temp; 
} 

// Utility function to print the inorder 
// traversal of the tree 
void PrintInorderBinaryTree(Node* root) 
{ 
    if (root == NULL) 
        return; 
    PrintInorderBinaryTree(root->left); 
    std::cout << root->data << " "; 
    PrintInorderBinaryTree(root->right); 
} 

// Function to make current node right of 
// the last node in the list 
void FlattenBinaryTree(Node* root, Node** last) 
{ 
    if (root == NULL) 
        return; 

    Node* left = root->left; 
    Node* right = root->right; 

    // Avoid first iteration where root is 
    // the only node in the list 
    if (root != *last) { 
        (*last)->right = root; 
        (*last)->left = NULL; 
        *last = root; 
    } 

    FlattenBinaryTree(left, last); 
    FlattenBinaryTree(right, last); 
    if (left == NULL && right == NULL) 
        *last = root; 
} 

// Driver Code 
int main() 
{ 

    // Build the tree 
    Node* root = AllocNode(1); 
    root->left = AllocNode(2); 
    root->left->left = AllocNode(3); 
    root->left->right = AllocNode(4); 
    root->right = AllocNode(5); 
    root->right->right = AllocNode(6); 

    // Print the inorder traversal of the 
    // original tree 
    std::cout << "Original inorder traversal : "; 
    PrintInorderBinaryTree(root); 
    std::cout << std::endl; 

    // Flatten a binary tree, at the beginning 
    // root node is the only and last in the list 
    Node* last = root; 
    FlattenBinaryTree(root, &last); 

    // Print the inorder traversal of the flattened 
    // binary tree 
    std::cout << "Flattened inorder traversal : "; 
    PrintInorderBinaryTree(root); 
    std::cout << std::endl; 

    return 0; 
} 

```

## Java

```java

// Java program to flatten the binary tree 
// using previous node approach 
class GFG 
{ 

// Structure to represent a node of the tree 
static class Node 
{ 
    int data; 
    Node left; 
    Node right; 
}; 

static Node AllocNode(int data) 
{ 
    Node temp = new Node(); 
    temp.left = null; 
    temp.right = null; 
    temp.data = data; 
    return temp; 
} 

// Utility function to print the inorder 
// traversal of the tree 
static void PrintInorderBinaryTree(Node root) 
{ 
    if (root == null) 
        return; 
    PrintInorderBinaryTree(root.left); 
    System.out.print( root.data + " "); 
    PrintInorderBinaryTree(root.right); 
} 

static Node last =null; 

// Function to make current node right of 
// the last node in the list 
static void FlattenBinaryTree(Node root) 
{ 
    if (root == null) 
        return; 

    Node left = root.left; 
    Node right = root.right; 

    // Avoid first iteration where root is 
    // the only node in the list 
    if (root != last) { 
        (last).right = root; 
        (last).left = null; 
        last = root; 
    } 

    FlattenBinaryTree(left); 
    FlattenBinaryTree(right); 
    if (left == null && right == null) 
        last = root; 
} 

// Driver Code 
public static void main(String args[]) 
{ 

    // Build the tree 
    Node root = AllocNode(1); 
    root.left = AllocNode(2); 
    root.left.left = AllocNode(3); 
    root.left.right = AllocNode(4); 
    root.right = AllocNode(5); 
    root.right.right = AllocNode(6); 

    // Print the inorder traversal of the 
    // original tree 
    System.out.print("Original inorder traversal : "); 
    PrintInorderBinaryTree(root); 
    System.out.println(); 

    // Flatten a binary tree, at the beginning 
    // root node is the only and last in the list 
    last = root; 
    FlattenBinaryTree(root); 

    // Print the inorder traversal of the flattened 
    // binary tree 
    System.out.print("Flattened inorder traversal : "); 
    PrintInorderBinaryTree(root); 
    System.out.println();  

} 
} 

// This code is contributed by Arnab Kundu 

```

## Python

```py

# Python program to flatten binary tree 
# using previous node approach 

# Node class to represent a node of the tree 
class Node: 
    def __init__(self, data): 
        self.data = data 
        self.right = None
        self.left = None

# Utility function to print the inorder 
# traversal of the tree 
def PrintInorderBinaryTree(root): 
    if(root == None): 
        return
    PrintInorderBinaryTree(root.left) 
    print(str(root.data), end = " ") 
    PrintInorderBinaryTree(root.right) 

# Function to make current node right of 
# the last node in the list 
def FlattenBinaryTree(root): 

    # A global variable which maitains the last node 
    # that was added to the linked list 
    global last 
    if(root == None): 
        return

    left = root.left 
    right = root.right 

    # Avoid first iteration where root is 
    # the only node in the list 
    if(root != last): 
        last.right = root 
        last.left = None
        last = root 
    FlattenBinaryTree(left) 
    FlattenBinaryTree(right) 
    if(left == None and right == None): 
        last = root 

# Build the tree 
root = Node(1) 
root.left = Node(2) 
root.left.left = Node(3) 
root.left.right = Node(4) 
root.right = Node(5) 
root.right.right = Node(6) 

# Print the inorder traversal of the 
# original tree 
print("Original inorder traversal : ", end = "") 
PrintInorderBinaryTree(root) 
print("") 

# Global variable to maintain the  
# last node added to the linked list 
last = root 

# Flatten the binary tree, at the beginning 
# root node is the only node in the list 
FlattenBinaryTree(root) 

# Print the inorder traversal of the flattened  
# binary tree 
print("Flattened inorder traversal : ", end = "") 
PrintInorderBinaryTree(root) 

# This code is contributed by Pranav Devarakonda 

```

## C#

```cs

// C# program to flatten the binary tree 
// using previous node approach 
using System; 

class GFG 
{ 

// Structure to represent a node of the tree 
public class Node 
{ 
    public int data; 
    public Node left; 
    public Node right; 
}; 

static Node AllocNode(int data) 
{ 
    Node temp = new Node(); 
    temp.left = null; 
    temp.right = null; 
    temp.data = data; 
    return temp; 
} 

// Utility function to print the inorder 
// traversal of the tree 
static void PrintInorderBinaryTree(Node root) 
{ 
    if (root == null) 
        return; 
    PrintInorderBinaryTree(root.left); 
    Console.Write(root.data + " "); 
    PrintInorderBinaryTree(root.right); 
} 

static Node last =null; 

// Function to make current node right of 
// the last node in the list 
static void FlattenBinaryTree(Node root) 
{ 
    if (root == null) 
        return; 

    Node left = root.left; 
    Node right = root.right; 

    // Avoid first iteration where root is 
    // the only node in the list 
    if (root != last)  
    { 
        (last).right = root; 
        (last).left = null; 
        last = root; 
    } 

    FlattenBinaryTree(left); 
    FlattenBinaryTree(right); 
    if (left == null && right == null) 
        last = root; 
} 

// Driver Code 
public static void Main(String []args) 
{ 

    // Build the tree 
    Node root = AllocNode(1); 
    root.left = AllocNode(2); 
    root.left.left = AllocNode(3); 
    root.left.right = AllocNode(4); 
    root.right = AllocNode(5); 
    root.right.right = AllocNode(6); 

    // Print the inorder traversal of the 
    // original tree 
    Console.Write("Original inorder traversal : "); 
    PrintInorderBinaryTree(root); 
    Console.WriteLine(); 

    // Flatten a binary tree, at the beginning 
    // root node is the only and last in the list 
    last = root; 
    FlattenBinaryTree(root); 

    // Print the inorder traversal of the flattened 
    // binary tree 
    Console.Write("Flattened inorder traversal : "); 
    PrintInorderBinaryTree(root); 
    Console.WriteLine();  
} 
} 

// This code is contributed by 29AjayKumar 

```

**输出**：

```
Original inorder traversal : 3 2 4 1 5 6 
Flattened inorder traversal : 1 2 3 4 5 6

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。