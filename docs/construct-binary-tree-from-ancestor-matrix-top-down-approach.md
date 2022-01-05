# 从祖先矩阵构建二叉树|自上而下的方法

> 原文:[https://www . geesforgeks . org/construct-二叉树-从祖先-矩阵-自上而下-进场/](https://www.geeksforgeeks.org/construct-binary-tree-from-ancestor-matrix-top-down-approach/)

给定一个祖先矩阵 mat[n][n]，其中祖先矩阵定义如下。

```
mat[i][j] = 1 if i is ancestor of j
mat[i][j] = 0, otherwise 
```

从给定的祖先矩阵构造二叉树，其中所有节点的值都是从 0 到 n-1。

*   可以假设提供给程序的输入是有效的，并且可以用它来构建树。
*   许多二叉树可以从一个输入构建。程序将构建其中的任何一个。

**示例:**

```
Input:
{ {0, 1, 1},
  {0, 0, 0},
  {0, 0, 0}
};
Output:
      0
    /   \
   1     2 

Input:
{ {0, 0, 0, 1, 1, 0},
  {0, 0, 0, 0, 0, 1},
  {1, 1, 0, 0, 0, 0},
  {0, 0, 0, 0, 0, 0},
  {0, 0, 0, 0, 0, 0},
  {0, 0, 0, 0, 0, 0}
};
Output:
          2
        /   \
       0      1
     /   \    /  
    3     4  5
```

**自下而上的方法** : [从祖先矩阵](https://www.geeksforgeeks.org/construct-tree-from-ancestor-matrix/)
构造树**方法:**
请参考本文首先，我们会找到树的根。根是列全为零的根。一旦找到根，我们就可以使用 [DFS](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/) 递归方法从根构建一棵树。
以下是上述方法的实施:

## C++

```
// C++ implementation of
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Node structure for
// Binary Tree
struct Node {
    int data;
    Node *left, *right;
    Node(int _val)
    {
        data = _val;
        left = right = NULL;
    }
};

// Function to return
// root index of a
// binary tree
int getRootIndex(vector<vector<int> >& arr)
{
    int root_index = -1;

    for (int j = 0; j < arr[0].size(); j++) {
        int count = 0;
        for (int i = 0; i < arr.size(); i++)
            if (arr[i][j] == 0) {
                count++;
            }

        if (count == arr.size()) {
            root_index = j;
            break;
        }
    }
    return root_index;
}

// Function to print
// in-order traversal of
// a tree
void printInorder(Node* node)
{
    if (node == NULL) {
        return;
    }
    printInorder(node->left);
    cout << node->data << " ";
    printInorder(node->right);
}

// Function to generate binary
// tree from parent matrix
Node* createTreeRec(vector<vector<int> >& arr, int index)
{

    Node* node = new Node(index);

    // If left is 1 then create
    // left child. (for 1st one in row)
    // If left is 2 then create
    // right child.(for 1st one in row)
    int left = 1;

    for (int j = 0; j < arr[index].size(); j++) {
        if (arr[index][j] == 1) {
            // recur for left sub-tree
            if (left == 1) {
                node->left = createTreeRec(arr, j);
            }
            // recur for right sub-tree
            else if (left == 2) {
                node->right = createTreeRec(arr, j);
            }
            left++;
        }
    }

    return node;
}

// Driver code
int main()
{

    // Assuming leftmost 1 in a
    // row is left child, if exists
    // and rightmost 1 in a row
    // is right child, if exists
    vector<vector<int> > arr = {
        { 0, 0, 0, 1, 1, 0 },
        { 0, 0, 0, 0, 0, 1 },
        { 1, 1, 0, 0, 0, 0 },
        { 0, 0, 0, 0, 0, 0 },
        { 0, 0, 0, 0, 0, 0 },
        { 0, 0, 0, 0, 0, 0 },
    };

    int root_index = getRootIndex(arr);
    Node* root = createTreeRec(arr, root_index);

    // Printing inorder traversal
    // of tree to check the output
    printInorder(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of
// the above approach
class GFG
{

// Node structure for
// Binary Tree
static class Node
{
    int data;
    Node left, right;
    Node(int _val)
    {
        data = _val;
        left = right = null;
    }
};

// Function to return
// root index of a
// binary tree
static int getRootIndex(int [][]arr)
{
    int root_index = -1;

    for (int j = 0; j < arr[0].length; j++)
    {
        int count = 0;
        for (int i = 0; i < arr.length; i++)
            if (arr[i][j] == 0)
            {
                count++;
            }

        if (count == arr.length)
        {
            root_index = j;
            break;
        }
    }
    return root_index;
}

// Function to print
// in-order traversal of
// a tree
static void printInorder(Node node)
{
    if (node == null)
    {
        return;
    }
    printInorder(node.left);
    System.out.print(node.data + " ");
    printInorder(node.right);
}

// Function to generate binary
// tree from parent matrix
static Node createTreeRec(int [][]arr, int index)
{

    Node node = new Node(index);

    // If left is 1 then create
    // left child. (for 1st one in row)
    // If left is 2 then create
    // right child.(for 1st one in row)
    int left = 1;

    for (int j = 0; j < arr[index].length; j++)
    {
        if (arr[index][j] == 1)
        {
            // recur for left sub-tree
            if (left == 1)
            {
                node.left = createTreeRec(arr, j);
            }

            // recur for right sub-tree
            else if (left == 2)
            {
                node.right = createTreeRec(arr, j);
            }
            left++;
        }
    }

    return node;
}

// Driver code
public static void main(String[] args)
{

    // Assuming leftmost 1 in a
    // row is left child, if exists
    // and rightmost 1 in a row
    // is right child, if exists
    int[][] arr = {
        { 0, 0, 0, 1, 1, 0 },
        { 0, 0, 0, 0, 0, 1 },
        { 1, 1, 0, 0, 0, 0 },
        { 0, 0, 0, 0, 0, 0 },
        { 0, 0, 0, 0, 0, 0 },
        { 0, 0, 0, 0, 0, 0 },
    };

    int root_index = getRootIndex(arr);
    Node root = createTreeRec(arr, root_index);

    // Printing inorder traversal
    // of tree to check the output
    printInorder(root);

}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of
# the above approach

# Node structure for
# Binary Tree
class Node:

    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# Function to return
# root index of a
# binary tree
def getRootIndex(arr : list) -> int:
    root_index = -1

    for j in range(len(arr)):
        count = 0
        for i in range(len(arr)):
            if (arr[i][j] == 0):
                count += 1

        if (count == len(arr)):
            root_index = j
            break

    return root_index

# Function to print
# in-order traversal of
# a tree
def printInorder(node : Node) -> None:

    if (node is None):
        return

    printInorder(node.left)
    print(node.data, end = " ")
    printInorder(node.right)

# Function to generate binary
# tree from parent matrix
def createTreeRec(arr : list,
                  index : int) -> Node:

    node = Node(index)

    # If left is 1 then create
    # left child. (for 1st one in row)
    # If left is 2 then create
    # right child.(for 1st one in row)
    left = 1

    for j in range(len(arr[index])):
        if (arr[index][j] == 1):
            # recur for left sub-tree
            if (left == 1):
                node.left = createTreeRec(arr, j)

            # recur for right sub-tree
            elif (left == 2):
                node.right = createTreeRec(arr, j)

            left += 1

    return node

# Driver code
if __name__ == "__main__":

    # Assuming leftmost 1 in a
    # row is left child, if exists
    # and rightmost 1 in a row
    # is right child, if exists
    arr = [[0, 0, 0, 1, 1, 0],
           [0, 0, 0, 0, 0, 1],
           [1, 1, 0, 0, 0, 0],
           [0, 0, 0, 0, 0, 0],
           [0, 0, 0, 0, 0, 0],
           [0, 0, 0, 0, 0, 0]]

    root_index = getRootIndex(arr)
    root = createTreeRec(arr, root_index)

    # Printing inorder traversal
    # of tree to check the output
    printInorder(root)

# This code is contributed by sanjeev2552
```

## C#

```
// C# implementation of
// the above approach
using System;

class GFG
{

// Node structure for
// Binary Tree
class Node
{
    public int data;
    public Node left, right;
    public Node(int _val)
    {
        data = _val;
        left = right = null;
    }
};

// Function to return
// root index of a
// binary tree
static int getRootIndex(int [,]arr)
{
    int root_index = -1;

    for (int j = 0; j < arr.GetLength(0); j++)
    {
        int count = 0;
        for (int i = 0; i < arr.GetLength(1); i++)
            if (arr[i, j] == 0)
            {
                count++;
            }

        if (count == arr.GetLength(0))
        {
            root_index = j;
            break;
        }
    }
    return root_index;
}

// Function to print
// in-order traversal of
// a tree
static void printInorder(Node node)
{
    if (node == null)
    {
        return;
    }
    printInorder(node.left);
    Console.Write(node.data + " ");
    printInorder(node.right);
}

// Function to generate binary
// tree from parent matrix
static Node createTreeRec(int [,]arr, int index)
{

    Node node = new Node(index);

    // If left is 1 then create
    // left child. (for 1st one in row)
    // If left is 2 then create
    // right child.(for 1st one in row)
    int left = 1;

    for (int j = 0; j < arr.GetLength(1); j++)
    {
        if (arr[index, j] == 1)
        {
            // recur for left sub-tree
            if (left == 1)
            {
                node.left = createTreeRec(arr, j);
            }

            // recur for right sub-tree
            else if (left == 2)
            {
                node.right = createTreeRec(arr, j);
            }
            left++;
        }
    }

    return node;
}

// Driver code
public static void Main(String[] args)
{

    // Assuming leftmost 1 in a
    // row is left child, if exists
    // and rightmost 1 in a row
    // is right child, if exists
    int[,] arr = {
        { 0, 0, 0, 1, 1, 0 },
        { 0, 0, 0, 0, 0, 1 },
        { 1, 1, 0, 0, 0, 0 },
        { 0, 0, 0, 0, 0, 0 },
        { 0, 0, 0, 0, 0, 0 },
        { 0, 0, 0, 0, 0, 0 },
    };

    int root_index = getRootIndex(arr);
    Node root = createTreeRec(arr, root_index);

    // Printing inorder traversal
    // of tree to check the output
    printInorder(root);

}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript implementation of
// the above approach

// Node structure for
// Binary Tree
class Node
{
    constructor(_val)
    {
        this.data = _val;
        this.left = null;
        this.right = null;
    }
};

// Function to return
// root index of a
// binary tree
function getRootIndex(arr)
{
    var root_index = -1;

    for(var j = 0; j < arr.length; j++)
    {
        var count = 0;
        for (var i = 0; i < arr.length; i++)
            if (arr[i][j] == 0)
            {
                count++;
            }

        if (count == arr[0].length)
        {
            root_index = j;
            break;
        }
    }
    return root_index;
}

// Function to print
// in-order traversal of
// a tree
function printInorder(node)
{
    if (node == null)
    {
        return;
    }
    printInorder(node.left);
    document.write(node.data + " ");
    printInorder(node.right);
}

// Function to generate binary
// tree from parent matrix
function createTreeRec(arr, index)
{

    var node = new Node(index);

    // If left is 1 then create
    // left child. (for 1st one in row)
    // If left is 2 then create
    // right child.(for 1st one in row)
    var left = 1;

    for (var j = 0; j < arr.length; j++)
    {
        if (arr[index][j] == 1)
        {
            // recur for left sub-tree
            if (left == 1)
            {
                node.left = createTreeRec(arr, j);
            }

            // recur for right sub-tree
            else if (left == 2)
            {
                node.right = createTreeRec(arr, j);
            }
            left++;
        }
    }

    return node;
}

// Driver code
// Assuming leftmost 1 in a
// row is left child, if exists
// and rightmost 1 in a row
// is right child, if exists
var arr = [
    [ 0, 0, 0, 1, 1, 0 ],
    [ 0, 0, 0, 0, 0, 1 ],
    [ 1, 1, 0, 0, 0, 0 ],
    [ 0, 0, 0, 0, 0, 0 ],
    [ 0, 0, 0, 0, 0, 0 ],
    [ 0, 0, 0, 0, 0, 0 ]
];
var root_index = getRootIndex(arr);
var root = createTreeRec(arr, root_index);
// Printing inorder traversal
// of tree to check the output
printInorder(root);

</script>
```

**Output:** 

```
3 0 4 2 5 1
```