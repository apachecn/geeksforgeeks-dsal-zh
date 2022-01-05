# BST 中两个节点之间的最短距离

> 原文:[https://www . geesforgeks . org/BST 中两个节点之间的最短距离/](https://www.geeksforgeeks.org/shortest-distance-between-two-nodes-in-bst/)

给定一把二叉查找树和两把钥匙。用给定的两个键找到两个节点之间的距离。可以假设两个键都存在于 BST 中。

![BST](img/6deded3c0776376a6dce32cc6717dcbf.png)

**示例:**

```
Input:  Root of above tree
         a = 3, b = 9
Output: 4
Distance between 3 and 9 in 
above BST is 4.

Input: Root of above tree
         a = 9, b = 25
Output: 3
Distance between 9 and 25 in 
above BST is 3.
```

我们已经讨论了二叉树中两个节点之间的[距离。这个解的时间复杂度是 O(n)
在 BST 的情况下，我们可以更快的找到距离。我们从根开始，对于每个节点，我们执行以下操作。](https://www.geeksforgeeks.org/find-distance-between-two-nodes-of-a-binary-tree/)

1.  如果两个键都大于当前节点，我们将移动到当前节点的右子节点。
2.  如果两个键都小于当前节点，我们就移到当前节点的左子节点。
3.  如果一个键较小，另一个键较大，则当前节点是两个节点的最低公共祖先。我们从两个键找到当前节点的距离，并返回这些距离的和。

## C++

```
// CPP program to find distance between
// two nodes in BST
#include <bits/stdc++.h>
using namespace std;

struct Node {
    struct Node* left, *right;
    int key;
};

struct Node* newNode(int key)
{
    struct Node* ptr = new Node;
    ptr->key = key;
    ptr->left = ptr->right = NULL;
    return ptr;
}

// Standard BST insert function
struct Node* insert(struct Node* root, int key)
{
    if (!root)
        root = newNode(key);
    else if (root->key > key)
        root->left = insert(root->left, key);
    else if (root->key < key)
        root->right = insert(root->right, key);
    return root;
}

// This function returns distance of x from
// root. This function assumes that x exists
// in BST and BST is not NULL.
int distanceFromRoot(struct Node* root, int x)
{
    if (root->key == x)
        return 0;
    else if (root->key > x)
        return 1 + distanceFromRoot(root->left, x);
    return 1 + distanceFromRoot(root->right, x);
}

// Returns minimum distance between a and b.
// This function assumes that a and b exist
// in BST.
int distanceBetween2(struct Node* root, int a, int b)
{
    if (!root)
        return 0;

    // Both keys lie in left
    if (root->key > a && root->key > b)
        return distanceBetween2(root->left, a, b);

    // Both keys lie in right
    if (root->key < a && root->key < b) // same path
        return distanceBetween2(root->right, a, b);

    // Lie in opposite directions (Root is
    // LCA of two nodes)
    if (root->key >= a && root->key <= b)
        return distanceFromRoot(root, a) +
               distanceFromRoot(root, b);
}

// This function make sure that a is smaller
// than b before making a call to findDistWrapper()
int findDistWrapper(Node *root, int a, int b)
{
   if (a > b)
     swap(a, b);
   return distanceBetween2(root, a, b);  
}

// Driver code
int main()
{
    struct Node* root = NULL;
    root = insert(root, 20);
    insert(root, 10);
    insert(root, 5);
    insert(root, 15);
    insert(root, 30);
    insert(root, 25);
    insert(root, 35);
    int a = 5, b = 55;
    cout << findDistWrapper(root, 5, 35);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find distance between
// two nodes in BST
class GfG {

static class Node {
    Node left, right;
    int key;
}

static Node newNode(int key)
{
    Node ptr = new Node();
    ptr.key = key;
    ptr.left = null;
    ptr.right = null;
    return ptr;
}

// Standard BST insert function
static Node insert(Node root, int key)
{
    if (root == null)
        root = newNode(key);
    else if (root.key > key)
        root.left = insert(root.left, key);
    else if (root.key < key)
        root.right = insert(root.right, key);
    return root;
}

// This function returns distance of x from
// root. This function assumes that x exists
// in BST and BST is not NULL.
static int distanceFromRoot(Node root, int x)
{
    if (root.key == x)
        return 0;
    else if (root.key > x)
        return 1 + distanceFromRoot(root.left, x);
    return 1 + distanceFromRoot(root.right, x);
}

// Returns minimum distance between a and b.
// This function assumes that a and b exist
// in BST.
static int distanceBetween2(Node root, int a, int b)
{
    if (root == null)
        return 0;

    // Both keys lie in left
    if (root.key > a && root.key > b)
        return distanceBetween2(root.left, a, b);

    // Both keys lie in right
    if (root.key < a && root.key < b) // same path
        return distanceBetween2(root.right, a, b);

    // Lie in opposite directions (Root is
    // LCA of two nodes)
    if (root.key >= a && root.key <= b)
        return distanceFromRoot(root, a) + distanceFromRoot(root, b);

    return 0;
}

// This function make sure that a is smaller
// than b before making a call to findDistWrapper()
static int findDistWrapper(Node root, int a, int b)
{
    int temp = 0;
if (a > b)
    {
    temp = a;
    a = b;
    b = temp;
    }
return distanceBetween2(root, a, b);
}

// Driver code
public static void main(String[] args)
{
    Node root = null;
    root = insert(root, 20);
    insert(root, 10);
    insert(root, 5);
    insert(root, 15);
    insert(root, 30);
    insert(root, 25);
    insert(root, 35);
    System.out.println(findDistWrapper(root, 5, 35));
}
}
```

## 蟒蛇 3

```
# Python3 program to find distance between
# two nodes in BST
class newNode:

    # Constructor to create a new node
    def __init__(self, data):
        self.key = data
        self.left = None
        self.right = None

# Standard BST insert function
def insert(root, key):
    if root == None:
        root = newNode(key)
    elif root.key > key:
        root.left = insert(root.left, key)
    elif root.key < key:
        root.right = insert(root.right, key)
    return root

# This function returns distance of x from
# root. This function assumes that x exists
# in BST and BST is not NULL.
def distanceFromRoot(root, x):
    if root.key == x:
        return 0
    elif root.key > x:
        return 1 + distanceFromRoot(root.left, x)
    return 1 + distanceFromRoot(root.right, x)

# Returns minimum distance between a and b.
# This function assumes that a and b exist
# in BST.
def distanceBetween2(root, a, b):
    if root == None:
        return 0

    # Both keys lie in left
    if root.key > a and root.key > b:
        return distanceBetween2(root.left, a, b)

    # Both keys lie in right
    if root.key < a and root.key < b: # same path
        return distanceBetween2(root.right, a, b)

    # Lie in opposite directions
    # (Root is LCA of two nodes)
    if root.key >= a and root.key <= b:
        return (distanceFromRoot(root, a) +
                distanceFromRoot(root, b))

# This function make sure that a is smaller
# than b before making a call to findDistWrapper()
def findDistWrapper(root, a, b):
    if a > b:
        a, b = b, a
    return distanceBetween2(root, a, b)

# Driver code
if __name__ == '__main__':
    root = None
    root = insert(root, 20)
    insert(root, 10)
    insert(root, 5)
    insert(root, 15)
    insert(root, 30)
    insert(root, 25)
    insert(root, 35)
    a, b = 5, 55
    print(findDistWrapper(root, 5, 35))

# This code is contributed by PranchalK
```

## C#

```
// C# program to find distance between
// two nodes in BST
using System;

class GfG
{

public class Node
{
    public Node left, right;
    public int key;
}

static Node newNode(int key)
{
    Node ptr = new Node();
    ptr.key = key;
    ptr.left = null;
    ptr.right = null;
    return ptr;
}

// Standard BST insert function
static Node insert(Node root, int key)
{
    if (root == null)
        root = newNode(key);
    else if (root.key > key)
        root.left = insert(root.left, key);
    else if (root.key < key)
        root.right = insert(root.right, key);
    return root;
}

// This function returns distance of x from
// root. This function assumes that x exists
// in BST and BST is not NULL.
static int distanceFromRoot(Node root, int x)
{
    if (root.key == x)
        return 0;
    else if (root.key > x)
        return 1 + distanceFromRoot(root.left, x);
    return 1 + distanceFromRoot(root.right, x);
}

// Returns minimum distance between a and b.
// This function assumes that a and b exist
// in BST.
static int distanceBetween2(Node root, int a, int b)
{
    if (root == null)
        return 0;

    // Both keys lie in left
    if (root.key > a && root.key > b)
        return distanceBetween2(root.left, a, b);

    // Both keys lie in right
    if (root.key < a && root.key < b) // same path
        return distanceBetween2(root.right, a, b);

    // Lie in opposite directions (Root is
    // LCA of two nodes)
    if (root.key >= a && root.key <= b)
        return distanceFromRoot(root, a) +
                distanceFromRoot(root, b);

    return 0;
}

// This function make sure that a is smaller
// than b before making a call to findDistWrapper()
static int findDistWrapper(Node root, int a, int b)
{
    int temp = 0;
if (a > b)
    {
    temp = a;
    a = b;
    b = temp;
    }
return distanceBetween2(root, a, b);
}

// Driver code
public static void Main(String[] args)
{
    Node root = null;
    root = insert(root, 20);
    insert(root, 10);
    insert(root, 5);
    insert(root, 15);
    insert(root, 30);
    insert(root, 25);
    insert(root, 35);
    Console.WriteLine(findDistWrapper(root, 5, 35));
}
}

// This code contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript program to find distance between
// two nodes in BST

     class Node {
            constructor() {
                this.key = 0;
                this.left = null;
                this.right = null;
            }
        }

    function newNode(key) {
var ptr = new Node();
        ptr.key = key;
        ptr.left = null;
        ptr.right = null;
        return ptr;
    }

    // Standard BST insert function
    function insert(root , key) {
        if (root == null)
            root = newNode(key);
        else if (root.key > key)
            root.left = insert(root.left, key);
        else if (root.key < key)
            root.right = insert(root.right, key);
        return root;
    }

    // This function returns distance of x from
    // root. This function assumes that x exists
    // in BST and BST is not NULL.
    function distanceFromRoot(root , x) {
        if (root.key == x)
            return 0;
        else if (root.key > x)
            return 1 + distanceFromRoot(root.left, x);
        return 1 + distanceFromRoot(root.right, x);
    }

    // Returns minimum distance between a and b.
    // This function assumes that a and b exist
    // in BST.
    function distanceBetween2(root , a , b) {
        if (root == null)
            return 0;

        // Both keys lie in left
        if (root.key > a && root.key > b)
            return distanceBetween2(root.left, a, b);

        // Both keys lie in right
        if (root.key < a && root.key < b) // same path
            return distanceBetween2(root.right, a, b);

        // Lie in opposite directions (Root is
        // LCA of two nodes)
        if (root.key >= a && root.key <= b)
            return distanceFromRoot(root, a) +
            distanceFromRoot(root, b);

        return 0;
    }

    // This function make sure that a is smaller
    // than b before making a call to findDistWrapper()
    function findDistWrapper(root , a , b) {
        var temp = 0;
        if (a > b) {
            temp = a;
            a = b;
            b = temp;
        }
        return distanceBetween2(root, a, b);
    }

    // Driver code

        var root = null;
        root = insert(root, 20);
        insert(root, 10);
        insert(root, 5);
        insert(root, 15);
        insert(root, 30);
        insert(root, 25);
        insert(root, 35);
        document.write(findDistWrapper(root, 5, 35));

// This code is contributed by todaysgaurav

</script>
```

**输出:**

```
4
```

**时间复杂度:** O(h)，其中 h 是二叉查找树的高度。

本文由 **Shweta Singh** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。