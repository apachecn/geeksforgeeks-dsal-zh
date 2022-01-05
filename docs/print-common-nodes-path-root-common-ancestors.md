# 打印从根(或公共祖先)开始的路径上的公共节点

> 原文:[https://www . geesforgeks . org/print-common-nodes-path-root-common-predents/](https://www.geeksforgeeks.org/print-common-nodes-path-root-common-ancestors/)

给定一个二叉树和两个节点，任务是打印二叉树中两个给定节点的所有公共节点。

**示例:**

```
Given binary tree is :
                     1
                  /    \
                2       3
              /   \     /  \
             4     5   6    7
            /        /  \
           8        9   10

Given nodes 9 and 7, so the common nodes are:-
1, 3
```

问于:[亚马逊](https://www.geeksforgeeks.org/amazon-interview-experience-set-341-off-campus-sde-1/)

1.  求给定两个节点的 [LCA](https://www.geeksforgeeks.org/lowest-common-ancestor-binary-tree-set-1/) 。
2.  打印 LCA 的所有祖先，如本[帖](https://www.geeksforgeeks.org/print-ancestors-of-a-given-node-in-binary-tree/)所做的，也打印 LCA。

## C++

```
// C++ Program to find common nodes for given two nodes
#include <bits/stdc++.h>
using namespace std;

// A Binary Tree Node
struct Node {
    struct Node* left, *right;
    int key;
};

// Utility function to create a new tree Node
Node* newNode(int key)
{
    Node* temp = new Node;
    temp->key = key;
    temp->left = temp->right = NULL;
    return temp;
}

// Utility function to find the LCA of two given values
// n1 and n2.
struct Node* findLCA(struct Node* root, int n1, int n2)
{
    // Base case
    if (root == NULL)
        return NULL;

    // If either n1 or n2 matches with root's key,
    // report the presence by returning root (Note
    // that if a key is ancestor of other, then the
    // ancestor key becomes LCA
    if (root->key == n1 || root->key == n2)
        return root;

    // Look for keys in left and right subtrees
    Node* left_lca = findLCA(root->left, n1, n2);
    Node* right_lca = findLCA(root->right, n1, n2);

    // If both of the above calls return Non-NULL, then
    // one key  is present in once subtree and other is
    // present in other, So this node is the LCA
    if (left_lca && right_lca)
        return root;

    // Otherwise check if left subtree or right
    // subtree is LCA
    return (left_lca != NULL) ? left_lca : right_lca;
}

// Utility Function to print all ancestors of LCA
bool printAncestors(struct Node* root, int target)
{
    /* base cases */
    if (root == NULL)
        return false;

    if (root->key == target) {
        cout << root->key << " ";
        return true;
    }

    /* If target is present in either left or right
      subtree of this node, then print this node */
    if (printAncestors(root->left, target) ||
        printAncestors(root->right, target)) {
        cout << root->key << " ";
        return true;
    }

    /* Else return false */
    return false;
}

// Function to find nodes common to given two nodes
bool findCommonNodes(struct Node* root, int first,
                                       int second)
{
    struct Node* LCA = findLCA(root, first, second);
    if (LCA == NULL)
        return false;

    printAncestors(root, LCA->key);
}

// Driver program to test above functions
int main()
{
    // Let us create binary tree given in the above
    // example
    Node* root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->left->right = newNode(5);
    root->right->left = newNode(6);
    root->right->right = newNode(7);
    root->left->left->left = newNode(8);
    root->right->left->left = newNode(9);
    root->right->left->right = newNode(10);

    if (findCommonNodes(root, 9, 7) == false)
        cout << "No Common nodes";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find common nodes for given two nodes
import java.util.LinkedList;

// Class to represent Tree node
class Node
{
    int data;
    Node left, right;

    public Node(int item)
    {
        data = item;
        left = null;
        right = null;
    }
}

// Class to count full nodes of Tree
class BinaryTree
{
    static Node root;
// Utility function to find the LCA of two given values
// n1 and n2.
static Node findLCA(Node root, int n1, int n2)
{
    // Base case
    if (root == null)
        return null;

    // If either n1 or n2 matches with root's key,
    // report the presence by returning root (Note
    // that if a key is ancestor of other, then the
    // ancestor key becomes LCA
    if (root.data == n1 || root.data == n2)
        return root;

    // Look for keys in left and right subtrees
    Node left_lca = findLCA(root.left, n1, n2);
    Node right_lca = findLCA(root.right, n1, n2);

    // If both of the above calls return Non-NULL, then
    // one key is present in once subtree and other is
    // present in other, So this node is the LCA
    if (left_lca!=null && right_lca!=null)
        return root;

    // Otherwise check if left subtree or right
    // subtree is LCA
    return (left_lca != null) ? left_lca : right_lca;
}

// Utility Function to print all ancestors of LCA
static boolean printAncestors(Node root, int target)
{
    /* base cases */
    if (root == null)
        return false;

    if (root.data == target) {
        System.out.print(root.data+ " ");
        return true;
    }

    /* If target is present in either left or right
    subtree of this node, then print this node */
    if (printAncestors(root.left, target) ||
        printAncestors(root.right, target)) {
        System.out.print(root.data+ " ");
        return true;
    }

    /* Else return false */
    return false;
}

// Function to find nodes common to given two nodes
static boolean findCommonNodes(Node root, int first,
                                    int second)
{
    Node LCA = findLCA(root, first, second);
    if (LCA == null)
        return false;

    printAncestors(root, LCA.data);
    return true;
}

// Driver program to test above functions
    public static void main(String args[])
    {
    /*Let us create Binary Tree shown in
        above example */

        BinaryTree tree = new BinaryTree();
        tree.root = new Node(1);
        tree.root.left = new Node(2);
        tree.root.right = new Node(3);
        tree.root.left.left = new Node(4);
        tree.root.left.right = new Node(5);
        tree.root.right.left = new Node(6);
        tree.root.right.right = new Node(7);
        tree.root.left.left.left = new Node(8);
        tree.root.right.left.left = new Node(9);
        tree.root.right.left.right = new Node(10);

   if (findCommonNodes(root, 9, 7) == false)
    System.out.println("No Common nodes");

    }
}

// This code is contributed by Mr Somesh Awasthi
```

## 蟒蛇 3

```
# Python3 Program to find common
# nodes for given two nodes

# Utility class to create a new tree Node
class newNode:
    def __init__(self, key):
        self.key = key
        self.left = self.right = None

# Utility function to find the LCA of
# two given values n1 and n2.
def findLCA(root, n1, n2):

    # Base case
    if (root == None):
        return None

    # If either n1 or n2 matches with root's key,
    # report the presence by returning root (Note
    # that if a key is ancestor of other, then the
    # ancestor key becomes LCA
    if (root.key == n1 or root.key == n2):
        return root

    # Look for keys in left and right subtrees
    left_lca = findLCA(root.left, n1, n2)
    right_lca = findLCA(root.right, n1, n2)

    # If both of the above calls return Non-None,
    # then one key is present in once subtree and
    # other is present in other, So this node is the LCA
    if (left_lca and right_lca):
        return root

    # Otherwise check if left subtree or
    # right subtree is LCA
    if (left_lca != None):
        return left_lca
    else:
        return right_lca

# Utility Function to print all ancestors of LCA
def printAncestors(root, target):

    # base cases
    if (root == None):
        return False

    if (root.key == target):
        print(root.key, end = " ")
        return True

    # If target is present in either left or right
    # subtree of this node, then prthis node
    if (printAncestors(root.left, target) or
        printAncestors(root.right, target)):
            print(root.key, end = " ")
            return True

    # Else return False
    return False

# Function to find nodes common to given two nodes
def findCommonNodes(root, first, second):
    LCA = findLCA(root, first, second)
    if (LCA == None):
        return False

    printAncestors(root, LCA.key)

# Driver Code
if __name__ == '__main__':

    # Let us create binary tree given
    # in the above example
    root = newNode(1)
    root.left = newNode(2)
    root.right = newNode(3)
    root.left.left = newNode(4)
    root.left.right = newNode(5)
    root.right.left = newNode(6)
    root.right.right = newNode(7)
    root.left.left.left = newNode(8)
    root.right.left.left = newNode(9)
    root.right.left.right = newNode(10)

    if (findCommonNodes(root, 9, 7) == False):
        print("No Common nodes")

# This code is contributed by PranchalK
```

## C#

```
using System;

// C# Program to find common nodes for given two nodes

// Class to represent Tree node
public class Node
{
    public int data;
    public Node left, right;

    public Node(int item)
    {
        data = item;
        left = null;
        right = null;
    }
}

// Class to count full nodes of Tree
public class BinaryTree
{
    public static Node root;
// Utility function to find the LCA of two given values
// n1 and n2.
public static Node findLCA(Node root, int n1, int n2)
{
    // Base case
    if (root == null)
    {
        return null;
    }

    // If either n1 or n2 matches with root's key,
    // report the presence by returning root (Note
    // that if a key is ancestor of other, then the
    // ancestor key becomes LCA
    if (root.data == n1 || root.data == n2)
    {
        return root;
    }

    // Look for keys in left and right subtrees
    Node left_lca = findLCA(root.left, n1, n2);
    Node right_lca = findLCA(root.right, n1, n2);

    // If both of the above calls return Non-NULL, then
    // one key is present in once subtree and other is
    // present in other, So this node is the LCA
    if (left_lca != null && right_lca != null)
    {
        return root;
    }

    // Otherwise check if left subtree or right
    // subtree is LCA
    return (left_lca != null) ? left_lca : right_lca;
}

// Utility Function to print all ancestors of LCA
public static bool printAncestors(Node root, int target)
{
    /* base cases */
    if (root == null)
    {
        return false;
    }

    if (root.data == target)
    {
        Console.Write(root.data + " ");
        return true;
    }

    /* If target is present in either left or right
    subtree of this node, then print this node */
    if (printAncestors(root.left, target)
    || printAncestors(root.right, target))
    {
        Console.Write(root.data + " ");
        return true;
    }

    /* Else return false */
    return false;
}

// Function to find nodes common to given two nodes
public static bool findCommonNodes(Node root,
                            int first, int second)
{
    Node LCA = findLCA(root, first, second);
    if (LCA == null)
    {
        return false;
    }

    printAncestors(root, LCA.data);
    return true;
}

// Driver program to test above functions
    public static void Main(string[] args)
    {
    /*Let us create Binary Tree shown in
        above example */

        BinaryTree tree = new BinaryTree();
        BinaryTree.root = new Node(1);
        BinaryTree.root.left = new Node(2);
        BinaryTree.root.right = new Node(3);
        BinaryTree.root.left.left = new Node(4);
        BinaryTree.root.left.right = new Node(5);
        BinaryTree.root.right.left = new Node(6);
        BinaryTree.root.right.right = new Node(7);
        BinaryTree.root.left.left.left = new Node(8);
        BinaryTree.root.right.left.left = new Node(9);
        BinaryTree.root.right.left.right = new Node(10);

if (findCommonNodes(root, 9, 7) == false)
{
    Console.WriteLine("No Common nodes");
}

    }
}

// This code is contributed by Shrikant13
```

## java 描述语言

```
<script>

// Javascript program to find common
// nodes for given two nodes
class Node
{
    constructor(data)
    {
        this.left = null;
        this.right = null;
        this.data = data;
    }
}

let root;

// Utility function to find the LCA of
// two given values n1 and n2.
function findLCA(root, n1, n2)
{

    // Base case
    if (root == null)
        return null;

    // If either n1 or n2 matches with root's key,
    // report the presence by returning root (Note
    // that if a key is ancestor of other, then the
    // ancestor key becomes LCA
    if (root.data == n1 || root.data == n2)
        return root;

    // Look for keys in left and right subtrees
    let left_lca = findLCA(root.left, n1, n2);
    let right_lca = findLCA(root.right, n1, n2);

    // If both of the above calls return Non-NULL, then
    // one key is present in once subtree and other is
    // present in other, So this node is the LCA
    if (left_lca!=null && right_lca!=null)
        return root;

    // Otherwise check if left subtree or right
    // subtree is LCA
    return (left_lca != null) ? left_lca : right_lca;
}

// Utility Function to print all ancestors of LCA
function printAncestors(root, target)
{

    // Base cases
    if (root == null)
        return false;

    if (root.data == target)
    {
        document.write(root.data + " ");
        return true;
    }

    // If target is present in either left or right
    // subtree of this node, then print this node
    if (printAncestors(root.left, target) ||
        printAncestors(root.right, target))
    {
        document.write(root.data+ " ");
        return true;
    }

    // Else return false
    return false;
}

// Function to find nodes common to given two nodes
function findCommonNodes(root, first, second)
{
    let LCA = findLCA(root, first, second);
    if (LCA == null)
        return false;

    printAncestors(root, LCA.data);
    return true;
}

// Driver code
root = new Node(1);
root.left = new Node(2);
root.right = new Node(3);
root.left.left = new Node(4);
root.left.right = new Node(5);
root.right.left = new Node(6);
root.right.right = new Node(7);
root.left.left.left = new Node(8);
root.right.left.left = new Node(9);
root.right.left.right = new Node(10);

if (findCommonNodes(root, 9, 7) == false)
    document.write("No Common nodes");

// This code is contributed by divyeshrabadiya07

</script>
```

**输出:**

```
3 1
```

本文由 [**萨哈布拉**](https://www.facebook.com/sahil.chhabra.965) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。