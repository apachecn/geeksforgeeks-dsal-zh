# 检查二叉树覆盖和未覆盖节点的和

> 原文:[https://www . geesforgeks . org/check-sum-covered-uncovered-nodes-二叉树/](https://www.geeksforgeeks.org/check-sum-covered-uncovered-nodes-binary-tree/)

给定一个二叉树，你需要检查所有覆盖元素的和是否等于所有未覆盖元素的和。
在二叉树中，如果一个节点出现在左边界或右边界，则称其为未覆盖。其余的节点称为覆盖节点。

例如，考虑下面的二叉树

```
In above binary tree,
Covered node:     6, 5, 7
Uncovered node:   9, 4, 3, 17, 22, 20

The output for this tree should be false as 
sum of covered and uncovered node is not same
```

**我们强烈建议你尽量减少浏览器，先自己试试这个。**
为了计算未覆盖节点的总和，我们将遵循以下步骤:
1)从根开始，向左并继续前进，直到左子节点可用，如果没有，则向右子节点并再次遵循相同的过程，直到到达叶节点。

2)在步骤 1 之后，将存储左侧边界的总和，现在对右侧部分再次执行相同的过程，但是现在继续向右，直到右子节点可用，如果没有，则向左子节点，并遵循相同的过程，直到到达叶节点。
经过以上 2 步，所有未覆盖节点的和将被存储，我们可以从总和中减去它，得到覆盖元素的和，并检查二叉树的分点。

## C++

```
// C++ program to find sum of Covered and Uncovered node of
// binary tree
#include <bits/stdc++.h>
using namespace std;

/* A binary tree node has key, pointer to left
   child and a pointer to right child */
struct Node
{
    int key;
    struct Node* left, *right;
};

/* To create a newNode of tree and return pointer */
struct Node* newNode(int key)
{
    Node* temp = new Node;
    temp->key = key;
    temp->left = temp->right = NULL;
    return (temp);
}

/* Utility function to calculate sum of all node of tree */
int sum(Node* t)
{
    if (t == NULL)
        return 0;
    return t->key + sum(t->left) + sum(t->right);
}

/* Recursive function to calculate sum of left boundary
   elements  */
int uncoveredSumLeft(Node* t)
{
    /*  If leaf node, then just return its key value   */
    if (t->left == NULL && t->right == NULL)
        return t->key;

    /*  If left is available then go left otherwise go right  */
    if (t->left != NULL)
        return t->key + uncoveredSumLeft(t->left);
    else
        return t->key + uncoveredSumLeft(t->right);
}

/* Recursive function to calculate sum of right boundary
   elements  */
int uncoveredSumRight(Node* t)
{
    /*  If leaf node, then just return its key value   */
    if (t->left == NULL && t->right == NULL)
        return t->key;

    /*  If right is available then go right otherwise go left  */
    if (t->right != NULL)
        return t->key + uncoveredSumRight(t->right);
    else
        return t->key + uncoveredSumRight(t->left);
}

// Returns sum of uncovered elements
int uncoverSum(Node* t)
{
    /* Initializing with 0 in case we don't have
       left or right boundary  */
    int lb = 0, rb = 0;

    if (t->left != NULL)
        lb = uncoveredSumLeft(t->left);
    if (t->right != NULL)
        rb = uncoveredSumRight(t->right);

    /* returning sum of root node, left boundary
       and right boundary*/
    return t->key + lb + rb;
}

// Returns true if sum of covered and uncovered elements
// is same.
bool isSumSame(Node *root)
{
    // Sum of uncovered elements
    int sumUC = uncoverSum(root);

    // Sum of all elements
    int sumT = sum(root);

    // Check if sum of covered and uncovered is same
    return (sumUC == (sumT - sumUC));
}

/* Helper function to print inorder traversal of
   binary tree   */
void inorder(Node* root)
{
    if (root)
    {
        inorder(root->left);
        printf("%d ", root->key);
        inorder(root->right);
    }
}

// Driver program to test above functions
int main()
{
    // Making above given diagram's binary tree
    Node* root = newNode(8);
    root->left = newNode(3);

    root->left->left = newNode(1);
    root->left->right = newNode(6);
    root->left->right->left = newNode(4);
    root->left->right->right = newNode(7);

    root->right = newNode(10);
    root->right->right = newNode(14);
    root->right->right->left = newNode(13);

    if (isSumSame(root))
        printf("Sum of covered and uncovered is same\n");
    else
        printf("Sum of covered and uncovered is not same\n");
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find sum of covered and uncovered nodes
// of a binary tree

/* A binary tree node has key, pointer to left child and
   a pointer to right child */
class Node
{
    int key;
    Node left, right;

    public Node(int key)
    {
        this.key = key;
        left = right = null;
    }
}

class BinaryTree
{
    Node root;

    /* Utility function to calculate sum of all node of tree */
    int sum(Node t)
    {
        if (t == null)
            return 0;
        return t.key + sum(t.left) + sum(t.right);
    }

    /* Recursive function to calculate sum of left boundary
       elements  */
    int uncoveredSumLeft(Node t)
    {
        /*  If left node, then just return its key value   */
        if (t.left == null && t.right == null)
            return t.key;

        /*  If left is available then go left otherwise go right  */
        if (t.left != null)
            return t.key + uncoveredSumLeft(t.left);
         else
            return t.key + uncoveredSumLeft(t.right);
    }

    /* Recursive function to calculate sum of right boundary
       elements  */
    int uncoveredSumRight(Node t)
    {
        /*  If left node, then just return its key value   */
        if (t.left == null && t.right == null)
            return t.key;

        /*  If right is available then go right otherwise go left  */
        if (t.right != null)
            return t.key + uncoveredSumRight(t.right);
        else
            return t.key + uncoveredSumRight(t.left);
    }

    // Returns sum of uncovered elements
    int uncoverSum(Node t)
    {
        /* Initializing with 0 in case we don't have
           left or right boundary  */
        int lb = 0, rb = 0;

        if (t.left != null)
            lb = uncoveredSumLeft(t.left);
        if (t.right != null)
            rb = uncoveredSumRight(t.right);

        /* returning sum of root node, left boundary
           and right boundary*/
        return t.key + lb + rb;
    }

    // Returns true if sum of covered and uncovered elements
    // is same.
    boolean isSumSame(Node root)
    {
        // Sum of uncovered elements
        int sumUC = uncoverSum(root);

        // Sum of all elements
        int sumT = sum(root);

        // Check if sum of covered and uncovered is same
        return (sumUC == (sumT - sumUC));
    }

    /* Helper function to print inorder traversal of
       binary tree   */
    void inorder(Node root)
    {
        if (root != null)
        {
            inorder(root.left);
            System.out.print(root.key + " ");
            inorder(root.right);
        }
    }

    // Driver program to test above functions
    public static void main(String[] args)
    {

        BinaryTree tree = new BinaryTree();

        // Making above given diagram's binary tree
        tree.root = new Node(8);
        tree.root.left = new Node(3);
        tree.root.left.left = new Node(1);
        tree.root.left.right = new Node(6);
        tree.root.left.right.left = new Node(4);
        tree.root.left.right.right = new Node(7);

        tree.root.right = new Node(10);
        tree.root.right.right = new Node(14);
        tree.root.right.right.left = new Node(13);

        if (tree.isSumSame(tree.root))
            System.out.println("Sum of covered and uncovered is same");
         else
            System.out.println("Sum of covered and uncovered is not same");
    }
}

// This code has been contributed by Mayank Jaiswal(mayank_24)
```

## 蟒蛇 3

```
# Python3 program to find sum of Covered and
# Uncovered node of binary tree

# To create a newNode of tree and return pointer
class newNode:
    def __init__(self, key):
        self.key = key
        self.left = self.right = None

# Utility function to calculate sum
# of all node of tree
def Sum(t):
    if (t == None):
        return 0
    return t.key + Sum(t.left) + Sum(t.right)

# Recursive function to calculate sum
# of left boundary elements
def uncoveredSumLeft(t):

    # If leaf node, then just return
    # its key value
    if (t.left == None and t.right == None):
        return t.key

    # If left is available then go
    # left otherwise go right
    if (t.left != None):
        return t.key + uncoveredSumLeft(t.left)
    else:
        return t.key + uncoveredSumLeft(t.right)

# Recursive function to calculate sum of
# right boundary elements
def uncoveredSumRight(t):

    # If leaf node, then just return
    # its key value
    if (t.left == None and t.right == None):
        return t.key

    # If right is available then go right
    # otherwise go left
    if (t.right != None):
        return t.key + uncoveredSumRight(t.right)
    else:
        return t.key + uncoveredSumRight(t.left)

# Returns sum of uncovered elements
def uncoverSum(t):

    # Initializing with 0 in case we
    # don't have left or right boundary
    lb = 0
    rb = 0

    if (t.left != None):
        lb = uncoveredSumLeft(t.left)
    if (t.right != None):
        rb = uncoveredSumRight(t.right)

    # returning sum of root node,
    # left boundary and right boundary
    return t.key + lb + rb

# Returns true if sum of covered and
# uncovered elements is same.
def isSumSame(root):

    # Sum of uncovered elements
    sumUC = uncoverSum(root)

    # Sum of all elements
    sumT = Sum(root)

    # Check if sum of covered and
    # uncovered is same
    return (sumUC == (sumT - sumUC))

# Helper function to prinorder
# traversal of binary tree
def inorder(root):
    if (root):
        inorder(root.left)
        print(root.key, end = " ")
        inorder(root.right)

# Driver Code
if __name__ == '__main__':

    # Making above given diagram's
    # binary tree
    root = newNode(8)
    root.left = newNode(3)

    root.left.left = newNode(1)
    root.left.right = newNode(6)
    root.left.right.left = newNode(4)
    root.left.right.right = newNode(7)

    root.right = newNode(10)
    root.right.right = newNode(14)
    root.right.right.left = newNode(13)

    if (isSumSame(root)):
        print("Sum of covered and uncovered is same")
    else:
        print("Sum of covered and uncovered is not same")

# This code is contributed by PranchalK
```

## C#

```
// C# program to find sum of covered
// and uncovered nodes of a binary tree
using System;

/* A binary tree node has key, pointer
to left child and a pointer to right child */
public class Node
{
    public int key;
    public Node left, right;

    public Node(int key)
    {
        this.key = key;
        left = right = null;
    }
}

class GFG
{
public Node root;

/* Utility function to calculate
sum of all node of tree */
public virtual int sum(Node t)
{
    if (t == null)
    {
        return 0;
    }
    return t.key + sum(t.left) +
                   sum(t.right);
}

/* Recursive function to calculate
sum of left boundary elements */
public virtual int uncoveredSumLeft(Node t)
{
    /* If left node, then just return
       its key value */
    if (t.left == null && t.right == null)
    {
        return t.key;
    }

    /* If left is available then go
       left otherwise go right */
    if (t.left != null)
    {
        return t.key + uncoveredSumLeft(t.left);
    }
    else
    {
        return t.key + uncoveredSumLeft(t.right);
    }
}

/* Recursive function to calculate
   sum of right boundary elements */
public virtual int uncoveredSumRight(Node t)
{
    /* If left node, then just return
       its key value */
    if (t.left == null && t.right == null)
    {
        return t.key;
    }

    /* If right is available then go
       right otherwise go left */
    if (t.right != null)
    {
        return t.key + uncoveredSumRight(t.right);
    }
    else
    {
        return t.key + uncoveredSumRight(t.left);
    }
}

// Returns sum of uncovered elements
public virtual int uncoverSum(Node t)
{
    /* Initializing with 0 in case we
    don't have left or right boundary */
    int lb = 0, rb = 0;

    if (t.left != null)
    {
        lb = uncoveredSumLeft(t.left);
    }
    if (t.right != null)
    {
        rb = uncoveredSumRight(t.right);
    }

    /* returning sum of root node,
    left boundary and right boundary*/
    return t.key + lb + rb;
}

// Returns true if sum of covered
// and uncovered elements is same.
public virtual bool isSumSame(Node root)
{
    // Sum of uncovered elements
    int sumUC = uncoverSum(root);

    // Sum of all elements
    int sumT = sum(root);

    // Check if sum of covered and
    // uncovered is same
    return (sumUC == (sumT - sumUC));
}

/* Helper function to print inorder
traversal of binary tree */
public virtual void inorder(Node root)
{
    if (root != null)
    {
        inorder(root.left);
        Console.Write(root.key + " ");
        inorder(root.right);
    }
}

// Driver Code
public static void Main(string[] args)
{

    GFG tree = new GFG();

    // Making above given diagram's binary tree
    tree.root = new Node(8);
    tree.root.left = new Node(3);
    tree.root.left.left = new Node(1);
    tree.root.left.right = new Node(6);
    tree.root.left.right.left = new Node(4);
    tree.root.left.right.right = new Node(7);

    tree.root.right = new Node(10);
    tree.root.right.right = new Node(14);
    tree.root.right.right.left = new Node(13);

    if (tree.isSumSame(tree.root))
    {
        Console.WriteLine("Sum of covered and " +
                            "uncovered is same");
    }
    else
    {
        Console.WriteLine("Sum of covered and " +
                        "uncovered is not same");
    }
}
}

// This code is contributed by Shrikant13
```

## java 描述语言

```
<script>

// Javascript program to find sum of covered
// and uncovered nodes of a binary tree

/* A binary tree node has key, pointer
to left child and a pointer to right child */
class Node
{
    constructor(key)
    {
        this.key = key;
        this.left= null;
        this.right = null;
    }
}

var root = null;

/* Utility function to calculate
sum of all node of tree */
function sum(t)
{
    if (t == null)
    {
        return 0;
    }
    return t.key + sum(t.left) +
                   sum(t.right);
}

/* Recursive function to calculate
sum of left boundary elements */
function uncoveredSumLeft(t)
{

    /* If left node, then just return
       its key value */
    if (t.left == null && t.right == null)
    {
        return t.key;
    }

    /* If left is available then go
       left otherwise go right */
    if (t.left != null)
    {
        return t.key + uncoveredSumLeft(t.left);
    }
    else
    {
        return t.key + uncoveredSumLeft(t.right);
    }
}

/* Recursive function to calculate
   sum of right boundary elements */
function uncoveredSumRight(t)
{

    /* If left node, then just return
       its key value */
    if (t.left == null && t.right == null)
    {
        return t.key;
    }

    /* If right is available then go
       right otherwise go left */
    if (t.right != null)
    {
        return t.key + uncoveredSumRight(t.right);
    }
    else
    {
        return t.key + uncoveredSumRight(t.left);
    }
}

// Returns sum of uncovered elements
function uncoverSum(t)
{

    /* Initializing with 0 in case we
    don't have left or right boundary */
    var lb = 0, rb = 0;

    if (t.left != null)
    {
        lb = uncoveredSumLeft(t.left);
    }
    if (t.right != null)
    {
        rb = uncoveredSumRight(t.right);
    }

    /* returning sum of root node,
    left boundary and right boundary*/
    return t.key + lb + rb;
}

// Returns true if sum of covered
// and uncovered elements is same.
function isSumSame(root)
{

    // Sum of uncovered elements
    var sumUC = uncoverSum(root);

    // Sum of all elements
    var sumT = sum(root);

    // Check if sum of covered and
    // uncovered is same
    return (sumUC == (sumT - sumUC));
}

/* Helper function to print inorder
traversal of binary tree */
function inorder(root)
{
    if (root != null)
    {
        inorder(root.left);
        document.write(root.key + " ");
        inorder(root.right);
    }
}

// Driver Code
// Making above given diagram's binary tree
var root = new Node(8);
root.left = new Node(3);
root.left.left = new Node(1);
root.left.right = new Node(6);
root.left.right.left = new Node(4);
root.left.right.right = new Node(7);
root.right = new Node(10);
root.right.right = new Node(14);
root.right.right.left = new Node(13);
if (isSumSame(root))
{
    document.write("Sum of covered and " +
                        "uncovered is same");
}
else
{
    document.write("Sum of covered and " +
                    "uncovered is not same");
}

// This code is contributed by itsok

</script>
```

**输出:**

```
Sum of covered and uncovered is not same

```

本文由乌卡什·特里维迪供稿。如果您发现任何不正确的地方，或者您想分享更多关于上面讨论的主题的信息，请写评论