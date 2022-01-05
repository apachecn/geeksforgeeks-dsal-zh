# 在给定的二叉树中找到最大的完全子树

> 原文:[https://www . geesforgeks . org/find-给定二叉树中最大的完整子树/](https://www.geeksforgeeks.org/find-the-largest-complete-subtree-in-a-given-binary-tree/)

给定一棵二叉树，任务是找到给定二叉树中最大的完全子树的大小。
**完整二叉树–**如果除了可能的最后一级之外所有级别都已完全填充，并且最后一级尽可能保留所有键，则二叉树为[完整二叉树](https://www.geeksforgeeks.org/binary-tree-set-3-types-of-binary-tree/)。

**注:**所有[完美二叉树](https://www.geeksforgeeks.org/binary-tree-set-3-types-of-binary-tree/)都是完整二叉树，但在**中相反**不成立。如果一棵树不完整，那么它也不是完美二叉树。

**示例:**

```
Input: 
              1
           /     \
          2        3
        /   \     /  \
       4      5   6   7  
     /  \    /        
    8   9   10      
Output:
Size : 10
Inorder Traversal : 8 4 9 2 10 5 1 6 3 7
The given tree a complete binary tree.

Input:
         50
      /      \
   30         60
  /   \      /    \ 
 5    20   45      70
          / 
         10
Output:
Size : 4
Inorder Traversal : 10 45 60 70
```

**方法:**简单地以自下而上的方式遍历树。然后，在从子树到父树的递归中，我们可以将关于子树的信息传递给父树。传递的信息只能由父节点在恒定的时间内进行完整树测试(对于父节点)。左右子树都需要告诉父树它们是否完美，是否完整，还需要返回到目前为止找到的完整二叉树的最大大小。

为了找到最大的完整子树，子树需要将以下信息传递到树上，这样我们就可以将最大大小与父树的数据进行比较，以检查完整二叉树属性。

1.  有一个布尔变量来检查左子树或右子树是否完美和完整。
2.  通过递归中的左右子调用，我们通过以下三种情况来确定父子树是否完整:
    *   如果左子树是完美的，右子树是完整的，并且高度也相同，那么子树根也是完整的二叉子树，其大小等于左子树和右子树之和加 1(对于当前根)。
    *   如果左子树是完整的，右子树是完美的，并且左的高度比右的高度大 1，那么子树根就是完整的二叉子树，其大小等于左、右子树之和加 1(对于当前根)。而根子树不可能是完美的二叉子树，因为在这种情况下它的左子树并不完美。
    *   否则这个子树不可能是一个完整的二叉树，只是返回到目前为止在左或右子树中找到的最大的完整子树。如果树不完整，那么它也不完美。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Node structure of the tree
struct node {
    int data;
    struct node* left;
    struct node* right;
};

// To create a new node
struct node* newNode(int data)
{
    struct node* node = (struct node*)malloc(sizeof(struct node));
    node->data = data;
    node->left = NULL;
    node->right = NULL;
    return node;
};

// Structure for return type of
// function findPerfectBinaryTree
struct returnType {

    // To store if sub-tree is perfect or not
    bool isPerfect;

    // To store if sub-tree is complete or not
    bool isComplete;

    // size of the tree
    int size;

    // Root of biggest complete sub-tree
    node* rootTree;
};

// helper function that returns height
// of the tree given size
int getHeight(int size)
{
    return ceil(log2(size + 1));
}

// Function to return the biggest
// complete binary sub-tree
returnType findCompleteBinaryTree(struct node* root)
{

    // Declaring returnType that
    // needs to be returned
    returnType rt;

    // If root is NULL then it is considered as both
    // perfect and complete binary tree of size 0
    if (root == NULL) {
        rt.isPerfect = true;
        rt.isComplete = true;
        rt.size = 0;
        rt.rootTree = NULL;
        return rt;
    }

    // Recursive call for left and right child
    returnType lv = findCompleteBinaryTree(root->left);
    returnType rv = findCompleteBinaryTree(root->right);

    // CASE - A
    // If left sub-tree is perfect and right is complete and
    // there height is also same then sub-tree root
    // is also complete binary sub-tree with size equal to
    // sum of left and right subtrees plus one for current root
    if (lv.isPerfect == true && rv.isComplete == true
        && getHeight(lv.size) == getHeight(rv.size)) {
        rt.isComplete = true;

        // If right sub-tree is perfect then
        // root is also perfect
        rt.isPerfect = (rv.isPerfect ? true : false);
        rt.size = lv.size + rv.size + 1;
        rt.rootTree = root;
        return rt;
    }

    // CASE - B
    // If left sub-tree is complete and right is perfect and the
    // height of left is greater than right by one then sub-tree root
    // is complete binary sub-tree with size equal to
    // sum of left and right subtrees plus one for current root.
    // But sub-tree cannot be perfect binary sub-tree.
    if (lv.isComplete == true && rv.isPerfect == true
        && getHeight(lv.size) == getHeight(rv.size) + 1) {
        rt.isComplete = true;
        rt.isPerfect = false;
        rt.size = lv.size + rv.size + 1;
        rt.rootTree = root;
        return rt;
    }

    // CASE - C
    // Else this sub-tree cannot be a complete binary tree
    // and simply return the biggest sized complete sub-tree
    // found till now in the left or right sub-trees
    rt.isPerfect = false;
    rt.isComplete = false;
    rt.size = max(lv.size, rv.size);
    rt.rootTree = (lv.size > rv.size ? lv.rootTree : rv.rootTree);
    return rt;
}

// Function to print the inorder traversal of the tree
void inorderPrint(node* root)
{
    if (root != NULL) {
        inorderPrint(root->left);
        cout << root->data << " ";
        inorderPrint(root->right);
    }
}

// Driver code
int main()
{
    // Create the tree
    struct node* root = newNode(50);
    root->left = newNode(30);
    root->right = newNode(60);
    root->left->left = newNode(5);
    root->left->right = newNode(20);
    root->right->left = newNode(45);
    root->right->right = newNode(70);
    root->right->left->left = newNode(10);

    // Get the biggest sized complete binary sub-tree
    struct returnType ans = findCompleteBinaryTree(root);

    cout << "Size : " << ans.size << endl;

    // Print the inorder traversal of the found sub-tree
    cout << "Inorder Traversal : ";
    inorderPrint(ans.rootTree);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class Sol
{

// Node structure of the tree
static class node
{
    int data;
    node left;
    node right;
};

// To create a new node
static node newNode(int data)
{
    node node = new node();
    node.data = data;
    node.left = null;
    node.right = null;
    return node;
};

// Structure for return type of
// function findPerfectBinaryTree
static class returnType
{

    // To store if sub-tree is perfect or not
    boolean isPerfect;

    // To store if sub-tree is complete or not
    boolean isComplete;

    // size of the tree
    int size;

    // Root of biggest complete sub-tree
    node rootTree;
};

// helper function that returns height
// of the tree given size
static int getHeight(int size)
{
    return (int)Math.ceil(Math.log(size + 1)/Math.log(2));
}

// Function to return the biggest
// complete binary sub-tree
static returnType findCompleteBinaryTree(node root)
{

    // Declaring returnType that
    // needs to be returned
    returnType rt=new returnType();

    // If root is null then it is considered as both
    // perfect and complete binary tree of size 0
    if (root == null)
    {
        rt.isPerfect = true;
        rt.isComplete = true;
        rt.size = 0;
        rt.rootTree = null;
        return rt;
    }

    // Recursive call for left and right child
    returnType lv = findCompleteBinaryTree(root.left);
    returnType rv = findCompleteBinaryTree(root.right);

    // CASE - A
    // If left sub-tree is perfect and right is complete and
    // there height is also same then sub-tree root
    // is also complete binary sub-tree with size equal to
    // sum of left and right subtrees plus one for current root
    if (lv.isPerfect == true && rv.isComplete == true
        && getHeight(lv.size) == getHeight(rv.size))
    {
        rt.isComplete = true;

        // If right sub-tree is perfect then
        // root is also perfect
        rt.isPerfect = (rv.isPerfect ? true : false);
        rt.size = lv.size + rv.size + 1;
        rt.rootTree = root;
        return rt;
    }

    // CASE - B
    // If left sub-tree is complete and right is perfect and the
    // height of left is greater than right by one then sub-tree root
    // is complete binary sub-tree with size equal to
    // sum of left and right subtrees plus one for current root.
    // But sub-tree cannot be perfect binary sub-tree.
    if (lv.isComplete == true && rv.isPerfect == true
        && getHeight(lv.size) == getHeight(rv.size) + 1)
    {
        rt.isComplete = true;
        rt.isPerfect = false;
        rt.size = lv.size + rv.size + 1;
        rt.rootTree = root;
        return rt;
    }

    // CASE - C
    // Else this sub-tree cannot be a complete binary tree
    // and simply return the biggest sized complete sub-tree
    // found till now in the left or right sub-trees
    rt.isPerfect = false;
    rt.isComplete = false;
    rt.size = Math.max(lv.size, rv.size);
    rt.rootTree = (lv.size > rv.size ? lv.rootTree : rv.rootTree);
    return rt;
}

// Function to print the inorder traversal of the tree
static void inorderPrint(node root)
{
    if (root != null)
    {
        inorderPrint(root.left);
        System.out.print( root.data + " ");
        inorderPrint(root.right);
    }
}

// Driver code
public static void main(String args[])
{
    // Create the tree
    node root = newNode(50);
    root.left = newNode(30);
    root.right = newNode(60);
    root.left.left = newNode(5);
    root.left.right = newNode(20);
    root.right.left = newNode(45);
    root.right.right = newNode(70);
    root.right.left.left = newNode(10);

    // Get the biggest sized complete binary sub-tree
    returnType ans = findCompleteBinaryTree(root);

    System.out.println( "Size : " + ans.size );

    // Print the inorder traversal of the found sub-tree
    System.out.print("Inorder Traversal : ");
    inorderPrint(ans.rootTree);

}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 implementation of the approach
import math

# Node structure of the tree
class node :
    def __init__(self):
        self.data = 0
        self.left = None
        self.right = None

# To create anode
def newNode(data):

    node_ = node()
    node_.data = data
    node_.left = None
    node_.right = None
    return node_

# Structure for return type of
# function findPerfectBinaryTree
class returnType :

    def __init__(self):

        # To store if sub-tree is perfect or not
        self.isPerfect = None

        # To store if sub-tree is complete or not
        self.isComplete = None

        # size of the tree
        self.size = 0

        # Root of biggest complete sub-tree
        self.rootTree = None

# helper function that returns height
# of the tree given size
def getHeight(size):

    return int(math.ceil(math.log(size + 1)/math.log(2)))

# Function to return the biggest
# complete binary sub-tree
def findCompleteBinaryTree(root) :

    # Declaring returnType that
    # needs to be returned
    rt = returnType()

    # If root is None then it is considered as both
    # perfect and complete binary tree of size 0
    if (root == None):

        rt.isPerfect = True
        rt.isComplete = True
        rt.size = 0
        rt.rootTree = None
        return rt

    # Recursive call for left and right child
    lv = findCompleteBinaryTree(root.left)
    rv = findCompleteBinaryTree(root.right)

    # CASE - A
    # If left sub-tree is perfect and right is complete and
    # there height is also same then sub-tree root
    # is also complete binary sub-tree with size equal to
    # sum of left and right subtrees plus one for current root
    if (lv.isPerfect == True and rv.isComplete == True
        and getHeight(lv.size) == getHeight(rv.size)) :

        rt.isComplete = True

        # If right sub-tree is perfect then
        # root is also perfect
        rt.isPerfect = rv.isPerfect
        rt.size = lv.size + rv.size + 1
        rt.rootTree = root
        return rt

    # CASE - B
    # If left sub-tree is complete and right is perfect and the
    # height of left is greater than right by one then sub-tree root
    # is complete binary sub-tree with size equal to
    # sum of left and right subtrees plus one for current root.
    # But sub-tree cannot be perfect binary sub-tree.
    if (lv.isComplete == True and rv.isPerfect == True
        and getHeight(lv.size) == getHeight(rv.size) + 1):

        rt.isComplete = True
        rt.isPerfect = False
        rt.size = lv.size + rv.size + 1
        rt.rootTree = root
        return rt

    # CASE - C
    # Else this sub-tree cannot be a complete binary tree
    # and simply return the biggest sized complete sub-tree
    # found till now in the left or right sub-trees
    rt.isPerfect = False
    rt.isComplete = False
    rt.size =max(lv.size, rv.size)
    if(lv.size > rv.size ):
        rt.rootTree = lv.rootTree
    else:
        rt.rootTree = rv.rootTree
    return rt

# Function to print the inorder traversal of the tree
def inorderPrint(root) :

    if (root != None) :

        inorderPrint(root.left)
        print( root.data ,end= " ")
        inorderPrint(root.right)

# Driver code

# Create the tree
root = newNode(50)
root.left = newNode(30)
root.right = newNode(60)
root.left.left = newNode(5)
root.left.right = newNode(20)
root.right.left = newNode(45)
root.right.right = newNode(70)
root.right.left.left = newNode(10)

# Get the biggest sized complete binary sub-tree
ans = findCompleteBinaryTree(root)

print( "Size : " , ans.size )

# Print the inorder traversal of the found sub-tree
print("Inorder Traversal : ")
inorderPrint(ans.rootTree)

# This code is contributed by Arnab Kundu
```

## C#

```
// C# implementation of the above approach:
using System;

class GFG
{

// Node structure of the tree
public class node
{
    public int data;
    public node left;
    public node right;
};

// To create a new node
static node newNode(int data)
{
    node node = new node();
    node.data = data;
    node.left = null;
    node.right = null;
    return node;
}

// Structure for return type of
// function findPerfectBinaryTree
public class returnType
{

    // To store if sub-tree is perfect or not
    public Boolean isPerfect;

    // To store if sub-tree is complete or not
    public Boolean isComplete;

    // size of the tree
    public int size;

    // Root of biggest complete sub-tree
    public node rootTree;
};

// helper function that returns height
// of the tree given size
static int getHeight(int size)
{
    return (int)Math.Ceiling(Math.Log(size + 1) /
                             Math.Log(2));
}

// Function to return the biggest
// complete binary sub-tree
static returnType findCompleteBinaryTree(node root)
{

    // Declaring returnType that
    // needs to be returned
    returnType rt=new returnType();

    // If root is null then it is considered
    // as both perfect and complete binary
    // tree of size 0
    if (root == null)
    {
        rt.isPerfect = true;
        rt.isComplete = true;
        rt.size = 0;
        rt.rootTree = null;
        return rt;
    }

    // Recursive call for left and right child
    returnType lv = findCompleteBinaryTree(root.left);
    returnType rv = findCompleteBinaryTree(root.right);

    // CASE - A
    // If left sub-tree is perfect and right is
    // complete and there height is also same
    // then sub-tree root is also complete binary
    // sub-tree with size equal to sum of left
    // and right subtrees plus one for current root
    if (lv.isPerfect == true &&
        rv.isComplete == true &&
        getHeight(lv.size) == getHeight(rv.size))
    {
        rt.isComplete = true;

        // If right sub-tree is perfect then
        // root is also perfect
        rt.isPerfect = (rv.isPerfect ? true : false);
        rt.size = lv.size + rv.size + 1;
        rt.rootTree = root;
        return rt;
    }

    // CASE - B
    // If left sub-tree is complete and right is
    // perfect and the height of left is greater than
    // right by one then sub-tree root is complete
    // binary sub-tree with size equal to
    // sum of left and right subtrees plus one
    // for current root. But sub-tree cannot be
    // perfect binary sub-tree.
    if (lv.isComplete == true &&
        rv.isPerfect == true &&
        getHeight(lv.size) == getHeight(rv.size) + 1)
    {
        rt.isComplete = true;
        rt.isPerfect = false;
        rt.size = lv.size + rv.size + 1;
        rt.rootTree = root;
        return rt;
    }

    // CASE - C
    // Else this sub-tree cannot be a complete
    // binary tree and simply return the biggest
    // sized complete sub-tree found till now
    // in the left or right sub-trees
    rt.isPerfect = false;
    rt.isComplete = false;
    rt.size = Math.Max(lv.size, rv.size);
    rt.rootTree = (lv.size > rv.size ?
                         lv.rootTree : rv.rootTree);
    return rt;
}

// Function to print the
// inorder traversal of the tree
static void inorderPrint(node root)
{
    if (root != null)
    {
        inorderPrint(root.left);
        Console.Write(root.data + " ");
        inorderPrint(root.right);
    }
}

// Driver code
public static void Main(String []args)
{
    // Create the tree
    node root = newNode(50);
    root.left = newNode(30);
    root.right = newNode(60);
    root.left.left = newNode(5);
    root.left.right = newNode(20);
    root.right.left = newNode(45);
    root.right.right = newNode(70);
    root.right.left.left = newNode(10);

    // Get the biggest sized complete binary sub-tree
    returnType ans = findCompleteBinaryTree(root);

    Console.WriteLine("Size : " + ans.size);

    // Print the inorder traversal
    // of the found sub-tree
    Console.Write("Inorder Traversal : ");
    inorderPrint(ans.rootTree);
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Node structure of the tree
class node
{
    constructor(data)
    {
        this.left = null;
        this.right = null;
        this.data = data;
    }
}

// To create a new node
function newNode(data)
{
    let Node = new node(data);
    return Node;
}

// Structure for return type of
// function findPerfectBinaryTree
class returnType
{
    constructor()
    {

        // To store if sub-tree is perfect or not
        this.isPerfect;

        // To store if sub-tree is complete or not
        this.isComplete;

        // size of the tree
        this.size;

        // Root of biggest complete sub-tree
        this.rootTree;
    }
}

// Helper function that returns height
// of the tree given size
function getHeight(size)
{
    return Math.ceil(Math.log(size + 1) /
                     Math.log(2));
}

// Function to return the biggest
// complete binary sub-tree
function findCompleteBinaryTree(root)
{

    // Declaring returnType that
    // needs to be returned
    let rt = new returnType();

    // If root is null then it is considered as both
    // perfect and complete binary tree of size 0
    if (root == null)
    {
        rt.isPerfect = true;
        rt.isComplete = true;
        rt.size = 0;
        rt.rootTree = null;
        return rt;
    }

    // Recursive call for left and right child
    let lv = findCompleteBinaryTree(root.left);
    let rv = findCompleteBinaryTree(root.right);

    // CASE - A
    // If left sub-tree is perfect and right is
    // complete and there height is also same
    // then sub-tree root is also complete
    // binary sub-tree with size equal to
    // sum of left and right subtrees plus
    // one for current root
    if (lv.isPerfect == true && rv.isComplete == true &&
        getHeight(lv.size) == getHeight(rv.size))
    {
        rt.isComplete = true;

        // If right sub-tree is perfect then
        // root is also perfect
        rt.isPerfect = (rv.isPerfect ? true : false);
        rt.size = lv.size + rv.size + 1;
        rt.rootTree = root;
        return rt;
    }

    // CASE - B
    // If left sub-tree is complete and right
    // is perfect and the height of left is
    // greater than right by one then sub-tree root
    // is complete binary sub-tree with size equal to
    // sum of left and right subtrees plus one for
    // current root. But sub-tree cannot be perfect
    // binary sub-tree.
    if (lv.isComplete == true && rv.isPerfect == true &&
        getHeight(lv.size) == getHeight(rv.size) + 1)
    {
        rt.isComplete = true;
        rt.isPerfect = false;
        rt.size = lv.size + rv.size + 1;
        rt.rootTree = root;
        return rt;
    }

    // CASE - C
    // Else this sub-tree cannot be a complete
    // binary tree and simply return the biggest
    // sized complete sub-tree found till now in
    // the left or right sub-trees
    rt.isPerfect = false;
    rt.isComplete = false;
    rt.size = Math.max(lv.size, rv.size);
    rt.rootTree = (lv.size > rv.size ?
                   lv.rootTree : rv.rootTree);
    return rt;
}

// Function to print the inorder
// traversal of the tree
function inorderPrint(root)
{
    if (root != null)
    {
        inorderPrint(root.left);
        document.write(root.data + " ");
        inorderPrint(root.right);
    }
}

// Driver code

// Create the tree
let root = newNode(50);
root.left = newNode(30);
root.right = newNode(60);
root.left.left = newNode(5);
root.left.right = newNode(20);
root.right.left = newNode(45);
root.right.right = newNode(70);
root.right.left.left = newNode(10);

// Get the biggest sized complete binary sub-tree
let ans = findCompleteBinaryTree(root);

document.write( "Size : " + ans.size + "</br>");

// Print the inorder traversal of the found sub-tree
document.write("Inorder Traversal : ");
inorderPrint(ans.rootTree);

// This code is contributed by suresh07

</script>
```

**Output:** 

```
Size : 4
Inorder Traversal : 10 45 60 70
```