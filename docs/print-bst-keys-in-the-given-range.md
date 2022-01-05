# 打印给定范围内的 BST 键

> 原文:[https://www . geesforgeks . org/print-BST-给定范围内的密钥/](https://www.geeksforgeeks.org/print-bst-keys-in-the-given-range/)

给定两个值 k1 和 k2(其中 k1 < k2) and a root pointer to a Binary Search Tree. Print all the keys of the tree in range k1 to k2\. i.e. print all x such that k1<=x<=k2 and x is a key of given BST. Print all the keys in increasing order. 
**示例:**

```
Graph:

Input: k1 = 10 and k2 = 22
Output: 12, 20 and 22.
Explanation: The keys are 4, 8, 12, 20, and 22.
So keys in range 10 to 22 is 12, 20 and 22.

Input: k1 = 1 and k2 = 10
Output: 4 and 8
Explanation: The keys are 4, 8, 12, 20, and 22.
So keys in range 1 to 10 is 4 and 8.
```

**方法:**按顺序遍历树。如果二叉查找树按顺序遍历，则键按递增顺序遍历。所以在有序遍历中遍历键时。如果密钥在范围内，打印密钥，否则跳过密钥。
**算法:**

1.  创建一个递归函数，以根为参数，范围为(k1，k2)
2.  如果根键的值大于 k1，则递归调用左子树。
3.  如果根键的值在范围内，则打印根键。
4.  递归调用右子树。

**实施:**

## C++

```
// C++ program to print BST in given range
#include<bits/stdc++.h>
using namespace std;

/* A tree node structure */
class node
{
    public:
    int data;
    node *left;
    node *right;
};

/* The functions prints all the keys
which in the given range [k1..k2].
    The function assumes than k1 < k2 */
void Print(node *root, int k1, int k2)
{
    /* base case */
    if ( NULL == root )
        return;

    /* Since the desired o/p is sorted,
        recurse for left subtree first
        If root->data is greater than k1,
        then only we can get o/p keys
        in left subtree */
    if ( k1 < root->data )
        Print(root->left, k1, k2);

    /* if root's data lies in range,
    then prints root's data */
    if ( k1 <= root->data && k2 >= root->data )
        cout<<root->data<<" ";

    /* recursively call the right subtree */
   Print(root->right, k1, k2);
}

/* Utility function to create a new Binary Tree node */
node* newNode(int data)
{
    node *temp = new node();
    temp->data = data;
    temp->left = NULL;
    temp->right = NULL;

    return temp;
}

/* Driver code */
int main()
{
    node *root = new node();
    int k1 = 10, k2 = 25;

    /* Constructing tree given
    in the above figure */
    root = newNode(20);
    root->left = newNode(8);
    root->right = newNode(22);
    root->left->left = newNode(4);
    root->left->right = newNode(12);

    Print(root, k1, k2);
    return 0;
}

// This code is contributed by rathbhupendra
```

## C

```
#include<stdio.h>
#include<stdlib.h>

/* A tree node structure */
struct node
{
  int data;
  struct node *left;
  struct node *right;
};

/* The functions prints all the keys which in
the given range [k1..k2]. The function assumes than k1 < k2 */
void Print(struct node *root, int k1, int k2)
{
   /* base case */
   if ( NULL == root )
      return;

   /* Since the desired o/p is sorted, recurse for left subtree first
      If root->data is greater than k1, then only we can get o/p keys
      in left subtree */
   if ( k1 < root->data )
     Print(root->left, k1, k2);

   /* if root's data lies in range, then prints root's data */
   if ( k1 <= root->data && k2 >= root->data )
     printf("%d ", root->data );

  /* recursively call the right subtree */
   Print(root->right, k1, k2);
}

/* Utility function to create a new Binary Tree node */
struct node* newNode(int data)
{
  struct node *temp = malloc(sizeof(struct node));
  temp->data = data;
  temp->left = NULL;
  temp->right = NULL;

  return temp;
}

/* Driver function to test above functions */
int main()
{
  struct node *root = malloc(sizeof(struct node));
  int k1 = 10, k2 = 25;

  /* Constructing tree given in the above figure */
  root = newNode(20);
  root->left = newNode(8);
  root->right = newNode(22);
  root->left->left = newNode(4);
  root->left->right = newNode(12);

  Print(root, k1, k2);

  getchar();
  return 0;
}

// This code was modified by italovinicius18
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print BST in given range

// A binary tree node
class Node {

    int data;
    Node left, right;

    Node(int d) {
        data = d;
        left = right = null;
    }
}

class BinaryTree {

    static Node root;

    /* The functions prints all the keys which in
     the given range [k1..k2]. The function assumes than k1 < k2 */
    void Print(Node node, int k1, int k2) {

        /* base case */
        if (node == null) {
            return;
        }

        /* Since the desired o/p is sorted, recurse for left subtree first
         If root->data is greater than k1, then only we can get o/p keys
         in left subtree */
        if (k1 < node.data) {
            Print(node.left, k1, k2);
        }

        /* if root's data lies in range, then prints root's data */
        if (k1 <= node.data && k2 >= node.data) {
            System.out.print(node.data + " ");
        }

        /* recursively call the right subtree  */
         Print(node.right, k1, k2);
    }

    public static void main(String[] args) {
        BinaryTree tree = new BinaryTree();
        int k1 = 10, k2 = 25;
        tree.root = new Node(20);
        tree.root.left = new Node(8);
        tree.root.right = new Node(22);
        tree.root.left.left = new Node(4);
        tree.root.left.right = new Node(12);

        tree.Print(root, k1, k2);
    }
}

// This code has been contributed by Mayank Jaiswal
```

## 计算机编程语言

```
# Python program to find BST keys in given range

# A binary tree node
class Node:

    # Constructor to create a new node
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# The function prints all the keys in the gicven range
# [k1..k2]. Assumes that k1 < k2
def Print(root, k1, k2):

    # Base Case
    if root is None:
        return

    # Since the desired o/p is sorted, recurse for left
    # subtree first. If root.data is greater than k1, then
    # only we can get o/p keys in left subtree
    if k1 < root.data :
        Print(root.left, k1, k2)

    # If root's data lies in range, then prints root's data
    if k1 <= root.data and k2 >= root.data:
        print root.data,

    # recursively call the right subtree
    Print(root.right, k1, k2)

# Driver function to test above function
k1 = 10 ; k2 = 25 ;
root = Node(20)
root.left = Node(8)
root.right = Node(22)
root.left.left = Node(4)
root.left.right = Node(12)

Print(root, k1, k2)

# This code is contributed by Nikhil Kumar Singh(nickzuck_007)
```

## C#

```
using System;

// C# program to print BST in given range

// A binary tree node
public class Node
{

    public int data;
    public Node left, right;

    public Node(int d)
    {
        data = d;
        left = right = null;
    }
}

public class BinaryTree
{

    public static Node root;

    /* The functions prints all the keys which in the
     given range [k1..k2]. The function assumes than k1 < k2 */
    public virtual void Print(Node node, int k1, int k2)
    {

        /* base case */
        if (node == null)
        {
            return;
        }

        /* Since the desired o/p is sorted, recurse for left subtree first
         If root->data is greater than k1, then only we can get o/p keys
         in left subtree */
        if (k1 < node.data)
        {
            Print(node.left, k1, k2);
        }

        /* if root's data lies in range, then prints root's data */
        if (k1 <= node.data && k2 >= node.data)
        {
            Console.Write(node.data + " ");
        }

        /* recursively call the right subtree */
            Print(node.right, k1, k2);
    }

    public static void Main(string[] args)
    {
        BinaryTree tree = new BinaryTree();
        int k1 = 10, k2 = 25;
        BinaryTree.root = new Node(20);
        BinaryTree.root.left = new Node(8);
        BinaryTree.root.right = new Node(22);
        BinaryTree.root.left.left = new Node(4);
        BinaryTree.root.left.right = new Node(12);

        tree.Print(root, k1, k2);
    }
}

// This code is contributed by Shrikant13
```

## java 描述语言

```
<script>

// JavaScript program to print BST in given range

// A binary tree node
class Node {
    constructor(val) {
        this.data = val;
        this.left = null;
        this.right = null;
    }
}
    var root = null;

    /*
     * The functions prints all the keys
     which in the given range [k1..k2]. The
     * function assumes than k1 < k2
     */
    function Print(node , k1 , k2) {

        /* base case */
        if (node == null) {
            return;
        }

        /*
         * Since the desired o/p is sorted,
         recurse for left subtree first If root->data
         * is greater than k1, then only we can
         get o/p keys in left subtree
         */
        if (k1 < node.data) {
            Print(node.left, k1, k2);
        }

        /* if root's data lies in range,
        then prints root's data */
        if (k1 <= node.data && k2 >= node.data) {
            document.write(node.data + " ");
        }

        /* recursively call the right subtree */
         Print(node.right, k1, k2);
    }

        var k1 = 10, k2 = 25;
        root = new Node(20);
        root.left = new Node(8);
        root.right = new Node(22);
        root.left.left = new Node(4);
        root.left.right = new Node(12);

        Print(root, k1, k2);

// This code is contributed by todaysgaurav

</script>
```

**输出:**

```
12 20 22
```

**复杂度分析:**

*   **时间复杂度:** O(n)，其中 n 为树中键的总数。
    需要对树进行一次遍历。
*   **空间复杂度:** O(树的高度)。//作为递归调用
*   不需要额外的空间。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。