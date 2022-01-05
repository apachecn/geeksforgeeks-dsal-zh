# 从左到右打印二叉树的所有叶节点

> 原文:[https://www . geesforgeks . org/print-leaf-nodes-left-right-二叉树/](https://www.geeksforgeeks.org/print-leaf-nodes-left-right-binary-tree/)

给定一棵二叉树，我们需要编写一个程序，从左到右打印给定二叉树的所有叶子节点。也就是说，节点应该按照它们在给定树中从左到右的顺序打印。

例如

![](img/909a1c04e02efb05f7e7340542a1a532.png)

对于上面的二叉树，输出将如下所示:

```
4 6 7 9 10
```

这样做的思路类似于 [DFS 算法](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/)。下面是实现这一点的分步算法:

1.  检查给定的节点是否为空。如果为空，则从函数返回。
2.  检查它是否是叶节点。如果该节点是叶节点，则打印其数据。
3.  如果在上述步骤中，该节点不是叶节点，则检查该节点的左右子节点是否存在。如果是，则递归调用该节点左右子节点的函数。

下面是上述方法的实现。

## C++

```
/* C++ program to print leaf nodes from left
   to right */
#include <iostream>
using namespace std;

// A Binary Tree Node
struct Node
{
    int data;
    struct Node *left, *right;
};

// function to print leaf
// nodes from left to right
void printLeafNodes(Node *root)
{
    // if node is null, return
    if (!root)
        return;

    // if node is leaf node, print its data   
    if (!root->left && !root->right)
    {
        cout << root->data << " ";
        return;
    }

    // if left child exists, check for leaf
    // recursively
    if (root->left)
       printLeafNodes(root->left);

    // if right child exists, check for leaf
    // recursively
    if (root->right)
       printLeafNodes(root->right);
}

// Utility function to create a new tree node
Node* newNode(int data)
{
    Node *temp = new Node;
    temp->data = data;
    temp->left = temp->right = NULL;
    return temp;
}

// Driver program to test above functions
int main()
{
    // Let us create binary tree shown in
    // above diagram
    Node *root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->right->left = newNode(5);
    root->right->right = newNode(8);
    root->right->left->left = newNode(6);
    root->right->left->right = newNode(7);
    root->right->right->left = newNode(9);
    root->right->right->right = newNode(10);

    // print leaf nodes of the given tree
    printLeafNodes(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print leaf nodes
// from left to right
import java.util.*;

class GFG{

// A Binary Tree Node
static class Node
{
    public int data;
    public Node left, right;
};

// Function to print leaf
// nodes from left to right
static void printLeafNodes(Node root)
{

    // If node is null, return
    if (root == null)
        return;

    // If node is leaf node, print its data    
    if (root.left == null &&
        root.right == null)
    {
        System.out.print(root.data + " ");
        return;
    }

    // If left child exists, check for leaf
    // recursively
    if (root.left != null)
        printLeafNodes(root.left);

    // If right child exists, check for leaf
    // recursively
    if (root.right != null)
        printLeafNodes(root.right);
}

// Utility function to create a new tree node
static Node newNode(int data)
{
    Node temp = new Node();
    temp.data = data;
    temp.left = null;
    temp.right = null;
    return temp;
}

// Driver code
public static void main(String []args)
{

    // Let us create binary tree shown in
    // above diagram
    Node root = newNode(1);
    root.left = newNode(2);
    root.right = newNode(3);
    root.left.left = newNode(4);
    root.right.left = newNode(5);
    root.right.right = newNode(8);
    root.right.left.left = newNode(6);
    root.right.left.right = newNode(7);
    root.right.right.left = newNode(9);
    root.right.right.right = newNode(10);

    // Print leaf nodes of the given tree
    printLeafNodes(root);
}
}

// This code is contributed by pratham76
```

## 蟒蛇 3

```
# Python3 program to print
# leaf nodes from left to right

# Binary tree node
class Node:

    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# Function to print leaf
# nodes from left to right
def printLeafNodes(root: Node) -> None:

    # If node is null, return
    if (not root):
        return

    # If node is leaf node,
    # print its data
    if (not root.left and
        not root.right):
        print(root.data,
              end = " ")
        return

    # If left child exists,
    # check for leaf recursively
    if root.left:
        printLeafNodes(root.left)

    # If right child exists,
    # check for leaf recursively
    if root.right:
        printLeafNodes(root.right)

# Driver Code
if __name__ == "__main__":

    # Let us create binary tree shown in
    # above diagram
    root = Node(1)
    root.left = Node(2)
    root.right = Node(3)
    root.left.left = Node(4)
    root.right.left = Node(5)
    root.right.right = Node(8)
    root.right.left.left = Node(6)
    root.right.left.right = Node(7)
    root.right.right.left = Node(9)
    root.right.right.right = Node(10)

    # print leaf nodes of the given tree
    printLeafNodes(root)

# This code is contributed by sanjeev2552
```

## C#

```
// C# program to print leaf nodes
// from left to right
using System;

class GFG{

// A Binary Tree Node
class Node
{
    public int data;
    public Node left, right;
};

// Function to print leaf
// nodes from left to right
static void printLeafNodes(Node root)
{

    // If node is null, return
    if (root == null)
        return;

    // If node is leaf node, print its data    
    if (root.left == null &&
        root.right == null)
    {
        Console.Write(root.data + " ");
        return;
    }

    // If left child exists, check for leaf
    // recursively
    if (root.left != null)
        printLeafNodes(root.left);

    // If right child exists, check for leaf
    // recursively
    if (root.right != null)
        printLeafNodes(root.right);
}

// Utility function to create a new tree node
static Node newNode(int data)
{
    Node temp = new Node();
    temp.data = data;
    temp.left = null;
    temp.right = null;
    return temp;
}

// Driver code
public static void Main()
{

    // Let us create binary tree shown in
    // above diagram
    Node root = newNode(1);
    root.left = newNode(2);
    root.right = newNode(3);
    root.left.left = newNode(4);
    root.right.left = newNode(5);
    root.right.right = newNode(8);
    root.right.left.left = newNode(6);
    root.right.left.right = newNode(7);
    root.right.right.left = newNode(9);
    root.right.right.right = newNode(10);

    // Print leaf nodes of the given tree
    printLeafNodes(root);
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

// Javascript program to print leaf nodes
// from left to right

// A Binary Tree Node
class Node
{
    constructor()
    {
        this.data = 0;
        this.left = null;
        this.right = null;
    }
};

// Function to print leaf
// nodes from left to right
function printLeafNodes(root)
{

    // If node is null, return
    if (root == null)
        return;

    // If node is leaf node, print its data    
    if (root.left == null &&
        root.right == null)
    {
        document.write(root.data + " ");
        return;
    }

    // If left child exists, check for leaf
    // recursively
    if (root.left != null)
        printLeafNodes(root.left);

    // If right child exists, check for leaf
    // recursively
    if (root.right != null)
        printLeafNodes(root.right);
}

// Utility function to create a new tree node
function newNode(data)
{
    var temp = new Node();
    temp.data = data;
    temp.left = null;
    temp.right = null;
    return temp;
}

// Driver code

// Let us create binary tree shown in
// above diagram
var root = newNode(1);
root.left = newNode(2);
root.right = newNode(3);
root.left.left = newNode(4);
root.right.left = newNode(5);
root.right.right = newNode(8);
root.right.left.left = newNode(6);
root.right.left.right = newNode(7);
root.right.right.left = newNode(9);
root.right.right.right = newNode(10);

// Print leaf nodes of the given tree
printLeafNodes(root);

// This code is contributed by rrrtnx

</script>
```

**输出:**

```
4 6 7 9 10
```

**时间复杂度** : O( n)，其中 n 为二叉树中的节点数。

https://youtu.be/rBekvLt23wY?list = plqm7 alhxfyshcxd 7 r1j 0k y9 ZG _ gbb1 dbk
本文由[T2【哈什·阿加瓦尔 T4【投稿】撰写。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用](https://www.facebook.com/harsh.agarwal.16752)[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。