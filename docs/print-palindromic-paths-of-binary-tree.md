# 打印二叉树回文路径

> 原文:[https://www . geesforgeks . org/print-回文-二叉树路径/](https://www.geeksforgeeks.org/print-palindromic-paths-of-binary-tree/)

给定一个二叉树，任务是打印这个二叉树的所有回文路径。

**回文路径:**从根到叶的数据串联与从叶到根相同的路径，如 1- > 2- > 2- > 1。

**示例:**

```
Input: 
                 1
                /  \ 
              2      3 
             /     /   \ 
            1     6     3 
                   \   / 
                    2 1 
Output: 
1, 2, 1
1, 3, 3, 1
Explanation:  
In above binary tree paths 1, 2, 1 and 1, 3, 3, 1
are palindromic paths because traversal of these paths 
are the same as root to leaf and leaf to root

Input:
                 7
                /  \ 
              4      3 
             /  \      \
            3     6     4 
           / \     \    / 
          1   4     4  1    
                   /
                  7
Output: 7, 4, 6, 4, 7
Explanation:
In the above binary tree, there is only one path
which is same as root to leaf and leaf to root.
that is 7->4->6->4->7
```

**方法:**思路是利用[预序遍历](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)遍历树，保持路径的轨迹。每当到达叶节点时，检查当前路径是否是回文路径。类似地，[通过回溯](https://www.geeksforgeeks.org/recursion/)树的路径，递归地遍历树的其他兄弟节点。以下是步骤:

*   用根节点开始树的[预序遍历](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)。
*   检查当前节点不为空，如果为是，则返回。

```
if (node == Null)
    return;
```

*   检查当前节点是否为[叶节点](https://www.geeksforgeeks.org/check-whether-a-node-is-leaf-node-or-not-for-multiple-queries/)，如果是，则检查当前路径是否为回文路径。

```
if (node->left == Null && 
   node->right == Null)
      isPalindromic(Path);
```

*   否则，如果当前节点不是叶节点，则[递归地](https://www.geeksforgeeks.org/recursion/)遍历当前节点的左右子节点。
*   要检查路径是否回文，请从根到叶连接节点的数据，然后检查形成的[字符串是否是回文](https://www.geeksforgeeks.org/c-program-check-given-string-palindrome/)。

下面是上述方法的实现:

## C++

```
// C++ implementation to print
// the palindromic paths of tree

#include <bits/stdc++.h>
using namespace std;

// Structure of tree node
struct Node {
    int key;
    struct Node *left, *right;
};

// Utility function to
// create a new node
Node* newNode(int key)
{
    Node* temp = new Node;
    temp->key = key;
    temp->left = temp->right = NULL;
    return (temp);
}
// Function to calculate
// the height of the tree
int findHeight(struct Node* node)
{
    // Base Case
    if (node == NULL)
        return 0;

    // Recursive call to find the height
    // of the left and right child nodes
    int leftHeight = findHeight(node->left);
    int rightHeight = findHeight(node->right);

    return 1 + (leftHeight > rightHeight ?
                leftHeight : rightHeight);
}

// Function to check that a string
// is a palindrom  or not
bool isPalindrome(string str)
{
    // Start from leftmost and
    // rightmost corners of str
    int l = 0;
    int h = str.length() - 1;

    // Keep comparing characters
    // while they are same
    while (h > l)
    {
        if (str[l++] != str[h--])
        {
            return false;
        }
    }
    return true;
}

// Function to check whether a path
// is a palindromic path or not
bool isPathPal(int* path, int index)
{
    int i = 0;
    string s;

    // Loop to concatenate the
    // data of the tree
    while (i <= index) {
        s += to_string(path[i]);
        i += 1;
    }
    return isPalindrome(s);
}

// Function to print the palindromic path
void printPalPath(int* path, int index)
{
    // Loop to print the path
    for (int i = 0; i < index; i++) {
        cout << path[i] << ", ";
    }
    cout << endl;
}

// Function to print all the palindromic
// paths of the binary tree
void printPath(struct Node* node,
            int* path, int index)
{
    // Base condition
    if (node == NULL) {
        return;
    }

    // Inserting the current node
    // into the current path
    path[index] = node->key;

    // Recursive call for
    // the left sub tree
    printPath(node->left, path,
                     index + 1);

    // Recursive call for
    // the right sub tree
    printPath(node->right, path,
                      index + 1);

    // Condition to check that current
    // node is a leaf node or not
    if (node->left == NULL &&
       node->right == NULL) {

        // Condition to check that
        // path is palindrome or not
        if (isPathPal(path, index)) {
            printPalPath(path, index + 1);
        }
    }
}

// Function to find all the
// palindromic paths of the tree
void PalindromicPath(struct Node* node)
{
    // Calculate the height
    // of the tree
    int height = findHeight(node);
    int* path = new int[height];
    memset(path, 0, sizeof(path));
    printPath(node, path, 0);
}

// Function to create a binary tree
// and print all the Palindromic paths
void createAndPrintPalPath(){
    /*       2
          /    \
         6     8
            / \
           8   5
          / \ / \
          1 2 3 8
               /
              2
    */

    // Creation of tree
    Node* root = newNode(2);
    root->left = newNode(6);
    root->right = newNode(8);

    root->right->left = newNode(8);
    root->right->right = newNode(5);

    root->right->left->left = newNode(1);
    root->right->left->right = newNode(2);
    root->right->right->left = newNode(3);
    root->right->right->right = newNode(8);
    root->right->right->right->left = newNode(2);

    // Function Call
    PalindromicPath(root);
}

// Driver Code
int main()
{
    // Function Call
    createAndPrintPalPath();
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to print
// the palindromic paths of tree
import java.util.*;

class GFG{

// Structure of tree node
static class Node {
    int key;
    Node left, right;
};

// Utility function to
// create a new node
static Node newNode(int key)
{
    Node temp = new Node();
    temp.key = key;
    temp.left = temp.right = null;
    return (temp);
}

// Function to calculate
// the height of the tree
static int findHeight(Node node)
{
    // Base Case
    if (node == null)
        return 0;

    // Recursive call to find the height
    // of the left and right child nodes
    int leftHeight = findHeight(node.left);
    int rightHeight = findHeight(node.right);

    return 1 + (leftHeight > rightHeight ?
                leftHeight : rightHeight);
}

// Function to check that a String
// is a palindrom  or not
static boolean isPalindrome(String str)
{
    // Start from leftmost and
    // rightmost corners of str
    int l = 0;
    int h = str.length() - 1;

    // Keep comparing characters
    // while they are same
    while (h > l)
    {
        if (str.charAt(l++) != str.charAt(h--))
        {
            return false;
        }
    }
    return true;
}

// Function to check whether a path
// is a palindromic path or not
static boolean isPathPal(int []path, int index)
{
    int i = 0;
    String s = "";

    // Loop to concatenate the
    // data of the tree
    while (i <= index) {
        s += String.valueOf(path[i]);
        i += 1;
    }
    return isPalindrome(s);
}

// Function to print the palindromic path
static void printPalPath(int []path, int index)
{
    // Loop to print the path
    for (int i = 0; i < index; i++) {
        System.out.print(path[i]+ ", ");
    }
    System.out.println();
}

// Function to print all the palindromic
// paths of the binary tree
static void printPath(Node node,
            int []path, int index)
{
    // Base condition
    if (node == null) {
        return;
    }

    // Inserting the current node
    // into the current path
    path[index] = node.key;

    // Recursive call for
    // the left sub tree
    printPath(node.left, path,
                     index + 1);

    // Recursive call for
    // the right sub tree
    printPath(node.right, path,
                      index + 1);

    // Condition to check that current
    // node is a leaf node or not
    if (node.left == null &&
       node.right == null) {

        // Condition to check that
        // path is palindrome or not
        if (isPathPal(path, index)) {
            printPalPath(path, index + 1);
        }
    }
}

// Function to find all the
// palindromic paths of the tree
static void PalindromicPath(Node node)
{
    // Calculate the height
    // of the tree
    int height = findHeight(node);
    int []path = new int[height];
    printPath(node, path, 0);
}

// Function to create a binary tree
// and print all the Palindromic paths
static void createAndPrintPalPath(){
    /*       2
          /    \
         6     8
            / \
           8   5
          / \ / \
          1 2 3 8
               /
              2
    */

    // Creation of tree
    Node root = newNode(2);
    root.left = newNode(6);
    root.right = newNode(8);

    root.right.left = newNode(8);
    root.right.right = newNode(5);

    root.right.left.left = newNode(1);
    root.right.left.right = newNode(2);
    root.right.right.left = newNode(3);
    root.right.right.right = newNode(8);
    root.right.right.right.left = newNode(2);

    // Function Call
    PalindromicPath(root);
}

// Driver Code
public static void main(String[] args)
{
    // Function Call
    createAndPrintPalPath();
}
}

// This code is contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python3 implementation to print
# the palindromic paths of tree
from collections import deque

# A Tree node
class Node:

    def __init__(self, x):

        self.key = x
        self.left = None
        self.right = None

minValue, maxValue = 0, 0

# Function to calculate the
# height of the tree
def findHeight(node):

    # Base condition
    if (node == None):
        return 0
    leftHeight = findHeight(node.left)
    rightHeight = findHeight(node.right)

    # Return the maximum of the height
    # of the left and right subtree
    if leftHeight > rightHeight:
        return leftHeight + 1

    return rightHeight + 1

# Function to check that
# a string is a palindrom
# or not
def isPalindrome(str):

    # Start from leftmost and
    # rightmost corners of str
    l = 0;
    h = len(str) - 1

    # Keep comparing characters
    # while they are same
    while (h > l):
        if (str[l] != str[h]):
            return False
        l += 1
        h -= 1

    return True

# Function to check whether
# a path is a palindromic
# path or not
def isPathPal(path, index):

    i = 0
    s = ""

    # Loop to concatenate the
    # data of the tree
    while (i <= index):
        s += str(path[i])
        i += 1
    return isPalindrome(s)

# Function to print the palindromic
# path
def printPalPath(path,index):

    # Loop to print the path
    for i in range(index):
        print(path[i], end = ", ")
    print()

# Function to prall the palindromic
# paths of the binary tree
def printPath(node, path, index):

    # Base condition
    if (node == None):
        return

    # Inserting the current node
    # into the current path
    path[index] = node.key;

    # Recursive call for
    # the left sub tree
    printPath(node.left,
              path, index + 1)

    # Recursive call for
    # the right sub tree
    printPath(node.right,
              path, index + 1)

    # Condition to check that
    # current node is a leaf
    # node or not
    if (node.left == None and
        node.right == None):

        # Condition to check that
        # path is palindrome or not
        if (isPathPal(path, index)):
            printPalPath(path,
                         index + 1)

# Function to find all the
# palindromic paths of the tree
def PalindromicPath(node):

    # Calculate the height
    # of the tree
    height = findHeight(node)
    path = [0] * height

    printPath(node, path, 0)

def createAndPrintPalPath():

    # /*       2
    #       /    \
    #      6     8
    #         / \
    #        8   5
    #       / \ / \
    #       1 2 3 8
    #            /
    #           2
    # */

    # Creation of tree
    root = Node(2)
    root.left = Node(6)
    root.right = Node(8)

    root.right.left = Node(8)
    root.right.right = Node(5)

    root.right.left.left = Node(1)
    root.right.left.right = Node(2)
    root.right.right.left = Node(3)
    root.right.right.right = Node(8)
    root.right.right.right.left = Node(2)

     # Function Call
    PalindromicPath(root)

# Driver Code
if __name__ == '__main__':

    createAndPrintPalPath()

# This code is contributed by Mohit Kumar 29
```

## C#

```
// C# implementation to print
// the palindromic paths of tree
using System;

public class GFG{

// Structure of tree node
class Node {
    public int key;
    public Node left, right;
};

// Utility function to
// create a new node
static Node newNode(int key)
{
    Node temp = new Node();
    temp.key = key;
    temp.left = temp.right = null;
    return (temp);
}

// Function to calculate
// the height of the tree
static int findHeight(Node node)
{
    // Base Case
    if (node == null)
        return 0;

    // Recursive call to find the height
    // of the left and right child nodes
    int leftHeight = findHeight(node.left);
    int rightHeight = findHeight(node.right);

    return 1 + (leftHeight > rightHeight ?
                leftHeight : rightHeight);
}

// Function to check that a String
// is a palindrom  or not
static bool isPalindrome(String str)
{
    // Start from leftmost and
    // rightmost corners of str
    int l = 0;
    int h = str.Length - 1;

    // Keep comparing characters
    // while they are same
    while (h > l)
    {
        if (str[l++] != str[h--])
        {
            return false;
        }
    }
    return true;
}

// Function to check whether a path
// is a palindromic path or not
static bool isPathPal(int []path, int index)
{
    int i = 0;
    String s = "";

    // Loop to concatenate the
    // data of the tree
    while (i <= index) {
        s += String.Join("",path[i]);
        i += 1;
    }
    return isPalindrome(s);
}

// Function to print the palindromic path
static void printPalPath(int []path, int index)
{
    // Loop to print the path
    for (int i = 0; i < index; i++) {
        Console.Write(path[i]+ ", ");
    }
    Console.WriteLine();
}

// Function to print all the palindromic
// paths of the binary tree
static void printPath(Node node,
            int []path, int index)
{
    // Base condition
    if (node == null) {
        return;
    }

    // Inserting the current node
    // into the current path
    path[index] = node.key;

    // Recursive call for
    // the left sub tree
    printPath(node.left, path,
                     index + 1);

    // Recursive call for
    // the right sub tree
    printPath(node.right, path,
                      index + 1);

    // Condition to check that current
    // node is a leaf node or not
    if (node.left == null &&
       node.right == null) {

        // Condition to check that
        // path is palindrome or not
        if (isPathPal(path, index)) {
            printPalPath(path, index + 1);
        }
    }
}

// Function to find all the
// palindromic paths of the tree
static void PalindromicPath(Node node)
{
    // Calculate the height
    // of the tree
    int height = findHeight(node);
    int []path = new int[height];
    printPath(node, path, 0);
}

// Function to create a binary tree
// and print all the Palindromic paths
static void createAndPrintPalPath(){
    /*       2
          /    \
         6     8
            / \
           8   5
          / \ / \
          1 2 3 8
               /
              2
    */

    // Creation of tree
    Node root = newNode(2);
    root.left = newNode(6);
    root.right = newNode(8);

    root.right.left = newNode(8);
    root.right.right = newNode(5);

    root.right.left.left = newNode(1);
    root.right.left.right = newNode(2);
    root.right.right.left = newNode(3);
    root.right.right.right = newNode(8);
    root.right.right.right.left = newNode(2);

    // Function Call
    PalindromicPath(root);
}

// Driver Code
public static void Main(String[] args)
{
    // Function Call
    createAndPrintPalPath();
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// Javascript implementation to print
// the palindromic paths of tree

// Structure of tree node
class Node
{
    // Utility function to
    // create a new node
    constructor(key)
    {
        this.key=key;
        this.left=this.right=null;
    }
}

// Function to calculate
// the height of the tree
function findHeight(node)
{
    // Base Case
    if (node == null)
        return 0;

    // Recursive call to find the height
    // of the left and right child nodes
    let leftHeight = findHeight(node.left);
    let rightHeight = findHeight(node.right);

    return 1 + (leftHeight > rightHeight ?
                leftHeight : rightHeight);
}

// Function to check that a String
// is a palindrom  or not
function isPalindrome(str)
{
    // Start from leftmost and
    // rightmost corners of str
    let l = 0;
    let h = str.length - 1;

    // Keep comparing characters
    // while they are same
    while (h > l)
    {
        if (str[l++] != str[h--])
        {
            return false;
        }
    }
    return true;
}

// Function to check whether a path
// is a palindromic path or not
function isPathPal(path,index)
{
    let i = 0;
    let s = "";

    // Loop to concatenate the
    // data of the tree
    while (i <= index) {
        s += (path[i]).toString();
        i += 1;
    }
    return isPalindrome(s);
}

// Function to print the palindromic path
function printPalPath(path,index)
{
    // Loop to print the path
    for (let i = 0; i < index; i++) {
        document.write(path[i]+ ", ");
    }
    document.write("<br>");
}

// Function to print all the palindromic
// paths of the binary tree
function printPath(node,path,index)
{
    // Base condition
    if (node == null) {
        return;
    }

    // Inserting the current node
    // into the current path
    path[index] = node.key;

    // Recursive call for
    // the left sub tree
    printPath(node.left, path,
                     index + 1);

    // Recursive call for
    // the right sub tree
    printPath(node.right, path,
                      index + 1);

    // Condition to check that current
    // node is a leaf node or not
    if (node.left == null &&
       node.right == null) {

        // Condition to check that
        // path is palindrome or not
        if (isPathPal(path, index)) {
            printPalPath(path, index + 1);
        }
    }
}

// Function to find all the
// palindromic paths of the tree
function PalindromicPath(node)
{
    // Calculate the height
    // of the tree
    let height = findHeight(node);
    let path = new Array(height);
    printPath(node, path, 0);
}

// Function to create a binary tree
// and print all the Palindromic paths
function createAndPrintPalPath()
{
    /*       2
          /    \
         6     8
            / \
           8   5
          / \ / \
          1 2 3 8
               /
              2
    */

    // Creation of tree
    let root = new Node(2);
    root.left = new Node(6);
    root.right = new Node(8);

    root.right.left = new Node(8);
    root.right.right = new Node(5);

    root.right.left.left = new Node(1);
    root.right.left.right = new Node(2);
    root.right.right.left = new Node(3);
    root.right.right.right = new Node(8);
    root.right.right.right.left = new Node(2);

    // Function Call
    PalindromicPath(root);
}

// Driver Code
// Function Call
createAndPrintPalPath();

// This code is contributed by patel2127
</script>
```

**Output:** 

```
2, 8, 8, 2, 
2, 8, 5, 8, 2,
```