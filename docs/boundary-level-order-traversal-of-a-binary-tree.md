# 二叉树的边界级顺序遍历

> 原文:[https://www . geesforgeks . org/二进制树的边界级顺序遍历/](https://www.geeksforgeeks.org/boundary-level-order-traversal-of-a-binary-tree/)

给定一个[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)，任务是以边界级顺序遍历打印该树的所有级别。

> **边界级别顺序遍历:**在此遍历中，首先打印级别的第一个元素(起始边界)，然后是最后一个元素(结束边界)。然后对第二个和最后一个元素重复该过程，直到打印出完整的级别。

**示例:**

```
Input: 
                   1
                /    \ 
              12       13 
             /  \     /   \ 
            11    6  4    11 
           /     /  \     / \
         23     7    9   2   4
Output:
1
12 13
11 11 6 4
23 4 7 2 9

Input: 
                  7
                /  \ 
              22     19
             /  \      \
            3     6     13 
           / \     \    / \
          1   5     8  1   4  
                   /
                  23 
Output:
7
22 19
3 13 6
1 4 5 1 8
23
```

**进场:**

*   为了在边界级别顺序遍历中打印级别，我们需要首先进行二叉树的[级别顺序遍历](https://www.geeksforgeeks.org/print-level-order-traversal-line-line/)来获取每个级别的值。
*   这里[队列数据结构](https://www.geeksforgeeks.org/queue-data-structure/)用于在执行级别顺序遍历时存储树的级别。
*   然后，对于每个级别，首先打印该级别的第一个元素(起始边界)，然后是最后一个元素(结束边界)。然后对第二个和最后一个元素重复该过程，直到打印出完整的级别。

以下是上述方法的实现:

## C++

```
// C++ program for printing a
// Levels of Binary Tree in a
// start end fashion

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

// Utility function to print level in
// start end fashion
void printLevelUtil(struct Node* queue[],
                    int index, int size)
{
    while (index < size) {
        cout << queue[index++]->key << " "
             << queue[size--]->key << " ";
    }
    if (index == size) {
        cout << queue[index]->key << " ";
    }

    cout << endl;
}

// Utility function to print level in  start
// end fashion in a given Binary tree
void printLevel(struct Node* node,
                struct Node* queue[],
                int index, int size)
{

    // Print root node value
    // as a single value in a
    // binary tree
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

        // Print level in a desire fashion
        printLevelUtil(queue, index, size - 1);
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

// Function to print level in start end
// fashion in a given binary tree
void printLevelInStartEndFashion(
    struct Node* node)
{
    int t_size = findSize(node);
    struct Node* queue[t_size];
    queue[0] = node;
    printLevel(node, queue, 0, 1);
}

// Driver Code
int main()
{
    /*     10
           / \
         13   13
          /     \
        14       15
        / \     / \
       21 22   22 21
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

    // Print Levels In Start End Fashion
    printLevelInStartEndFashion(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for printing a
// Levels of Binary Tree in a
// start end fashion
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

// Utility function to print level in
// start end fashion
static void printLevelUtil(Node queue[],
                    int index, int size)
{
    while (index < size) {
        System.out.print(queue[index++].key+ " "
             + queue[size--].key+ " ");
    }
    if (index == size) {
        System.out.print(queue[index].key+ " ");
    }

    System.out.println();
}

// Utility function to print level in  start
// end fashion in a given Binary tree
static void printLevel(Node node,
                Node queue[],
                int index, int size)
{

    // Print root node value
    // as a single value in a
    // binary tree
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

        // Print level in a desire fashion
        printLevelUtil(queue, index, size - 1);
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

// Function to print level in start end
// fashion in a given binary tree
static void printLevelInStartEndFashion(
    Node node)
{
    int t_size = findSize(node);
    Node []queue = new Node[t_size];
    queue[0] = node;
    printLevel(node, queue, 0, 1);
}

// Driver Code
public static void main(String[] args)
{
    /*     10
           / \
         13   13
          /     \
        14       15
        / \     / \
       21 22   22 21
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

    // Print Levels In Start End Fashion
    printLevelInStartEndFashion(root);

}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 program for printing a
# Levels of Binary Tree in a
# start end fashion

# A Tree node
class Node:

    def __init__(self, key):

        self.key = key
        self.left = None
        self.right = None

# function to create a
# new node
def newNode(key):

    temp = Node(key);   
    return temp;

# Utility function to print
# level in start end fashion
def printLevelUtil(queue,
                   index, size):

    while (index < size):
        print(str(queue[index].key) + ' ' +
              str(queue[size].key), end = ' ')
        size -= 1
        index += 1

    if (index == size):
        print(queue[index].key,
              end = ' ')   
    print()

# Utility function to print
# level in  start end fashion
# in a given Binary tree
def printLevel(node, queue,
               index, size):

    # Print root node value
    # as a single value in a
    # binary tree
    print(queue[index].key)

    # Level order traversal
    # of Tree
    while (index < size):
        curr_size = size;       
        while (index < curr_size):
            temp = queue[index];
            if (temp.left != None):
                queue[size] = temp.left;
                size += 1
            if (temp.right != None):
                queue[size] = temp.right;
                size += 1

            index += 1   

        # Print level in a desire
        # fashion
        printLevelUtil(queue, index,
                       size - 1);   

# Function to find total
# no of nodes
def findSize(node):

    if (node == None):
        return 0;

    return (1 + findSize(node.left) +
                findSize(node.right));

# Function to print level in start
# end fashion in a given binary tree
def printLevelInStartEndFashion(node):

    t_size = findSize(node);
    queue=[0 for i in range(t_size)];
    queue[0] = node;
    printLevel(node, queue, 0, 1);

# Driver code   
if __name__=="__main__":

    '''     10
           / \
         13   13
          /     \
        14       15
        / \     / \
       21 22   22 21
                  /
                 8 '''

    # Create Binary Tree as shown
    root = newNode(10);
    root.left = newNode(13);
    root.right = newNode(13);

    root.right.left = newNode(14);
    root.right.right = newNode(15);

    root.right.left.left = newNode(21);
    root.right.left.right = newNode(22);
    root.right.right.left = newNode(22);
    root.right.right.right = newNode(21);
    root.right.right.right.left = newNode(8);

    # Print Levels In Start End Fashion
    printLevelInStartEndFashion(root);

# This code is contributed by Rutvik_56
```

## C#

```
// C# program for printing a
// Levels of Binary Tree in a
// start end fashion
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

// Utility function to print level in
// start end fashion
static void printLevelUtil(Node []queue,
                    int index, int size)
{
    while (index < size) {
        Console.Write(queue[index++].key+ " "
             + queue[size--].key+ " ");
    }
    if (index == size) {
        Console.Write(queue[index].key+ " ");
    }

    Console.WriteLine();
}

// Utility function to print level in  start
// end fashion in a given Binary tree
static void printLevel(Node node,
                Node []queue,
                int index, int size)
{

    // Print root node value
    // as a single value in a
    // binary tree
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

        // Print level in a desire fashion
        printLevelUtil(queue, index, size - 1);
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

// Function to print level in start end
// fashion in a given binary tree
static void printLevelInStartEndFashion(
    Node node)
{
    int t_size = findSize(node);
    Node []queue = new Node[t_size];
    queue[0] = node;
    printLevel(node, queue, 0, 1);
}

// Driver Code
public static void Main(String[] args)
{
    /*     10
           / \
         13   13
          /     \
        14       15
        / \     / \
       21 22   22 21
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

    // Print Levels In Start End Fashion
    printLevelInStartEndFashion(root);
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// JavaScript program for printing a
// Levels of Binary Tree in a
// start end fashion

// A Tree node
class Node {
    constructor()
    {
        this.key = 0;
        this.left = null;
        this.right = null;
    }
};

// Utility function to create a new node
function newNode(key)
{
    var temp = new Node();
    temp.key = key;
    temp.left = temp.right = null;
    return (temp);
}

// Utility function to print level in
// start end fashion
function printLevelUtil(queue, index, size)
{
    while (index < size) {
        document.write(queue[index++].key+ " "
             + queue[size--].key+ " ");
    }
    if (index == size) {
        document.write(queue[index].key+ " ");
    }

    document.write("<br>");
}

// Utility function to print level in  start
// end fashion in a given Binary tree
function printLevel(node, queue, index, size)
{

    // Print root node value
    // as a single value in a
    // binary tree
    document.write(queue[index].key +"<br>");

    // Level order traversal of Tree
    while (index < size) {
        var curr_size = size;
        while (index < curr_size) {
            var temp = queue[index];

            if (temp.left != null) {
                queue[size++] = temp.left;
            }

            if (temp.right != null) {
                queue[size++] = temp.right;
            }

            index++;
        }

        // Print level in a desire fashion
        printLevelUtil(queue, index, size - 1);
    }
}

// Function to find total no of nodes
function findSize(node)
{

    if (node == null)
        return 0;

    return 1
           + findSize(node.left)
           + findSize(node.right);
}

// Function to print level in start end
// fashion in a given binary tree
function printLevelInStartEndFashion( node)
{
    var t_size = findSize(node);
    var queue = Array(t_size);
    queue[0] = node;
    printLevel(node, queue, 0, 1);
}

// Driver Code
/*     10
       / \
     13   13
      /     \
    14       15
    / \     / \
   21 22   22 21
              /
             8 */

// Create Binary Tree as shown
var root = newNode(10);
root.left = newNode(13);
root.right = newNode(13);

root.right.left = newNode(14);
root.right.right = newNode(15);

root.right.left.left = newNode(21);
root.right.left.right = newNode(22);
root.right.right.left = newNode(22);
root.right.right.right = newNode(21);
root.right.right.right.left = newNode(8);

// Print Levels In Start End Fashion
printLevelInStartEndFashion(root);

</script>
```

**Output:** 

```
10
13 13 
14 15 
21 21 22 22 
8
```