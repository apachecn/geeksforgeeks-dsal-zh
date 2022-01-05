# 检查给定的二叉树是否像红黑树一样高度平衡

> 原文:[https://www . geesforgeks . org/check-given-二叉树-follow-height-property-red-black-tree/](https://www.geeksforgeeks.org/check-given-binary-tree-follows-height-property-red-black-tree/)

在[红黑树](https://www.geeksforgeeks.org/red-black-tree-set-1-introduction-2/)中，一个节点的最大高度最多是最小高度的两倍([四个红黑树属性](https://www.geeksforgeeks.org/red-black-tree-set-1-introduction-2/)确保始终遵循这一点)。给定一个二叉查找树，我们需要检查以下属性。
*对于每个节点，最长叶到节点路径的长度不超过从节点到叶最短路径上节点的两倍。*

```
    12                                        40
      \                                     /    \ 
       14                                 10      100    
         \                                        /  \
          16                                     60   150    
 Cannot be a Red-Black Tree              It can be Red-Black Tree
 with any color assignment
 Max height of 12 is 1
 Min height of 12 is 3

          10
        /   \
      5     100
           /   \
          50   150
         /
        40 
 It can also be Red-Black Tree
```

预期时间复杂度为 0(n)。在解决方案中，树最多应该遍历一次。
***我们强烈建议尽量减少浏览器，先自己试试这个。***
对于每个节点，我们需要得到最大和最小高度并进行比较。这个想法是遍历树，检查每个节点是否平衡。我们需要写一个递归函数，返回三个东西，一个布尔值来指示树是否平衡，最小高度和最大高度。为了返回多个值，我们可以使用一个结构或者通过引用传递变量。我们通过引用传递了 maxh 和 minh，以便这些值可以在父调用中使用。

## C++

```
/* Program to check if a given Binary Tree is balanced like a Red-Black Tree */
#include <bits/stdc++.h>
using namespace std;

struct Node
{
    int key;
    Node *left, *right;
};

/* utility that allocates a new Node with the given key  */
Node* newNode(int key)
{
    Node* node = new Node;
    node->key = key;
    node->left = node->right = NULL;
    return (node);
}

// Returns returns tree if the Binary tree is balanced like a Red-Black
// tree. This function also sets value in maxh and minh (passed by
// reference). maxh and minh are set as maximum and minimum heights of root.
bool isBalancedUtil(Node *root, int &maxh, int &minh)
{
    // Base case
    if (root == NULL)
    {
        maxh = minh = 0;
        return true;
    }

    int lmxh, lmnh; // To store max and min heights of left subtree
    int rmxh, rmnh; // To store max and min heights of right subtree

    // Check if left subtree is balanced, also set lmxh and lmnh
    if (isBalancedUtil(root->left, lmxh, lmnh) == false)
        return false;

    // Check if right subtree is balanced, also set rmxh and rmnh
    if (isBalancedUtil(root->right, rmxh, rmnh) == false)
        return false;

    // Set the max and min heights of this node for the parent call
    maxh = max(lmxh, rmxh) + 1;
    minh = min(lmnh, rmnh) + 1;

    // See if this node is balanced
    if (maxh <= 2*minh)
        return true;

    return false;
}

// A wrapper over isBalancedUtil()
bool isBalanced(Node *root)
{
    int maxh, minh;
    return isBalancedUtil(root, maxh, minh);
}

/* Driver program to test above functions*/
int main()
{
    Node * root = newNode(10);
    root->left = newNode(5);
    root->right = newNode(100);
    root->right->left = newNode(50);
    root->right->right = newNode(150);
    root->right->left->left = newNode(40);
    isBalanced(root)? cout << "Balanced" : cout << "Not Balanced";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to check if a given Binary
// Tree is balanced like a Red-Black Tree
class GFG
{

static class Node
{
    int key;
    Node left, right;
    Node(int key)
    {
        left = null;
        right = null;
        this.key = key;
    }
}

static class INT
{
    static int d;
    INT()
    {
        d = 0;
    }
}

// Returns returns tree if the Binary
// tree is balanced like a Red-Black
// tree. This function also sets value
// in maxh and minh (passed by reference).
// maxh and minh are set as maximum and
// minimum heights of root.
static boolean isBalancedUtil(Node root,
                        INT maxh, INT minh)
{

    // Base case
    if (root == null)
    {
        maxh.d = minh.d = 0;
        return true;
    }

    // To store max and min heights of left subtree
    INT lmxh=new INT(), lmnh=new INT();

    // To store max and min heights of right subtree
    INT rmxh=new INT(), rmnh=new INT();

    // Check if left subtree is balanced,
    // also set lmxh and lmnh
    if (isBalancedUtil(root.left, lmxh, lmnh) == false)
        return false;

    // Check if right subtree is balanced,
    // also set rmxh and rmnh
    if (isBalancedUtil(root.right, rmxh, rmnh) == false)
        return false;

    // Set the max and min heights
    // of this node for the parent call
    maxh.d = Math.max(lmxh.d, rmxh.d) + 1;
    minh.d = Math.min(lmnh.d, rmnh.d) + 1;

    // See if this node is balanced
    if (maxh.d <= 2*minh.d)
        return true;

    return false;
}

// A wrapper over isBalancedUtil()
static boolean isBalanced(Node root)
{
    INT maxh=new INT(), minh=new INT();
    return isBalancedUtil(root, maxh, minh);
}

// Driver code
public static void main(String args[])
{
    Node root = new Node(10);
    root.left = new Node(5);
    root.right = new Node(100);
    root.right.left = new Node(50);
    root.right.right = new Node(150);
    root.right.left.left = new Node(40);
    System.out.println(isBalanced(root) ?
            "Balanced" : "Not Balanced");
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
""" Program to check if a given Binary
Tree is balanced like a Red-Black Tree """

# Helper function that allocates a new
# node with the given data and None
# left and right poers.                                
class newNode:

    # Construct to create a new node
    def __init__(self, key):
        self.data = key
        self.left = None
        self.right = None

# Returns returns tree if the Binary
# tree is balanced like a Red-Black
# tree. This function also sets value
# in maxh and minh (passed by
# reference). maxh and minh are set
# as maximum and minimum heights of root.
def isBalancedUtil(root, maxh, minh) :

    # Base case
    if (root == None) :

        maxh = minh = 0
        return True

    lmxh=0

    # To store max and min
    # heights of left subtree
    lmnh=0

    # To store max and min
    # heights of right subtree
    rmxh, rmnh=0,0 

    # Check if left subtree is balanced,
    # also set lmxh and lmnh
    if (isBalancedUtil(root.left, lmxh, lmnh) == False) :
        return False

    # Check if right subtree is balanced,
    # also set rmxh and rmnh
    if (isBalancedUtil(root.right, rmxh, rmnh) == False) :
        return False

    # Set the max and min heights of
    # this node for the parent call
    maxh = max(lmxh, rmxh) + 1
    minh = min(lmnh, rmnh) + 1

    # See if this node is balanced
    if (maxh <= 2 * minh) :
        return True

    return False

# A wrapper over isBalancedUtil()
def isBalanced(root) :

    maxh, minh =0,0
    return isBalancedUtil(root, maxh, minh)

# Driver Code
if __name__ == '__main__':
    root = newNode(10)
    root.left = newNode(5)
    root.right = newNode(100)
    root.right.left = newNode(50)
    root.right.right = newNode(150)
    root.right.left.left = newNode(40)
    if (isBalanced(root)):
        print("Balanced")
    else:
        print("Not Balanced")

# This code is contributed by
# Shubham Singh(SHUBHAMSINGH10)
```

## C#

```
// C# Program to check if a given Binary
// Tree is balanced like a Red-Black Tree
using System;

class GFG
{

public class Node
{
    public int key;
    public Node left, right;
    public Node(int key)
    {
        left = null;
        right = null;
        this.key = key;
    }
}

public class INT
{
    public int d;
    public INT()
    {
        d = 0;
    }
}

// Returns returns tree if the Binary
// tree is balanced like a Red-Black
// tree. This function also sets value
// in maxh and minh (passed by reference).
// maxh and minh are set as maximum and
// minimum heights of root.
static bool isBalancedUtil(Node root,
                        INT maxh, INT minh)
{

    // Base case
    if (root == null)
    {
        maxh.d = minh.d = 0;
        return true;
    }

    // To store max and min heights of left subtree
    INT lmxh = new INT(), lmnh = new INT();

    // To store max and min heights of right subtree
    INT rmxh = new INT(), rmnh = new INT();

    // Check if left subtree is balanced,
    // also set lmxh and lmnh
    if (isBalancedUtil(root.left, lmxh, lmnh) == false)
        return false;

    // Check if right subtree is balanced,
    // also set rmxh and rmnh
    if (isBalancedUtil(root.right, rmxh, rmnh) == false)
        return false;

    // Set the max and min heights
    // of this node for the parent call
    maxh.d = Math.Max(lmxh.d, rmxh.d) + 1;
    minh.d = Math.Min(lmnh.d, rmnh.d) + 1;

    // See if this node is balanced
    if (maxh.d <= 2 * minh.d)
        return true;

    return false;
}

// A wrapper over isBalancedUtil()
static bool isBalanced(Node root)
{
    INT maxh = new INT(), minh = new INT();
    return isBalancedUtil(root, maxh, minh);
}

// Driver code
public static void Main(String []args)
{
    Node root = new Node(10);
    root.left = new Node(5);
    root.right = new Node(100);
    root.right.left = new Node(50);
    root.right.right = new Node(150);
    root.right.left.left = new Node(40);
    Console.WriteLine(isBalanced(root) ?
            "Balanced" : "Not Balanced");
}
}

// This code contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript Program to check if a given Binary
// Tree is balanced like a Red-Black Tree    
class Node {
    constructor(val) {
        this.key = val;
        this.left = null;
        this.right = null;
    }
}

     class INT {
         constructor() {
            this.d = 0;
        }
    }

    // Returns returns tree if the Binary
    // tree is balanced like a Red-Black
    // tree. This function also sets value
    // in maxh and minh (passed by reference).
    // maxh and minh are set as maximum and
    // minimum heights of root.
    function isBalancedUtil(root,  maxh,  minh) {

        // Base case
        if (root == null) {
            maxh.d = minh.d = 0;
            return true;
        }

        // To store max and min heights of left subtree
        var lmxh = new INT(), lmnh = new INT();

        // To store max and min heights of right subtree
        var rmxh = new INT(), rmnh = new INT();

        // Check if left subtree is balanced,
        // also set lmxh and lmnh
        if (isBalancedUtil(root.left, lmxh, lmnh) == false)
            return false;

        // Check if right subtree is balanced,
        // also set rmxh and rmnh
        if (isBalancedUtil(root.right, rmxh, rmnh) == false)
            return false;

        // Set the max and min heights
        // of this node for the parent call
        maxh.d = Math.max(lmxh.d, rmxh.d) + 1;
        minh.d = Math.min(lmnh.d, rmnh.d) + 1;

        // See if this node is balanced
        if (maxh.d <= 2 * minh.d)
            return true;

        return false;
    }

    // A wrapper over isBalancedUtil()
    function isBalanced(root) {
        var maxh = new INT(), minh = new INT();
        return isBalancedUtil(root, maxh, minh);
    }

    // Driver code

        var root = new Node(10);
        root.left = new Node(5);
        root.right = new Node(100);
        root.right.left = new Node(50);
        root.right.right = new Node(150);
        root.right.left.left = new Node(40);
        document.write(isBalanced(root) ?
        "Balanced" : "Not Balanced");

// This code contributed by umadevi9616

</script>
```

**输出:**

```
Balanced 
```

**时间复杂度:**上述代码的时间复杂度为 O(n)，因为代码进行简单的树遍历。
如发现任何不正确的地方，请写评论，或者您想分享更多关于上述话题的信息