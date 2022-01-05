# 打印二叉树的所有回文层级

> 原文:[https://www . geesforgeks . org/print-all-回文-二进制树的级别/](https://www.geeksforgeeks.org/print-all-palindromic-levels-of-a-binary-tree/)

给定一棵 [**二叉树**](https://www.geeksforgeeks.org/binary-tree-data-structure/) ，任务是打印这棵树的所有回文层级。

**回文层级**二叉树的任何层级，如果从左向右遍历，结果与从右向左遍历该层级相同，则称为回文层级。

**示例:**

```
Input: 
                 1
                /  \ 
              12    13 
             /     /   \ 
            11    6     11 
                   \    / 
                   2   2  
Output:
1
11 6 11
2 2
Explanation:
First, third and fourth levels are palindrome.

Input: 
                 7
                /  \ 
              22      22 
             /  \      \
            3     6     3 
           / \     \    / 
          1   5     8   1    
                   /
                  23 
Output:
7
22 22
3 6 3
23

Explanation:
First, second, third and fifth levels are palindrome.
```

**方法:**为了检查每个级别是否是回文级别，我们需要首先对二叉树进行[级别顺序遍历，得到每个级别的值。然后对于每一级，检查它是否是回文。
这里一个](https://www.geeksforgeeks.org/print-level-order-traversal-line-line/)[队列数据结构](https://www.geeksforgeeks.org/queue-data-structure/)用于存储树的级别，同时进行级别顺序遍历。

下面是上述方法的实现:

## C++

```
// C++ program for printing a
// Palindromic Levels of Binary Tree

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

// Function to print a Palindromic level
void printLevel(struct Node* queue[],
                int index, int size)
{
    for (int i = index; i < size; i++) {
        cout << queue[i]->key << " ";
    }

    cout << endl;
}

// Function to check whether given level
// is Palindromic level or not
bool isPalindrome(struct Node* queue[],
                  int index, int size)
{

    while (index < size) {
        // check value of two nodes are
        // equal or not
        if (queue[index++]->key
            != queue[size--]->key)
            return false;
    }

    return true;
}

// Utility function to get palindromic
// level of a given Binary tree
void printPalLevel(struct Node* node,
                   struct Node* queue[],
                   int index, int size)
{

    // Print root node value
    // as a single value in a
    // level is also a Palindrome
    cout << queue[index]->key << endl;

    // Level order traversal of Tree
    while (index < size) {
        int curr_size = size;
        while (index < curr_size) {
            struct Node* temp = queue[index];

            if (temp->left != NULL) {
                queue[size++] = temp->left;
            }

            if (temp->right != NULL) {
                queue[size++] = temp->right;
            }

            index++;
        }

        // Check if level is Palindrome or not
        if (isPalindrome(queue, index, size - 1)) {
            printLevel(queue, index, size);
        }
    }
}

// Function to find total no of nodes
int findSize(struct Node* node)
{

    if (node == NULL)
        return 0;

    return 1
           + findSize(node->left)
           + findSize(node->right);
}

// Function to find palindromic level
// In a given binary tree
void printPalindromicLevel(struct Node* node)
{
    int t_size = findSize(node);
    struct Node* queue[t_size];
    queue[0] = node;
    printPalLevel(node, queue, 0, 1);
}

// Driver Code
int main()
{
    /*     10
        /    \
       13     13
        /       \
        14        15
        / \        / \
       21 22      22 21
                     /
                    8 */

    // Create Binary Tree as shown
    Node* root = newNode(10);
    root->left = newNode(13);
    root->right = newNode(13);

    root->right->left = newNode(14);
    root->right->right = newNode(15);

    root->right->left->left = newNode(21);
    root->right->left->right = newNode(22);
    root->right->right->left = newNode(22);
    root->right->right->right = newNode(21);
    root->right->right->right->left = newNode(8);

    // Print Palindromic Levels
    printPalindromicLevel(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for printing a
// Palindromic Levels of Binary Tree
class GFG{

// A Tree node
static class Node {
    int key;
    Node left, right;
};

// Utility function to create a new node
static Node newNode(int key)
{
    Node temp = new Node();
    temp.key = key;
    temp.left = temp.right = null;
    return (temp);
}

// Function to print a Palindromic level
static void printLevel(Node queue[],
                int index, int size)
{
    for (int i = index; i < size; i++) {
        System.out.print(queue[i].key+ " ");
    }

    System.out.println();
}

// Function to check whether given level
// is Palindromic level or not
static boolean isPalindrome(Node queue[],
                  int index, int size)
{

    while (index < size) {
        // check value of two nodes are
        // equal or not
        if (queue[index++].key
            != queue[size--].key)
            return false;
    }

    return true;
}

// Utility function to get palindromic
// level of a given Binary tree
static void printPalLevel(Node node,
                   Node queue[],
                   int index, int size)
{

    // Print root node value
    // as a single value in a
    // level is also a Palindrome
    System.out.print(queue[index].key +"\n");

    // Level order traversal of Tree
    while (index < size) {
        int curr_size = size;
        while (index < curr_size) {
            Node temp = queue[index];

            if (temp.left != null) {
                queue[size++] = temp.left;
            }

            if (temp.right != null) {
                queue[size++] = temp.right;
            }

            index++;
        }

        // Check if level is Palindrome or not
        if (isPalindrome(queue, index, size - 1)) {
            printLevel(queue, index, size);
        }
    }
}

// Function to find total no of nodes
static int findSize(Node node)
{

    if (node == null)
        return 0;

    return 1
           + findSize(node.left)
           + findSize(node.right);
}

// Function to find palindromic level
// In a given binary tree
static void printPalindromicLevel(Node node)
{
    int t_size = findSize(node);
    Node []queue = new Node[t_size];
    queue[0] = node;
    printPalLevel(node, queue, 0, 1);
}

// Driver Code
public static void main(String[] args)
{
    /*     10
        /    \
       13     13
        /       \
        14        15
        / \        / \
       21 22      22 21
                     /
                    8 */

    // Create Binary Tree as shown
    Node root = newNode(10);
    root.left = newNode(13);
    root.right = newNode(13);

    root.right.left = newNode(14);
    root.right.right = newNode(15);

    root.right.left.left = newNode(21);
    root.right.left.right = newNode(22);
    root.right.right.left = newNode(22);
    root.right.right.right = newNode(21);
    root.right.right.right.left = newNode(8);

    // Print Palindromic Levels
    printPalindromicLevel(root);

}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program for printing a
# Palindromic Levels of Binary Tree

# A BST node
class Node:

    def __init__(self, x):

        self.key = x
        self.left = None
        self.right = None

# Function to pra Palindromic level
def printLevel(queue, index, size):

    for i in range(index, size):
        print(queue[i].key, end = " ")

    print()

# Function to check whether given level
# is Palindromic level or not
def isPalindrome(queue, index, size):

    #print(index,size)

    while (index < size):

        # Check value of two nodes are
        # equal or not
        if (queue[index].key != queue[size].key):
            return False

        index += 1
        size -= 1

    return True

# Utility function to get palindromic
# level of a given Binary tree
def printPalLevel(node, queue, index, size):

    # Print root node value
    # as a single value in a
    # level is also a Palindrome
    print(queue[index].key)

    # Level order traversal of Tree
    while (index < size):
        curr_size = size

        while (index < curr_size):
            temp = queue[index]

            if (temp.left != None):
                queue[size] = temp.left
                size += 1

            if (temp.right != None):
                queue[size] = temp.right
                size += 1

            index += 1

        # Check if level is Palindrome or not
        if (isPalindrome(queue, index, size - 1) == True):
            printLevel(queue, index, size)

# Function to find total no of nodes
def findSize(node):

    if (node == None):
        return 0

    return (1 + findSize(node.left) +
                findSize(node.right))

# Function to find palindromic level
# In a given binary tree
def printPalindromicLevel(node):

    t_size = findSize(node)
    queue = [None for i in range(t_size)]
    queue[0] = node
    printPalLevel(node, queue, 0, 1)

# Driver Code
if __name__ == '__main__':

    #       10
    #     /    \
    #    13     13
    #     /       \
    #     14        15
    #     / \        / \
    #    21 22      22 21
    #                  /
    #                 8

    # Create Binary Tree as shown
    root = Node(10)
    root.left = Node(13)
    root.right = Node(13)

    root.right.left = Node(14)
    root.right.right = Node(15)

    root.right.left.left = Node(21)
    root.right.left.right = Node(22)
    root.right.right.left = Node(22)
    root.right.right.right = Node(21)
    root.right.right.right.left = Node(8)

    # Print Palindromic Levels
    printPalindromicLevel(root)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for printing a
// Palindromic Levels of Binary Tree
using System;

class GFG{

// A Tree node
class Node {
    public int key;
    public Node left, right;
};

// Utility function to create a new node
static Node newNode(int key)
{
    Node temp = new Node();
    temp.key = key;
    temp.left = temp.right = null;
    return (temp);
}

// Function to print a Palindromic level
static void printLevel(Node []queue,
                int index, int size)
{
    for (int i = index; i < size; i++) {
        Console.Write(queue[i].key+ " ");
    }

    Console.WriteLine();
}

// Function to check whether given level
// is Palindromic level or not
static bool isPalindrome(Node []queue,
                  int index, int size)
{

    while (index < size) {
        // check value of two nodes are
        // equal or not
        if (queue[index++].key
            != queue[size--].key)
            return false;
    }

    return true;
}

// Utility function to get palindromic
// level of a given Binary tree
static void printPalLevel(Node node,
                   Node []queue,
                   int index, int size)
{

    // Print root node value
    // as a single value in a
    // level is also a Palindrome
    Console.Write(queue[index].key +"\n");

    // Level order traversal of Tree
    while (index < size) {
        int curr_size = size;
        while (index < curr_size) {
            Node temp = queue[index];

            if (temp.left != null) {
                queue[size++] = temp.left;
            }

            if (temp.right != null) {
                queue[size++] = temp.right;
            }

            index++;
        }

        // Check if level is Palindrome or not
        if (isPalindrome(queue, index, size - 1)) {
            printLevel(queue, index, size);
        }
    }
}

// Function to find total no of nodes
static int findSize(Node node)
{

    if (node == null)
        return 0;

    return 1
           + findSize(node.left)
           + findSize(node.right);
}

// Function to find palindromic level
// In a given binary tree
static void printPalindromicLevel(Node node)
{
    int t_size = findSize(node);
    Node []queue = new Node[t_size];
    queue[0] = node;
    printPalLevel(node, queue, 0, 1);
}

// Driver Code
public static void Main(String[] args)
{
    /*     10
        /    \
       13     13
        /       \
        14        15
        / \        / \
       21 22      22 21
                     /
                    8 */

    // Create Binary Tree as shown
    Node root = newNode(10);
    root.left = newNode(13);
    root.right = newNode(13);

    root.right.left = newNode(14);
    root.right.right = newNode(15);

    root.right.left.left = newNode(21);
    root.right.left.right = newNode(22);
    root.right.right.left = newNode(22);
    root.right.right.right = newNode(21);
    root.right.right.right.left = newNode(8);

    // Print Palindromic Levels
    printPalindromicLevel(root);

}
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>

// Javascript program for printing a
// Palindromic Levels of Binary Tree

// A Tree node
class Node
{

    // Utility function to create
    // a new node
    constructor(key)
    {
        this.key = key;
        this.left = this.right = null;
    }
}

// Function to print a Palindromic level
function printLevel(queue, index, size)
{
    for(let i = index; i < size; i++)
    {
        document.write(queue[i].key + " ");
    }
    document.write("<br>");
}

// Function to check whether given level
// is Palindromic level or not
function isPalindrome(queue, index, size)
{
    while (index < size)
    {

        // Check value of two nodes are
        // equal or not
        if (queue[index++].key !=
            queue[size--].key)
            return false;
    }
    return true;
}

// Utility function to get palindromic
// level of a given Binary tree
function printPalLevel(node, queue,
                       index, size)
{

    // Print root node value
    // as a single value in a
    // level is also a Palindrome
    document.write(queue[index].key + "<br>");

    // Level order traversal of Tree
    while (index < size)
    {
        let curr_size = size;
        while (index < curr_size)
        {
            let temp = queue[index];

            if (temp.left != null)
            {
                queue[size++] = temp.left;
            }

            if (temp.right != null)
            {
                queue[size++] = temp.right;
            }
            index++;
        }

        // Check if level is Palindrome or not
        if (isPalindrome(queue, index, size - 1))
        {
            printLevel(queue, index, size);
        }
    }
}

// Function to find total no of nodes
function findSize(node)
{
    if (node == null)
        return 0;

    return 1 + findSize(node.left) +
               findSize(node.right);
}

// Function to find palindromic level
// In a given binary tree
function printPalindromicLevel(node)
{
    let t_size = findSize(node);
    let queue = new Array(t_size);
    queue[0] = node;

    printPalLevel(node, queue, 0, 1);
}

// Driver Code
/*     10
        /    \
       13     13
        /       \
        14        15
        / \        / \
       21 22      22 21
                     /
                    8 */

// Create Binary Tree as shown
let root = new Node(10);
root.left = new Node(13);
root.right = new Node(13);

root.right.left = new Node(14);
root.right.right = new Node(15);

root.right.left.left = new Node(21);
root.right.left.right = new Node(22);
root.right.right.left = new Node(22);
root.right.right.right = new Node(21);
root.right.right.right.left = new Node(8);

// Print Palindromic Levels
printPalindromicLevel(root);

// This code is contributed by unknown2108

</script>
```

**Output:** 

```
10
13 13 
21 22 22 21 
8
```