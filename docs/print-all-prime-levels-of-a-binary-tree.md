# 打印二叉树的所有素数级

> 原文:[https://www . geeksforgeeks . org/print-所有素数级别的二进制树/](https://www.geeksforgeeks.org/print-all-prime-levels-of-a-binary-tree/)

给定一个[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)，任务是打印该树的所有**质数**。

> 如果二叉树的任何一级的所有节点都是素数，则称该级为**素数级**。

**示例:**

```
Input: 
                 1
                /  \ 
              15    13 
             /     /   \ 
            11    7     29 
                   \    / 
                   2   3  
Output: 11 7 29
         2 3
Explanation: 
Third and Fourth levels are prime levels.

Input:
                  7
                /  \ 
              23     41 
             /  \      \
            31   16     3 
           / \     \    / 
          2   5    17  11    
                   /
                  23 
Output: 7
         23 41
         2 5 17 11
         23
Explanation: 
First, Second, Fourth and 
Fifth levels are prime levels.
```

**方法:**为了检查一个级别是否是 Prime 级别，

*   我们首先需要对二叉树进行[级的顺序遍历，得到每一级的节点值。](https://www.geeksforgeeks.org/print-level-order-traversal-line-line/)
*   这里一个[队列数据结构](https://www.geeksforgeeks.org/queue-data-structure/)用于存储树的级别，同时进行级别顺序遍历。
*   然后对于每一级，[检查是否是质数](https://www.geeksforgeeks.org/primality-test-set-1-introduction-and-school-method/)级。

下面是上述方法的实现:

## C++

```
// C++ program for printing a prime
// levels of binary Tree

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

// Function to check whether node
// Value is prime or not
bool isPrime(int n)
{
    if (n == 1)
        return false;

    // Iterate from 2 to sqrt(n)
    for (int i = 2; i * i <= n; i++) {

        // If it has a factor
        if (n % i == 0) {
            return false;
        }
    }

    return true;
}

// Function to print a Prime level
void printLevel(struct Node* queue[],
                int index, int size)
{
    for (int i = index; i < size; i++) {
        cout << queue[i]->key << " ";
    }

    cout << endl;
}

// Function to check whether given level is
// prime level or not
bool isLevelPrime(struct Node* queue[],
                  int index, int size)
{
    for (int i = index; i < size; i++) {
        // Check value of node is
        // pPrime or not
        if (!isPrime(queue[index++]->key)) {
            return false;
        }
    }

    // Return true if for loop
    // iIterate completely
    return true;
}

// Utility function to get Prime
// Level of a given Binary tree
void findPrimeLevels(struct Node* node,
                     struct Node* queue[],
                     int index, int size)
{
    // Print root node value, if Prime
    if (isPrime(queue[index]->key)) {
        cout << queue[index]->key << endl;
    }

    // Run while loop
    while (index < size) {
        int curr_size = size;

        // Run inner while loop
        while (index < curr_size) {
            struct Node* temp = queue[index];

            // Push left child in a queue
            if (temp->left != NULL)
                queue[size++] = temp->left;

            // Push right child in a queue
            if (temp->right != NULL)
                queue[size++] = temp->right;

            // Increment index
            index++;
        }

        // If condition to check, level is
        // prime or not
        if (isLevelPrime(
                queue, index, size - 1)) {

            // Function call to print
            // prime level
            printLevel(queue, index, size);
        }
    }
}

// Function to find total no of nodes
// In a given binary tree
int findSize(struct Node* node)
{
    // Base condition
    if (node == NULL)
        return 0;

    return 1
           + findSize(node->left)
           + findSize(node->right);
}

// Function to find Prime levels
// In a given binary tree
void printPrimeLevels(struct Node* node)
{
    int t_size = findSize(node);

    // Create queue
    struct Node* queue[t_size];

    // Push root node in a queue
    queue[0] = node;

    // Function call
    findPrimeLevels(node, queue, 0, 1);
}

// Driver Code
int main()
{
    /*      10
         /    \
        13     11
            /  \
           19    23
          / \    / \
         21 29 43 15
                  /
                 7 */

    // Create Binary Tree as shown

    Node* root = newNode(10);
    root->left = newNode(13);
    root->right = newNode(11);

    root->right->left = newNode(19);
    root->right->right = newNode(23);

    root->right->left->left = newNode(21);
    root->right->left->right = newNode(29);
    root->right->right->left = newNode(43);
    root->right->right->right = newNode(15);
    root->right->right->right->left = newNode(7);

    // Print Prime Levels
    printPrimeLevels(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
public class Main
{
    // A Tree node
    static class Node {

        public int key;
        public Node left, right;

        public Node(int key)
        {
            this.key = key;
            left = right = null;
        }
    }

    // Utility function to create a new node
    static Node newNode(int key)
    {
        Node temp = new Node(key);
        return temp;
    }

    // Function to check whether node
    // Value is prime or not
    static boolean isPrime(int n)
    {
        if (n == 1)
            return false;

        // Iterate from 2 to sqrt(n)
        for(int i = 2; i * i <= n; i++)
        {

            // If it has a factor
            if (n % i == 0)
            {
                return false;
            }
        }
        return true;
    }

    // Function to print a Prime level
    static void printLevel(Node[] queue, int index, int size)
    {
        for(int i = index; i < size; i++)
        {
            System.out.print(queue[i].key + " ");
        }
        System.out.println();
    }

    // Function to check whether given level is
    // prime level or not
    static boolean isLevelPrime(Node[] queue, int index, int size)
    {
        for(int i = index; i < size; i++)
        {

            // Check value of node is
            // pPrime or not
            if (!isPrime(queue[index++].key))
            {
                return false;
            }
        }

        // Return true if for loop
        // iIterate completely
        return true;
    }

    // Utility function to get Prime
    // Level of a given Binary tree
    static void findPrimeLevels(Node node, Node[] queue, int index, int size)
    {

        // Print root node value, if Prime
        if (isPrime(queue[index].key))
        {
            System.out.println(queue[index].key);
        }

        // Run while loop
        while (index < size)
        {
            int curr_size = size;

            // Run inner while loop
            while (index < curr_size)
            {
                Node temp = queue[index];

                // Push left child in a queue
                if (temp.left != null)
                    queue[size++] = temp.left;

                // Push right child in a queue
                if (temp.right != null)
                    queue[size++] = temp.right;

                // Increment index
                index++;
            }

            // If condition to check, level is
            // prime or not
            if (isLevelPrime(queue, index, size - 1))
            {

                // Function call to print
                // prime level
                printLevel(queue, index, size);
            }
        }
    }

    // Function to find total no of nodes
    // In a given binary tree
    static int findSize(Node node)
    {

        // Base condition
        if (node == null)
            return 0;

        return 1 + findSize(node.left) +
                   findSize(node.right);
    }

    // Function to find Prime levels
    // In a given binary tree
    static void printPrimeLevels(Node node)
    {
        int t_size = findSize(node);

        // Create queue
        Node[] queue = new Node[t_size];
        for(int i = 0; i < t_size; i++)
        {
            queue[i] = new Node(0);
        }

        // Push root node in a queue
        queue[0] = node;

        // Function call
        findPrimeLevels(node, queue, 0, 1);
    }

    public static void main(String[] args) {
        /*     10
             /    \
            13     11
                  /  \
                19    23
               / \    / \
              21 29 43 15
                      /
                     7 */

        // Create Binary Tree as shown
        Node root = newNode(10);
        root.left = newNode(13);
        root.right = newNode(11);

        root.right.left = newNode(19);
        root.right.right = newNode(23);

        root.right.left.left = newNode(21);
        root.right.left.right = newNode(29);
        root.right.right.left = newNode(43);
        root.right.right.right = newNode(15);
        root.right.right.right.left = newNode(7);

        // Print Prime Levels
        printPrimeLevels(root);
    }
}

// This code is contributed by suresh07.
```

## 蟒蛇 3

```
# Python3 program for printing a prime
# levels of binary Tree

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

# Function to check whether
# node Value is prime or not
def isPrime(n):

    if (n == 1):
        return False;   
    i = 2

    # Iterate from 2
    # to sqrt(n)
    while(i * i <= n):

        # If it has a factor
        if (n % i == 0):
            return False;
        i += 1

    return True;

# Function to print a
# Prime level
def printLevel(queue,
               index, size):

    for i in range(index, size):
        print(queue[i].key, end = ' ')
    print()

# Function to check whether
# given level is prime level
# or not
def isLevelPrime(queue,
                 index, size):

    for i in range(index, size):

        # Check value of node is
        # pPrime or not
        if (not isPrime(queue[index].key)):
            index += 1
            return False;       

    # Return true if for loop
    # iIterate completely
    return True;

# Utility function to get Prime
# Level of a given Binary tree
def findPrimeLevels(node, queue,
                    index, size):

    # Print root node value, if Prime
    if (isPrime(queue[index].key)):
        print(queue[index].key)

    # Run while loop
    while (index < size):
        curr_size = size;

        # Run inner while loop
        while (index < curr_size):
            temp = queue[index];

            # Push left child in a queue
            if (temp.left != None):
                queue[size] = temp.left;
                size+=1

            # Push right child in a queue
            if (temp.right != None):
                queue[size] = temp.right;
                size+=1

            # Increment index
            index+=1;

        # If condition to check, level
        # is prime or not
        if (isLevelPrime(queue, index,
                         size - 1)):

            # Function call to print
            # prime level
            printLevel(queue,
                       index, size);       

# Function to find total no
# of nodes In a given binary
# tree
def findSize(node):

    # Base condition
    if (node == None):
        return 0;

    return (1 + findSize(node.left) +
                findSize(node.right));

# Function to find Prime levels
# In a given binary tree
def printPrimeLevels(node):

    t_size = findSize(node);

    # Create queue
    queue=[0 for i in range(t_size)]

    # Push root node in a queue
    queue[0] = node;

    # Function call
    findPrimeLevels(node, queue,
                    0, 1);

# Driver code    
if __name__ == "__main__":

    '''      10
         /    \
        13     11
            /  \
           19    23
          / \    / \
         21 29 43 15
                  /
                 7 '''

    # Create Binary Tree as shown
    root = newNode(10);
    root.left = newNode(13);
    root.right = newNode(11);

    root.right.left = newNode(19);
    root.right.right = newNode(23);

    root.right.left.left = newNode(21);
    root.right.left.right = newNode(29);
    root.right.right.left = newNode(43);
    root.right.right.right = newNode(15);
    root.right.right.right.left = newNode(7);

    # Print Prime Levels
    printPrimeLevels(root);

# This code is contributed by Rutvik_56
```

## C#

```
// C# program for printing a prime
// levels of binary Tree
using System;
using System.Collections.Generic;
class GFG {

    // A Tree node
    class Node {

        public int key;
        public Node left, right;

        public Node(int key)
        {
            this.key = key;
            left = right = null;
        }
    }

    // Utility function to create a new node
    static Node newNode(int key)
    {
        Node temp = new Node(key);
        return temp;
    }

    // Function to check whether node
    // Value is prime or not
    static bool isPrime(int n)
    {
        if (n == 1)
            return false;

        // Iterate from 2 to sqrt(n)
        for(int i = 2; i * i <= n; i++)
        {

            // If it has a factor
            if (n % i == 0)
            {
                return false;
            }
        }
        return true;
    }

    // Function to print a Prime level
    static void printLevel(Node[] queue, int index, int size)
    {
        for(int i = index; i < size; i++)
        {
            Console.Write(queue[i].key + " ");
        }
        Console.WriteLine();
    }

    // Function to check whether given level is
    // prime level or not
    static bool isLevelPrime(Node[] queue, int index, int size)
    {
        for(int i = index; i < size; i++)
        {

            // Check value of node is
            // pPrime or not
            if (!isPrime(queue[index++].key))
            {
                return false;
            }
        }

        // Return true if for loop
        // iIterate completely
        return true;
    }

    // Utility function to get Prime
    // Level of a given Binary tree
    static void findPrimeLevels(Node node, Node[] queue, int index, int size)
    {

        // Print root node value, if Prime
        if (isPrime(queue[index].key))
        {
            Console.WriteLine(queue[index].key);
        }

        // Run while loop
        while (index < size)
        {
            int curr_size = size;

            // Run inner while loop
            while (index < curr_size)
            {
                Node temp = queue[index];

                // Push left child in a queue
                if (temp.left != null)
                    queue[size++] = temp.left;

                // Push right child in a queue
                if (temp.right != null)
                    queue[size++] = temp.right;

                // Increment index
                index++;
            }

            // If condition to check, level is
            // prime or not
            if (isLevelPrime(queue, index, size - 1))
            {

                // Function call to print
                // prime level
                printLevel(queue, index, size);
            }
        }
    }

    // Function to find total no of nodes
    // In a given binary tree
    static int findSize(Node node)
    {

        // Base condition
        if (node == null)
            return 0;

        return 1 + findSize(node.left) +
                   findSize(node.right);
    }

    // Function to find Prime levels
    // In a given binary tree
    static void printPrimeLevels(Node node)
    {
        int t_size = findSize(node);

        // Create queue
        Node[] queue = new Node[t_size];
        for(int i = 0; i < t_size; i++)
        {
            queue[i] = new Node(0);
        }

        // Push root node in a queue
        queue[0] = node;

        // Function call
        findPrimeLevels(node, queue, 0, 1);
    }

  static void Main() {
    /*     10
         /    \
        13     11
              /  \
            19    23
           / \    / \
          21 29 43 15
                  /
                 7 */

    // Create Binary Tree as shown
    Node root = newNode(10);
    root.left = newNode(13);
    root.right = newNode(11);

    root.right.left = newNode(19);
    root.right.right = newNode(23);

    root.right.left.left = newNode(21);
    root.right.left.right = newNode(29);
    root.right.right.left = newNode(43);
    root.right.right.right = newNode(15);
    root.right.right.right.left = newNode(7);

    // Print Prime Levels
    printPrimeLevels(root);
  }
}

// This code is contributed by mukesh07.
```

## java 描述语言

```
<script>

// Javascript program for printing a
// prime levels of binary Tree

// A Tree node
class Node
{
    constructor(key)
    {
        this.left = null;
        this.right = null;
        this.key = key;
    }
}

// Utility function to create a new node
function newNode(key)
{
    let temp = new Node(key);
    return (temp);
}

// Function to check whether node
// Value is prime or not
function isPrime(n)
{
    if (n == 1)
        return false;

    // Iterate from 2 to sqrt(n)
    for(let i = 2; i * i <= n; i++)
    {

        // If it has a factor
        if (n % i == 0)
        {
            return false;
        }
    }
    return true;
}

// Function to print a Prime level
function printLevel(queue, index, size)
{
    for(let i = index; i < size; i++)
    {

        document.write(queue[i].key + " ");
    }
    document.write("</br>");
}

// Function to check whether given level is
// prime level or not
function isLevelPrime(queue, index, size)
{
    for(let i = index; i < size; i++)
    {

        // Check value of node is
        // pPrime or not
        if (!isPrime(queue[index++].key))
        {
            return false;
        }
    }

    // Return true if for loop
    // iIterate completely
    return true;
}

// Utility function to get Prime
// Level of a given Binary tree
function findPrimeLevels(node, queue, index, size)
{

    // Print root node value, if Prime
    if (isPrime(queue[index].key))
    {
        document.write(queue[index].key + "</br>");
    }

    // Run while loop
    while (index < size)
    {
        let curr_size = size;

        // Run inner while loop
        while (index < curr_size)
        {
            let temp = queue[index];

            // Push left child in a queue
            if (temp.left != null)
                queue[size++] = temp.left;

            // Push right child in a queue
            if (temp.right != null)
                queue[size++] = temp.right;

            // Increment index
            index++;
        }

        // If condition to check, level is
        // prime or not
        if (isLevelPrime(queue, index, size - 1))
        {

            // Function call to print
            // prime level
            printLevel(queue, index, size);
        }
    }
}

// Function to find total no of nodes
// In a given binary tree
function findSize(node)
{

    // Base condition
    if (node == null)
        return 0;

    return 1 + findSize(node.left) +
               findSize(node.right);
}

// Function to find Prime levels
// In a given binary tree
function printPrimeLevels(node)
{
    let t_size = findSize(node);

    // Create queue
    let queue = new Array(t_size);
    for(let i = 0; i < t_size; i++)
    {
        queue[i] = new Node();
    }

    // Push root node in a queue
    queue[0] = node;

    // Function call
    findPrimeLevels(node, queue, 0, 1);
}

// Driver code
/*     10
     /    \
    13     11
          /  \
        19    23
       / \    / \
      21 29 43 15
              /
             7 */

// Create Binary Tree as shown
let root = newNode(10);
root.left = newNode(13);
root.right = newNode(11);

root.right.left = newNode(19);
root.right.right = newNode(23);

root.right.left.left = newNode(21);
root.right.left.right = newNode(29);
root.right.right.left = newNode(43);
root.right.right.right = newNode(15);
root.right.right.right.left = newNode(7);

// Print Prime Levels
printPrimeLevels(root);

// This code is contributed by mukesh07

</script>
```

**Output:** 

```
13 11 
19 23 
7
```