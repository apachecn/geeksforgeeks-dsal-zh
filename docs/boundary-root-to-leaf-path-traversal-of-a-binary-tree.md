# 二叉树的边界根到叶路径遍历

> 原文:[https://www . geesforgeks . org/boundary-二叉树的根到叶路径遍历/](https://www.geeksforgeeks.org/boundary-root-to-leaf-path-traversal-of-a-binary-tree/)

给定一棵[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)，任务是在边界根到叶路径遍历中打印该树的所有根到叶路径。

> **边界根到叶路径遍历:**在此遍历中，首先打印第一个根到叶路径(左边界)，然后按相反顺序打印最后一个根到叶路径(右边界)。然后对第二个也是倒数第二个根到叶路径重复该过程，直到打印出所有根到叶路径。

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
Output:  1 15 11
         3 29 13 1
         1 13 7 2

Explanation:
First of all print first path from Root to the Leaf 
which is 1 15 11
Then, print the last path from the Leaf to Root
which is 3 29 13 1
Then, print the second path from Root to Leaf 
which is 1 13 7 2

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

Output:  7 23 31 2
         11 3 41 7
         7 23 31 5
         23 17 16 23 7
```

**方法:**为了打印边界根到叶路径遍历中的路径，

*   我们首先需要对二叉树进行[预序遍历](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)，得到特定路径的所有节点值。
*   在这里，数组用于存储树的路径，同时执行 Preorder 遍历，然后将该路径存储到矩阵中。
*   然后对于每个路径，打印第一行(**从左到右**)然后最后一行(**从右到左**)的矩阵，以此类推。

下面是上述方法的实现:

## C++

```
// C++ implementation to print the
// path in Boundary Root to Leaf
// Path Traversal.

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
// Function to calculate the length
// of longest path of the tree
int lengthOfLongestPath(struct Node* node)
{
    // Base Case
    if (node == NULL)
        return 0;

    // Recursive call to calculate the length
    // of longest path
    int left = lengthOfLongestPath(node->left);
    int right = lengthOfLongestPath(node->right);

    return 1 + (left > right ? left : right);
}

// Function to copy the complete
// path in a matrix
void copyPath(int* path, int index,
              int** mtrx, int row)
{
    // Loop to copy the path
    for (int i = 0; i < index; i++) {
        mtrx[row][i] = path[i];
    }
}

// Function to store all path
// one by one in matrix
void storePath(struct Node* node,
               int* path, int index,
               int** mtrx, int& row)
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
    storePath(node->left, path,
              index + 1, mtrx, row);

    // Recursive call for
    // the right sub tree
    storePath(node->right, path,
              index + 1, mtrx, row);

    // Condition to check that current
    // node is a leaf node or not
    if (node->left == NULL
        && node->right == NULL) {

        // Increamentation for changing
        // row
        row = row + 1;
        // Function call for copying
        // the path
        copyPath(path, index + 1,
                 mtrx, row);
    }
}

// Function to calculate
// total path
int totalPath(Node* node)
{
    static int count = 0;
    if (node == NULL) {
        return count;
    }
    if (node->left == NULL
        && node->right == NULL) {
        return count + 1;
    }
    count = totalPath(node->left);
    return totalPath(node->right);
}

// Function for Clockwise Spiral Traversal
// of Binary Tree
void traverse_matrix(int** mtrx,
                     int height,
                     int width)
{
    int j = 0, k1 = 0, k2 = 0;
    int k3 = height - 1;
    int k4 = width - 1;

    for (int round = 0; round < height/2; round++)
    {
        for (j = k2; j < width; j++) {

            // Only print those values which
            // are not MAX_INTEGER
            if (mtrx[k1][j] != INT_MAX) {
                cout << mtrx[k1][j] << " ";
            }
        }
        cout << endl;

        k2 = 0;
        k1++;

        for (j = k4; j >= 0; j--) {

            // Only print those values which
            // are not MAX_INTEGER
            if (mtrx[k3][j] != INT_MAX) {
                cout << mtrx[k3][j] << " ";
            }
        }
        cout << endl;

        k4 = width - 1;
        k3--;
    }

    // Condition (one row may be left
    // traversing)
    // If number of rows in matrix are odd
    if (height % 2 != 0) {
        for (j = k2; j < width; j++) {

            // Only print those values which are
            // not MAX_INTEGER
            if (mtrx[k1][j] != INT_MAX) {
                cout << mtrx[k1][j] << " ";
            }
        }
    }
}

// Function to print all the paths
// in Boundary Root to Leaf
// Path Traversal
void PrintPath(Node* node)
{
    // Calculate the length of
    // longest path of the tree
    int max_len = lengthOfLongestPath(node);

    // Calculate total path
    int total_path = totalPath(node);

    // Array to store path
    int* path = new int[max_len];
    memset(path, 0, sizeof(path));

    // Use double pointer to create
    // 2D array which will contain
    // all path of the tree
    int** mtrx = new int*[total_path];

    // Initialize width for each row
    // of matrix
    for (int i = 0; i < total_path; i++)
    {
        mtrx[i] = new int[max_len];
    }

    // Initialize complete matrix with
    // MAX INTEGER(purpose garbage)
    for (int i = 0; i < total_path; i++)
    {
        for (int j = 0; j < max_len; j++)
        {
            mtrx[i][j] = INT_MAX;
        }
    }

    int row = -1;
    storePath(node, path, 0, mtrx, row);

    // Print the circular clockwise spiral
    // traversal of the tree
    traverse_matrix(mtrx, total_path,
                    max_len);

    // Release extra memory
    // allocated for matrix
    free(mtrx);
}

// Driver Code
int main()
{
    /*      10 
           /  \ 
         13    11 
              /  \ 
            19    23 
           / \    / \ 
          21 29 43  15
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

    // Function Call
    PrintPath(root);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to print the 
// path in Boundary Root to Leaf 
// Path Traversal.
import java.util.*;

class GFG{

static int row;
static int count = 0;

// Structure of tree node
static class Node
{
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

// Function to calculate the length
// of longest path of the tree
static int lengthOfLongestPath(Node node)
{

    // Base Case
    if (node == null)
        return 0;

    // Recursive call to calculate the
    // length of longest path
    int left = lengthOfLongestPath(node.left);
    int right = lengthOfLongestPath(node.right);

    return 1 + (left > right ? left : right);
}

// Function to copy the complete
// path in a matrix
static void copyPath(int[] path, int index,
                     int[][] mtrx, int r)
{

    // Loop to copy the path
    for(int i = 0; i < index; i++)
    {
        mtrx[r][i] = path[i];
    }
}

// Function to store all path
// one by one in matrix
static void storePath(Node node, int[] path,
                      int index, int[][] mtrx)
{

    // Base condition
    if (node == null)
    {
        return;
    }

    // Inserting the current node
    // into the current path
    path[index] = node.key;

    // Recursive call for
    // the left sub tree
    storePath(node.left, path,
              index + 1, mtrx);

    // Recursive call for
    // the right sub tree
    storePath(node.right, path,
              index + 1, mtrx);

    // Condition to check that current
    // node is a leaf node or not
    if (node.left == null &&
        node.right == null)
    {

        // Increamentation for changing
        // row
        row = row + 1;

        // Function call for copying
        // the path
        copyPath(path, index + 1, mtrx, row);
    }
}

// Function to calculate
// total path
static int totalPath(Node node)
{
    if (node == null)
    {
        return count;
    }
    if (node.left == null &&
        node.right == null)
    {
        return count + 1;
    }
    count = totalPath(node.left);
    return totalPath(node.right);
}

// Function for Clockwise Spiral Traversal
// of Binary Tree
static void traverse_matrix(int[][] mtrx,
                            int height,
                            int width)
{
    int j = 0, k1 = 0, k2 = 0;
    int k3 = height - 1;
    int k4 = width - 1;

    for(int round = 0;
            round < height / 2;
            round++)
    {
        for(j = k2; j < width; j++)
        {

            // Only print those values which
            // are not MAX_INTEGER
            if (mtrx[k1][j] != Integer.MAX_VALUE)
            {
                System.out.print(mtrx[k1][j] + " ");
            }
        }
        System.out.println();

        k2 = 0;
        k1++;

        for(j = k4; j >= 0; j--)
        {

            // Only print those values which
            // are not MAX_INTEGER
            if (mtrx[k3][j] != Integer.MAX_VALUE)
            {
                System.out.print(mtrx[k3][j] + " ");
            }
        }
        System.out.println();

        k4 = width - 1;
        k3--;
    }

    // Condition (one row may be left
    // traversing)
    // If number of rows in matrix are odd
    if (height % 2 != 0)
    {
        for(j = k2; j < width; j++)
        {

            // Only print those values which are
            // not MAX_INTEGER
            if (mtrx[k1][j] != Integer.MAX_VALUE)
            {
                System.out.print(mtrx[k1][j] + " ");
            }
        }
    }
}

// Function to print all the paths
// in Boundary Root to Leaf
// Path Traversal
static void PrintPath(Node node)
{

    // Calculate the length of
    // longest path of the tree
    int max_len = lengthOfLongestPath(node);

    // Calculate total path
    int total_path = totalPath(node);

    // Array to store path
    int[] path = new int[max_len];
    Arrays.fill(path, 0);

    // Use double pointer to create
    // 2D array which will contain
    // all path of the tree
    int[][] mtrx = new int[total_path][max_len];

    // Initialize complete matrix with
    // MAX INTEGER(purpose garbage)
    for(int i = 0; i < total_path; i++)
    {
        for(int j = 0; j < max_len; j++)
        {
            mtrx[i][j] = Integer.MAX_VALUE;
        }
    }

    row = -1;
    storePath(node, path, 0, mtrx);

    // Print the circular clockwise spiral
    // traversal of the tree
    traverse_matrix(mtrx, total_path, max_len);
}

// Driver Code
public static void main(String[] args)
{

    /* 10
      /  \
     13  11
        /  \
       19   23
      / \   / \
     21 29 43  15
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

    // Function Call
    PrintPath(root);
}
}

// This code is contributed by sanjeev2552
```

## 蟒蛇 3

```
# Python3 implementation to print the
# path in Boundary Root to Leaf
# Path Traversal.

# Structure of tree node
class Node:

    def __init__(self, key):

        self.key = key
        self.left = None
        self.right = None

row = 0
count = 0

# Utility function to
# create a new node
def newNode(key):

    temp = Node(key)
    return temp

# Function to calculate the length
# of longest path of the tree
def lengthOfLongestPath(node):

    # Base Case
    if (node == None):
        return 0;

    # Recursive call to calculate the length
    # of longest path
    left = lengthOfLongestPath(node.left);
    right = lengthOfLongestPath(node.right);

    return 1 + (left if left > right else right);

# Function to copy the complete
# path in a matrix
def copyPath(path, index, mtrx, r):

    # Loop to copy the path
    for i in range(index):

        mtrx[r][i] = path[i];

# Function to store all path
# one by one in matrix
def storePath(node, path, index, mtrx):
    global row

    # Base condition
    if (node == None):
        return;

    # Inserting the current node
    # into the current path
    path[index] = node.key;

    # Recursive call for
    # the left sub tree
    storePath(node.left, path,
              index + 1, mtrx);

    # Recursive call for
    # the right sub tree
    storePath(node.right, path,
              index + 1, mtrx);

    # Condition to check that current
    # node is a leaf node or not
    if (node.left == None and node.right == None):

        # Increamentation for changing
        # row
        row = row + 1;

        # Function call for copying
        # the path
        copyPath(path, index + 1,
                 mtrx, row);

# Function to calculate
# total path
def totalPath(node):
    global count

    if (node == None):
        return count;

    if (node.left == None and node.right == None):
        return count + 1;

    count = totalPath(node.left);
    return totalPath(node.right);

# Function for Clockwise Spiral Traversal
# of Binary Tree
def traverse_matrix( mtrx, height, width):

    j = 0
    k1 = 0
    k2 = 0;
    k3 = height - 1;
    k4 = width - 1;

    for round in range(height//2):
        for j in range(k2, width):

            # Only print those values which
            # are not MAX_INTEGER
            if (mtrx[k1][j] != 1000000):
                print(mtrx[k1][j], end=' ')

        print()       
        k2 = 0;
        k1 += 1

        for j in range(k4, -1, -1):

            # Only print those values which
            # are not MAX_INTEGER
            if (mtrx[k3][j] != 1000000):
                print(mtrx[k3][j], end=' ')

        print()
        k4 = width - 1;
        k3 -= 1

    # Condition (one row may be left
    # traversing)
    # If number of rows in matrix are odd
    if (height % 2 != 0):

        for j in range(k2, width):

            # Only print those values which are
            # not MAX_INTEGER
            if (mtrx[k1][j] != 1000000):
                print(mtrx[k1][j], end=' ')

# Function to print all the paths
# in Boundary Root to Leaf
# Path Traversal
def PrintPath(node):   
    global row

    # Calculate the length of
    # longest path of the tree
    max_len = lengthOfLongestPath(node);

    # Calculate total path
    total_path = totalPath(node);

    # Array to store path
    path = [0 for i in range(max_len)]

    # Use double pointer to create
    # 2D array which will contain
    # all path of the tree
    mtrx = [[1000000 for j in range(max_len)]
                for i in range(total_path)]

    row = -1;
    storePath(node, path, 0, mtrx);

    # Print the circular clockwise spiral
    # traversal of the tree
    traverse_matrix(mtrx, total_path,
                    max_len);

# Driver Code
if __name__=='__main__':

    '''      10 
           /  \ 
         13    11 
              /  \ 
            19    23 
           / \    / \ 
          21 29 43  15
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

    # Function Call
    PrintPath(root);

    # This code is contributed by pratham76
```

## C#

```
// C# implementation to print the 
// path in Boundary Root to Leaf 
// Path Traversal.

using System;
using System.Collections;

class GFG{

static int row;
static int count = 0;

// Structure of tree node
public class Node
{
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

// Function to calculate the length
// of longest path of the tree
static int lengthOfLongestPath(Node node)
{

    // Base Case
    if (node == null)
        return 0;

    // Recursive call to calculate the
    // length of longest path
    int left = lengthOfLongestPath(node.left);
    int right = lengthOfLongestPath(node.right);

    return 1 + (left > right ? left : right);
}

// Function to copy the complete
// path in a matrix
static void copyPath(int[] path, int index,
                     int[,] mtrx, int r)
{

    // Loop to copy the path
    for(int i = 0; i < index; i++)
    {
        mtrx[r, i] = path[i];
    }
}

// Function to store all path
// one by one in matrix
static void storePath(Node node, int[] path,
                      int index, int[,] mtrx)
{

    // Base condition
    if (node == null)
    {
        return;
    }

    // Inserting the current node
    // into the current path
    path[index] = node.key;

    // Recursive call for
    // the left sub tree
    storePath(node.left, path,
              index + 1, mtrx);

    // Recursive call for
    // the right sub tree
    storePath(node.right, path,
              index + 1, mtrx);

    // Condition to check that current
    // node is a leaf node or not
    if (node.left == null &&
        node.right == null)
    {

        // Increamentation for changing
        // row
        row = row + 1;

        // Function call for copying
        // the path
        copyPath(path, index + 1, mtrx, row);
    }
}

// Function to calculate
// total path
static int totalPath(Node node)
{
    if (node == null)
    {
        return count;
    }
    if (node.left == null &&
        node.right == null)
    {
        return count + 1;
    }
    count = totalPath(node.left);
    return totalPath(node.right);
}

// Function for Clockwise Spiral Traversal
// of Binary Tree
static void traverse_matrix(int[,] mtrx,
                            int height,
                            int width)
{
    int j = 0, k1 = 0, k2 = 0;
    int k3 = height - 1;
    int k4 = width - 1;

    for(int round = 0;
            round < height / 2;
            round++)
    {
        for(j = k2; j < width; j++)
        {

            // Only print those values which
            // are not MAX_INTEGER
            if (mtrx[k1, j] != 10000000)
            {
                Console.Write(mtrx[k1, j] + " ");
            }
        }
        Console.WriteLine();

        k2 = 0;
        k1++;

        for(j = k4; j >= 0; j--)
        {

            // Only print those values which
            // are not MAX_INTEGER
            if (mtrx[k3, j] != 10000000)
            {
                Console.Write(mtrx[k3, j] + " ");
            }
        }
        Console.WriteLine();

        k4 = width - 1;
        k3--;
    }

    // Condition (one row may be left
    // traversing)
    // If number of rows in matrix are odd
    if (height % 2 != 0)
    {
        for(j = k2; j < width; j++)
        {

            // Only print those values which are
            // not MAX_INTEGER
            if (mtrx[k1, j] != 10000000)
            {
                Console.Write(mtrx[k1, j] + " ");
            }
        }
    }
}

// Function to print all the paths
// in Boundary Root to Leaf
// Path Traversal
static void PrintPath(Node node)
{

    // Calculate the length of
    // longest path of the tree
    int max_len = lengthOfLongestPath(node);

    // Calculate total path
    int total_path = totalPath(node);

    // Array to store path
    int[] path = new int[max_len];
    Array.Fill(path, 0);

    // Use double pointer to create
    // 2D array which will contain
    // all path of the tree
    int[,] mtrx = new int[total_path, max_len];

    // Initialize complete matrix with
    // MAX INTEGER(purpose garbage)
    for(int i = 0; i < total_path; i++)
    {
        for(int j = 0; j < max_len; j++)
        {
            mtrx[i, j] = 10000000;
        }
    }

    row = -1;
    storePath(node, path, 0, mtrx);

    // Print the circular clockwise spiral
    // traversal of the tree
    traverse_matrix(mtrx, total_path, max_len);
}

// Driver Code
public static void Main(string[] args)
{

    /* 10
      /  \
     13  11
        /  \
       19   23
      / \   / \
     21 29 43  15
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

    // Function Call
    PrintPath(root);
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

    // JavaScript implementation to print the
    // path in Boundary Root to Leaf
    // Path Traversal.

    let row;
    let count = 0;

    // Structure of tree node
    class Node
    {
        constructor(key) {
           this.left = null;
           this.right = null;
           this.key = key;
        }
    }

    // Utility function to
    // create a new node
    function newNode(key)
    {
        let temp = new Node(key);
        return (temp);
    }

    // Function to calculate the length
    // of longest path of the tree
    function lengthOfLongestPath(node)
    {

        // Base Case
        if (node == null)
            return 0;

        // Recursive call to calculate the
        // length of longest path
        let left = lengthOfLongestPath(node.left);
        let right = lengthOfLongestPath(node.right);

        return 1 + (left > right ? left : right);
    }

    // Function to copy the complete
    // path in a matrix
    function copyPath(path, index, mtrx, r)
    {

        // Loop to copy the path
        for(let i = 0; i < index; i++)
        {
            mtrx[r][i] = path[i];
        }
    }

    // Function to store all path
    // one by one in matrix
    function storePath(node, path, index, mtrx)
    {

        // Base condition
        if (node == null)
        {
            return;
        }

        // Inserting the current node
        // into the current path
        path[index] = node.key;

        // Recursive call for
        // the left sub tree
        storePath(node.left, path,
                  index + 1, mtrx);

        // Recursive call for
        // the right sub tree
        storePath(node.right, path,
                  index + 1, mtrx);

        // Condition to check that current
        // node is a leaf node or not
        if (node.left == null &&
            node.right == null)
        {

            // Increamentation for changing
            // row
            row = row + 1;

            // Function call for copying
            // the path
            copyPath(path, index + 1, mtrx, row);
        }
    }

    // Function to calculate
    // total path
    function totalPath(node)
    {
        if (node == null)
        {
            return count;
        }
        if (node.left == null &&
            node.right == null)
        {
            return count + 1;
        }
        count = totalPath(node.left);
        return totalPath(node.right);
    }

    // Function for Clockwise Spiral Traversal
    // of Binary Tree
    function traverse_matrix(mtrx, height, width)
    {
        let j = 0, k1 = 0, k2 = 0;
        let k3 = height - 1;
        let k4 = width - 1;

        for(let round = 0; round < parseInt(height / 2, 10);
        round++)
        {
            for(j = k2; j < width; j++)
            {

                // Only print those values which
                // are not MAX_INTEGER
                if (mtrx[k1][j] != Number.MAX_VALUE)
                {
                    document.write(mtrx[k1][j] + " ");
                }
            }
            document.write("</br>");

            k2 = 0;
            k1++;

            for(j = k4; j >= 0; j--)
            {

                // Only print those values which
                // are not MAX_INTEGER
                if (mtrx[k3][j] != Number.MAX_VALUE)
                {
                    document.write(mtrx[k3][j] + " ");
                }
            }
            document.write("</br>");

            k4 = width - 1;
            k3--;
        }

        // Condition (one row may be left
        // traversing)
        // If number of rows in matrix are odd
        if (height % 2 != 0)
        {
            for(j = k2; j < width; j++)
            {

                // Only print those values which are
                // not MAX_INTEGER
                if (mtrx[k1][j] != Number.MAX_VALUE)
                {
                    document.write(mtrx[k1][j] + " ");
                }
            }
        }
    }

    // Function to print all the paths
    // in Boundary Root to Leaf
    // Path Traversal
    function PrintPath(node)
    {

        // Calculate the length of
        // longest path of the tree
        let max_len = lengthOfLongestPath(node);

        // Calculate total path
        let total_path = totalPath(node);

        // Array to store path
        let path = new Array(max_len);
        path.fill(0);

        // Use double pointer to create
        // 2D array which will contain
        // all path of the tree
        let mtrx = new Array(total_path);

        // Initialize complete matrix with
        // MAX INTEGER(purpose garbage)
        for(let i = 0; i < total_path; i++)
        {
            mtrx[i] = new Array(max_len);
            for(let j = 0; j < max_len; j++)
            {
                mtrx[i][j] = Number.MAX_VALUE;
            }
        }

        row = -1;
        storePath(node, path, 0, mtrx);

        // Print the circular clockwise spiral
        // traversal of the tree
        traverse_matrix(mtrx, total_path, max_len);
    }

    /* 10
      /  \
     13  11
        /  \
       19   23
      / \   / \
     21 29 43  15
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

    // Function Call
    PrintPath(root);

</script>
```

**Output:** 

```
10 13 
7 15 23 11 10 
10 11 19 21 
43 23 11 10 
10 11 19 29
```