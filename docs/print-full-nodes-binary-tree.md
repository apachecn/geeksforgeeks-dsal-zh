# 打印二叉树中的所有完整节点

> 原文:[https://www.geeksforgeeks.org/print-full-nodes-binary-tree/](https://www.geeksforgeeks.org/print-full-nodes-binary-tree/)

给定一个二叉树，打印的所有节点都将是满节点。**完整节点**是左右子节点都为非空的节点。
**例:**

```
Input :    10
          /  \
         8    2
        / \   /
       3   5 7
Output : 10 8

Input :   1
         / \
        2   3
           / \
          4   6     
Output : 1 3
```

这是一个简单的问题。我们执行任何一个 transversal([order、Pre order、Pos torder、](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/) level order 遍历)，并保持将具有模式左右子节点的节点打印为非空。

## C++

```
// A C++ program to find the all full nodes in
// a given binary tree
#include <bits/stdc++.h>
using namespace std;

struct Node
{
    int data;
    struct Node *left, *right;
};

Node *newNode(int data)
{
    Node *temp = new Node;
    temp->data = data;
    temp->left = temp->right = NULL;
    return temp;
}

// Traverses given tree in Inorder fashion and
// prints all nodes that have both children as
// non-empty.
void findFullNode(Node *root)
{
    if (root != NULL)
    {
        findFullNode(root->left);
        if (root->left != NULL && root->right != NULL)
            cout << root->data << " ";
        findFullNode(root->right);
    }
}

// Driver program to test above function
int main()
{
    Node* root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->right->left = newNode(5);
    root->right->right = newNode(6);
    root->right->left->right = newNode(7);
    root->right->right->right = newNode(8);
    root->right->left->right->left = newNode(9);
    findFullNode(root);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the all full nodes in
// a given binary tree
public class FullNodes {

    // Traverses given tree in Inorder fashion and
    // prints all nodes that have both children as
    // non-empty.
    public static void findFullNode(Node root)
    {
        if (root != null)
        {
            findFullNode(root.left);
            if (root.left != null && root.right != null)
                System.out.print(root.data+" ");
            findFullNode(root.right);
        }
    }

    public static void main(String args[]) {
        Node root = new Node(1);
        root.left = new Node(2);
        root.right = new Node(3);
        root.left.left = new Node(4);
        root.right.left = new Node(5);
        root.right.right = new Node(6);
        root.right.left.right = new Node(7);
        root.right.right.right = new Node(8);
        root.right.left.right.left = new Node(9);
        findFullNode(root);
    }
}

/* A binary tree node */
class Node
{
    int data;
    Node left, right;
    Node(int data)
    {
        left=right=null;
        this.data=data;
    }
};
//This code is contributed by Gaurav Tiwari
```

## 蟒蛇 3

```
# Python3 program to find the all
# full nodes in a given binary tree

# Binary Tree Node
""" utility that allocates a newNode
with the given key """
class newNode:

    # Construct to create a newNode
    def __init__(self, key):
        self.data = key
        self.left = None
        self.right = None

# Traverses given tree in Inorder
# fashion and prints all nodes that
# have both children as non-empty.
def findFullNode(root) :

    if (root != None) :

        findFullNode(root.left)
        if (root.left != None and
            root.right != None) :
            print(root.data, end = " ")
        findFullNode(root.right)

# Driver Code
if __name__ == '__main__':

    root = newNode(1)
    root.left = newNode(2)
    root.right = newNode(3)
    root.left.left = newNode(4)
    root.right.left = newNode(5)
    root.right.right = newNode(6)
    root.right.left.right = newNode(7)
    root.right.right.right = newNode(8)
    root.right.left.right.left = newNode(9)
    findFullNode(root)

# This code is contributed by
# Shubham Singh(SHUBHAMSINGH10)
```

## C#

```
// C# program to find the all full nodes in
// a given binary tree
using System;

public class FullNodes
{

    // Traverses given tree in Inorder fashion and
    // prints all nodes that have both children as
    // non-empty.
    static void findFullNode(Node root)
    {
        if (root != null)
        {
            findFullNode(root.left);
            if (root.left != null && root.right != null)
                Console.Write(root.data + " ");
            findFullNode(root.right);
        }
    }

    public static void Main(String []args)
    {
        Node root = new Node(1);
        root.left = new Node(2);
        root.right = new Node(3);
        root.left.left = new Node(4);
        root.right.left = new Node(5);
        root.right.right = new Node(6);
        root.right.left.right = new Node(7);
        root.right.right.right = new Node(8);
        root.right.left.right.left = new Node(9);
        findFullNode(root);
    }
}

/* A binary tree node */
class Node
{
    public int data;
    public Node left, right;
    public Node(int data)
    {
        left = right = null;
        this.data = data;
    }
};

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program to find the all full nodes in
// a given binary tree

/* A binary tree node */
class Node
{
    constructor(data)
    {
        this.left=this.right=null;
        this.data=data;
    }
}

// Traverses given tree in Inorder fashion and
    // prints all nodes that have both children as
    // non-empty.
function findFullNode(root)
{
    if (root != null)
        {
            findFullNode(root.left);
            if (root.left != null && root.right != null)
                document.write(root.data+" ");
            findFullNode(root.right);
        }
}

let root = new Node(1);
root.left = new Node(2);
root.right = new Node(3);
root.left.left = new Node(4);
root.right.left = new Node(5);
root.right.right = new Node(6);
root.right.left.right = new Node(7);
root.right.right.right = new Node(8);
root.right.left.right.left = new Node(9);
findFullNode(root);

// This code is contributed by rag2127

</script>
```

**输出:**

```
1 3
```

**时间复杂度:** O(n)
本文由 [**拉克什·库马尔**](https://www.facebook.com/Rakesh2raj) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。