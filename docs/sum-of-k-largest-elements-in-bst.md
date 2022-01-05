# BST 中 k 个最大元素之和

> 原文:[https://www . geesforgeks . org/sum-of-k-最大元素 in-bst/](https://www.geeksforgeeks.org/sum-of-k-largest-elements-in-bst/)

给定一个 [BST](https://www.geeksforgeeks.org/binary-search-tree-set-1-search-and-insertion/) ，任务是求大于等于第 kth 个最大元素的所有元素的和。

**示例:**

```
Input : K = 3
              8
            /   \
           7     10
         /      /   \
        2      9     13
Output : 32
Explanation: 3rd largest element is 9 so sum of all
             elements greater than or equal to 9 are
             9 + 10 + 13 = 32.

Input : K = 2
           8
         /   \
        5    11
      /  \
     2    7
      \
       3
Output : 19
Explanation: 2nd largest element is 8 so sum of all
             elements greater than or equal to 8 are
             8 + 11 = 19.
```

**方式:**
思路是**遍历 BST，以**反向**方式(右根左)遍历**。
请注意，BST 的无序遍历以排序(或递增)顺序访问元素，因此无序遍历的反向将是排序顺序(**递减**)。遍历时，跟踪已访问节点的计数，并不断添加节点，直到计数变为 k

## C++

```
// C++ program to find Sum Of All Elements larger
// than or equal to Kth Largest Element In BST
#include <bits/stdc++.h>
using namespace std;

struct Node {
    int data;
    Node *left, *right;
};

// utility function new Node of BST
struct Node* cNode(int data)
{
    Node* node = new Node;
    node->left = NULL;
    node->right = NULL;
    node->data = data;
    return node;
}

// A utility function to insert a new Node
// with given key in BST
struct Node* add(Node* root, int key)
{
    // If the tree is empty, return a new Node
    if (root == NULL)
        return cNode(key);

    // Otherwise, recur down the tree
    if (root->data > key)
        root->left = add(root->left, key);

    else if (root->data < key)
        root->right = add(root->right, key);

    // return the (unchanged) Node pointer
    return root;
}

// function to return sum of all elements larger than
// and equal to Kth largest element
int klargestElementSumUtil(Node* root, int k, int& c)
{
    // Base cases
    if (root == NULL)
        return 0;
    if (c > k)
        return 0;

    // Compute sum of elements in right subtree
    int ans = klargestElementSumUtil(root->right, k, c);
    if (c >= k)
        return ans;

    // Add root's data
    ans += root->data;

    // Add current Node
    c++;
    if (c >= k)
        return ans;

    // If c is less than k, return left subtree Nodes
    return ans + klargestElementSumUtil(root->left, k, c);
}

// Wrapper over klargestElementSumRec()
int klargestElementSum(struct Node* root, int k)
{
    int c = 0;
    klargestElementSumUtil(root, k, c);
}

// Drivers code
int main()
{
    /*   19
        /    \
       7     21
     /   \
    3     11
         /   \
        9    13
          */

    Node* root = NULL;
    root = add(root, 19);
    root = add(root, 7);
    root = add(root, 3);
    root = add(root, 11);
    root = add(root, 9);
    root = add(root, 13);
    root = add(root, 21);

    int k = 2;
    cout << klargestElementSum(root, k) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find Sum Of All Elements larger
// than or equal to Kth Largest Element In BST
import java.util.*;

class GFG
{

static class Node
{
    int data;
    Node left, right;
};
static int c;

// Utility function new Node of BST
static Node cNode(int data)
{
    Node node = new Node();
    node.left = null;
    node.right = null;
    node.data = data;
    return node;
}

// A utility function to insert a new Node
// with given key in BST
static Node add(Node root, int key)
{
    // If the tree is empty, return a new Node
    if (root == null)
        return cNode(key);

    // Otherwise, recur down the tree
    if (root.data > key)
        root.left = add(root.left, key);

    else if (root.data < key)
        root.right = add(root.right, key);

    // return the (unchanged) Node pointer
    return root;
}

// function to return sum of all elements larger than
// and equal to Kth largest element
static int klargestElementSumUtil(Node root, int k)
{
    // Base cases
    if (root == null)
        return 0;
    if (c > k)
        return 0;

    // Compute sum of elements in right subtree
    int ans = klargestElementSumUtil(root.right, k);
    if (c >= k)
        return ans;

    // Add root's data
    ans += root.data;

    // Add current Node
    c++;
    if (c >= k)
        return ans;

    // If c is less than k, return left subtree Nodes
    return ans + klargestElementSumUtil(root.left, k);
}

// Wrapper over klargestElementSumRec()
static int klargestElementSum(Node root, int k)
{
    c = 0;
    return klargestElementSumUtil(root, k);
}

// Drivers code
public static void main(String[] args)
{
    /* 19
        / \
    7     21
    / \
    3     11
        / \
        9 13
        */

    Node root = null;
    root = add(root, 19);
    root = add(root, 7);
    root = add(root, 3);
    root = add(root, 11);
    root = add(root, 9);
    root = add(root, 13);
    root = add(root, 21);

    int k = 2;
    System.out.print(klargestElementSum(root, k) +"\n");
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program to find sum of all elements larger
# than or equal to Kth largest element In BST
c = 0

class cNode:

    def __init__(self, data):

        self.data = data
        self.left = None
        self.right = None

# A utility function to insert a new Node
# with given key in BST
def add(root, key):

    # If the tree is empty, return a new Node
    if (root == None):
        return cNode(key)

    # Otherwise, recur down the tree
    if (root.data > key):
        root.left = add(root.left, key)

    elif(root.data < key):
        root.right = add(root.right, key)

    # return the (unchanged) Node pointer
    return root

# Function to return sum of all elements
# larger than and equal to Kth largest element
def klargestElementSumUtil(root, k):

    global c

    # Base cases
    if (root == None):
        return 0
    if (c > k):
        return 0

    # Compute sum of elements in right subtree
    ans = klargestElementSumUtil(root.right, k)

    if (c >= k):
        return ans

    # Add root's data
    ans += root.data

    # Add current Node
    c += 1

    if (c >= k):
        return ans

    # If c is less than k, return left subtree Nodes
    return ans + klargestElementSumUtil(root.left, k)

# Wrapper over klargestElementSumRec()
def klargestElementSum(root, k):

    return klargestElementSumUtil(root, k)

# Driver code
if __name__ == '__main__':

    '''
    /*    19
        /    \
       7     21
     /   \
    3     11
         /   \
        9    13
          */ '''
    root = None
    root = add(root, 19)
    root = add(root, 7)
    root = add(root, 3)
    root = add(root, 11)
    root = add(root, 9)
    root = add(root, 13)
    root = add(root, 21)

    k = 2

    print(klargestElementSum(root, k))

# This code is contributed by bgangwar59
```

## C#

```
// C# program to find Sum Of All Elements larger
// than or equal to Kth Largest Element In BST
using System;

class GFG
{

class Node
{
    public int data;
    public Node left, right;
};
static int c;

// Utility function new Node of BST
static Node cNode(int data)
{
    Node node = new Node();
    node.left = null;
    node.right = null;
    node.data = data;
    return node;
}

// A utility function to insert a new Node
// with given key in BST
static Node add(Node root, int key)
{
    // If the tree is empty, return a new Node
    if (root == null)
        return cNode(key);

    // Otherwise, recur down the tree
    if (root.data > key)
        root.left = add(root.left, key);

    else if (root.data < key)
        root.right = add(root.right, key);

    // return the (unchanged) Node pointer
    return root;
}

// function to return sum of all elements larger than
// and equal to Kth largest element
static int klargestElementSumUtil(Node root, int k)
{
    // Base cases
    if (root == null)
        return 0;
    if (c > k)
        return 0;

    // Compute sum of elements in right subtree
    int ans = klargestElementSumUtil(root.right, k);
    if (c >= k)
        return ans;

    // Add root's data
    ans += root.data;

    // Add current Node
    c++;
    if (c >= k)
        return ans;

    // If c is less than k, return left subtree Nodes
    return ans + klargestElementSumUtil(root.left, k);
}

// Wrapper over klargestElementSumRec()
static int klargestElementSum(Node root, int k)
{
    c = 0;
    return klargestElementSumUtil(root, k);
}

// Drivers code
public static void Main(String[] args)
{
    /* 19
        / \
    7     21
    / \
    3     11
        / \
        9 13
        */

    Node root = null;
    root = add(root, 19);
    root = add(root, 7);
    root = add(root, 3);
    root = add(root, 11);
    root = add(root, 9);
    root = add(root, 13);
    root = add(root, 21);

    int k = 2;
    Console.Write(klargestElementSum(root, k) +"\n");
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript program to find Sum
// Of All Elements larger than or
// equal to Kth Largest Element In BST
class Node
{
    constructor(data)
    {
        this.left = null;
        this.right = null;
        this.data = data;
    }
}

let c;

// Utility function new Node of BST
function cNode(data)
{
    let node = new Node(data);

    return node;
}

// A utility function to insert a new Node
// with given key in BST
function add(root, key)
{

    // If the tree is empty, return a new Node
    if (root == null)
        return cNode(key);

    // Otherwise, recur down the tree
    if (root.data > key)
        root.left = add(root.left, key);

    else if (root.data < key)
        root.right = add(root.right, key);

    // Return the (unchanged) Node pointer
    return root;
}

// Function to return sum of all elements
// larger than and equal to Kth largest element
function klargestElementSumUtil(root, k)
{

    // Base cases
    if (root == null)
        return 0;
    if (c > k)
        return 0;

    // Compute sum of elements in right subtree
    let ans = klargestElementSumUtil(root.right, k);
    if (c >= k)
        return ans;

    // Add root's data
    ans += root.data;

    // Add current Node
    c++;
    if (c >= k)
        return ans;

    // If c is less than k, return left subtree Nodes
    return ans + klargestElementSumUtil(root.left, k);
}

// Wrapper over klargestElementSumRec()
function klargestElementSum(root, k)
{
    c = 0;
    return klargestElementSumUtil(root, k);
}

// Driver code
/* 19
    / \
7     21
/ \
3     11
    / \
    9 13
    */

let root = null;
root = add(root, 19);
root = add(root, 7);
root = add(root, 3);
root = add(root, 11);
root = add(root, 9);
root = add(root, 13);
root = add(root, 21);

let k = 2;
document.write(
    klargestElementSum(root, k) + "</br>");

// This code is contributed by divyeshrabadiya07

</script>
```

**输出:**

```
40
```