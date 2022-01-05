# 二叉树中的范围系数

> 原文:[https://www . geesforgeks . org/二叉树区间系数/](https://www.geeksforgeeks.org/coefficient-of-range-in-a-binary-tree/)

给定一棵二叉树，任务是找到其中的**范围系数**。
**范围**定义为一组数据中最大值和最小值之差，**范围系数**是范围离散度的相对度量。假设一个数据集中的最大值为 *maxVal* ，最小值为 *minVal* ，那么范围系数可以定义为:

> **范围系数**=(maxVal–minVal)/(maxVal+minVal)

考虑下面的二叉树:

![](img/f0d1bb5c0e487540c8e33da38afc9267.png)

**例如**，上述二叉树中最大值为 9，最小值为 1，因此范围系数为((9–1)/(9+1))= 0.8。

**方法:**在[二叉查找树](https://www.geeksforgeeks.org/binary-search-tree-set-1-search-and-insertion/)中，我们可以通过遍历右指针直到到达最右边的节点来找到最大值。但是在**二叉树**中，我们必须访问每个节点来计算最大值。所以我们的想法是遍历给定的树，对于每个节点返回最大 3 个值。

1.  节点的数据。
2.  节点左子树中的最大值。
3.  节点右子树中的最大值。

同样，在二叉树中找到最小值，计算范围系数。
以下是上述方法的实现:

## C++

```
// CPP program to find Coefficient of
// Range in a Binary Tree

#include <bits/stdc++.h>
using namespace std;

// A tree node
struct Node {
    float data;
    struct Node *left, *right;
};

// A utility function to create a new node
struct Node* newNode(float data)
{
    struct Node* newnode = new Node();
    newnode->data = data;
    newnode->left = newnode->right = NULL;
    return (newnode);
}

// Returns maximum value in a given Binary Tree
float findMax(struct Node* root)
{
    // Base case
    if (root == NULL)
        return INT_MIN;

    // Return maximum of 3 values:
    // 1) Root's data 2) Max in Left Subtree
    // 3) Max in right subtree
    float res = root->data;
    float lres = findMax(root->left);
    float rres = findMax(root->right);
    if (lres > res)
        res = lres;
    if (rres > res)
        res = rres;

    return res;
}

// Returns minimum value in a given Binary Tree
float findMin(struct Node* root)
{
    // Base case
    if (root == NULL)
        return INT_MAX;

    // Return minimum of 3 values:
    // 1) Root's data 2) Min in Left Subtree
    // 3) Min in right subtree
    float res = root->data;
    float lres = findMin(root->left);
    float rres = findMin(root->right);
    if (lres < res)
        res = lres;
    if (rres < res)
        res = rres;

    return res;
}

// Function to find the value of the Coefficient
// of range in the Binary Tree
float coefRange(Node* root)
{
    float max = findMax(root);
    float min = findMin(root);

    return (max - min) / (max + min);
}

// Driver Code
int main(void)
{
    // Construct the Binary Tree
    struct Node* root = newNode(2);
    root->left = newNode(7);
    root->right = newNode(5);
    root->left->right = newNode(6);
    root->left->right->left = newNode(1);
    root->left->right->right = newNode(11);
    root->right->right = newNode(9);
    root->right->right->left = newNode(4);

    cout << "Coefficient of Range is " << coefRange(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA program to find Coefficient of
// Range in a Binary Tree

class GFG
{

// A tree node
static class Node
{
    float data;
    Node left, right;
};

// A utility function to create a new node
static Node newNode(float data)
{
    Node node = new Node();
    node.data = data;
    node.left = node.right = null;
    return (node);
}

// Returns maximum value in a given Binary Tree
static float findMax(Node root)
{
    // Base case
    if (root == null)
        return Integer.MIN_VALUE;

    // Return maximum of 3 values:
    // 1) Root's data 2) Max in Left Subtree
    // 3) Max in right subtree
    float res = root.data;
    float lres = findMax(root.left);
    float rres = findMax(root.right);
    if (lres > res)
        res = lres;
    if (rres > res)
        res = rres;

    return res;
}

// Returns minimum value in a given Binary Tree
static float findMin(Node root)
{
    // Base case
    if (root == null)
        return Integer.MAX_VALUE;

    // Return minimum of 3 values:
    // 1) Root's data 2) Min in Left Subtree
    // 3) Min in right subtree
    float res = root.data;
    float lres = findMin(root.left);
    float rres = findMin(root.right);
    if (lres < res)
        res = lres;
    if (rres < res)
        res = rres;

    return res;
}

// Function to find the value of the Coefficient
// of range in the Binary Tree
static float coefRange(Node root)
{
    float max = findMax(root);
    float min = findMin(root);

    return (max - min) / (max + min);
}

// Driver Code
public static void main(String[] args)
{
    // Construct the Binary Tree
    Node root = newNode(2);
    root.left = newNode(7);
    root.right = newNode(5);
    root.left.right = newNode(6);
    root.left.right.left = newNode(1);
    root.left.right.right = newNode(11);
    root.right.right = newNode(9);
    root.right.right.left = newNode(4);

    System.out.print("Coefficient of Range is " + coefRange(root));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program to find Coefficient of
# Range in a Binary Tree
from sys import maxsize
INT_MIN = -maxsize
INT_MAX = maxsize

# A tree node
class Node:
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# Returns maximum value in a given Binary Tree
def findMax(root: Node) -> float:

    # Base case
    if root is None:
        return INT_MIN

    # Return maximum of 3 values:
    # 1) Root's data 2) Max in Left Subtree
    # 3) Max in right subtree
    res = root.data
    lres = findMax(root.left)
    rres = findMax(root.right)
    if lres > res:
        res = lres
    if rres > res:
        res = rres

    return res

# Returns minimum value in a given Binary Tree
def findMin(root: Node) -> float:

    # Base case
    if root is None:
        return INT_MAX

    # Return minimum of 3 values:
    # 1) Root's data 2) Min in Left Subtree
    # 3) Min in right subtree
    res = root.data
    lres = findMin(root.left)
    rres = findMin(root.right)
    if lres < res:
        res = lres
    if rres < res:
        res = rres

    return res

# Function to find the value of the Coefficient
# of range in the Binary Tree
def coefRange(root: Node) -> float:
    maxx = findMax(root)
    minn = findMin(root)

    return (maxx - minn) / (maxx + minn)

# Driver Code
if __name__ == "__main__":

    # Construct the Binary Tree
    root = Node(2)
    root.left = Node(7)
    root.right = Node(5)
    root.left.right = Node(6)
    root.left.right.left = Node(1)
    root.left.right.right = Node(11)
    root.right.right = Node(9)
    root.right.right.left = Node(4)

    print("Coefficient of Range is", coefRange(root))

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# program to find Coefficient of
// Range in a Binary Tree
using System;

class GFG
{

// A tree node
class Node
{
    public float data;
    public Node left, right;
};

// A utility function to create a new node
static Node newNode(float data)
{
    Node node = new Node();
    node.data = data;
    node.left = node.right = null;
    return (node);
}

// Returns maximum value in a given Binary Tree
static float findMax(Node root)
{
    // Base case
    if (root == null)
        return int.MinValue;

    // Return maximum of 3 values:
    // 1) Root's data 2) Max in Left Subtree
    // 3) Max in right subtree
    float res = root.data;
    float lres = findMax(root.left);
    float rres = findMax(root.right);
    if (lres > res)
        res = lres;
    if (rres > res)
        res = rres;

    return res;
}

// Returns minimum value in a given Binary Tree
static float findMin(Node root)
{
    // Base case
    if (root == null)
        return int.MaxValue;

    // Return minimum of 3 values:
    // 1) Root's data 2) Min in Left Subtree
    // 3) Min in right subtree
    float res = root.data;
    float lres = findMin(root.left);
    float rres = findMin(root.right);
    if (lres < res)
        res = lres;
    if (rres < res)
        res = rres;

    return res;
}

// Function to find the value of the Coefficient
// of range in the Binary Tree
static float coefRange(Node root)
{
    float max = findMax(root);
    float min = findMin(root);

    return (max - min) / (max + min);
}

// Driver Code
public static void Main(String[] args)
{
    // Construct the Binary Tree
    Node root = newNode(2);
    root.left = newNode(7);
    root.right = newNode(5);
    root.left.right = newNode(6);
    root.left.right.left = newNode(1);
    root.left.right.right = newNode(11);
    root.right.right = newNode(9);
    root.right.right.left = newNode(4);

    Console.Write("Coefficient of Range is " + 
                             coefRange(root));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// javascript program to find Coefficient of
// Range in a Binary Tree
    // A tree node
class Node {
    constructor(val) {
        this.data = val;
        this.left = null;
        this.right = null;
    }
}

    // A utility function to create a new node
    function newNode(data) {
var node = new Node();
        node.data = data;
        node.left = node.right = null;
        return (node);
    }

    // Returns maximum value in a given Binary Tree
    function findMax(root) {
        // Base case
        if (root == null)
            return Number.MIN_VALUE;

        // Return maximum of 3 values:
        // 1) Root's data 2) Max in Left Subtree
        // 3) Max in right subtree
        var res = root.data;
        var lres = findMax(root.left);
        var rres = findMax(root.right);
        if (lres > res)
            res = lres;
        if (rres > res)
            res = rres;

        return res;
    }

    // Returns minimum value in a given Binary Tree
    function findMin(root) {
        // Base case
        if (root == null)
            return Number.MAX_VALUE;

        // Return minimum of 3 values:
        // 1) Root's data 2) Min in Left Subtree
        // 3) Min in right subtree
        var res = root.data;
        var lres = findMin(root.left);
        var rres = findMin(root.right);
        if (lres < res)
            res = lres;
        if (rres < res)
            res = rres;

        return res;
    }

    // Function to find the value of the Coefficient
    // of range in the Binary Tree
    function coefRange(root) {
        var max = findMax(root);
        var min = findMin(root);

        return (max - min) / (max + min);
    }

    // Driver Code

        // Construct the Binary Tree
var root = newNode(2);
        root.left = newNode(7);
        root.right = newNode(5);
        root.left.right = newNode(6);
        root.left.right.left = newNode(1);
        root.left.right.right = newNode(11);
        root.right.right = newNode(9);
        root.right.right.left = newNode(4);

        document.write("Coefficient of Range is " + coefRange(root).toFixed(6));

// This code contributed by umadevi9616 
</script>
```

**Output:** 

```
Coefficient of Range is 0.833333
```

**时间复杂度:** O(n)，其中 n 为节点数。
***辅助空间** : O(n)*