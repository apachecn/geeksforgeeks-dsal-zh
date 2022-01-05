# 找到给定二叉树中最大的 BST 子树|集合 1

> 原文:[https://www . geesforgeks . org/find-树中最大的子树-也就是 bst/](https://www.geeksforgeeks.org/find-the-largest-subtree-in-a-tree-that-is-also-a-bst/)

给定一棵二叉树，写一个函数，返回最大的子树的大小，它也是一个二叉查找树树。如果完整的二叉树是 BST，那么返回整个树的大小。
**例:**

```
Input: 
      5
    /  \
   2    4
 /  \
1    3

Output: 3 
The following subtree is the maximum size BST subtree 
   2  
 /  \
1    3

Input: 
       50
     /    \
  30       60
 /  \     /  \ 
5   20   45    70
              /  \
            65    80
Output: 5
The following subtree is the maximum size BST subtree 
      60
     /  \ 
   45    70
        /  \
      65    80
```

**方法 1(简单但低效)**
从根开始，对树进行有序遍历。对于每个节点 N，检查以 N 为根的子树是否为 BST。如果是 BST，则返回以 n 为根的子树的大小，否则，沿左右子树向下循环，并返回左右子树返回的最大值。

## C

```
/*
  See https://www.geeksforgeeks.org/write-a-c-program-to-calculate-size-of-a-tree/ for implementation of size()

  See Method 3 of https://www.geeksforgeeks.org/a-program-to-check-if-a-binary-tree-is-bst-or-not/ for
  implementation of isBST()

  max() returns maximum of two integers
*/  
int largestBST(struct node *root)
{
  // Base Case
  if(root == NULL)
    return 0;

   if (isBST(root))
     return size(root);
   else
    return max(largestBST(root->left), largestBST(root->right));
}

// This code is contributed by mahi_07
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/*
  See

  https://www.geeksforgeeks.org/write-a-c-program-to-calculate-size-of-a-tree/
  for implementation of size()

  See Method 3 of
  https://www.geeksforgeeks.org/a-program-to-check-if-a-binary-tree-is-bst-or-not/
  for
  implementation of isBST()
  max() returns maximum of two integers
*/

import java.io.*;

class GFG {

    int largestBST(Node root)
    {
        if (root == null)
            return 0;

        if (isBST(root))
            return size(root);

        return Math.max(largestBST(root.left),
                        largestBST(root.right));
    }
}
```

## java 描述语言

```
<script>

/*
  See

  https://www.geeksforgeeks.org/write-a-c-program-to-calculate-size-of-a-tree/
  for implementation of size()

  See Method 3 of
  https://www.geeksforgeeks.org/a-program-to-check-if-a-binary-tree-is-bst-or-not/
  for
  implementation of isBST()

  max() returns maximum of two integers
*/  
function largestBST(root)
{
   if (isBST(root))
     return size(root);
   else
    return Math.max(largestBST(root.left), largestBST(root.right));
}

</script>
```

时间复杂度:这种方法最差的时间复杂度是 O(n^2).考虑一个用于最坏情况分析的倾斜树。
**方法 2(棘手且高效)**
在方法 1 中，我们以自上而下的方式遍历树，并对每个节点进行 BST 测试。如果我们以自下而上的方式遍历树，那么我们可以将关于子树的信息传递给父树。传递的信息只能由父节点在恒定时间(或 O(1)时间)内进行 BST 测试(对于父节点)。一个左子树需要告诉父树它是否是 BST，还需要传递其中的最大值。这样我们就可以将最大值与父数据进行比较，以检查 BST 属性。同样，右子树需要将最小值向上传递给树。为了找到最大的基站，子树需要将以下信息传递到树上。
1)子树本身是否为 BST(在下面的代码中，is_bst_ref 用于此目的)
2)如果子树是其父树的左子树，则其中的最大值。如果它是正确的子树，那么它的最小值。
3)这个子树的大小如果这个子树是 BST(在下面的代码中，返回值 largestBSTtil()用于此目的)
max_ref 用于向上传递树的最大值，min_ptr 用于向上传递树的最小值。

## C++

```
// C++ program of above approach
#include<bits/stdc++.h>

using namespace std;

/* A binary tree node has data,
pointer to left child and a pointer
to right child */
class node
{
    public:
    int data;
    node* left;
    node* right;

    /* Constructor that allocates
    a new node with the given data
    and NULL left and right pointers. */
    node(int data)
    {
        this->data = data;
        this->left = NULL;
        this->right = NULL;

    }
};

int largestBSTUtil(node* node, int *min_ref, int *max_ref,
                    int *max_size_ref, bool *is_bst_ref);

/* Returns size of the largest BST
subtree in a Binary Tree
(efficient version). */
int largestBST(node* node)
{
    // Set the initial values for
    // calling largestBSTUtil()
    int min = INT_MAX; // For minimum value in right subtree
    int max = INT_MIN; // For maximum value in left subtree

    int max_size = 0; // For size of the largest BST
    bool is_bst = 0;

    largestBSTUtil(node, &min, &max,
                    &max_size, &is_bst);

    return max_size;
}

/* largestBSTUtil() updates *max_size_ref
for the size of the largest BST subtree.
Also, if the tree rooted with node is
non-empty and a BST, then returns size
of the tree. Otherwise returns 0.*/
int largestBSTUtil(node* node, int *min_ref, int *max_ref,
                    int *max_size_ref, bool *is_bst_ref)
{

    /* Base Case */
    if (node == NULL)
    {
        *is_bst_ref = 1; // An empty tree is BST
        return 0; // Size of the BST is 0
    }

    int min = INT_MAX;

    /* A flag variable for left subtree property
        i.e., max(root->left) < root->data */
    bool left_flag = false;

    /* A flag variable for right subtree property
        i.e., min(root->right) > root->data */
    bool right_flag = false;

    int ls, rs; // To store sizes of left and right subtrees

    /* Following tasks are done by
    recursive call for left subtree
        a) Get the maximum value in left
        subtree (Stored in *max_ref)
        b) Check whether Left Subtree is
        BST or not (Stored in *is_bst_ref)
        c) Get the size of maximum size BST
        in left subtree (updates *max_size) */
    *max_ref = INT_MIN;
    ls = largestBSTUtil(node->left, min_ref, max_ref,
                        max_size_ref, is_bst_ref);
    if (*is_bst_ref == 1 && node->data > *max_ref)
        left_flag = true;

    /* Before updating *min_ref, store the min
    value in left subtree. So that we have the
    correct minimum value for this subtree */
    min = *min_ref;

    /* The following recursive call
    does similar (similar to left subtree)
    task for right subtree */
    *min_ref = INT_MAX;
    rs = largestBSTUtil(node->right, min_ref,
                        max_ref, max_size_ref, is_bst_ref);
    if (*is_bst_ref == 1 && node->data < *min_ref)
        right_flag = true;

    // Update min and max values for
    // the parent recursive calls
    if (min < *min_ref)
        *min_ref = min;
    if (node->data < *min_ref) // For leaf nodes
        *min_ref = node->data;
    if (node->data > *max_ref)
        *max_ref = node->data;

    /* If both left and right subtrees are BST.
    And left and right subtree properties hold
    for this node, then this tree is BST.
    So return the size of this tree */
    if(left_flag && right_flag)
    {
        if (ls + rs + 1 > *max_size_ref)
            *max_size_ref = ls + rs + 1;
        return ls + rs + 1;
    }
    else
    {
        // Since this subtree is not BST,
        // set is_bst flag for parent calls
        *is_bst_ref = 0;
        return 0;
    }
}

/* Driver code*/
int main()
{
        /* Let us construct the following Tree
            50
        / \
        10 60
        / \ / \
    5 20 55 70
                / / \
            45 65 80
    */

    node *root = new node(50);
    root->left = new node(10);
    root->right = new node(60);
    root->left->left = new node(5);
    root->left->right = new node(20);
    root->right->left = new node(55);
    root->right->left->left = new node(45);
    root->right->right = new node(70);
    root->right->right->left = new node(65);
    root->right->right->right = new node(80);

    /* The complete tree is not BST
    as 45 is in right subtree of 50.
    The following subtree is the largest BST
            60
        / \
        55 70
    / / \
    45 65 80
    */
    cout<<" Size of the largest BST is "<< largestBST(root);

    return 0;
}

// This code is contributed by rathbhupendra
```

## C

```
#include <stdio.h>
#include <stdlib.h>
#include <limits.h>

/* A binary tree node has data, pointer to left child
   and a pointer to right child */
struct node
{
    int data;
    struct node* left;
    struct node* right;
};

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

int largestBSTUtil(struct node* node, int *min_ref, int *max_ref,
                             int *max_size_ref, bool *is_bst_ref);

/* Returns size of the largest BST subtree in a Binary Tree
  (efficient version). */
int largestBST(struct node* node)
{
  // Set the initial values for calling largestBSTUtil()
  int min = INT_MAX;  // For minimum value in right subtree
  int max = INT_MIN;  // For maximum value in left subtree

  int max_size = 0;  // For size of the largest BST
  bool is_bst = 0;

  largestBSTUtil(node, &min, &max, &max_size, &is_bst);

  return max_size;
}

/* largestBSTUtil() updates *max_size_ref for the size of the largest BST
   subtree.   Also, if the tree rooted with node is non-empty and a BST,
   then returns size of the tree. Otherwise returns 0.*/
int largestBSTUtil(struct node* node, int *min_ref, int *max_ref,
                            int *max_size_ref, bool *is_bst_ref)
{

  /* Base Case */
  if (node == NULL)
  {
     *is_bst_ref = 1; // An empty tree is BST
     return 0;    // Size of the BST is 0
  }

  int min = INT_MAX;

  /* A flag variable for left subtree property
     i.e., max(root->left) < root->data */
  bool left_flag = false;

  /* A flag variable for right subtree property
     i.e., min(root->right) > root->data */
  bool right_flag = false;

  int ls, rs; // To store sizes of left and right subtrees

  /* Following tasks are done by recursive call for left subtree
    a) Get the maximum value in left subtree (Stored in *max_ref)
    b) Check whether Left Subtree is BST or not (Stored in *is_bst_ref)
    c) Get the size of maximum size BST in left subtree (updates *max_size) */
  *max_ref = INT_MIN;
  ls = largestBSTUtil(node->left, min_ref, max_ref, max_size_ref, is_bst_ref);
  if (*is_bst_ref == 1 && node->data > *max_ref)
     left_flag = true;

  /* Before updating *min_ref, store the min value in left subtree. So that we
     have the correct minimum value for this subtree */
  min = *min_ref;

  /* The following recursive call does similar (similar to left subtree)
    task for right subtree */
  *min_ref =  INT_MAX;
  rs = largestBSTUtil(node->right, min_ref, max_ref, max_size_ref, is_bst_ref);
  if (*is_bst_ref == 1 && node->data < *min_ref)
     right_flag = true;

  // Update min and max values for the parent recursive calls
  if (min < *min_ref)
     *min_ref = min;
  if (node->data < *min_ref) // For leaf nodes
     *min_ref = node->data;
  if (node->data > *max_ref)
     *max_ref = node->data;

  /* If both left and right subtrees are BST. And left and right
     subtree properties hold for this node, then this tree is BST.
     So return the size of this tree */
  if(left_flag && right_flag)
  {
     if (ls + rs + 1 > *max_size_ref)
         *max_size_ref = ls + rs + 1;
     return ls + rs + 1;
  }
  else
  {
    //Since this subtree is not BST, set is_bst flag for parent calls
     *is_bst_ref = 0;
     return 0;
  }
}

/* Driver program to test above functions*/
int main()
{
    /* Let us construct the following Tree
          50
       /      \
     10        60
    /  \       /  \
   5   20    55    70
            /     /  \
          45     65    80
  */

  struct node *root = newNode(50);
  root->left        = newNode(10);
  root->right       = newNode(60);
  root->left->left  = newNode(5);
  root->left->right = newNode(20);
  root->right->left  = newNode(55);
  root->right->left->left  = newNode(45);
  root->right->right = newNode(70);
  root->right->right->left = newNode(65);
  root->right->right->right = newNode(80);

  /* The complete tree is not BST as 45 is in right subtree of 50.
     The following subtree is the largest BST
        60
      /  \
    55    70
   /     /  \
 45     65    80
  */
  printf(" Size of the largest BST is %d", largestBST(root));

  getchar();
  return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find largest BST subtree in given Binary Tree

class Node {

    int data;
    Node left, right;

    Node(int d) {
        data = d;
        left = right = null;
    }
}

class Value {

    int max_size = 0; // for size of largest BST
    boolean is_bst = false;
    int min = Integer.MAX_VALUE;  // For minimum value in right subtree
    int max = Integer.MIN_VALUE;  // For maximum value in left subtree

}

class BinaryTree {

    static Node root;
    Value val = new Value();

    /* Returns size of the largest BST subtree in a Binary Tree
     (efficient version). */
    int largestBST(Node node) {

        largestBSTUtil(node, val, val, val, val);

        return val.max_size;
    }

    /* largestBSTUtil() updates *max_size_ref for the size of the largest BST
     subtree.   Also, if the tree rooted with node is non-empty and a BST,
     then returns size of the tree. Otherwise returns 0.*/
    int largestBSTUtil(Node node, Value min_ref, Value max_ref,
            Value max_size_ref, Value is_bst_ref) {

        /* Base Case */
        if (node == null) {
            is_bst_ref.is_bst = true; // An empty tree is BST
            return 0;    // Size of the BST is 0
        }

        int min = Integer.MAX_VALUE;

        /* A flag variable for left subtree property
         i.e., max(root->left) < root->data */
        boolean left_flag = false;

        /* A flag variable for right subtree property
         i.e., min(root->right) > root->data */
        boolean right_flag = false;

        int ls, rs; // To store sizes of left and right subtrees

        /* Following tasks are done by recursive call for left subtree
         a) Get the maximum value in left subtree (Stored in *max_ref)
         b) Check whether Left Subtree is BST or not (Stored in *is_bst_ref)
         c) Get the size of maximum size BST in left subtree (updates *max_size) */
        max_ref.max = Integer.MIN_VALUE;
        ls = largestBSTUtil(node.left, min_ref, max_ref, max_size_ref, is_bst_ref);
        if (is_bst_ref.is_bst == true && node.data > max_ref.max) {
            left_flag = true;
        }

        /* Before updating *min_ref, store the min value in left subtree. So that we
         have the correct minimum value for this subtree */
        min = min_ref.min;

        /* The following recursive call does similar (similar to left subtree)
         task for right subtree */
        min_ref.min = Integer.MAX_VALUE;
        rs = largestBSTUtil(node.right, min_ref, max_ref, max_size_ref, is_bst_ref);
        if (is_bst_ref.is_bst == true && node.data < min_ref.min) {
            right_flag = true;
        }

        // Update min and max values for the parent recursive calls
        if (min < min_ref.min) {
            min_ref.min = min;
        }
        if (node.data < min_ref.min) // For leaf nodes
        {
            min_ref.min = node.data;
        }
        if (node.data > max_ref.max) {
            max_ref.max = node.data;
        }

        /* If both left and right subtrees are BST. And left and right
         subtree properties hold for this node, then this tree is BST.
         So return the size of this tree */
        if (left_flag && right_flag) {
            if (ls + rs + 1 > max_size_ref.max_size) {
                max_size_ref.max_size = ls + rs + 1;
            }
            return ls + rs + 1;
        } else {
            //Since this subtree is not BST, set is_bst flag for parent calls
            is_bst_ref.is_bst = false;
            return 0;
        }
    }

    public static void main(String[] args) {
        /* Let us construct the following Tree
                50
             /      \
            10        60
           /  \       /  \
          5   20    55    70
         /     /  \
        45   65    80
         */

        BinaryTree tree = new BinaryTree();
        tree.root = new Node(50);
        tree.root.left = new Node(10);
        tree.root.right = new Node(60);
        tree.root.left.left = new Node(5);
        tree.root.left.right = new Node(20);
        tree.root.right.left = new Node(55);
        tree.root.right.left.left = new Node(45);
        tree.root.right.right = new Node(70);
        tree.root.right.right.left = new Node(65);
        tree.root.right.right.right = new Node(80);

        /* The complete tree is not BST as 45 is in right subtree of 50.
         The following subtree is the largest BST
             60
            /  \
          55    70
          /     /  \
        45     65   80
        */
        System.out.println("Size of largest BST is " + tree.largestBST(root));
    }
}

// This code has been contributed by Mayank Jaiswal
```

## 蟒蛇 3

```
# Helper function that allocates a new
# node with the given data and NULL left
# and right pointers.
class newNode:

    # Constructor to create a new node
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# Returns size of the largest BST subtree
# in a Binary Tree (efficient version).
def largestBST(node):

    # Set the initial values for calling
    # largestBSTUtil()
    Min = [999999999999] # For minimum value in    
                         # right subtree
    Max = [-999999999999] # For maximum value in
                          # left subtree

    max_size = [0] # For size of the largest BST
    is_bst = [0]

    largestBSTUtil(node, Min, Max,
                         max_size, is_bst)

    return max_size[0]

# largestBSTUtil() updates max_size_ref[0]
# for the size of the largest BST subtree.
# Also, if the tree rooted with node is
# non-empty and a BST, then returns size of
# the tree. Otherwise returns 0.
def largestBSTUtil(node, min_ref, max_ref,
                         max_size_ref, is_bst_ref):

    # Base Case
    if node == None:
        is_bst_ref[0] = 1 # An empty tree is BST
        return 0 # Size of the BST is 0

    Min = 999999999999

    # A flag variable for left subtree property
    # i.e., max(root.left) < root.data
    left_flag = False

    # A flag variable for right subtree property
    # i.e., min(root.right) > root.data
    right_flag = False

    ls, rs = 0, 0    # To store sizes of left and
                     # right subtrees

    # Following tasks are done by recursive
    # call for left subtree
    # a) Get the maximum value in left subtree
    #   (Stored in max_ref[0])
    # b) Check whether Left Subtree is BST or
    #    not (Stored in is_bst_ref[0])
    # c) Get the size of maximum size BST in
    #    left subtree (updates max_size[0])
    max_ref[0] = -999999999999
    ls = largestBSTUtil(node.left, min_ref, max_ref,
                           max_size_ref, is_bst_ref)
    if is_bst_ref[0] == 1 and node.data > max_ref[0]:
        left_flag = True

    # Before updating min_ref[0], store the min
    # value in left subtree. So that we have the 
    # correct minimum value for this subtree
    Min = min_ref[0]

    # The following recursive call does similar 
    # (similar to left subtree) task for right subtree
    min_ref[0] = 999999999999
    rs = largestBSTUtil(node.right, min_ref, max_ref,
                        max_size_ref, is_bst_ref)
    if is_bst_ref[0] == 1 and node.data < min_ref[0]:
        right_flag = True

    # Update min and max values for the
    # parent recursive calls
    if Min < min_ref[0]:
        min_ref[0] = Min
    if node.data < min_ref[0]: # For leaf nodes
        min_ref[0] = node.data
    if node.data > max_ref[0]:
        max_ref[0] = node.data

    # If both left and right subtrees are BST.
    # And left and right subtree properties hold
    # for this node, then this tree is BST.
    # So return the size of this tree
    if left_flag and right_flag:
        if ls + rs + 1 > max_size_ref[0]:
            max_size_ref[0] = ls + rs + 1
        return ls + rs + 1
    else:

        # Since this subtree is not BST, set is_bst
        # flag for parent calls is_bst_ref[0] = 0;
        return 0

# Driver Code
if __name__ == '__main__':

    # Let us construct the following Tree
    #     50
    # /     \
    # 10     60
    # / \     / \
    # 5 20 55 70
    #         /     / \
    #     45     65 80
    root = newNode(50)
    root.left     = newNode(10)
    root.right     = newNode(60)
    root.left.left = newNode(5)
    root.left.right = newNode(20)
    root.right.left = newNode(55)
    root.right.left.left = newNode(45)
    root.right.right = newNode(70)
    root.right.right.left = newNode(65)
    root.right.right.right = newNode(80)

# The complete tree is not BST as 45 is in
# right subtree of 50\. The following subtree
# is the largest BST
#     60
# / \
# 55     70
# /     / \
# 45     65 80

print("Size of the largest BST is",
                  largestBST(root))

# This code is contributed by PranchalK
```

## C#

```
using System;

// C# program to find largest BST subtree in given Binary Tree

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

public class Value
{

    public int max_size = 0; // for size of largest BST
    public bool is_bst = false;
    public int min = int.MaxValue; // For minimum value in right subtree
    public int max = int.MinValue; // For maximum value in left subtree

}

public class BinaryTree
{

    public static Node root;
    public Value val = new Value();

    /* Returns size of the largest BST subtree in a Binary Tree
     (efficient version). */
    public virtual int largestBST(Node node)
    {

        largestBSTUtil(node, val, val, val, val);

        return val.max_size;
    }

    /* largestBSTUtil() updates *max_size_ref for the size of the largest BST
     subtree.   Also, if the tree rooted with node is non-empty and a BST,
     then returns size of the tree. Otherwise returns 0.*/
    public virtual int largestBSTUtil(Node node, Value min_ref, Value max_ref, Value max_size_ref, Value is_bst_ref)
    {

        /* Base Case */
        if (node == null)
        {
            is_bst_ref.is_bst = true; // An empty tree is BST
            return 0; // Size of the BST is 0
        }

        int min = int.MaxValue;

        /* A flag variable for left subtree property
         i.e., max(root->left) < root->data */
        bool left_flag = false;

        /* A flag variable for right subtree property
         i.e., min(root->right) > root->data */
        bool right_flag = false;

        int ls, rs; // To store sizes of left and right subtrees

        /* Following tasks are done by recursive call for left subtree
         a) Get the maximum value in left subtree (Stored in *max_ref)
         b) Check whether Left Subtree is BST or not (Stored in *is_bst_ref)
         c) Get the size of maximum size BST in left subtree (updates *max_size) */
        max_ref.max = int.MinValue;
        ls = largestBSTUtil(node.left, min_ref, max_ref, max_size_ref, is_bst_ref);
        if (is_bst_ref.is_bst == true && node.data > max_ref.max)
        {
            left_flag = true;
        }

        /* Before updating *min_ref, store the min value in left subtree. So that we
         have the correct minimum value for this subtree */
        min = min_ref.min;

        /* The following recursive call does similar (similar to left subtree) 
         task for right subtree */
        min_ref.min = int.MaxValue;
        rs = largestBSTUtil(node.right, min_ref, max_ref, max_size_ref, is_bst_ref);
        if (is_bst_ref.is_bst == true && node.data < min_ref.min)
        {
            right_flag = true;
        }

        // Update min and max values for the parent recursive calls
        if (min < min_ref.min)
        {
            min_ref.min = min;
        }
        if (node.data < min_ref.min) // For leaf nodes
        {
            min_ref.min = node.data;
        }
        if (node.data > max_ref.max)
        {
            max_ref.max = node.data;
        }

        /* If both left and right subtrees are BST. And left and right
         subtree properties hold for this node, then this tree is BST.
         So return the size of this tree */
        if (left_flag && right_flag)
        {
            if (ls + rs + 1 > max_size_ref.max_size)
            {
                max_size_ref.max_size = ls + rs + 1;
            }
            return ls + rs + 1;
        }
        else
        {
            //Since this subtree is not BST, set is_bst flag for parent calls
            is_bst_ref.is_bst = false;
            return 0;
        }
    }

    public static void Main(string[] args)
    {
        /* Let us construct the following Tree
                50
             /      \
            10        60
           /  \       /  \
          5   20    55    70
         /     /  \
        45   65    80
         */

        BinaryTree tree = new BinaryTree();
        BinaryTree.root = new Node(50);
        BinaryTree.root.left = new Node(10);
        BinaryTree.root.right = new Node(60);
        BinaryTree.root.left.left = new Node(5);
        BinaryTree.root.left.right = new Node(20);
        BinaryTree.root.right.left = new Node(55);
        BinaryTree.root.right.left.left = new Node(45);
        BinaryTree.root.right.right = new Node(70);
        BinaryTree.root.right.right.left = new Node(65);
        BinaryTree.root.right.right.right = new Node(80);

        /* The complete tree is not BST as 45 is in right subtree of 50.
         The following subtree is the largest BST
             60
            /  \
          55    70
          /     /  \
        45     65   80
        */
        Console.WriteLine("Size of largest BST is " + tree.largestBST(root));
    }
}

  // This code is contributed by Shrikant13
```

## java 描述语言

```
<script>

// JavaScript program to find largest
// BST subtree in given Binary Tree

class Node {
        constructor(val) {
            this.data = val;
            this.left = null;
            this.right = null;
        }
    }

class Value {
constructor(){
    this.max_size = 0; // for size of largest BST
    this.is_bst = false;
    // For minimum value in right subtree
    this.min = Number.MAX_VALUE;
    // For maximum value in left subtree
    this.max = Number.MIN_VALUE; 
}
}

    var root;
    var val = new Value();

    /* Returns size of the largest
    BST subtree in a Binary Tree
     (efficient version). */
    function largestBST(node) {

        largestBSTUtil(node, val, val, val, val);

        return val.max_size;
    }

    /* largestBSTUtil() updates *max_size_ref
    for the size of the largest BST
     subtree.   Also, if the tree rooted with
     node is non-empty and a BST,
     then returns size of the tree. Otherwise returns 0.*/
    function largestBSTUtil(node,  min_ref,  max_ref,
             max_size_ref,  is_bst_ref) {

        /* Base Case */
        if (node == null)
        {
        // An empty tree is BST
            is_bst_ref.is_bst = true;
            return 0;    // Size of the BST is 0
        }

        var min = Number.MAX_VALUE;

        /* A flag variable for left subtree property
         i.e., max(root->left) < root->data */
        var left_flag = false;

        /* A flag variable for right subtree property
         i.e., min(root->right) > root->data */
        var right_flag = false;

        // To store sizes of left and right subtrees
        var ls, rs;

        /* Following tasks are done by
        recursive call for left subtree
         a) Get the maximum value in left
         subtree (Stored in *max_ref)
         b) Check whether Left Subtree is
         BST or not (Stored in *is_bst_ref)
         c) Get the size of maximum size BST
         in left subtree (updates *max_size) */
        max_ref.max = Number.MIN_VALUE;
        ls = largestBSTUtil(node.left, min_ref,
        max_ref, max_size_ref, is_bst_ref);
        if (is_bst_ref.is_bst ==
        true && node.data > max_ref.max)
        {
            left_flag = true;
        }

        /* Before updating *min_ref, store the min
        value in left subtree. So that we
         have the correct minimum value for this subtree */
        min = min_ref.min;

        /* The following recursive call does
        similar (similar to left subtree)
         task for right subtree */
        min_ref.min = Number.MAX_VALUE;
        rs = largestBSTUtil(node.right, min_ref,
        max_ref, max_size_ref, is_bst_ref);
        if (is_bst_ref.is_bst == true &&
        node.data < min_ref.min)
        {
            right_flag = true;
        }

        // Update min and max values for
        // the parent recursive calls
        if (min < min_ref.min) {
            min_ref.min = min;
        }
        if (node.data < min_ref.min) // For leaf nodes
        {
            min_ref.min = node.data;
        }
        if (node.data > max_ref.max) {
            max_ref.max = node.data;
        }

        /* If both left and right subtrees
         are BST. And left and right
         subtree properties hold for
         this node, then this tree is BST.
         So return the size of this tree */
        if (left_flag && right_flag) {
            if (ls + rs + 1 > max_size_ref.max_size)
            {
                max_size_ref.max_size = ls + rs + 1;
            }
            return ls + rs + 1;
        } else {
            // Since this subtree is not BST,
            // set is_bst flag for parent calls
            is_bst_ref.is_bst = false;
            return 0;
        }
    }

        /* Let us construct the following Tree
                50
             /      \
            10        60
           /  \       /  \
          5   20    55    70
         /     /  \
        45   65    80
         */

        root = new Node(50);
        root.left = new Node(10);
        root.right = new Node(60);
        root.left.left = new Node(5);
        root.left.right = new Node(20);
        root.right.left = new Node(55);
        root.right.left.left = new Node(45);
        root.right.right = new Node(70);
        root.right.right.left = new Node(65);
        root.right.right.right = new Node(80);

        /* The complete tree is not BST
        as 45 is in right subtree of 50.
         The following subtree is the largest BST
             60
            /  \
          55    70
          /     /  \
        45     65   80
        */
        document.write("Size of largest BST is " +
        largestBST(root));

// This code contributed by gauravrajput1

</script>
```

**输出:**

```
Size of largest BST is 6
```

**时间复杂度:** O(n)，其中 n 是给定二叉树中的节点数。
[**二叉树中最大的 BST |第二集**](https://www.geeksforgeeks.org/largest-bst-binary-tree-set-2/)
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。