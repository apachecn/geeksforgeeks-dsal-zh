# 打印具有 K 个叶子的二叉树中的所有节点

> 原文:[https://www . geesforgeks . org/print-nodes-binary-tree-k-leaks/](https://www.geeksforgeeks.org/print-nodes-binary-tree-k-leaves/)

给定一棵二叉树和一个整数值 K，任务是在给定的二叉树中找到所有节点，这些节点在以它们为根的子树中有 K 个叶子。

![](img/3fe68e1f4fb92b42bda15ee46d1b9ba1.png)

**例:**

```
// For above binary tree
Input : k = 2
Output: {3}
// here node 3 have k = 2 leaves

Input : k = 1
Output: {6}
// here node 6 have k = 1 leave
```

这里任何有 K 个叶子的节点都意味着左子树和右子树的叶子之和必须等于 K，所以我们用树的后序遍历来解决这个问题。首先我们计算左边子树的叶子，然后计算右边子树的叶子，如果和等于 K，那么打印当前节点。在每次递归调用中，我们将左子树和右子树的叶子的和返回给它的祖先。
以下是上述方法的实施:

## C++

```
// C++ program to count all nodes having k leaves
// in subtree rooted with them
#include<bits/stdc++.h>
using namespace std;

/* A binary tree node  */
struct Node
{
    int data ;
    struct Node * left, * right ;
};

/* Helper function that allocates a new node with the
   given data and NULL left and right pointers. */
struct Node * newNode(int data)
{
    struct Node * node = new Node;
    node->data = data;
    node->left = node->right = NULL;
    return (node);
}

// Function to print all nodes having k leaves
int kLeaves(struct Node *ptr,int k)
{
    // Base Conditions : No leaves
    if (ptr == NULL)
        return 0;

    // if node is leaf
    if (ptr->left == NULL && ptr->right == NULL)
        return 1;

    // total leaves in subtree rooted with this
    // node
    int total = kLeaves(ptr->left, k) +
                kLeaves(ptr->right, k);

    // Print this node if total is k
    if (k == total)
        cout << ptr->data << " ";

    return total;
}

// Driver program to run the case
int main()
{
    struct Node *root = newNode(1);
    root->left        = newNode(2);
    root->right       = newNode(4);
    root->left->left  = newNode(5);
    root->left->right = newNode(6);
    root->left->left->left  = newNode(9);
    root->left->left->right  = newNode(10);
    root->right->right = newNode(8);
    root->right->left  = newNode(7);
    root->right->left->left  = newNode(11);
    root->right->left->right  = newNode(12);

    kLeaves(root, 2);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count all nodes having k leaves
// in subtree rooted with them
class GfG {

/* A binary tree node */
static class Node
{
    int data ;
    Node left, right ;
    Node(int data)
    {
        this.data = data;
    }
    Node()
    {

    }
}

/* Helper function that allocates a new node with the
given data and NULL left and right pointers. */
static Node newNode(int data)
{
    Node node = new Node();
    node.data = data;
    node.left = null;
    node.right = null;
    return (node);
}

// Function to print all nodes having k leaves
static int kLeaves(Node ptr,int k)
{
    // Base Conditions : No leaves
    if (ptr == null)
        return 0;

    // if node is leaf
    if (ptr.left == null && ptr.right == null)
        return 1;

    // total leaves in subtree rooted with this
    // node
    int total = kLeaves(ptr.left, k) + kLeaves(ptr.right, k);

    // Print this node if total is k
    if (k == total)
        System.out.print(ptr.data + " ");

    return total;
}

// Driver program to run the case
public static void main(String[] args)
{
    Node root = newNode(1);
    root.left     = newNode(2);
    root.right     = newNode(4);
    root.left.left = newNode(5);
    root.left.right = newNode(6);
    root.left.left.left = newNode(9);
    root.left.left.right = newNode(10);
    root.right.right = newNode(8);
    root.right.left = newNode(7);
    root.right.left.left = newNode(11);
    root.right.left.right = newNode(12);

    kLeaves(root, 2);

}
}
```

## 蟒蛇 3

```
# Python3 program to count all nodes 
# having k leaves in subtree rooted with them

# A binary tree node has data, pointer to
# left child and a pointer to right child
# Helper function that allocates a new node 
# with the given data and None left and
# right pointers
class newNode:
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# Function to print all nodes having k leaves
def kLeaves(ptr, k):

    # Base Conditions : No leaves
    if (ptr == None):
        return 0

    # if node is leaf
    if (ptr.left == None and
        ptr.right == None):
        return 1

    # total leaves in subtree rooted with this
    # node
    total = kLeaves(ptr.left, k) + \
            kLeaves(ptr.right, k)

    # Prthis node if total is k
    if (k == total):
        print(ptr.data, end = " ")

    return total

# Driver code
root = newNode(1)
root.left = newNode(2)
root.right = newNode(4)
root.left.left = newNode(5)
root.left.right = newNode(6)
root.left.left.left = newNode(9)
root.left.left.right = newNode(10)
root.right.right = newNode(8)
root.right.left = newNode(7)
root.right.left.left = newNode(11)
root.right.left.right = newNode(12)

kLeaves(root, 2)

# This code is contributed by SHUBHAMSINGH10
```

## C#

```
// C# program to count all nodes having k leaves
// in subtree rooted with them
using System;

class GfG
{

/* A binary tree node */
public class Node
{
    public int data ;
    public Node left, right ;
    public Node(int data)
    {
        this.data = data;
    }
    public Node()
    {

    }
}

/* Helper function that allocates a new node with the
given data and NULL left and right pointers. */
static Node newNode(int data)
{
    Node node = new Node();
    node.data = data;
    node.left = null;
    node.right = null;
    return (node);
}

// Function to print all nodes having k leaves
static int kLeaves(Node ptr,int k)
{
    // Base Conditions : No leaves
    if (ptr == null)
        return 0;

    // if node is leaf
    if (ptr.left == null && ptr.right == null)
        return 1;

    // total leaves in subtree rooted with this
    // node
    int total = kLeaves(ptr.left, k) + kLeaves(ptr.right, k);

    // Print this node if total is k
    if (k == total)
        Console.Write(ptr.data + " ");

    return total;
}

// Driver program to run the case
public static void Main(String[] args)
{
    Node root = newNode(1);
    root.left = newNode(2);
    root.right = newNode(4);
    root.left.left = newNode(5);
    root.left.right = newNode(6);
    root.left.left.left = newNode(9);
    root.left.left.right = newNode(10);
    root.right.right = newNode(8);
    root.right.left = newNode(7);
    root.right.left.left = newNode(11);
    root.right.left.right = newNode(12);

    kLeaves(root, 2);

}
}

// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript program to count all nodes having k leaves
// in subtree rooted with them

/* A binary tree node */
class Node
{
    /* Helper function that allocates a new node with the
given data and NULL left and right pointers. */
    constructor(data)
    {
        this.data = data;
        this.left=this.right=null;
    }
}

// Function to print all nodes having k leaves
function kLeaves(ptr,k)
{
    // Base Conditions : No leaves
    if (ptr == null)
        return 0;

    // if node is leaf
    if (ptr.left == null && ptr.right == null)
        return 1;

    // total leaves in subtree rooted with this
    // node
    let total = kLeaves(ptr.left, k) + kLeaves(ptr.right, k);

    // Print this node if total is k
    if (k == total)
        document.write(ptr.data + " ");

    return total;
}

// Driver program to run the case
let root = new Node(1);
root.left     = new Node(2);
root.right     = new Node(4);
root.left.left = new Node(5);
root.left.right = new Node(6);
root.left.left.left = new Node(9);
root.left.left.right = new Node(10);
root.right.right = new Node(8);
root.right.left = new Node(7);
root.right.left.left = new Node(11);
root.right.left.right = new Node(12);

kLeaves(root, 2);

// This code is contributed by rag2127
</script>
```

**输出:**

```
5 7
```

**时间复杂度:** O(n)

本文由 [**沙莎克·米什拉(古卢)**](https://www.facebook.com/shashank.mishra.92167) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。