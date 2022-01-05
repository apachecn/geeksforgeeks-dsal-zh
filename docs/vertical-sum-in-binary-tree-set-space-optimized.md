# 二叉树中的垂直和|集合 2(空间优化)

> 原文:[https://www . geeksforgeeks . org/垂直-二进制求和-树集-空间优化/](https://www.geeksforgeeks.org/vertical-sum-in-binary-tree-set-space-optimized/)

给定一棵二叉树，求在同一条垂直线上的节点的垂直和。通过不同的垂直线打印所有总和。

**示例:**

```
      1
    /   \
  2      3
 / \    / \
4   5  6   7
```

树有 5 条竖线
竖线-1 只有一个节点 4 = >竖线和为 4
竖线-2:只有一个节点 2= >竖线和为 2
竖线-3:有三个节点:1，5，6 = >竖线和为 1+5+6 = 12
竖线-4:只有一个节点 3 = >竖线和为 3
竖线-5:只有一个节点 7 = >竖线

我们已经在 [**第 1 集**](https://www.geeksforgeeks.org/vertical-sum-in-a-given-binary-tree/) 中讨论了[哈希](http://geeksquiz.com/hashing-set-1-introduction/)基础解决方案。基于哈希的解决方案需要维护哈希表。我们知道哈希需要的空间比其中条目的数量多。本文讨论了基于[双向链表](http://geeksquiz.com/doubly-linked-list/)的解决方案。这里讨论的解决方案只需要链表的 n 个节点，其中 n 是二叉树中垂直线的总数。下面是算法。

```
verticalSumDLL(root)
1)  Create a node of doubly linked list node 
    with value 0\. Let the node be llnode.
2)  verticalSumDLL(root, llnode)

verticalSumDLL(tnode, llnode)
1) Add current node's data to its vertical line
        llnode.data = llnode.data + tnode.data;
2) Recursively process left subtree
   // If left child is not empty
   if (tnode.left != null)
   {
      if (llnode.prev == null)
      {
          llnode.prev = new LLNode(0);
          llnode.prev.next = llnode;
      }
      verticalSumDLLUtil(tnode.left, llnode.prev);
   }
3)  Recursively process right subtree
   if (tnode.right != null)
   {
      if (llnode.next == null)
      {
          llnode.next = new LLNode(0);
          llnode.next.prev = llnode;
      }
      verticalSumDLLUtil(tnode.right, llnode.next);
   }

```

## C++

```
/// C++ program of space optimized solution
/// to find vertical sum of binary tree.
#include <bits/stdc++.h>

using namespace std;

/// Tree node structure
struct TNode{
    int key;
    struct TNode *left, *right;
};

/// Function to create new tree node
TNode* newTNode(int key)
{
    TNode* temp = new TNode;
    temp->key = key;
    temp->left = temp->right = NULL;
    return temp;
}

/// Doubly linked list structure
struct LLNode{
    int key;
    struct LLNode *prev, *next;
};

/// Function to create new Linked List Node
LLNode* newLLNode(int key)
{
    LLNode* temp = new LLNode;
    temp->key = key;
    temp->prev = temp->next = NULL;
    return temp;
}

/// Function that creates Linked list and store
/// vertical sum in it.
void verticalSumDLLUtil(TNode *root, LLNode *sumNode)
{
    /// Update sum of current line by adding value
    /// of current tree node.
    sumNode->key = sumNode->key + root->key;

    /// Recursive call to left subtree.
    if(root->left)
    {
        if(sumNode->prev == NULL)
        {
            sumNode->prev = newLLNode(0);
            sumNode->prev->next = sumNode;
        }
        verticalSumDLLUtil(root->left, sumNode->prev);
    }

    /// Recursive call to right subtree.
    if(root->right)
    {
        if(sumNode->next == NULL)
        {
            sumNode->next = newLLNode(0);
            sumNode->next->prev = sumNode;
        }
        verticalSumDLLUtil(root->right, sumNode->next);
    }
}

/// Function to print vertical sum of Tree.
/// It uses verticalSumDLLUtil() to calculate sum.
void verticalSumDLL(TNode* root)
{
    /// Create Linked list node for
    /// line passing through root.
    LLNode* sumNode = newLLNode(0);

    /// Compute vertical sum of different lines.
    verticalSumDLLUtil(root, sumNode);

    /// Make doubly linked list pointer point
    /// to first node in list.
    while(sumNode->prev != NULL){
        sumNode = sumNode->prev;
    }

    /// Print vertical sum of different lines
    /// of binary tree.
    while(sumNode != NULL){
        cout << sumNode->key <<" ";
        sumNode = sumNode->next;
    }
}

int main()
{
    /*
                 1
                / \
               /   \
              2     3
             / \   / \
            /   \ /   \
           4    5 6    7
    */
    TNode *root = newTNode(1);
    root->left = newTNode(2);
    root->right = newTNode(3);
    root->left->left = newTNode(4);
    root->left->right = newTNode(5);
    root->right->left = newTNode(6);
    root->right->right = newTNode(7);

    cout << "Vertical Sums are\n";
    verticalSumDLL(root);
    return 0;
}

// This code is contributed by Rahul Titare
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of space optimized solution
// to find vertical sum.

public class VerticalSumBinaryTree
{
    // Prints vertical sum of different vertical
    // lines in tree. This method mainly uses
    // verticalSumDLLUtil().
    static void verticalSumDLL(TNode root)
    {
        // Create a doubly linked list node to
        // store sum of lines going through root.
        // Vertical sum is initialized as 0.
        LLNode llnode = new LLNode(0);

        // Compute vertical sum of different lines
        verticalSumDLLUtil(root, llnode);

        // llnode refers to sum of vertical line
        // going through root. Move llnode to the
        // leftmost line.
        while (llnode.prev != null)
            llnode = llnode.prev;

        // Prints vertical sum of all lines starting
        // from leftmost vertical line
        while (llnode != null)
        {
            System.out.print(llnode.data +" ");
            llnode = llnode.next;
        }
    }

    // Constructs linked list
    static void verticalSumDLLUtil(TNode tnode,
                                   LLNode llnode)
    {
        // Add current node's data to its vertical line
        llnode.data = llnode.data + tnode.data;

        // Recursively process left subtree
        if (tnode.left != null)
        {
            if (llnode.prev == null)
            {
                llnode.prev = new LLNode(0);
                llnode.prev.next = llnode;
            }
            verticalSumDLLUtil(tnode.left, llnode.prev);
        }

        // Process right subtree
        if (tnode.right != null)
        {
            if (llnode.next == null)
            {
                llnode.next = new LLNode(0);
                llnode.next.prev = llnode;
            }
            verticalSumDLLUtil(tnode.right, llnode.next);
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        // Let us construct the tree shown above
        TNode root = new TNode(1);
        root.left = new TNode(2);
        root.right = new TNode(3);
        root.left.left = new TNode(4);
        root.left.right = new TNode(5);
        root.right.left = new TNode(6);
        root.right.right = new TNode(7);

        System.out.println("Vertical Sums are");
        verticalSumDLL(root);
    }

    // Doubly Linked List Node
    static class LLNode
    {
        int data;
        LLNode prev, next;
        public LLNode(int d) { data = d; }
    }

    // Binary Tree Node
    static class TNode
    {
        int data;
        TNode left, right;
        public TNode(int d) { data = d; }
    }
}
```

## 蟒蛇 3

```
# Python3 program of space optimized
# solution to find vertical sum of
# binary tree.

# Tree node structure
class TNode:

    def __init__(self, key):

        self.key = key
        self.left = None
        self.right = None

# Doubly linked list structure
class LLNode:

    def __init__(self, key):

        self.key = key
        self.prev = None
        self.next = None

# Function that creates Linked list and store
# vertical sum in it.
def verticalSumDLLUtil(root: TNode,
                    sumNode: LLNode) -> None:

    # Update sum of current line by adding
    # value of current tree node.
    sumNode.key = sumNode.key + root.key

    # Recursive call to left subtree.
    if (root.left):
        if (sumNode.prev == None):
            sumNode.prev = LLNode(0)
            sumNode.prev.next = sumNode

        verticalSumDLLUtil(root.left,
                           sumNode.prev)

    # Recursive call to right subtree.
    if (root.right):
        if (sumNode.next == None):
            sumNode.next = LLNode(0)
            sumNode.next.prev = sumNode

        verticalSumDLLUtil(root.right,
                           sumNode.next)

# Function to print vertical sum of Tree.
# It uses verticalSumDLLUtil() to calculate sum.
def verticalSumDLL(root: TNode) -> None:

    # Create Linked list node for
    # line passing through root.
    sumNode = LLNode(0)

    # Compute vertical sum of different lines.
    verticalSumDLLUtil(root, sumNode)

    # Make doubly linked list pointer point
    # to first node in list.
    while (sumNode.prev != None):
        sumNode = sumNode.prev

    # Print vertical sum of different lines
    # of binary tree.
    while (sumNode != None):
        print(sumNode.key, end = " ")
        sumNode = sumNode.next

# Driver code
if __name__ == "__main__":

    '''
                 1
                / \
               /   \
              2     3
             / \   / \
            /   \ /   \
           4    5 6    7
    '''
    root = TNode(1)
    root.left = TNode(2)
    root.right = TNode(3)
    root.left.left = TNode(4)
    root.left.right = TNode(5)
    root.right.left = TNode(6)
    root.right.right = TNode(7)

    print("Vertical Sums are")

    verticalSumDLL(root)

# This code is contributed by sanjeev2552
```

## C#

```
// C# implementation of space optimized
// solution to find vertical sum.
using System;

class GFG
{
// Prints vertical sum of different vertical
// lines in tree. This method mainly uses
// verticalSumDLLUtil().
public static void verticalSumDLL(TNode root)
{
    // Create a doubly linked list node to
    // store sum of lines going through root.
    // Vertical sum is initialized as 0.
    LLNode llnode = new LLNode(0);

    // Compute vertical sum of different lines
    verticalSumDLLUtil(root, llnode);

    // llnode refers to sum of vertical line
    // going through root. Move llnode to the
    // leftmost line.
    while (llnode.prev != null)
    {
        llnode = llnode.prev;
    }

    // Prints vertical sum of all lines
    // starting from leftmost vertical line
    while (llnode != null)
    {
        Console.Write(llnode.data + " ");
        llnode = llnode.next;
    }
}

// Constructs linked list
public static void verticalSumDLLUtil(TNode tnode,
                                     LLNode llnode)
{
    // Add current node's data to
    // its vertical line
    llnode.data = llnode.data + tnode.data;

    // Recursively process left subtree
    if (tnode.left != null)
    {
        if (llnode.prev == null)
        {
            llnode.prev = new LLNode(0);
            llnode.prev.next = llnode;
        }
        verticalSumDLLUtil(tnode.left, llnode.prev);
    }

    // Process right subtree
    if (tnode.right != null)
    {
        if (llnode.next == null)
        {
            llnode.next = new LLNode(0);
            llnode.next.prev = llnode;
        }
        verticalSumDLLUtil(tnode.right, llnode.next);
    }
}

// Doubly Linked List Node
public class LLNode
{
    public int data;
    public LLNode prev, next;
    public LLNode(int d)
    {
        data = d;
    }
}

// Binary Tree Node
public class TNode
{
    public int data;
    public TNode left, right;
    public TNode(int d)
    {
        data = d;
    }
}

// Driver code
public static void Main(string[] args)
{
    // Let us construct the tree shown above
    TNode root = new TNode(1);
    root.left = new TNode(2);
    root.right = new TNode(3);
    root.left.left = new TNode(4);
    root.left.right = new TNode(5);
    root.right.left = new TNode(6);
    root.right.right = new TNode(7);

    Console.WriteLine("Vertical Sums are");
    verticalSumDLL(root);
}
}

// This code is contributed by Shrikant13
```

## java 描述语言

```
<script>

// Javascript implementation of space optimized
// solution to find vertical sum.

// Prints vertical sum of different vertical
// lines in tree. This method mainly uses
// verticalSumDLLUtil().
function verticalSumDLL(root)
{

    // Create a doubly linked list node to
    // store sum of lines going through root.
    // Vertical sum is initialized as 0.
    var llnode = new LLNode(0);

    // Compute vertical sum of different lines
    verticalSumDLLUtil(root, llnode);

    // llnode refers to sum of vertical line
    // going through root. Move llnode to the
    // leftmost line.
    while (llnode.prev != null)
    {
        llnode = llnode.prev;
    }

    // Prints vertical sum of all lines
    // starting from leftmost vertical line
    while (llnode != null)
    {
        document.write(llnode.data + " ");
        llnode = llnode.next;
    }
}

// Constructs linked list
function verticalSumDLLUtil(tnode, llnode)
{

    // Add current node's data to
    // its vertical line
    llnode.data = llnode.data + tnode.data;

    // Recursively process left subtree
    if (tnode.left != null)
    {
        if (llnode.prev == null)
        {
            llnode.prev = new LLNode(0);
            llnode.prev.next = llnode;
        }
        verticalSumDLLUtil(tnode.left, llnode.prev);
    }

    // Process right subtree
    if (tnode.right != null)
    {
        if (llnode.next == null)
        {
            llnode.next = new LLNode(0);
            llnode.next.prev = llnode;
        }
        verticalSumDLLUtil(tnode.right, llnode.next);
    }
}

// Doubly Linked List Node
class LLNode
{
    constructor(d)
    {
        this.data = d;
        this.prev = null;
        this.next = null;
    }
}

// Binary Tree Node
class TNode
{
    constructor(d)
    {
        this.data = d;
        this.left = null;
        this.right = null;
    }
}

// Driver code

// Let us construct the tree shown above
var root = new TNode(1);
root.left = new TNode(2);
root.right = new TNode(3);
root.left.left = new TNode(4);
root.left.right = new TNode(5);
root.right.left = new TNode(6);
root.right.right = new TNode(7);
document.write("Vertical Sums are<br>");

verticalSumDLL(root);

// This code is contributed by itsok

</script>
```

**输出:**

```
Vertical Sums are
4 2 12 3 7 
```

本文由 **Rahul Titare** 供稿。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。