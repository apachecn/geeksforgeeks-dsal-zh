# 打印二叉树中给定节点的祖先

> 原文:[https://www . geesforgeks . org/print-给定二叉树中节点的祖先/](https://www.geeksforgeeks.org/print-ancestors-of-a-given-node-in-binary-tree/)

给定一棵二叉树和一个键，编写一个函数，打印给定二叉树中键的所有祖先。
例如，如果给定的树跟在二叉树后面，键是 7，那么你的函数应该打印 4、2 和 1。

```
              1
            /   \
          2      3
        /  \
      4     5
     /
    7
```

感谢 Mike、Sambasiva 和 wgpshashank 的贡献。

## C++

```
// C++ program to print ancestors of given node
#include<bits/stdc++.h>

using namespace std;

/* A binary tree node has data, pointer to left child
   and a pointer to right child */
struct node
{
   int data;
   struct node* left;
   struct node* right;
};

/* If target is present in tree, then prints the ancestors
   and returns true, otherwise returns false. */
bool printAncestors(struct node *root, int target)
{
  /* base cases */
  if (root == NULL)
     return false;

  if (root->data == target)
     return true;

  /* If target is present in either left or right subtree of this node,
     then print this node */
  if ( printAncestors(root->left, target) ||
       printAncestors(root->right, target) )
  {
    cout << root->data << " ";
    return true;
  }

  /* Else return false */
  return false;
}

/* Helper function that allocates a new node with the
   given data and NULL left and right pointers. */
struct node* newnode(int data)
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

  /* Construct the following binary tree
              1
            /   \
          2      3
        /  \
      4     5
     /
    7
  */
  struct node *root = newnode(1);
  root->left        = newnode(2);
  root->right       = newnode(3);
  root->left->left  = newnode(4);
  root->left->right = newnode(5);
  root->left->left->left  = newnode(7);

  printAncestors(root, 7);

  getchar();
  return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print ancestors of given node

/* A binary tree node has data, pointer to left child
   and a pointer to right child */
class Node
{
    int data;
    Node left, right, nextRight;

    Node(int item)
    {
        data = item;
        left = right = nextRight = null;
    }
}

class BinaryTree
{
    Node root;

    /* If target is present in tree, then prints the ancestors
       and returns true, otherwise returns false. */
    boolean printAncestors(Node node, int target)
    {
         /* base cases */
        if (node == null)
            return false;

        if (node.data == target)
            return true;

        /* If target is present in either left or right subtree
           of this node, then print this node */
        if (printAncestors(node.left, target)
                || printAncestors(node.right, target))
        {
            System.out.print(node.data + " ");
            return true;
        }

        /* Else return false */
        return false;
    }

    /* Driver program to test above functions */
    public static void main(String args[])
    {
        BinaryTree tree = new BinaryTree();

        /* Construct the following binary tree
                  1
                /   \
               2     3
              /  \
             4    5
            /
           7
        */
        tree.root = new Node(1);
        tree.root.left = new Node(2);
        tree.root.right = new Node(3);
        tree.root.left.left = new Node(4);
        tree.root.left.right = new Node(5);
        tree.root.left.left.left = new Node(7);

        tree.printAncestors(tree.root, 7);

    }
}

// This code has been contributed by Mayank Jaiswal
```

## 计算机编程语言

```
# Python program to print ancestors of given node in
# binary tree

# A Binary Tree node
class Node:

    # Constructor to create a new node
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# If target is present in tree, then prints the ancestors
# and returns true, otherwise returns false
def printAncestors(root, target):

    # Base case
    if root == None:
        return False

    if root.data == target:
        return True

    # If target is present in either left or right subtree
    # of this node, then print this node
    if (printAncestors(root.left, target) or
        printAncestors(root.right, target)):
        print root.data,
        return True

    # Else return False
    return False

# Driver program to test above function
root = Node(1)
root.left = Node(2)
root.right = Node(3)
root.left.left = Node(4)
root.left.right = Node(5)
root.left.left.left = Node(7)

printAncestors(root, 7)

# This code is contributed by Nikhil Kumar Singh(nickzuck_007)
```

## C#

```
using System;

// C# program to print ancestors of given node

/* A binary tree node has data, pointer to left child
and a pointer to right child */
public class Node
{
    public int data;
    public Node left, right, nextRight;

    public Node(int item)
    {
        data = item;
        left = right = nextRight = null;
    }
}

public class BinaryTree
{
    public Node root;

    /* If target is present in tree, then prints the ancestors
    and returns true, otherwise returns false. */
    public virtual bool printAncestors(Node node, int target)
    {
        /* base cases */
        if (node == null)
        {
            return false;
        }

        if (node.data == target)
        {
            return true;
        }

        /* If target is present in either left or right subtree
        of this node, then print this node */
        if (printAncestors(node.left, target)
        || printAncestors(node.right, target))
        {
            Console.Write(node.data + " ");
            return true;
        }

        /* Else return false */
        return false;
    }

    /* Driver program to test above functions */
    public static void Main(string[] args)
    {
        BinaryTree tree = new BinaryTree();

        /* Construct the following binary tree
                1
                / \
            2     3
            / \
            4 5
            /
        7
        */
        tree.root = new Node(1);
        tree.root.left = new Node(2);
        tree.root.right = new Node(3);
        tree.root.left.left = new Node(4);
        tree.root.left.right = new Node(5);
        tree.root.left.left.left = new Node(7);

        tree.printAncestors(tree.root, 7);

    }
}

// This code is contributed by Shrikant13
```

## java 描述语言

```
<script>

    // JavaScript program to print ancestors of given node

    class Node
    {
        constructor(item) {
              this.data = item;
            this.left = null;
            this.right = null;
            this.nextRight = null;
        }
    }

    let root;

    /* If target is present in tree, then prints the ancestors
       and returns true, otherwise returns false. */
    function printAncestors(node, target)
    {
         /* base cases */
        if (node == null)
            return false;

        if (node.data == target)
            return true;

        /* If target is present in either left or right subtree
           of this node, then print this node */
        if (printAncestors(node.left, target)
                || printAncestors(node.right, target))
        {
            document.write(node.data + " ");
            return true;
        }

        /* Else return false */
        return false;
    }

    /* Construct the following binary tree
                    1
                  /   \
                 2     3
                /  \
               4    5
              /
             7
          */
    root = new Node(1);
    root.left = new Node(2);
    root.right = new Node(3);
    root.left.left = new Node(4);
    root.left.right = new Node(5);
    root.left.left.left = new Node(7);

    printAncestors(root, 7);

</script>
```

**输出:**

```
4 2 1
```

**时间复杂度:** O(n)，其中 n 是给定二叉树中的节点数。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。