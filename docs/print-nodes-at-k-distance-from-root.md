# 打印距根的 k 距离处的节点

> 原文:[https://www . geesforgeks . org/print-nodes-at-k-distance-from-root/](https://www.geeksforgeeks.org/print-nodes-at-k-distance-from-root/)

给定一个树根和一个整数 k。打印离树根 k 距离的所有节点。
例如，在下面的树中，4，5 & 8 离根的距离为 2。

```
            1
          /   \
        2      3
      /  \    /
    4     5  8 
```

这个问题可以用递归来解决。感谢埃尔多提出的解决方案。

## C++

```
#include<bits/stdc++.h>

using namespace std;

/* A binary tree node has data,
pointer to left child and
a pointer to right child */
class node
{
    public:
    int data;
    node* left;
    node* right;

    /* Constructor that allocates a new node with the
    given data and NULL left and right pointers. */
    node(int data)
    {
        this->data = data;
        this->left = NULL;
        this->right = NULL;
    }
};

void printKDistant(node *root , int k)
{
    if(root == NULL|| k < 0 )
        return;
    if( k == 0 )
    {
        cout << root->data << " ";
         return;
    }

        printKDistant( root->left, k - 1 ) ;
        printKDistant( root->right, k - 1 ) ;

}

/* Driver code*/
int main()
{

    /* Constructed binary tree is
            1
            / \
        2     3
        / \     /
        4 5 8
    */
    node *root = new node(1);
    root->left = new node(2);
    root->right = new node(3);
    root->left->left = new node(4);
    root->left->right = new node(5);
    root->right->left = new node(8);

    printKDistant(root, 2);
    return 0;
}

// This code is contributed by rathbhupendra
```

## C

```
#include <stdio.h>
#include <stdlib.h>

/* A binary tree node has data, pointer to left child
   and a pointer to right child */
struct node
{
   int data;
   struct node* left;
   struct node* right;
};

void printKDistant(struct node *root , int k)   
{
   if(root == NULL|| k < 0 )
      return;
   if( k == 0 )
   {
      printf( "%d ", root->data );
      return ;
   }

      printKDistant( root->left, k-1 ) ;
      printKDistant( root->right, k-1 ) ;

}

/* Helper function that allocates a new node with the
   given data and NULL left and right pointers. */
struct node* newNode(int data)
{
  struct node* node = (struct node*)
                       malloc(sizeof(struct node));
  node->data = data;
  node->left = NULL;
  node->right = NULL;

  return(node);
}

/* Driver program to test above functions*/
int main()
{

  /* Constructed binary tree is
            1
          /   \
        2      3
      /  \    /
    4     5  8
  */
  struct node *root = newNode(1);
  root->left        = newNode(2);
  root->right       = newNode(3);
  root->left->left  = newNode(4);
  root->left->right = newNode(5);
  root->right->left = newNode(8); 

  printKDistant(root, 2);

  getchar();
  return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print nodes at k distance from root

/* A binary tree node has data, pointer to left child
   and a pointer to right child */
class Node
{
    int data;
    Node left, right;

    Node(int item)
    {
        data = item;
        left = right = null;
    }
}

class BinaryTree
{
    Node root;

    void printKDistant(Node node, int k)
    {
        if (node == null|| k < 0 )
              //Base case
            return;
        if (k == 0)
        {
            System.out.print(node.data + " ");
            return;
        }
       //recursively traversing
            printKDistant(node.left, k - 1);
            printKDistant(node.right, k - 1);

    }

    /* Driver program to test above functions */
    public static void main(String args[]) {
        BinaryTree tree = new BinaryTree();

        /* Constructed binary tree is
                1
              /   \
             2     3
            /  \   /
           4    5 8
        */
        tree.root = new Node(1);
        tree.root.left = new Node(2);
        tree.root.right = new Node(3);
        tree.root.left.left = new Node(4);
        tree.root.left.right = new Node(5);
        tree.root.right.left = new Node(8);

        tree.printKDistant(tree.root, 2);
    }
}

// This code has been contributed by Mayank Jaiswal
```

## 计算机编程语言

```
# Python program to find the nodes at k distance from root

# A Binary tree node
class Node:

    # Constructor to create a new node
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

def printKDistant(root, k):

    if root is None:
        return
    if k == 0:
        print root.data,
    else:
        printKDistant(root.left, k-1)
        printKDistant(root.right, k-1)

# Driver program to test above function
"""
   Constructed binary tree is
            1
          /   \
        2      3
      /  \    /
    4     5  8
"""
root = Node(1)
root.left = Node(2)
root.right = Node(3)
root.left.left = Node(4)
root.left.right = Node(5)
root.right.left = Node(8)

printKDistant(root, 2)

# This code is contributed by Nikhil Kumar Singh(nickzuck_007)
```

## C#

```
using System;

// c# program to print nodes at k distance from root

/* A binary tree node has data, pointer to left child
   and a pointer to right child */
public class Node
{
    public int data;
    public Node left, right;

    public Node(int item)
    {
        data = item;
        left = right = null;
    }
}

public class BinaryTree
{
    public Node root;

    public virtual void printKDistant(Node node, int k)
    {
        if (node == null|| k < 0 )
        {
            return;
        }
        if (k == 0)
        {
            Console.Write(node.data + " ");
            return;
        }

            printKDistant(node.left, k - 1);
            printKDistant(node.right, k - 1);

    }

    /* Driver program to test above functions */
    public static void Main(string[] args)
    {
        BinaryTree tree = new BinaryTree();

        /* Constructed binary tree is
                1
              /   \
             2     3
            /  \   /
           4    5 8 
        */
        tree.root = new Node(1);
        tree.root.left = new Node(2);
        tree.root.right = new Node(3);
        tree.root.left.left = new Node(4);
        tree.root.left.right = new Node(5);
        tree.root.right.left = new Node(8);

        tree.printKDistant(tree.root, 2);
    }
}

// This code is contributed by Shrikant13
```

## java 描述语言

```
<script>

// Javascript program to print nodes at k distance from root

/* A binary tree node has data, pointer to left child
   and a pointer to right child */
class Node
{
    constructor(item)
    {
        this.data = item;
        this.left = null;
        this.right = null;
    }
}

var root =null;

function printKDistant(node, k)
{
    if (node == null|| k < 0 )
    {
        return;
    }
    if (k == 0)
    {
        document.write(node.data + " ");
        return;
    }

        printKDistant(node.left, k - 1);
        printKDistant(node.right, k - 1);

}

/* Driver program to test above functions */

/* Constructed binary tree is
        1
      /   \
     2     3
    /  \   /
   4    5 8 
*/
root = new Node(1);
root.left = new Node(2);
root.right = new Node(3);
root.left.left = new Node(4);
root.left.right = new Node(5);
root.right.left = new Node(8);
printKDistant(root, 2);

// This code is contributed by importantly.
</script>
```

**输出:**

```
4 5 8 
```

**时间复杂度:** O(n)，其中 n 是给定二叉树中的节点数。

**空间复杂度:** O(二叉树的高度)。

**注-**

*   **如果是真的，打印节点–**始终检查每个节点的 K 距离== 0
*   **当你经过它的子树
    时，左边或右边的子树–**将距离减少 1

如果你发现上面的代码/算法不正确，请写评论，或者找到更好的方法来解决同样的问题。