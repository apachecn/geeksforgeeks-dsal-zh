# 在给定的二叉树中找到最大的完美子树

> 原文:[https://www . geesforgeks . org/find-给定二叉树中最大的完美子树/](https://www.geeksforgeeks.org/find-the-largest-perfect-subtree-in-a-given-binary-tree/)

给定一棵二叉树，任务是找到给定二叉树中最大完美子树的大小。

**完美二叉树–**二叉树是[完美二叉树](https://www.geeksforgeeks.org/binary-tree-set-3-types-of-binary-tree/)，其中所有内部节点都有两个子节点，所有叶子都在同一级别。

**示例:**

```
Input: 
      1
    /   \
   2     3
 /  \   /
4    5 6
Output:
Size : 3
Inorder Traversal : 4 2 5
The following sub-tree is the maximum size Perfect sub-tree 
   2  
 /  \
4    5

Input:
         50
      /      \
   30         60
  /   \      /    \ 
 5    20   45      70
          /  \     /  \
         10   85  65  80
Output:
Size : 7
Inorder Traversal : 10 45 85 60 65 70 80
```

**方法:**简单地以自下而上的方式遍历树。然后，在从子树到父树的递归中，我们可以将关于子树的信息传递给父树。传递的信息只能由父节点在恒定时间内用来进行完美树测试(对于父节点)。左边的子树需要告诉父树是否是完美二叉树，还需要传递来自左边子树的完美二叉树的最大高度。同样，右子树也需要通过来自右子树的完美二叉树的最大高度。

为了找到最大的完美子树，子树需要将以下信息传递到树上，这样我们就可以将最大高度与父树的数据进行比较，以检查完美二叉树的属性。

1.  有一个 bool 变量来检查左边的子树或右边的子树是否完美。
2.  通过递归中的左右子调用，我们通过以下两种情况来确定父子树是否完美:
    *   如果左边的子树和右边的子树都是完美的二叉树，并且具有相同的高度，那么父树也是一棵完美的二叉树，其高度加上它的一个子树。
    *   如果上述情况不成立，则父树不能是完美二叉树，只需通过比较它们的高度，返回来自左侧或右侧子树的最大大小的完美二叉树。

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

    // Height of the tree
    int height;

    // Root of biggest perfect sub-tree
    node* rootTree;
};

// Function to return the biggest
// perfect binary sub-tree
returnType findPerfectBinaryTree(struct node* root)
{

    // Declaring returnType that
    // needs to be returned
    returnType rt;

    // If root is NULL then it is considered as
    // perfect binary tree of height 0
    if (root == NULL) {
        rt.isPerfect = true;
        rt.height = 0;
        rt.rootTree = NULL;
        return rt;
    }

    // Recursive call for left and right child
    returnType lv = findPerfectBinaryTree(root->left);
    returnType rv = findPerfectBinaryTree(root->right);

    // If both left and right sub-trees are perfect and
    // there height is also same then sub-tree root
    // is also perfect binary subtree with height
    // plus one of its child sub-trees
    if (lv.isPerfect && rv.isPerfect && lv.height == rv.height) {
        rt.height = lv.height + 1;
        rt.isPerfect = true;
        rt.rootTree = root;
        return rt;
    }

    // Else this sub-tree cannot be a perfect binary tree
    // and simply return the biggest sized perfect sub-tree
    // found till now in the left or right sub-trees
    rt.isPerfect = false;
    rt.height = max(lv.height, rv.height);
    rt.rootTree = (lv.height > rv.height ? lv.rootTree : rv.rootTree);
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
    // Create tree
    struct node* root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->left->right = newNode(5);
    root->right->left = newNode(6);

    // Get the biggest sizes perfect binary sub-tree
    struct returnType ans = findPerfectBinaryTree(root);

    // Height of the found sub-tree
    int h = ans.height;

    cout << "Size : " << pow(2, h) - 1 << endl;

    // Print the inorder traversal of the found sub-tree
    cout << "Inorder Traversal : ";
    inorderPrint(ans.rootTree);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
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

    // Height of the tree
    int height;

    // Root of biggest perfect sub-tree
    node rootTree;
};

// Function to return the biggest
// perfect binary sub-tree
static returnType findPerfectBinaryTree(node root)
{

    // Declaring returnType that
    // needs to be returned
    returnType rt = new returnType();

    // If root is null then it is considered as
    // perfect binary tree of height 0
    if (root == null)
    {
        rt.isPerfect = true;
        rt.height = 0;
        rt.rootTree = null;
        return rt;
    }

    // Recursive call for left and right child
    returnType lv = findPerfectBinaryTree(root.left);
    returnType rv = findPerfectBinaryTree(root.right);

    // If both left and right sub-trees are perfect and
    // there height is also same then sub-tree root
    // is also perfect binary subtree with height
    // plus one of its child sub-trees
    if (lv.isPerfect && rv.isPerfect &&
        lv.height == rv.height)
    {
        rt.height = lv.height + 1;
        rt.isPerfect = true;
        rt.rootTree = root;
        return rt;
    }

    // Else this sub-tree cannot be a perfect binary tree
    // and simply return the biggest sized perfect sub-tree
    // found till now in the left or right sub-trees
    rt.isPerfect = false;
    rt.height = Math.max(lv.height, rv.height);
    rt.rootTree = (lv.height > rv.height ?
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
        System.out.print(root.data + " ");
        inorderPrint(root.right);
    }
}

// Driver code
public static void main(String[] args)
{
    // Create tree
    node root = newNode(1);
    root.left = newNode(2);
    root.right = newNode(3);
    root.left.left = newNode(4);
    root.left.right = newNode(5);
    root.right.left = newNode(6);

    // Get the biggest sizes perfect binary sub-tree
    returnType ans = findPerfectBinaryTree(root);

    // Height of the found sub-tree
    int h = ans.height;

    System.out.println("Size : " +
                      (Math.pow(2, h) - 1));

    // Print the inorder traversal of the found sub-tree
    System.out.print("Inorder Traversal : ");
    inorderPrint(ans.rootTree);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of above approach

# Tree node
class Node:
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# To create a new node
def newNode(data):

    node = Node(0)
    node.data = data
    node.left = None
    node.right = None
    return node

# Structure for return type of
# function findPerfectBinaryTree
class returnType:

    def __init__(self):

        # To store if sub-tree is perfect or not
        isPerfect = 0

        # Height of the tree
        height = 0

        # Root of biggest perfect sub-tree
        rootTree = 0

# Function to return the biggest
# perfect binary sub-tree
def findPerfectBinaryTree(root):

    # Declaring returnType that
    # needs to be returned
    rt = returnType()

    # If root is None then it is considered as
    # perfect binary tree of height 0
    if (root == None) :
        rt.isPerfect = True
        rt.height = 0
        rt.rootTree = None
        return rt

    # Recursive call for left and right child
    lv = findPerfectBinaryTree(root.left)
    rv = findPerfectBinaryTree(root.right)

    # If both left and right sub-trees are perfect and
    # there height is also same then sub-tree root
    # is also perfect binary subtree with height
    # plus one of its child sub-trees
    if (lv.isPerfect and rv.isPerfect and
        lv.height == rv.height) :
        rt.height = lv.height + 1
        rt.isPerfect = True
        rt.rootTree = root
        return rt

    # Else this sub-tree cannot be a perfect binary tree
    # and simply return the biggest sized perfect sub-tree
    # found till now in the left or right sub-trees
    rt.isPerfect = False
    rt.height = max(lv.height, rv.height)
    if (lv.height > rv.height ):
        rt.rootTree = lv.rootTree
    else :
        rt.rootTree = rv.rootTree
    return rt

# Function to print the inorder traversal of the tree
def inorderPrint(root):

    if (root != None) :
        inorderPrint(root.left)
        print (root.data, end = " ")
        inorderPrint(root.right)

# Driver code

# Create tree
root = newNode(1)
root.left = newNode(2)
root.right = newNode(3)
root.left.left = newNode(4)
root.left.right = newNode(5)
root.right.left = newNode(6)

# Get the biggest sizes perfect binary sub-tree
ans = findPerfectBinaryTree(root)

# Height of the found sub-tree
h = ans.height

print ("Size : " , pow(2, h) - 1)

# Print the inorder traversal of the found sub-tree
print ("Inorder Traversal : ", end = " ")
inorderPrint(ans.rootTree)

# This code is contributed by Arnab Kundu
```

## C#

```
// C# implementation of the approach
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
    public bool isPerfect;

    // Height of the tree
    public int height;

    // Root of biggest perfect sub-tree
    public node rootTree;
};

// Function to return the biggest
// perfect binary sub-tree
static returnType findPerfectBinaryTree(node root)
{

    // Declaring returnType that
    // needs to be returned
    returnType rt = new returnType();

    // If root is null then it is considered as
    // perfect binary tree of height 0
    if (root == null)
    {
        rt.isPerfect = true;
        rt.height = 0;
        rt.rootTree = null;
        return rt;
    }

    // Recursive call for left and right child
    returnType lv = findPerfectBinaryTree(root.left);
    returnType rv = findPerfectBinaryTree(root.right);

    // If both left and right sub-trees are perfect and
    // there height is also same then sub-tree root
    // is also perfect binary subtree with height
    // plus one of its child sub-trees
    if (lv.isPerfect && rv.isPerfect &&
        lv.height == rv.height)
    {
        rt.height = lv.height + 1;
        rt.isPerfect = true;
        rt.rootTree = root;
        return rt;
    }

    // Else this sub-tree cannot be a perfect binary tree
    // and simply return the biggest sized perfect sub-tree
    // found till now in the left or right sub-trees
    rt.isPerfect = false;
    rt.height = Math.Max(lv.height, rv.height);
    rt.rootTree = (lv.height > rv.height ?
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
public static void Main(String[] args)
{
    // Create tree
    node root = newNode(1);
    root.left = newNode(2);
    root.right = newNode(3);
    root.left.left = newNode(4);
    root.left.right = newNode(5);
    root.right.left = newNode(6);

    // Get the biggest sizes perfect binary sub-tree
    returnType ans = findPerfectBinaryTree(root);

    // Height of the found sub-tree
    int h = ans.height;

    Console.WriteLine("Size : " +
                     (Math.Pow(2, h) - 1));

    // Print the inorder traversal of the found sub-tree
    Console.Write("Inorder Traversal : ");
    inorderPrint(ans.rootTree);
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

    // JavaScript program to print postorder
    // traversal iteratively

    // Node structure of the tree
    class node
    {
        constructor(data) {
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
        constructor(data) {
           this.isPerfect;
           this.height;
           this.rootTree;
        }
    }

    // Function to return the biggest
    // perfect binary sub-tree
    function findPerfectBinaryTree(root)
    {

        // Declaring returnType that
        // needs to be returned
        let rt = new returnType();

        // If root is null then it is considered as
        // perfect binary tree of height 0
        if (root == null)
        {
            rt.isPerfect = true;
            rt.height = 0;
            rt.rootTree = null;
            return rt;
        }

        // Recursive call for left and right child
        let lv = findPerfectBinaryTree(root.left);
        let rv = findPerfectBinaryTree(root.right);

        // If both left and right sub-trees are perfect and
        // there height is also same then sub-tree root
        // is also perfect binary subtree with height
        // plus one of its child sub-trees
        if (lv.isPerfect && rv.isPerfect &&
            lv.height == rv.height)
        {
            rt.height = lv.height + 1;
            rt.isPerfect = true;
            rt.rootTree = root;
            return rt;
        }

        // Else this sub-tree cannot be a perfect binary tree
        // and simply return the biggest sized perfect sub-tree
        // found till now in the left or right sub-trees
        rt.isPerfect = false;
        rt.height = Math.max(lv.height, rv.height);
        rt.rootTree = (lv.height > rv.height ?
                                 lv.rootTree : rv.rootTree);
        return rt;
    }

    // Function to print the
    // inorder traversal of the tree
    function inorderPrint(root)
    {
        if (root != null)
        {
            inorderPrint(root.left);
            document.write(root.data + " ");
            inorderPrint(root.right);
        }
    }

    // Create tree
    let root = newNode(1);
    root.left = newNode(2);
    root.right = newNode(3);
    root.left.left = newNode(4);
    root.left.right = newNode(5);
    root.right.left = newNode(6);

    // Get the biggest sizes perfect binary sub-tree
    let ans = findPerfectBinaryTree(root);

    // Height of the found sub-tree
    let h = ans.height;

    document.write("Size : " + (Math.pow(2, h) - 1) + "</br>");

    // Print the inorder traversal of the found sub-tree
    document.write("Inorder Traversal : ");
    inorderPrint(ans.rootTree);

</script>
```

**Output:** 

```
Size : 3
Inorder Traversal : 4 2 5
```