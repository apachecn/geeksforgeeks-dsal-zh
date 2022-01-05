# 计算二叉树叶节点的程序

> 原文:[https://www . geesforgeks . org/write-a-c-program-to-get-count-of-leaf-in-a-binary-tree/](https://www.geeksforgeeks.org/write-a-c-program-to-get-count-of-leaf-nodes-in-a-binary-tree/)

如果节点的左右子节点都为空，则该节点为叶节点。
这里有一个得到叶节点数的算法。

```
getLeafCount(node)
1) If node is NULL then return 0.
2) Else If left and right child nodes are NULL return 1.
3) Else recursively calculate leaf count of the tree using below formula.
    Leaf count of a tree = Leaf count of left subtree + 
                                 Leaf count of right subtree
```

![Example Tree](img/34a0f18bcfea93de93a6282740c0a4b6.png)

上述树的叶数为 3。

**实施:**

## C++

```
// C++ implementation to find leaf
// count of a given Binary tree
#include <bits/stdc++.h>
using namespace std;

/* A binary tree node has data,
pointer to left child and
a pointer to right child */
struct node
{
    int data;
    struct node* left;
    struct node* right;
};

/* Function to get the count
of leaf nodes in a binary tree*/
unsigned int getLeafCount(struct node* node)
{
    if(node == NULL)    
        return 0;
    if(node->left == NULL && node->right == NULL)
        return 1;        
    else
        return getLeafCount(node->left)+
            getLeafCount(node->right);
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

/*Driver code*/
int main()
{
    /*create a tree*/
    struct node *root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->left->right = newNode(5);

/*get leaf count of the above created tree*/
cout << "Leaf count of the tree is : "<<
                getLeafCount(root) << endl;
return 0;
}

// This code is contributed by SHUBHAMSINGH10
```

## C

```
// C implementation to find leaf count of a given Binary tree
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

/* Function to get the count of leaf nodes in a binary tree*/
unsigned int getLeafCount(struct node* node)
{
  if(node == NULL)      
    return 0;
  if(node->left == NULL && node->right==NULL)     
    return 1;           
  else
    return getLeafCount(node->left)+
           getLeafCount(node->right);     
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

/*Driver program to test above functions*/ 
int main()
{
  /*create a tree*/ 
  struct node *root = newNode(1);
  root->left        = newNode(2);
  root->right       = newNode(3);
  root->left->left  = newNode(4);
  root->left->right = newNode(5);   

  /*get leaf count of the above created tree*/
  printf("Leaf count of the tree is %d", getLeafCount(root));

  getchar();
  return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find leaf count of a given Binary tree

/* Class containing left and right child of current
 node and key value*/
class Node
{
    int data;
    Node left, right;

    public Node(int item)
    {
        data = item;
        left = right = null;
    }
}

public class BinaryTree
{
    //Root of the Binary Tree
    Node root;

    /* Function to get the count of leaf nodes in a binary tree*/
    int getLeafCount()
    {
        return getLeafCount(root);
    }

    int getLeafCount(Node node)
    {
        if (node == null)
            return 0;
        if (node.left == null && node.right == null)
            return 1;
        else
            return getLeafCount(node.left) + getLeafCount(node.right);
    }

    /* Driver program to test above functions */
    public static void main(String args[])
    {
        /* create a tree */
        BinaryTree tree = new BinaryTree();
        tree.root = new Node(1);
        tree.root.left = new Node(2);
        tree.root.right = new Node(3);
        tree.root.left.left = new Node(4);
        tree.root.left.right = new Node(5);

        /* get leaf count of the above tree */
        System.out.println("The leaf count of binary tree is : "
                             + tree.getLeafCount());
    }
}

// This code has been contributed by Mayank Jaiswal(mayank_24)
```

## 计算机编程语言

```
# Python program to count leaf nodes in Binary Tree

# A Binary tree node
class Node:

    # Constructor to create a new node
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# Function to get the count of leaf nodes in binary tree
def getLeafCount(node):
    if node is None:
        return 0
    if(node.left is None and node.right is None):
        return 1
    else:
        return getLeafCount(node.left) + getLeafCount(node.right)

# Driver program to test above function
root = Node(1)
root.left = Node(2)
root.right = Node(3)
root.left.left = Node(4)
root.left.right = Node(5)

print "Leaf count of the tree is %d" %(getLeafCount(root))

#This code is contributed by Nikhil Kumar Singh(nickzuck_007)
```

## C#

```
using System;

// C# implementation to find leaf count of a given Binary tree

/* Class containing left and right child of current 
 node and key value*/
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
    //Root of the Binary Tree
    public Node root;

    /* Function to get the count of leaf nodes in a binary tree*/
    public virtual int LeafCount
    {
        get
        {
            return getLeafCount(root);
        }
    }

    public virtual int getLeafCount(Node node)
    {
        if (node == null)
        {
            return 0;
        }
        if (node.left == null && node.right == null)
        {
            return 1;
        }
        else
        {
            return getLeafCount(node.left) + getLeafCount(node.right);
        }
    }

    /* Driver program to test above functions */
    public static void Main(string[] args)
    {
        /* create a tree */
        BinaryTree tree = new BinaryTree();
        tree.root = new Node(1);
        tree.root.left = new Node(2);
        tree.root.right = new Node(3);
        tree.root.left.left = new Node(4);
        tree.root.left.right = new Node(5);

        /* get leaf count of the above tree */
        Console.WriteLine("The leaf count of binary tree is : " + tree.LeafCount);
    }
}

  // This code is contributed by Shrikant13
```

## java 描述语言

```
<script>
    // Javascript implementation to find leaf count of a given Binary tree

    /* A binary tree node has data,
    pointer to left child and
    a pointer to right child */
    class node
    {
        constructor(data) {
           this.left = null;
           this.right = null;
           this.data = data;
        }
    }

    /* Function to get the count
    of leaf nodes in a binary tree*/
    function getLeafCount(node)
    {
        if(node == null)    
            return 0;
        if(node.left == null && node.right == null)
            return 1;        
        else
            return getLeafCount(node.left)+
                getLeafCount(node.right);
    }

    /* Helper function that allocates a new node with the
    given data and NULL left and right pointers. */
    function newNode(data)
    {
        let Node = new node(data);
        return(Node);
    }

    /*create a tree*/
    let root = newNode(1);
    root.left = newNode(2);
    root.right = newNode(3);
    root.left.left = newNode(4);
    root.left.right = newNode(5);

    /*get leaf count of the above created tree*/
    document.write("The leaf count of binary tree is : " + getLeafCount(root));

    // This code is contributed by mukesh07.
</script>
```

**输出:**

```
The leaf count of binary tree is : 3
```

**时间&空间复杂度:**由于本程序类似于树的遍历，时间和空间复杂度将与树遍历相同(详见我们的[树遍历](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)帖子)

如果您发现上述程序/算法或其他解决相同问题的方法有任何 bug，请写评论。