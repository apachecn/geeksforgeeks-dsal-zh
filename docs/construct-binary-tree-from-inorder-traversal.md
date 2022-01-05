# 从给定的有序遍历中构建特殊二叉树

> 原文:[https://www . geesforgeks . org/construct-二叉树-从-到-遍历/](https://www.geeksforgeeks.org/construct-binary-tree-from-inorder-traversal/)

给定特殊二叉树的有序遍历，其中每个节点的键大于左右子节点的键，构造二叉树并返回根。

**示例:**

```
Input: inorder[] = {5, 10, 40, 30, 28}
Output: root of following tree
         40
       /   \
      10     30
     /         \
    5          28 

Input: inorder[] = {1, 5, 10, 40, 30, 
                    15, 28, 20}
Output: root of following tree
          40
        /   \
       10     30
      /         \
     5          28
    /          /  \
   1         15    20
```

这里可以使用[从给定的有序和预有序遍历](https://www.geeksforgeeks.org/construct-tree-from-given-inorder-and-preorder-traversal/)构造树中使用的思想。假设给定的数组是{1，5，10，40，30，15，28，20}。给定数组中的最大元素必须是根元素。最大元素左侧的元素在左子树，右侧的元素在右子树。

```
         40
      /       \  
   {1,5,10}   {30,15,28,20}
```

我们递归地按照上面的步骤进行左右子树，最后得到下面的树。

```
          40
        /   \
       10     30
      /         \
     5          28
    /          /  \
   1         15    20
```

**算法:** buildTree()
1)求数组中最大元素的索引。最大元素必须是二叉树的根。
2)用步骤 1 中找到的最大值作为数据创建一个新的树节点“根”。
3)为最大元素之前的元素调用构建树，并使构建树成为“根”的左子树。
5)对最大元素后的元素调用 buildTree，将构建的树作为‘根’的右子树。
6)返回‘根’。

**实现:**以下是上述算法的实现。

## C++

```
/* C++ program to construct tree
from inorder traversal */
#include <bits/stdc++.h>
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
};

/* Prototypes of a utility function to get the maximum
value in inorder[start..end] */
int max(int inorder[], int strt, int end);

/* A utility function to allocate memory for a node */
node* newNode(int data);

/* Recursive function to construct binary of size len from
Inorder traversal inorder[]. Initial values of start and end
should be 0 and len -1\. */
node* buildTree (int inorder[], int start, int end)
{
    if (start > end)
        return NULL;

    /* Find index of the maximum element from Binary Tree */
    int i = max (inorder, start, end);

    /* Pick the maximum value and make it root */
    node *root = newNode(inorder[i]);

    /* If this is the only element in inorder[start..end],
    then return it */
    if (start == end)
        return root;

    /* Using index in Inorder traversal, construct left and
    right subtress */
    root->left = buildTree (inorder, start, i - 1);
    root->right = buildTree (inorder, i + 1, end);

    return root;
}

/* UTILITY FUNCTIONS */
/* Function to find index of the maximum value in arr[start...end] */
int max (int arr[], int strt, int end)
{
    int i, max = arr[strt], maxind = strt;
    for(i = strt + 1; i <= end; i++)
    {
        if(arr[i] > max)
        {
            max = arr[i];
            maxind = i;
        }
    }
    return maxind;
}

/* Helper function that allocates a new node with the
given data and NULL left and right pointers. */
node* newNode (int data)
{
    node* Node = new node();
    Node->data = data;
    Node->left = NULL;
    Node->right = NULL;

    return Node;
}

/* This function is here just to test buildTree() */
void printInorder (node* node)
{
    if (node == NULL)
        return;

    /* first recur on left child */
    printInorder (node->left);

    /* then print the data of node */
    cout<<node->data<<" ";

    /* now recur on right child */
    printInorder (node->right);
}

/* Driver code*/
int main()
{
    /* Assume that inorder traversal of following tree is given
        40
        / \
        10 30
        /     \
        5     28 */

    int inorder[] = {5, 10, 40, 30, 28};
    int len = sizeof(inorder)/sizeof(inorder[0]);
    node *root = buildTree(inorder, 0, len - 1);

    /* Let us test the built tree by printing Inorder traversal */
    cout << "Inorder traversal of the constructed tree is \n";
    printInorder(root);
    return 0;
}

// This is code is contributed by rathbhupendra
```

## C

```
/* program to construct tree from inorder traversal */
#include<stdio.h>
#include<stdlib.h>

/* A binary tree node has data, pointer to left child
   and a pointer to right child */
struct node
{
    int data;
    struct node* left;
    struct node* right;
};

/* Prototypes of a utility function to get the maximum
   value in inorder[start..end] */
int max(int inorder[], int strt, int end);

/* A utility function to allocate memory for a node */
struct node* newNode(int data);

/* Recursive function to construct binary of size len from
   Inorder traversal inorder[]. Initial values of start and end
   should be 0 and len -1.  */
struct node* buildTree (int inorder[], int start, int end)
{
    if (start > end)
        return NULL;

    /* Find index of the maximum element from Binary Tree */
    int i = max (inorder, start, end);

    /* Pick the maximum value and make it root */
    struct node *root = newNode(inorder[i]);

    /* If this is the only element in inorder[start..end],
       then return it */
    if (start == end)
        return root;

    /* Using index in Inorder traversal, construct left and
       right subtress */
    root->left  = buildTree (inorder, start, i-1);
    root->right = buildTree (inorder, i+1, end);

    return root;
}

/* UTILITY FUNCTIONS */
/* Function to find index of the maximum value in arr[start...end] */
int max (int arr[], int strt, int end)
{
    int i, max = arr[strt], maxind = strt;
    for(i = strt+1; i <= end; i++)
    {
        if(arr[i] > max)
        {
            max = arr[i];
            maxind = i;
        }
    }
    return maxind;
}

/* Helper function that allocates a new node with the
   given data and NULL left and right pointers. */
struct node* newNode (int data)
{
    struct node* node = (struct node*)malloc(sizeof(struct node));
    node->data = data;
    node->left = NULL;
    node->right = NULL;

    return node;
}

/* This function is here just to test buildTree() */
void printInorder (struct node* node)
{
    if (node == NULL)
        return;

    /* first recur on left child */
    printInorder (node->left);

    /* then print the data of node */
    printf("%d ", node->data);

    /* now recur on right child */
    printInorder (node->right);
}

/* Driver program to test above functions */
int main()
{
   /* Assume that inorder traversal of following tree is given
         40
       /   \
      10     30
     /         \
    5          28 */

    int inorder[] = {5, 10, 40, 30, 28};
    int len = sizeof(inorder)/sizeof(inorder[0]);
    struct node *root = buildTree(inorder, 0, len - 1);

    /* Let us test the built tree by printing Inorder traversal */
    printf("\n Inorder traversal of the constructed tree is \n");
    printInorder(root);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to construct tree from inorder traversal

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

    /* Recursive function to construct binary of size len from
       Inorder traversal inorder[]. Initial values of start and end
       should be 0 and len -1.  */
    Node buildTree(int inorder[], int start, int end, Node node)
    {
        if (start > end)
            return null;

        /* Find index of the maximum element from Binary Tree */
        int i = max(inorder, start, end);

        /* Pick the maximum value and make it root */
        node = new Node(inorder[i]);

        /* If this is the only element in inorder[start..end],
         then return it */
        if (start == end)
            return node;

        /* Using index in Inorder traversal, construct left and
         right subtress */
        node.left = buildTree(inorder, start, i - 1, node.left);
        node.right = buildTree(inorder, i + 1, end, node.right);

        return node;
    }

    /* UTILITY FUNCTIONS */

    /* Function to find index of the maximum value in arr[start...end] */
    int max(int arr[], int strt, int end)
    {
        int i, max = arr[strt], maxind = strt;
        for (i = strt + 1; i <= end; i++)
        {
            if (arr[i] > max)
            {
                max = arr[i];
                maxind = i;
            }
        }
        return maxind;
    }

    /* This function is here just to test buildTree() */
    void printInorder(Node node)
    {
        if (node == null)
            return;

        /* first recur on left child */
        printInorder(node.left);

        /* then print the data of node */
        System.out.print(node.data + " ");

        /* now recur on right child */
        printInorder(node.right);
    }

    public static void main(String args[])
    {
        BinaryTree tree = new BinaryTree();

        /* Assume that inorder traversal of following tree is given
             40
            /   \
          10     30
         /         \
        5          28 */
        int inorder[] = new int[]{5, 10, 40, 30, 28};
        int len = inorder.length;
        Node mynode = tree.buildTree(inorder, 0, len - 1, tree.root);

        /* Let us test the built tree by printing Inorder traversal */
        System.out.println("Inorder traversal of the constructed tree is ");
        tree.printInorder(mynode);
    }
}

// This code has been contributed by Mayank Jaiswal
```

## 蟒蛇 3

```
# Python3 program to construct tree from
# inorder traversal

# Helper class that allocates a new node
# with the given data and None left and
# right pointers.
class newNode:
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# Prototypes of a utility function to get
# the maximum value in inorder[start..end]

# Recursive function to construct binary of
# size len from Inorder traversal inorder[].
# Initial values of start and end should be
# 0 and len -1.
def buildTree (inorder, start, end):
    if start > end:
        return None

    # Find index of the maximum element
    # from Binary Tree
    i = Max (inorder, start, end)

    # Pick the maximum value and make it root
    root = newNode(inorder[i])

    # If this is the only element in
    # inorder[start..end], then return it
    if start == end:
        return root

    # Using index in Inorder traversal,
    # construct left and right subtress
    root.left = buildTree (inorder, start, i - 1)
    root.right = buildTree (inorder, i + 1, end)

    return root

# UTILITY FUNCTIONS

# Function to find index of the maximum
# value in arr[start...end]
def Max(arr, strt, end):
    i, Max = 0, arr[strt]
    maxind = strt
    for i in range(strt + 1, end + 1):
        if arr[i] > Max:
            Max = arr[i]
            maxind = i
    return maxind

# This function is here just to test buildTree()
def printInorder (node):
    if node == None:
        return

    # first recur on left child
    printInorder (node.left)

    # then print the data of node
    print(node.data, end = " ")

    # now recur on right child
    printInorder (node.right)

# Driver Code
if __name__ == '__main__':

    # Assume that inorder traversal of
    # following tree is given
    #     40
    # / \
    # 10     30
    # /         \
    #5         28

    inorder = [5, 10, 40, 30, 28]
    Len = len(inorder)
    root = buildTree(inorder, 0, Len - 1)

    # Let us test the built tree by
    # printing Inorder traversal
    print("Inorder traversal of the",
              "constructed tree is ")
    printInorder(root)

# This code is contributed by PranchalK
```

## C#

```
// C# program to construct tree
// from inorder traversal
using System;

/* A binary tree node has data,
pointer to left child and a pointer
to right child */
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

class GFG
{
public Node root;

/* Recursive function to construct binary
of size len from Inorder traversal inorder[].
Initial values of start and end should be 0
and len -1\. */
public virtual Node buildTree(int[] inorder, int start,
                              int end, Node node)
{
    if (start > end)
    {
        return null;
    }

    /* Find index of the maximum
    element from Binary Tree */
    int i = max(inorder, start, end);

    /* Pick the maximum value and
    make it root */
    node = new Node(inorder[i]);

    /* If this is the only element in
    inorder[start..end], then return it */
    if (start == end)
    {
        return node;
    }

    /* Using index in Inorder traversal,
    construct left and right subtress */
    node.left = buildTree(inorder, start,
                          i - 1, node.left);
    node.right = buildTree(inorder, i + 1,
                           end, node.right);

    return node;
}

/* UTILITY FUNCTIONS */

/* Function to find index of the
maximum value in arr[start...end] */
public virtual int max(int[] arr,
                       int strt, int end)
{
    int i, max = arr[strt], maxind = strt;
    for (i = strt + 1; i <= end; i++)
    {
        if (arr[i] > max)
        {
            max = arr[i];
            maxind = i;
        }
    }
    return maxind;
}

/* This function is here just
   to test buildTree() */
public virtual void printInorder(Node node)
{
    if (node == null)
    {
        return;
    }

    /* first recur on left child */
    printInorder(node.left);

    /* then print the data of node */
    Console.Write(node.data + " ");

    /* now recur on right child */
    printInorder(node.right);
}

// Driver Code
public static void Main(string[] args)
{
    GFG tree = new GFG();

    /* Assume that inorder traversal
       of following tree is given
        40
        / \
    10     30
    /         \
    5         28 */
    int[] inorder = new int[]{5, 10, 40, 30, 28};
    int len = inorder.Length;
    Node mynode = tree.buildTree(inorder, 0,
                                 len - 1, tree.root);

    /* Let us test the built tree by
       printing Inorder traversal */
    Console.WriteLine("Inorder traversal of " +
                   "the constructed tree is ");
    tree.printInorder(mynode);
}
}

// This code is contributed by Shrikant13
```

## java 描述语言

```
<script>

// JavaScript program to construct tree
// from inorder traversal

/* A binary tree node has data,
pointer to left child and a pointer
to right child */
class Node
{
    constructor(item)
    {
        this.data = item;
        this.left = null;
        this.right = null;
    }
}

var root = null;

/* Recursive function to construct binary
of size len from Inorder traversal inorder[].
Initial values of start and end should be 0
and len -1\. */
function buildTree(inorder, start, end, node)
{
    if (start > end)
    {
        return null;
    }

    /* Find index of the maximum
    element from Binary Tree */
    var i = max(inorder, start, end);

    /* Pick the maximum value and
    make it root */
    node = new Node(inorder[i]);

    /* If this is the only element in
    inorder[start..end], then return it */
    if (start == end)
    {
        return node;
    }

    /* Using index in Inorder traversal,
    construct left and right subtress */
    node.left = buildTree(inorder, start,
                          i - 1, node.left);
    node.right = buildTree(inorder, i + 1,
                           end, node.right);

    return node;
}

/* UTILITY FUNCTIONS */

/* Function to find index of the
maximum value in arr[start...end] */
function max(arr, strt, end)
{
    var i, maxi = arr[strt], maxind = strt;
    for (i = strt + 1; i <= end; i++)
    {
        if (arr[i] > maxi)
        {
            maxi = arr[i];
            maxind = i;
        }
    }
    return maxind;
}

/* This function is here just
   to test buildTree() */
function printInorder(node)
{
    if (node == null)
    {
        return;
    }

    /* first recur on left child */
    printInorder(node.left);

    /* then print the data of node */
    document.write(node.data + " ");

    /* now recur on right child */
    printInorder(node.right);
}

// Driver Code

/* Assume that inorder traversal
   of following tree is given
    40
    / \
10     30
/         \
5         28 */
var inorder = [5, 10, 40, 30, 28];
var len = inorder.length;
var mynode = buildTree(inorder, 0, len - 1, root);
/* Let us test the built tree by
   printing Inorder traversal */
document.write("Inorder traversal of " +
               "the constructed tree is <br>");
printInorder(mynode);

</script>
```

**输出:**

```
 Inorder traversal of the constructed tree is
 5 10 40 30 28
```

**时间复杂度:** O(n^2)

如果发现有不正确的地方，请写评论，或者想分享更多关于以上讨论话题的信息