# 检查给定的二叉树是否是偏斜二叉树？

> 原文:[https://www . geesforgeks . org/check-给定的二叉树是否是偏斜的二叉树/](https://www.geeksforgeeks.org/check-whether-a-given-binary-tree-is-skewed-binary-tree-or-not/)

给定一棵二叉树，检查它是否是偏斜二叉树。倾斜树是每个节点只有一个子节点或没有子节点的树。
**例:**

```
Input :         5
             /   
            4
              \
               3
             /
           2
Output : Yes

Input :       5
            /
           4
            \
             3
           /  \
          2    4
Output : No
```

这个想法是检查一个节点是否有两个子节点。如果节点有两个子节点，则返回 false，否则递归计算有一个子节点的子树是否为斜树。如果节点是叶节点，则返回 true。
以下是上述方法的实施:

## C++

```
// C++ program to Check whether a given
// binary tree is skewed binary tree or not?

#include <bits/stdc++.h>
using namespace std;

// A Tree node
struct Node {
    int key;
    struct Node *left, *right;
};

// Utility function to create a new node
Node* newNode(int key)
{
    Node* temp = new Node;
    temp->key = key;
    temp->left = temp->right = NULL;
    return (temp);
}

bool isSkewedBT(Node* root)
{
    // check if node is NULL or is a leaf node
    if (root == NULL || (root->left == NULL &&
                        root->right == NULL))
        return true;

    // check if node has two children if
    // yes, return false
    if (root->left && root->right)
        return false;
    if (root->left)
        return isSkewedBT(root->left);
    return isSkewedBT(root->right);
}

// Driver program
int main()
{
    /*   10
       /     \
     12       13
           /     \
         14       15   
        /   \     /  \
       21   22   23   24          
    Let us create Binary Tree shown in above example */
    Node* root = newNode(10);
    root->left = newNode(12);
    root->left->right = newNode(15);
    cout << isSkewedBT(root) << endl;

    root = newNode(5);
    root->right = newNode(4);
    root->right->left = newNode(3);
    root->right->left->right = newNode(2);
    cout << isSkewedBT(root) << endl;

    root = newNode(5);
    root->left = newNode(4);
    root->left->right = newNode(3);
    root->left->right->left = newNode(2);
    root->left->right->right = newNode(4);
    cout << isSkewedBT(root) << endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Check whether a given
// binary tree is skewed binary tree or not?

class Solution
{
// A Tree node
 static class Node {
    int key;
     Node left, right;
}

// Utility function to create a new node
static Node newNode(int key)
{
    Node temp = new Node();
    temp.key = key;
    temp.left = temp.right = null;
    return (temp);
}

static boolean isSkewedBT(Node root)
{
    // check if node is null or is a leaf node
    if (root == null || (root.left == null &&
                        root.right == null))
        return true;

    // check if node has two children if
    // yes, return false
    if (root.left!=null && root.right!=null)
        return false;
    if (root.left!=null)
        return isSkewedBT(root.left);
    return isSkewedBT(root.right);
}

// Driver program
public static void main(String args[])
{
    /* 10
    /     \
    12     13
        /     \
        14     15    
        / \     / \
    21 22 23 24        
    Let us create Binary Tree shown in above example */
    Node root = newNode(10);
    root.left = newNode(12);
    root.left.right = newNode(15);
    System.out.println( isSkewedBT(root)?1:0 );

    root = newNode(5);
    root.right = newNode(4);
    root.right.left = newNode(3);
    root.right.left.right = newNode(2);
    System.out.println( isSkewedBT(root)?1:0 );

    root = newNode(5);
    root.left = newNode(4);
    root.left.right = newNode(3);
    root.left.right.left = newNode(2);
    root.left.right.right = newNode(4);
    System.out.println(  isSkewedBT(root)?1:0 );
}
}
//contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 program to Check whether a given
# binary tree is skewed binary tree or not?

# Binary Tree Node
""" utility that allocates a newNode
with the given key """
class newNode:

    # Construct to create a newNode
    def __init__(self, key):
        self.data = key
        self.left = None
        self.right = None

def isSkewedBT(root):

    # check if node is None or is a leaf node
    if (root == None or (root.left == None and
                         root.right == None)):
        return 1

    # check if node has two children if
    # yes, return false
    if (root.left and root.right):
        return 0
    if (root.left) :
        return isSkewedBT(root.left)
    return isSkewedBT(root.right)

# Driver Code
if __name__ == '__main__':

    """ 10
    /     \
    12     13
        /     \
        14     15    
        / \     / \
    21 22 23 24        
    Let us create Binary Tree shown in above example """
    root = newNode(10)
    root.left = newNode(12)
    root.left.right = newNode(15)
    print(isSkewedBT(root))

    root = newNode(5)
    root.right = newNode(4)
    root.right.left = newNode(3)
    root.right.left.right = newNode(2)
    print(isSkewedBT(root))

    root = newNode(5)
    root.left = newNode(4)
    root.left.right = newNode(3)
    root.left.right.left = newNode(2)
    root.left.right.right = newNode(4)
    print(isSkewedBT(root))

# This code is contributed by
# Shubham Singh(SHUBHAMSINGH10)
```

## C#

```
// C# program to Check whether a given
// binary tree is skewed binary tree or not?
using System;

public class GFG
{

// A Tree node
class Node
{
    public int key;
    public Node left, right;
}

// Utility function to create a new node
static Node newNode(int key)
{
    Node temp = new Node();
    temp.key = key;
    temp.left = temp.right = null;
    return (temp);
}

static bool isSkewedBT(Node root)
{
    // check if node is null or is a leaf node
    if (root == null || (root.left == null &&
                        root.right == null))
        return true;

    // check if node has two children if
    // yes, return false
    if (root.left!=null && root.right!=null)
        return false;
    if (root.left!=null)
        return isSkewedBT(root.left);
    return isSkewedBT(root.right);
}

// Driver code
public static void Main()
{
    /* 10
    / \
    12 13
        / \
        14 15
        / \ / \
    21 22 23 24
    Let us create Binary Tree shown in above example */
    Node root = newNode(10);
    root.left = newNode(12);
    root.left.right = newNode(15);
    Console.WriteLine( isSkewedBT(root)?1:0 );

    root = newNode(5);
    root.right = newNode(4);
    root.right.left = newNode(3);
    root.right.left.right = newNode(2);
    Console.WriteLine( isSkewedBT(root)?1:0 );

    root = newNode(5);
    root.left = newNode(4);
    root.left.right = newNode(3);
    root.left.right.left = newNode(2);
    root.left.right.right = newNode(4);
    Console.WriteLine( isSkewedBT(root)?1:0 );
}
}

/* This code is contributed by Rajput-Ji*/
```

## java 描述语言

```
<script>
    // Javascript program to Check whether a given
    // binary tree is skewed binary tree or not?

    // Binary tree node
    class Node
    {
        constructor(key) {
           this.left = null;
           this.right = null;
           this.data = key;
        }
    }

    // Utility function to create a new node
    function newNode(key)
    {
        let temp = new Node(key);
        return (temp);
    }

    function isSkewedBT(root)
    {
        // check if node is null or is a leaf node
        if (root == null || (root.left == null &&
                            root.right == null))
            return true;

        // check if node has two children if
        // yes, return false
        if (root.left!=null && root.right!=null)
            return false;
        if (root.left!=null)
            return isSkewedBT(root.left);
        return isSkewedBT(root.right);
    }

    /* 10
    /     \
    12     13
        /     \
        14     15    
        / \     / \
    21 22 23 24        
    Let us create Binary Tree shown in above example */
    let root = newNode(10);
    root.left = newNode(12);
    root.left.right = newNode(15);
    document.write(isSkewedBT(root)?1 + "</br>":0 + "</br>");

    root = newNode(5);
    root.right = newNode(4);
    root.right.left = newNode(3);
    root.right.left.right = newNode(2);
    document.write(isSkewedBT(root)?1 + "</br>":0 + "</br>");

    root = newNode(5);
    root.left = newNode(4);
    root.left.right = newNode(3);
    root.left.right.left = newNode(2);
    root.left.right.right = newNode(4);
    document.write(isSkewedBT(root)?1 + "</br>":0 + "</br>");

 // This code is contributed by decode2207.
</script>
```

**Output:** 

```
1
1
0
```

该解的时间复杂度为
最佳情况:当 root 有两个子节点时为 O(1)。
最坏情况:当树是斜树时为 0(h)。