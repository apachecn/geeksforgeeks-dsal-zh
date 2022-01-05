# 排序数组到平衡 BST

> 原文:[https://www.geeksforgeeks.org/sorted-array-to-balanced-bst/](https://www.geeksforgeeks.org/sorted-array-to-balanced-bst/)

给定一个排序数组。编写一个使用数组元素创建平衡二叉查找树的函数。
**例:**

```
Input:  Array {1, 2, 3}
Output: A Balanced BST
     2
   /  \
  1    3 

Input: Array {1, 2, 3, 4}
Output: A Balanced BST
      3
    /  \
   2    4
 /
1
```

**算法**
在[之前的帖子](https://www.geeksforgeeks.org/sorted-linked-list-to-balanced-bst/)中，我们讨论了从排序链表构建 BST。在 O(n)时间内从排序数组构造更简单，因为我们可以在 O(1)时间内得到中间元素。下面是一个简单的算法，我们首先找到列表的中间节点，并使它成为要构建的树的根。

```
1) Get the Middle of the array and make it root.
2) Recursively do same for left half and right half.
      a) Get the middle of left half and make it left child of the root
          created in step 1.
      b) Get the middle of right half and make it right child of the
          root created in step 1.
```

下面是上述算法的实现。突出显示了创建平衡基站的主要代码。

## C++

```
// C++ program to print BST in given range
#include<bits/stdc++.h>
using namespace std;

/* A Binary Tree node */
class TNode
{
    public:
    int data;
    TNode* left;
    TNode* right;
};

TNode* newNode(int data);

/* A function that constructs Balanced
Binary Search Tree from a sorted array */
TNode* sortedArrayToBST(int arr[],
                        int start, int end)
{
    /* Base Case */
    if (start > end)
    return NULL;

    /* Get the middle element and make it root */
    int mid = (start + end)/2;
    TNode *root = newNode(arr[mid]);

    /* Recursively construct the left subtree
    and make it left child of root */
    root->left = sortedArrayToBST(arr, start,
                                    mid - 1);

    /* Recursively construct the right subtree
    and make it right child of root */
    root->right = sortedArrayToBST(arr, mid + 1, end);

    return root;
}

/* Helper function that allocates a new node
with the given data and NULL left and right
pointers. */
TNode* newNode(int data)
{
    TNode* node = new TNode();
    node->data = data;
    node->left = NULL;
    node->right = NULL;

    return node;
}

/* A utility function to print
preorder traversal of BST */
void preOrder(TNode* node)
{
    if (node == NULL)
        return;
    cout << node->data << " ";
    preOrder(node->left);
    preOrder(node->right);
}

// Driver Code
int main()
{
    int arr[] = {1, 2, 3, 4, 5, 6, 7};
    int n = sizeof(arr) / sizeof(arr[0]);

    /* Convert List to BST */
    TNode *root = sortedArrayToBST(arr, 0, n-1);
    cout << "PreOrder Traversal of constructed BST \n";
    preOrder(root);

    return 0;
}

// This code is contributed by rathbhupendra
```

## C

```
#include<stdio.h>
#include<stdlib.h>

/* A Binary Tree node */
struct TNode
{
    int data;
    struct TNode* left;
    struct TNode* right;
};

struct TNode* newNode(int data);

/* A function that constructs Balanced Binary Search Tree from a sorted array */
struct TNode* sortedArrayToBST(int arr[], int start, int end)
{
    /* Base Case */
    if (start > end)
      return NULL;

    /* Get the middle element and make it root */
    int mid = (start + end)/2;
    struct TNode *root = newNode(arr[mid]);

    /* Recursively construct the left subtree and make it
       left child of root */
    root->left =  sortedArrayToBST(arr, start, mid-1);

    /* Recursively construct the right subtree and make it
       right child of root */
    root->right = sortedArrayToBST(arr, mid+1, end);

    return root;
}

/* Helper function that allocates a new node with the
   given data and NULL left and right pointers. */
struct TNode* newNode(int data)
{
    struct TNode* node = (struct TNode*)
                         malloc(sizeof(struct TNode));
    node->data = data;
    node->left = NULL;
    node->right = NULL;

    return node;
}

/* A utility function to print preorder traversal of BST */
void preOrder(struct TNode* node)
{
    if (node == NULL)
        return;
    printf("%d ", node->data);
    preOrder(node->left);
    preOrder(node->right);
}

/* Driver program to test above functions */
int main()
{
    int arr[] = {1, 2, 3, 4, 5, 6, 7};
    int n = sizeof(arr)/sizeof(arr[0]);

    /* Convert List to BST */
    struct TNode *root = sortedArrayToBST(arr, 0, n-1);
    printf("n PreOrder Traversal of constructed BST ");
    preOrder(root);

    return 0;
}
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

    /* A function that constructs Balanced Binary Search Tree
     from a sorted array */
    Node sortedArrayToBST(int arr[], int start, int end) {

        /* Base Case */
        if (start > end) {
            return null;
        }

        /* Get the middle element and make it root */
        int mid = (start + end) / 2;
        Node node = new Node(arr[mid]);

        /* Recursively construct the left subtree and make it
         left child of root */
        node.left = sortedArrayToBST(arr, start, mid - 1);

        /* Recursively construct the right subtree and make it
         right child of root */
        node.right = sortedArrayToBST(arr, mid + 1, end);

        return node;
    }

    /* A utility function to print preorder traversal of BST */
    void preOrder(Node node) {
        if (node == null) {
            return;
        }
        System.out.print(node.data + " ");
        preOrder(node.left);
        preOrder(node.right);
    }

    public static void main(String[] args) {
        BinaryTree tree = new BinaryTree();
        int arr[] = new int[]{1, 2, 3, 4, 5, 6, 7};
        int n = arr.length;
        root = tree.sortedArrayToBST(arr, 0, n - 1);
        System.out.println("Preorder traversal of constructed BST");
        tree.preOrder(root);
    }
}

// This code has been contributed by Mayank Jaiswal
```

## 计算机编程语言

```
# Python code to convert a sorted array
# to a balanced Binary Search Tree

# binary tree node
class Node:
    def __init__(self, d):
        self.data = d
        self.left = None
        self.right = None

# function to convert sorted array to a
# balanced BST
# input : sorted array of integers
# output: root node of balanced BST
def sortedArrayToBST(arr):

    if not arr:
        return None

    # find middle
    mid = (len(arr)) / 2

    # make the middle element the root
    root = Node(arr[mid])

    # left subtree of root has all
    # values <arr[mid]
    root.left = sortedArrayToBST(arr[:mid])

    # right subtree of root has all
    # values >arr[mid]
    root.right = sortedArrayToBST(arr[mid+1:])
    return root

# A utility function to print the preorder
# traversal of the BST
def preOrder(node):
    if not node:
        return

    print node.data,
    preOrder(node.left)
    preOrder(node.right)

# driver program to test above function
"""
Constructed balanced BST is
    4
/ \
2 6
/ \ / \
1 3 5 7
"""

arr = [1, 2, 3, 4, 5, 6, 7]
root = sortedArrayToBST(arr)
print "PreOrder Traversal of constructed BST ",
preOrder(root)

# This code is contributed by Ishita Tripathi
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

    /* A function that constructs Balanced Binary Search Tree 
     from a sorted array */
    public virtual Node sortedArrayToBST(int[] arr, int start, int end)
    {

        /* Base Case */
        if (start > end)
        {
            return null;
        }

        /* Get the middle element and make it root */
        int mid = (start + end) / 2;
        Node node = new Node(arr[mid]);

        /* Recursively construct the left subtree and make it
         left child of root */
        node.left = sortedArrayToBST(arr, start, mid - 1);

        /* Recursively construct the right subtree and make it
         right child of root */
        node.right = sortedArrayToBST(arr, mid + 1, end);

        return node;
    }

    /* A utility function to print preorder traversal of BST */
    public virtual void preOrder(Node node)
    {
        if (node == null)
        {
            return;
        }
        Console.Write(node.data + " ");
        preOrder(node.left);
        preOrder(node.right);
    }

    public static void Main(string[] args)
    {
        BinaryTree tree = new BinaryTree();
        int[] arr = new int[]{1, 2, 3, 4, 5, 6, 7};
        int n = arr.Length;
        root = tree.sortedArrayToBST(arr, 0, n - 1);
        Console.WriteLine("Preorder traversal of constructed BST");
        tree.preOrder(root);
    }
}

  // This code is contributed by Shrikant13
```

## java 描述语言

```
<script>

// JavaScript program to print BST in given range

// A binary tree node
class Node
{
    constructor(d)
    {
        this.data = d;
        this.left = null;
        this.right = null;
    }
}

var root = null;

/* A function that constructs Balanced Binary Search Tree 
 from a sorted array */
function sortedArrayToBST(arr, start, end)
{
    /* Base Case */
    if (start > end)
    {
        return null;
    }
    /* Get the middle element and make it root */
    var mid = parseInt((start + end) / 2);
    var node = new Node(arr[mid]);
    /* Recursively construct the left subtree and make it
     left child of root */
    node.left = sortedArrayToBST(arr, start, mid - 1);
    /* Recursively construct the right subtree and make it
     right child of root */
    node.right = sortedArrayToBST(arr, mid + 1, end);
    return node;
}
/* A utility function to print preorder traversal of BST */
function preOrder(node)
{
    if (node == null)
    {
        return;
    }
    document.write(node.data + " ");
    preOrder(node.left);
    preOrder(node.right);
}

var arr = [1, 2, 3, 4, 5, 6, 7];
var n = arr.length;
root = sortedArrayToBST(arr, 0, n - 1);
document.write("Preorder traversal of constructed BST<br>");
preOrder(root);

</script>
```

**输出:**

```
Preorder traversal of constructed BST
4 2 1 3 6 5 7 
```

```
Tree representation of above output:
     4  
 2      6
1  3  5   7
```

**时间复杂度:** O(n)
以下是 sortedArrayToBST()的递归关系。

```
  T(n) = 2T(n/2) + C
  T(n) -->  Time taken for an array of size n
   C   -->  Constant (Finding middle of array and linking root to left 
                      and right subtrees take constant time) 
```

上述递推可以用[主定理](http://en.wikipedia.org/wiki/Master_theorem)求解，因为它属于情况 1。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。