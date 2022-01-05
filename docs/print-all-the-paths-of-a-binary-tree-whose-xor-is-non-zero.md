# 打印异或为非零的二叉树的所有根到叶路径

> 原文:[https://www . geeksforgeeks . org/print-所有路径的二叉树-其-xor-是非零的/](https://www.geeksforgeeks.org/print-all-the-paths-of-a-binary-tree-whose-xor-is-non-zero/)

给定一个**二叉树**，任务是打印该树的所有根到叶路径，其 xor 值为非零。

**示例:**

```
Input: 
             10   
            /   \   
           10    3   
               /   \   
              10     3   
              / \   / \   
             7   3 42 13   
                      /   
                     7   
Output:
10 3 10 7 
10 3 3 42
Explanation: 
All the paths in the given binary tree are :
{10, 10} xor value of the path is 
    = 10 ^ 10 = 0
{10, 3, 10, 7} xor value of the path is 
    = 10 ^ 3 ^ 10 ^ 7 != 0
{10, 3, 3, 42} xor value of the path is 
    = 10 ^ 3 ^ 3 ^ 42 != 0
{10, 3, 10, 3} xor value of the path is 
    = 10 ^ 3 ^ 10 ^ 3 = 0
{10, 3, 3, 13, 7} xor value of the path is 
    = 10 ^ 3 ^ 3 ^ 13 ^ 7 = 0\. 
Hence, {10, 3, 10, 7} and {10, 3, 3, 42} are 
the paths whose xor value is non-zero.

Input:
            5
           /  \ 
         21     77 
        /  \      \
       5   21     16 
             \    / 
              5  3             
Output :
5 21 5
5 77 16 3
Explanation: 
{5, 21, 5} and {5, 77, 16, 3} are the paths
whose xor value is non-zero.
```

**方法:**
为了解决上述问题，主要思想是遍历树，检查该路径中所有元素的异或是否为零。

*   我们需要使用 [**预先顺序遍历**](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/) 递归遍历树**。**
*   对于每个节点，继续计算从根到当前节点的路径的异或。
*   如果节点是左边的叶节点，并且当前节点的右边的子节点为空，那么我们检查路径的 xor 值是否非零，如果非零，那么我们打印整个路径。

下面是上述方法的实现:

## C++

```
// C++ program to Print all the Paths of a
// Binary Tree whose XOR gives a non-zero value

#include <bits/stdc++.h>
using namespace std;

// A Tree node
struct Node {
    int key;
    struct Node *left, *right;
};

// Function to create a new node
Node* newNode(int key)
{
    Node* temp = new Node;
    temp->key = key;
    temp->left = temp->right = NULL;
    return (temp);
}

// Function to check whether Path
// is has non-zero xor value or not
bool PathXor(vector<int>& path)
{

    int ans = 0;

    // Iterating through the array
    // to find the xor value
    for (auto x : path) {
        ans ^= x;
    }

    return (ans != 0);
}

// Function to print a path
void printPaths(vector<int>& path)
{
    for (auto x : path) {
        cout << x << " ";
    }

    cout << endl;
}

// Function to find the paths of
// binary tree having non-zero xor value
void findPaths(struct Node* root,
               vector<int>& path)
{
    // Base case
    if (root == NULL)
        return;

    // Store the value in path vector
    path.push_back(root->key);

    // Recursively call for left sub tree
    findPaths(root->left, path);

    // Recursively call for right sub tree
    findPaths(root->right, path);

    // Condition to check, if leaf node
    if (root->left == NULL
        && root->right == NULL) {

        // Condition to check,
        // if path has non-zero xor or not
        if (PathXor(path)) {

            // Print the path
            printPaths(path);
        }
    }

    // Remove the last element
    // from the path vector
    path.pop_back();
}

// Function to find the paths
// having non-zero xor value
void printPaths(struct Node* node)
{
    vector<int> path;

    findPaths(node, path);
}

// Driver Code
int main()
{
    /*          10
            /    \
          10      3
                /   \
              10     3
            /   \   /   \
            7    3 42   13
                        /
                       7
    */

    // Create Binary Tree as shown
    Node* root = newNode(10);
    root->left = newNode(10);
    root->right = newNode(3);

    root->right->left = newNode(10);
    root->right->right = newNode(3);

    root->right->left->left = newNode(7);
    root->right->left->right = newNode(3);
    root->right->right->left = newNode(42);
    root->right->right->right = newNode(13);
    root->right->right->right->left = newNode(7);

    // Print non-zero XOR Paths
    printPaths(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Print all the Paths of a
// Binary Tree whose XOR gives a non-zero value
import java.util.*;
class GFG{

// A Tree node
static class Node
{
    int key;
    Node left, right;
};

// Function to create a new node
static Node newNode(int key)
{
    Node temp = new Node();
    temp.key = key;
    temp.left = temp.right = null;
    return (temp);
}

// Function to check whether Path
// is has non-zero xor value or not
static boolean PathXor(Vector<Integer> path)
{
    int ans = 0;

    // Iterating through the array
    // to find the xor value
    for (int x : path)
    {
        ans ^= x;
    }
    return (ans != 0);
}

// Function to print a path
static void printPaths(Vector<Integer> path)
{
    for (int x : path)
    {
        System.out.print(x + " ");
    }
    System.out.println();
}

// Function to find the paths of
// binary tree having non-zero xor value
static void findPaths(Node root,
                      Vector<Integer> path)
{
    // Base case
    if (root == null)
        return;

    // Store the value in path vector
    path.add(root.key);

    // Recursively call for left sub tree
    findPaths(root.left, path);

    // Recursively call for right sub tree
    findPaths(root.right, path);

    // Condition to check, if leaf node
    if (root.left == null &&
        root.right == null)
    {
        // Condition to check,
        // if path has non-zero xor or not
        if (PathXor(path))
        {
            // Print the path
            printPaths(path);
        }
    }

    // Remove the last element
    // from the path vector
    path.remove(path.size() - 1);
}

// Function to find the paths
// having non-zero xor value
static void printPaths(Node node)
{
    Vector<Integer> path = new Vector<Integer>();
    findPaths(node, path);
}

// Driver Code
public static void main(String[] args)
{
    /*        10
            /    \
          10      3
                /   \
              10     3
            /   \   /   \
            7    3 42   13
                        /
                       7
    */

    // Create Binary Tree as shown
    Node root = newNode(10);
    root.left = newNode(10);
    root.right = newNode(3);

    root.right.left = newNode(10);
    root.right.right = newNode(3);

    root.right.left.left = newNode(7);
    root.right.left.right = newNode(3);
    root.right.right.left = newNode(42);
    root.right.right.right = newNode(13);
    root.right.right.right.left = newNode(7);

    // Print non-zero XOR Paths
    printPaths(root);
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 program to print all
# the paths of a Binary Tree
# whose XOR gives a non-zero value

# A Tree node
class Node:

    def __init__(self, key):

        self.key = key
        self.left = None
        self.right = None

# Function to check whether Path
# is has non-zero xor value or not
def PathXor(path: list) -> bool:

    ans = 0

    # Iterating through the array
    # to find the xor value
    for x in path:
        ans ^= x

    return (ans != 0)

# Function to print a path
def printPathsList(path: list) -> None:

    for x in path:
        print(x, end = " ")

    print()

# Function to find the paths of
# binary tree having non-zero xor value
def findPaths(root: Node, path: list) -> None:

    # Base case
    if (root == None):
        return

    # Store the value in path vector
    path.append(root.key)

    # Recursively call for left sub tree
    findPaths(root.left, path)

    # Recursively call for right sub tree
    findPaths(root.right, path)

    # Condition to check, if leaf node
    if (root.left == None and
        root.right == None):

        # Condition to check, if path
        # has non-zero xor or not
        if (PathXor(path)):

            # Print the path
            printPathsList(path)

    # Remove the last element
    # from the path vector
    path.pop()

# Function to find the paths
# having non-zero xor value
def printPaths(node: Node) -> None:

    path = []
    newNode = node

    findPaths(newNode, path)

# Driver Code
if __name__ == "__main__":

    '''       10
            /    \
          10      3
                /   \
              10     3
            /   \   /   \
            7    3 42   13
                        /
                       7
    '''

    # Create Binary Tree as shown
    root = Node(10)
    root.left = Node(10)
    root.right = Node(3)

    root.right.left = Node(10)
    root.right.right = Node(3)

    root.right.left.left = Node(7)
    root.right.left.right = Node(3)
    root.right.right.left = Node(42)
    root.right.right.right = Node(13)
    root.right.right.right.left = Node(7)

    # Print non-zero XOR Paths
    printPaths(root)

# This code is contributed by sanjeev2552
```

## C#

```
// C# program to Print all the Paths of a
// Binary Tree whose XOR gives a non-zero value
using System;
using System.Collections.Generic;
class GFG{

// A Tree node
class Node
{
    public int key;
    public Node left, right;
};

// Function to create a new node
static Node newNode(int key)
{
    Node temp = new Node();
    temp.key = key;
    temp.left = temp.right = null;
    return (temp);
}

// Function to check whether Path
// is has non-zero xor value or not
static bool PathXor(List<int> path)
{
    int ans = 0;

    // Iterating through the array
    // to find the xor value
    foreach (int x in path)
    {
        ans ^= x;
    }
    return (ans != 0);
}

// Function to print a path
static void printPaths(List<int> path)
{
    foreach (int x in path)
    {
        Console.Write(x + " ");
    }
    Console.WriteLine();
}

// Function to find the paths of
// binary tree having non-zero xor value
static void findPaths(Node root,
                      List<int> path)
{
    // Base case
    if (root == null)
        return;

    // Store the value in path vector
    path.Add(root.key);

    // Recursively call for left sub tree
    findPaths(root.left, path);

    // Recursively call for right sub tree
    findPaths(root.right, path);

    // Condition to check, if leaf node
    if (root.left == null &&
        root.right == null)
    {
        // Condition to check,
        // if path has non-zero xor or not
        if (PathXor(path))
        {
            // Print the path
            printPaths(path);
        }
    }

    // Remove the last element
    // from the path vector
    path.RemoveAt(path.Count - 1);
}

// Function to find the paths
// having non-zero xor value
static void printPaths(Node node)
{
    List<int> path = new List<int>();
    findPaths(node, path);
}

// Driver Code
public static void Main(String[] args)
{
    /*        10
            /    \
          10      3
                /   \
              10     3
            /   \   /   \
            7    3 42   13
                        /
                       7
    */

    // Create Binary Tree as shown
    Node root = newNode(10);
    root.left = newNode(10);
    root.right = newNode(3);

    root.right.left = newNode(10);
    root.right.right = newNode(3);

    root.right.left.left = newNode(7);
    root.right.left.right = newNode(3);
    root.right.right.left = newNode(42);
    root.right.right.right = newNode(13);
    root.right.right.right.left = newNode(7);

    // Print non-zero XOR Paths
    printPaths(root);
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

    // JavaScript program to Print all the Paths of a
    // Binary Tree whose XOR gives a non-zero value

    // A Tree node
    class Node
    {
       constructor(key) {
           this.left = null;
           this.right = null;
           this.key = key;
        }
    }

    // Function to create a new node
    function newNode(key)
    {
        let temp = new Node(key);
        return (temp);
    }

    // Function to check whether Path
    // is has non-zero xor value or not
    function PathXor(path)
    {
        let ans = 0;

        // Iterating through the array
        // to find the xor value
        for (let x = 0; x < path.length; x++)
        {
            ans ^= path[x];
        }
        if(ans != 0)
        {
            return true;
        }
        else{
            return false;
        }
    }

    // Function to print a path
    function printPaths(path)
    {
        for (let x = 0; x < path.length; x++)
        {
            document.write(path[x] + " ");
        }
        document.write("</br>");
    }

    // Function to find the paths of
    // binary tree having non-zero xor value
    function findPaths(root, path)
    {
        // Base case
        if (root == null)
            return;

        // Store the value in path vector
        path.push(root.key);

        // Recursively call for left sub tree
        findPaths(root.left, path);

        // Recursively call for right sub tree
        findPaths(root.right, path);

        // Condition to check, if leaf node
        if (root.left == null &&
            root.right == null)
        {
            // Condition to check,
            // if path has non-zero xor or not
            if (PathXor(path))
            {
                // Print the path
                printPaths(path);
            }
        }

        // Remove the last element
        // from the path vector
        path.pop();
    }

    // Function to find the paths
    // having non-zero xor value
    function printpaths(node)
    {
        let path = [];
        findPaths(node, path);
    }

    /*        10
            /    \
          10      3
                /   \
              10     3
            /   \   /   \
            7    3 42   13
                        /
                       7
    */

    // Create Binary Tree as shown
    let root = newNode(10);
    root.left = newNode(10);
    root.right = newNode(3);

    root.right.left = newNode(10);
    root.right.right = newNode(3);

    root.right.left.left = newNode(7);
    root.right.left.right = newNode(3);
    root.right.right.left = newNode(42);
    root.right.right.right = newNode(13);
    root.right.right.right.left = newNode(7);

    // Print non-zero XOR Paths
    printpaths(root);

</script>
```

**Output:** 

```
10 3 10 7 
10 3 3 42
```