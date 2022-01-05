# 最小绝对差配对| BST

> 原文:[https://www . geesforgeks . org/pair-with-mini-绝对值差-bst/](https://www.geeksforgeeks.org/pair-with-minimum-absolute-difference-bst/)

给定一个大小为 **N > 1** 的[二叉查找树](http://www.geeksforgeeks.org/binary-search-tree-set-1-search-and-insertion/)，任务是找到任意两个节点之间的最小绝对差。

**示例:**

```
Input: 
          5 
        /   \ 
       3     7 
      / \   / \ 
     2   4 6   8
Output: 1
Difference between all the consecutive nodes if sorted is 1.
Thus, the answer is 1.

Input:
     1
      \
       6
Output: 5
```

**方法:**我们知道二叉查找树的有序遍历是按排序顺序遍历的。因此，对于每个节点，我们将在树的有序遍历中找到它与前一个节点的区别。如果这个差值小于之前的最小差值，我们将更新之前的最小差值。以下是要遵循的步骤:

1.  创建一个变量“prev”来存储指向有序遍历中前一个节点的指针。
2.  创建一个变量“ans”来存储最小差异。
3.  对于有序遍历中的每个节点，将其绝对差值与前一个节点进行比较，并更新到目前为止找到的最小绝对差值。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Node of the binary tree
struct node {
    int data;
    node* left;
    node* right;
    node(int data)
    {
        this->data = data;
        left = NULL;
        right = NULL;
    }
};

// Function for in-order traversal of the tree
void inorder(node* curr, node*& prev, int& ans)
{

    // Base-case
    if (curr == NULL)
        return;

    // Calling in-order on the left sub-tree
    inorder(curr->left, prev, ans);

    if (prev != NULL)
        ans = min(curr->data - prev->data, ans);
    prev = curr;

    // Calling in-order on the right sub-tree
    inorder(curr->right, prev, ans);
}

// Function to return the minimum
// difference between any two nodes
// of the given binary search tree
int minDiff(node* root)
{

    // Pointer to previous node in the
    // in-order traversal of the BST
    node* prev = NULL;

    // To store the final ans
    int ans = INT_MAX;

    // Call in-order for the BST
    inorder(root, prev, ans);

    // Returning the final answer
    return ans;
}

// Driver code
int main()
{
    node* root = new node(5);
    root->left = new node(3);
    root->right = new node(7);
    root->left->left = new node(2);
    root->left->right = new node(4);
    root->right->left = new node(6);
    root->right->right = new node(8);

    cout << minDiff(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Node of the binary tree
static class node
{
    int data;
    node left;
    node right;
    node(int data)
    {
        this.data = data;
        left = null;
        right = null;
    }
};
static node prev;
static int ans;

// Function for in-order traversal of the tree
static void inorder(node curr)
{

    // Base-case
    if (curr == null)
        return;

    // Calling in-order on the left sub-tree
    inorder(curr.left);

    if (prev != null)
        ans = Math.min(curr.data -
                       prev.data, ans);
    prev = curr;

    // Calling in-order on the right sub-tree
    inorder(curr.right);
}

// Function to return the minimum
// difference between any two nodes
// of the given binary search tree
static int minDiff(node root)
{

    // Pointer to previous node in the
    // in-order traversal of the BST
    prev = null;

    // To store the final ans
    ans = Integer.MAX_VALUE;

    // Call in-order for the BST
    inorder(root);

    // Returning the final answer
    return ans;
}

// Driver code
public static void main(String[] args)
{
    node root = new node(5);
    root.left = new node(3);
    root.right = new node(7);
    root.left.left = new node(2);
    root.left.right = new node(4);
    root.right.left = new node(6);
    root.right.right = new node(8);

    System.out.println(minDiff(root));
}
}

// This code is contributed by 29AjayKumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Node of the binary tree
public class node
{
    public int data;
    public node left;
    public node right;
    public node(int data)
    {
        this.data = data;
        left = null;
        right = null;
    }
};
static node prev;
static int ans;

// Function for in-order traversal of the tree
static void inorder(node curr)
{

    // Base-case
    if (curr == null)
        return;

    // Calling in-order on the left sub-tree
    inorder(curr.left);

    if (prev != null)
        ans = Math.Min(curr.data -
                       prev.data, ans);
    prev = curr;

    // Calling in-order on the right sub-tree
    inorder(curr.right);
}

// Function to return the minimum
// difference between any two nodes
// of the given binary search tree
static int minDiff(node root)
{

    // Pointer to previous node in the
    // in-order traversal of the BST
    prev = null;

    // To store the final ans
    ans = int.MaxValue;

    // Call in-order for the BST
    inorder(root);

    // Returning the final answer
    return ans;
}

// Driver code
public static void Main(String[] args)
{
    node root = new node(5);
    root.left = new node(3);
    root.right = new node(7);
    root.left.left = new node(2);
    root.left.right = new node(4);
    root.right.left = new node(6);
    root.right.right = new node(8);

    Console.WriteLine(minDiff(root));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Node of the binary tree
class node
{
    constructor(data)
    {
        this.data = data;
        this.left = null;
        this.right = null;
    }
};

var prev = null;
var ans =0;

// Function for in-order traversal of the tree
function inorder(curr)
{

    // Base-case
    if (curr == null)
        return;

    // Calling in-order on the left sub-tree
    inorder(curr.left);

    if (prev != null)
        ans = Math.min(curr.data -
                       prev.data, ans);
    prev = curr;

    // Calling in-order on the right sub-tree
    inorder(curr.right);
}

// Function to return the minimum
// difference between any two nodes
// of the given binary search tree
function minDiff(root)
{

    // Pointer to previous node in the
    // in-order traversal of the BST
    prev = null;

    // To store the final ans
    ans = 10000000000;

    // Call in-order for the BST
    inorder(root);

    // Returning the final answer
    return ans;
}

// Driver code
var root = new node(5);
root.left = new node(3);
root.right = new node(7);
root.left.left = new node(2);
root.left.right = new node(4);
root.right.left = new node(6);
root.right.right = new node(8);

document.write(minDiff(root));

// This code is contributed by noob2000

</script>
```

## 蟒蛇 3

```
# Python 3 implementation of the approach
import math
# Node of the binary tree

class node:
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# Function for in-order traversal of the tree

def inorder(curr, prev):
    global ans

    # Base-case
    if (curr == None):
        return

    # Calling in-order on the left sub-tree
    inorder(curr.left, prev)

    if (prev != None):
        ans = min(curr.data - prev.data, ans)
    prev = curr

    # Calling in-order on the right sub-tree
    inorder(curr.right, prev)

# Function to return the minimum
# difference between any two nodes
# of the given binary search tree

def minDiff(root):

    # Pointer to previous node in the
    # in-order traversal of the BST
    prev = None

    # To store the final ans
    global ans
    ans = math.inf

    # Call in-order for the BST
    inorder(root, prev)

    # Returning the final answer
    return ans

# Driver code
if __name__ == '__main__':

    root = node(5)
    root.left = node(3)
    root.right = node(7)
    root.left.left = node(2)
    root.left.right = node(4)
    root.right.left = node(6)
    root.right.right = node(8)

    print(minDiff(root))
```

**Output**

```
1
```

**另一种具有 O(N)空间复杂度的方法:**

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Node of the binary tree
import math
class Node: 

    # Constructor to create a new node 
    def __init__(self, data): 
        self.data = data 
        self.left = None
        self.right = None
#Set the target to infinity
target=math.inf 
#Function to find the minimum absolute difference
def absolute_diff(root,target):
    if root is None:
        return target

    if root.left is not None:
        left=root.data-root.left.data
        target=min(target,left)
    if root.right is not None:
        right=root.right.data-root.data
        target=min(target,right)
    #Find the minimum in the left subtree
    p=absolute_diff(root.left,target)
    #Find the minimum in the right subtree
    q=absolute_diff(root.right,target)
    return min(p,q)

// Driver code
root=Node(5)
root.left =  Node(3)
root.right = Node(7)
root.left.left =  Node(2)
root.left.right =  Node(4)
root.right.left =  Node(6)
root.right.right = Node(8)
print(absolute_diff(root,target))
```

**Output:** 

```
1
```

**时间复杂度:**O(N)
T3】额外空间: O(N)由于递归。