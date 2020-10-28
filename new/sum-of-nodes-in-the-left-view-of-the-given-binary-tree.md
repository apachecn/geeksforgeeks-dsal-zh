# 给定二叉树

> 原文：[https://www.geeksforgeeks.org/sum-of-nodes-in-the-left-view-of-the-given-binary-tree/](https://www.geeksforgeeks.org/sum-of-nodes-in-the-left-view-of-the-given-binary-tree/)

左侧视图中的节点总数

给定一个二叉树，任务是找到在左视图中可见的节点的总和。 二叉树的左视图是从左侧查看树时可见的节点集。

**示例**：

```
Input:
       1
      /  \
     2    3
    / \    \
   4   5    6
Output: 7
1 + 2 + 4 = 7

Input:
       1
      /  \
    2      3
      \   
        4  
          \
            5
             \
               6
Output: 18

```

**方法**：可以使用简单的递归遍历来解决该问题。 我们可以通过将参数传递给所有递归调用来跟踪节点的级别。 想法是也要跟踪最大级别，并以在左子树之前访问左子树的方式遍历该树。 每当遇到其级别超过最大级别的节点时，都将节点的值添加到总和中，因为它是其级别中的第一个节点（请注意，左子树在右子树之前被遍历）。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation of the approach 
#include <bits/stdc++.h> 
using namespace std; 

class Node { 
public: 
    int data; 
    Node *left, *right; 
}; 

// A utility function to create 
// a new Binary Tree Node 
Node* newNode(int item) 
{ 
    Node* temp = new Node(); 
    temp->data = item; 
    temp->left = temp->right = NULL; 
    return temp; 
} 

// Recursive function to find the sum of nodes 
// of the left view of the given binary tree 
void sumLeftViewUtil(Node* root, int level, int* max_level, int* sum) 
{ 
    // Base Case 
    if (root == NULL) 
        return; 

    // If this is the first Node of its level 
    if (*max_level < level) { 
        *sum += root->data; 
        *max_level = level; 
    } 

    // Recur for left and right subtrees 
    sumLeftViewUtil(root->left, level + 1, max_level, sum); 
    sumLeftViewUtil(root->right, level + 1, max_level, sum); 
} 

// A wrapper over sumLeftViewUtil() 
void sumLeftView(Node* root) 
{ 
    int max_level = 0; 
    int sum = 0; 
    sumLeftViewUtil(root, 1, &max_level, &sum); 
    cout << sum; 
} 

// Driver code 
int main() 
{ 
    Node* root = newNode(12); 
    root->left = newNode(10); 
    root->right = newNode(30); 
    root->right->left = newNode(25); 
    root->right->right = newNode(40); 

    sumLeftView(root); 

    return 0; 
} 

```

## Java

```java

// Java implementation of the approach 

// Class for a node of the tree 
class Node { 
    int data; 
    Node left, right; 

    public Node(int item) 
    { 
        data = item; 
        left = right = null; 
    } 
} 

class BinaryTree { 
    Node root; 
    static int max_level = 0; 
    static int sum = 0; 

    // Recursive function to find the sum of nodes 
    // of the left view of the given binary tree 
    void sumLeftViewUtil(Node node, int level) 
    { 
        // Base Case 
        if (node == null) 
            return; 

        // If this is the first node of its level 
        if (max_level < level) { 
            sum += node.data; 
            max_level = level; 
        } 

        // Recur for left and right subtrees 
        sumLeftViewUtil(node.left, level + 1); 
        sumLeftViewUtil(node.right, level + 1); 
    } 

    // A wrapper over sumLeftViewUtil() 
    void sumLeftView() 
    { 

        sumLeftViewUtil(root, 1); 
        System.out.print(sum); 
    } 

    // Driver code 
    public static void main(String args[]) 
    { 
        BinaryTree tree = new BinaryTree(); 
        tree.root = new Node(12); 
        tree.root.left = new Node(10); 
        tree.root.right = new Node(30); 
        tree.root.right.left = new Node(25); 
        tree.root.right.right = new Node(40); 

        tree.sumLeftView(); 
    } 
} 

```

## Python3

```py

# Python3 implementation of the approach 

# A binary tree node  
class Node:  

    # Constructor to create a new node  
    def __init__(self, data):  
        self.data = data  
        self.left = None
        self.right = None

# Recursive function to find the sum of nodes  
# of the left view of the given binary tree 
def sumLeftViewUtil(root, level, max_level, sum):  

    # Base Case  
    if root is None:  
        return

    # If this is the first node of its level  
    if (max_level[0] < level):  
        sum[0]+= root.data  
        max_level[0] = level  

    # Recur for left and right subtree  
    sumLeftViewUtil(root.left, level + 1, max_level, sum)  
    sumLeftViewUtil(root.right, level + 1, max_level, sum)  

# A wrapper over sumLeftViewUtil()  
def sumLeftView(root):  
    max_level = [0]  
    sum =[0] 
    sumLeftViewUtil(root, 1, max_level, sum)  
    print(sum[0]) 

# Driver code 
root = Node(12)  
root.left = Node(10)  
root.right = Node(20)  
root.right.left = Node(25)  
root.right.right = Node(40)  
sumLeftView(root) 

```

## C#

```cs

// C# implementation of the approach 
using System; 

// Class for a node of the tree 
public class Node { 
    public int data; 
    public Node left, right; 

    public Node(int item) 
    { 
        data = item; 
        left = right = null; 
    } 
} 

public class BinaryTree { 
    public Node root; 
    public static int max_level = 0; 
    public static int sum = 0; 

    // Recursive function to find the sum of nodes 
    // of the left view of the given binary tree 
    public virtual void leftViewUtil(Node node, int level) 
    { 
        // Base Case 
        if (node == null) { 
            return; 
        } 

        // If this is the first node of its level 
        if (max_level < level) { 
            sum += node.data; 
            max_level = level; 
        } 

        // Recur for left and right subtrees 
        leftViewUtil(node.left, level + 1); 
        leftViewUtil(node.right, level + 1); 
    } 

    // A wrapper over leftViewUtil() 
    public virtual void leftView() 
    { 
        leftViewUtil(root, 1); 
        Console.Write(sum); 
    } 

    // Driver code 
    public static void Main(string[] args) 
    { 
        BinaryTree tree = new BinaryTree(); 
        tree.root = new Node(12); 
        tree.root.left = new Node(10); 
        tree.root.right = new Node(30); 
        tree.root.right.left = new Node(25); 
        tree.root.right.right = new Node(40); 

        tree.leftView(); 
    } 
} 

```

**Output:**

```
47

```



* * *

* * *



