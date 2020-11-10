# 给定二叉树

> 原文：[https://www.geeksforgeeks.org/sum-of-nodes-in-the-right-view-of-the-given-binary-tree/](https://www.geeksforgeeks.org/sum-of-nodes-in-the-right-view-of-the-given-binary-tree/)

右侧视图中的节点总数

给定一个二叉树，任务是找到在右视图中可见的节点的总和。 二叉树的右视图是从右侧查看树时可见的节点集。

**示例**：

```
Input:
       1
      /  \
     2    3
    / \    \
   4   5    6
Output: 10
1 + 3 + 6 = 10

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
Output: 19

```

**方法**：可以使用简单的递归遍历来解决该问题。 我们可以通过将参数传递给所有递归调用来跟踪节点的级别。 想法是也要跟踪最大级别，并以在左子树之前访问右子树的方式遍历树。 每当遇到其级别超过最大级别的节点时，将节点的值添加到总和中，因为它是其级别中的最后一个节点（请注意，右子树在左子树之前被遍历）。

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
// of the right view of the given binary tree 
void sumRightViewUtil(Node* root, int level, 
                      int* max_level, int* sum) 
{ 
    // Base Case 
    if (root == NULL) 
        return; 

    // If this is the last Node of its level 
    if (*max_level < level) { 
        *sum += root->data; 
        *max_level = level; 
    } 

    // Recur for left and right subtrees 
    sumRightViewUtil(root->right, level + 1, max_level, sum); 
    sumRightViewUtil(root->left, level + 1, max_level, sum); 
} 

// A wrapper over sumRightViewUtil() 
void sumRightView(Node* root) 
{ 
    int max_level = 0; 
    int sum = 0; 
    sumRightViewUtil(root, 1, &max_level, &sum); 
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

    sumRightView(root); 

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
    // of the right view of the given binary tree 
    void sumRightViewUtil(Node node, int level) 
    { 
        // Base Case 
        if (node == null) 
            return; 

        // If this is the last node of its level 
        if (max_level < level) { 
            sum += node.data; 
            max_level = level; 
        } 

        // Recur for left and right subtrees 
        sumRightViewUtil(node.right, level + 1); 
        sumRightViewUtil(node.left, level + 1); 
    } 

    // A wrapper over sumRightViewUtil() 
    void sumRightView() 
    { 

        sumRightViewUtil(root, 1); 
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

        tree.sumRightView(); 
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
# of the right view of the given binary tree 
def sumRightViewUtil(root, level, max_level, sum):  

    # Base Case  
    if root is None:  
        return

    # If this is the last node of its level  
    if (max_level[0] < level):  
        sum[0]+= root.data  
        max_level[0] = level  

    # Recur for left and right subtree  
    sumRightViewUtil(root.right, level + 1, max_level, sum)  
    sumRightViewUtil(root.left, level + 1, max_level, sum)  

# A wrapper over sumRightViewUtil()  
def sumRightView(root):  
    max_level = [0]  
    sum =[0] 
    sumRightViewUtil(root, 1, max_level, sum)  
    print(sum[0]) 

# Driver code 
root = Node(12)  
root.left = Node(10)  
root.right = Node(30)  
root.right.left = Node(25)  
root.right.right = Node(40)  
sumRightView(root) 

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
    // of the right view of the given binary tree 
    public virtual void sumrightViewUtil(Node node, int level) 
    { 
        // Base Case 
        if (node == null) { 
            return; 
        } 

        // If this is the last node of its level 
        if (max_level < level) { 
            sum += node.data; 
            max_level = level; 
        } 

        // Recur for left and right subtrees 
        sumrightViewUtil(node.right, level + 1); 
        sumrightViewUtil(node.left, level + 1); 
    } 

    // A wrapper over sumrightViewUtil() 
    public virtual void sumrightView() 
    { 
        sumrightViewUtil(root, 1); 
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

        tree.sumrightView(); 
    } 
} 

```

**输出**：

```
82

```



* * *

* * *



