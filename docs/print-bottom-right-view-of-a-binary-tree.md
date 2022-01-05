# 打印二叉树的右下方视图

> 原文:[https://www . geesforgeks . org/print-右下角-二叉树视图/](https://www.geeksforgeeks.org/print-bottom-right-view-of-a-binary-tree/)

给定一个二叉树，打印它的右下视图。二叉树的右下方视图是从右下方访问树时可见的一组节点，返回从右向左排序的节点值。
在右下视图中，从右下侧以 45 度角查看树时，只有几个节点可见，其余节点隐藏在后面。
**例:**

```
Input :
   1           
 /   \
2     3        
 \     \
  5     4    
Output : [4, 5]
Visible nodes from the bottom right direction are 4 and 5

Input :
     1           
   /   \
  2     3        
 /     /
4     5
       \
        6
Output: [3, 6, 4]
```

**进场:**

*   这个问题可以用简单的递归遍历来解决。
*   通过向所有递归调用传递参数来跟踪节点的级别。以 45%的角度考虑一棵树的高度(如一个例子中所解释的)，所以每当我们向左移动时，它的高度就会增加一。
*   其思想是跟踪最大级别，并以在访问左子树之前访问右子树的方式遍历树。
*   级别超过最大级别的节点，打印该节点，因为这是其级别中的最后一个节点(在左子树之前遍历右子树)。

以下是上述方法的实现:

## C++

```
// C++ program to print bottom
// right view of binary tree
#include<bits/stdc++.h>
using namespace std;

// A binary tree node
struct Node
{
    int data;
    Node *left, *right;

    Node(int item)
    {
        data = item;
        left = right = NULL;
    }
};

// class to access maximum level
// by reference
struct _Max_level
{
    int _max_level;
};

Node *root;
_Max_level *_max = new _Max_level();

// Recursive function to print bottom
// right view of a binary tree
void bottomRightViewUtil(Node* node, int level,
                        _Max_level *_max_level)
{

    // Base Case
    if (node == NULL)
        return;

    // Recur for right subtree first
    bottomRightViewUtil(node->right,
                        level, _max_level);

    // If this is the last Node of its level
    if (_max_level->_max_level < level)
    {
        cout << node->data << " ";
        _max_level->_max_level = level;
    }

    // Recur for left subtree
    // with increased level
    bottomRightViewUtil(node->left,
                        level + 1, _max_level);
}

// A wrapper over bottomRightViewUtil()
void bottomRightView(Node *node)
{
    bottomRightViewUtil(node, 1, _max);
}

void bottomRightView()
{
    bottomRightView(root);
}

// Driver Code
int main()
{
    root = new Node(1);
    root->left = new Node(2);
    root->right = new Node(3);
    root->left->left = new Node(4);
    root->right->left = new Node(5);
    root->right->left->right = new Node(6);

    bottomRightView();
}

// This code is contributed by Arnab Kundu
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print bottom
// right view of binary tree

// A binary tree node
class Node {

    int data;
    Node left, right;

    Node(int item)
    {
        data = item;
        left = right = null;
    }
}

// class to access maximum level by reference
class Max_level {

    int max_level;
}

class BinaryTree {

    Node root;
    Max_level max = new Max_level();

    // Recursive function to print bottom
    // right view of a binary tree.
    void bottomRightViewUtil(Node node, int level,
                             Max_level max_level)
    {

        // Base Case
        if (node == null)
            return;

        // Recur for right subtree first
        bottomRightViewUtil(node.right,
                            level, max_level);

        // If this is the last Node of its level
        if (max_level.max_level < level) {
            System.out.print(node.data + " ");
            max_level.max_level = level;
        }

        // Recur for left subtree with increased level
        bottomRightViewUtil(node.left,
                            level + 1, max_level);
    }

    void bottomRightView()
    {
        bottomRightView(root);
    }

    // A wrapper over bottomRightViewUtil()
    void bottomRightView(Node node)
    {

        bottomRightViewUtil(node, 1, max);
    }

    // Driver program to test the above functions
    public static void main(String args[])
    {
        BinaryTree tree = new BinaryTree();
        tree.root = new Node(1);
        tree.root.left = new Node(2);
        tree.root.right = new Node(3);
        tree.root.left.left = new Node(4);
        tree.root.right.left = new Node(5);
        tree.root.right.left.right = new Node(6);

        tree.bottomRightView();
    }
}
```

## 蟒蛇 3

```
# Python3 program to print bottom
# right view of binary tree

# A binary tree node
class Node:

    # Construct to create a newNode
    def __init__(self, item):
        self.data = item
        self.left = None
        self.right = None

maxlevel = [0]

# Recursive function to print bottom
# right view of a binary tree.
def bottomRightViewUtil(node, level, maxlevel):

    # Base Case
    if (node == None):
        return

    # Recur for right subtree first
    bottomRightViewUtil(node.right, level,
                                 maxlevel)

    # If this is the last Node of its level
    if (maxlevel[0] < level):
        print(node.data, end = " ")
        maxlevel[0] = level

    # Recur for left subtree with increased level
    bottomRightViewUtil(node.left, level + 1, 
                                maxlevel)

# A wrapper over bottomRightViewUtil()
def bottomRightView(node):

    bottomRightViewUtil(node, 1, maxlevel)

# Driver Code
root = Node(1)
root.left = Node(2)
root.right = Node(3)
root.left.left = Node(4)
root.right.left = Node(5)
root.right.left.right = Node(6)

bottomRightView(root)

# This code is contributed by SHUBHAMSINGH10
```

## C#

```
// C# program to print bottom
// right view of binary tree
using System;

// A binary tree node
class Node
{
    public int data;
    public Node left, right;

    public Node(int item)
    {
        data = item;
        left = right = null;
    }
}

// class to access maximum level by reference
class Max_level
{
    public int max_level;
}

class GFG
{
    Node root;
    Max_level max = new Max_level();

    // Recursive function to print bottom
    // right view of a binary tree.
    void bottomRightViewUtil(Node node, int level,
                             Max_level max_level)
    {

        // Base Case
        if (node == null)
            return;

        // Recur for right subtree first
        bottomRightViewUtil(node.right,
                            level, max_level);

        // If this is the last Node of its level
        if (max_level.max_level < level)
        {
            Console.Write(node.data + " ");
            max_level.max_level = level;
        }

        // Recur for left subtree with increased level
        bottomRightViewUtil(node.left,
                            level + 1, max_level);
    }

    void bottomRightView()
    {
        bottomRightView(root);
    }

    // A wrapper over bottomRightViewUtil()
    void bottomRightView(Node node)
    {

        bottomRightViewUtil(node, 1, max);
    }

    // Driver Code
    public static void Main(String []args)
    {
        GFG tree = new GFG();
        tree.root = new Node(1);
        tree.root.left = new Node(2);
        tree.root.right = new Node(3);
        tree.root.left.left = new Node(4);
        tree.root.right.left = new Node(5);
        tree.root.right.left.right = new Node(6);

        tree.bottomRightView();
    }
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript program to print bottom
// right view of binary tree

// A binary tree node
class Node
{
    constructor(item)
    {
        this.data = item;
        this.left = null;
        this.right = null;
    }
}

// class to access maximum level by reference
class Max_level
{
    constructor()
    {
        this.max_level = 0;
    }
}

var max = new Max_level();
// Recursive function to print bottom
// right view of a binary tree.
function bottomRightViewUtil(node, level,max_level)
{
    // Base Case
    if (node == null)
        return;
    // Recur for right subtree first
    bottomRightViewUtil(node.right,
                        level, max_level);
    // If this is the last Node of its level
    if (max_level.max_level < level)
    {
        document.write(node.data + " ");
        max_level.max_level = level;
    }
    // Recur for left subtree with increased level
    bottomRightViewUtil(node.left,
                        level + 1, max_level);
}

// A wrapper over bottomRightViewUtil()
function bottomRightView(node)
{
    bottomRightViewUtil(node, 1, max);
}

// Driver Code
var root = new Node(1);
root.left = new Node(2);
root.right = new Node(3);
root.left.left = new Node(4);
root.right.left = new Node(5);
root.right.left.right = new Node(6);
bottomRightView(root);

// This code is contributed by rrrtnx.
</script>
```

**Output:** 

```
3 6 4
```

**时间复杂度:** O(N)，其中 N 为二叉树的节点数。