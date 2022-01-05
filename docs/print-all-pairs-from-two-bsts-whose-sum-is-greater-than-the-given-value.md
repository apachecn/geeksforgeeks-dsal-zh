# 打印两个 BST 中总和大于给定值的所有对

> 原文:[https://www . geeksforgeeks . org/print-所有来自两个 BST 的配对-其总和大于给定值/](https://www.geeksforgeeks.org/print-all-pairs-from-two-bsts-whose-sum-is-greater-than-the-given-value/)

给定两个[二叉查找树](https://www.geeksforgeeks.org/binary-search-tree-set-1-search-and-insertion/)(**BST**)和一个值 **X** ，问题是打印两个 BST 中总和大于给定值 **X** 的所有对。

**示例:**

```
Input: 
BST 1:
                  5        
                /   \      
               3     7      
              / \   / \    
             2  4  6   8   
BST 2:
                 10        
                /   \      
               6     15      
              / \   /  \    
             3  8  11  18
X = 20
Output: The pairs are:
        (3, 18)
        (4, 18)
        (5, 18)
        (6, 18)
        (7, 18)
        (8, 18)
        (6, 15)
        (7, 15)
        (8, 15)
```

**天真方法:**对于 BST 1 中的每个节点值 A，[搜索 BST 2 中大于(X–A)的值](https://www.geeksforgeeks.org/binary-search-tree-set-1-search-and-insertion/)。如果找到该值，则打印该对。

***时间复杂度:** O(n1 * h2)* ，其中 n1 为第一个 BST 中的节点数，h2 为第二个 BST 的高度。

**有效方法:**

1.  通过取索引 I 从最小值到节点到最大值遍历 BST 1，这可以借助[实现，以便遍历](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)。
2.  通过取索引 j，从最大值节点到最小值节点遍历 BST 2。这可以在有序遍历的帮助下实现。
3.  逐个执行这两个策略，并存储到两个数组中。
4.  在一个特定的遍历实例中，总结两个 BSt 中相应节点的值。
    *   如果 sum > x，则打印对并将 j 减 1。
    *   如果 x > sum，则 I 增加 1。

下面是上述方法的实现:

## C++

```
// C++ implementation to print pairs
// from two BSTs whose sum is greater
// the given value x

#include <bits/stdc++.h>
using namespace std;

// Structure of each node of BST
struct node {
    int key;
    struct node *left, *right;
};

// Function to create a new BST node
node* newNode(int item)
{
    node* temp = new node();
    temp->key = item;
    temp->left = temp->right = NULL;
    return temp;
}

// A utility function to insert a
// new node with given key in BST
struct node* insert(struct node* node,
                    int key)
{
    // If the tree is empty, return a new node
    if (node == NULL)
        return newNode(key);

    // Otherwise, recur down the tree
    if (key < node->key)
        node->left = insert(node->left,
                            key);
    else if (key > node->key)
        node->right = insert(node->right,
                             key);

    // Return the (unchanged) node pointer
    return node;
}

// Function to return the size of
// the tree
int sizeOfTree(node* root)
{
    if (root == NULL) {
        return 0;
    }

    // Calculate left size recursively
    int left = sizeOfTree(root->left);

    // Calculate right size recursively
    int right = sizeOfTree(root->right);

    // Return total size recursively
    return (left + right + 1);
}

// Function to store inorder
// traversal of BST
void storeInorder(node* root,
                  int inOrder[],
                  int& index)
{
    // Base condition
    if (root == NULL) {
        return;
    }

    // Left recursive call
    storeInorder(root->left,
                 inOrder,
                 index);

    // Store elements in inorder array
    inOrder[index++] = root->key;

    // Right recursive call
    storeInorder(root->right,
                 inOrder,
                 index);
}

// Function to print the pairs
void print(int inOrder1[], int i,
           int index1, int value)
{
    while (i < index1) {
        cout << "(" << inOrder1[i]
             << ", " << value
             << ")" << endl;
        i++;
    }
}

// Utility function to check the
// pair of BSTs whose sum is
// greater than given value x
void printPairUtil(int inOrder1[],
                   int inOrder2[],
                   int index1,
                   int j, int k)
{
    int i = 0;

    while (i < index1 && j >= 0) {

        if (inOrder1[i] + inOrder2[j] > k) {
            print(inOrder1, i,
                  index1, inOrder2[j]);
            j--;
        }
        else {
            i++;
        }
    }
}

// Function to check the
// pair of BSTs whose sum is
// greater than given value x
void printPairs(node* root1,
                node* root2, int k)
{
    // Store the size of BST1
    int numNode = sizeOfTree(root1);

    // Take auxiliary array for storing
    // The inorder traversal of BST1
    int inOrder1[numNode + 1];
    int index1 = 0;

    // Store the size of BST2
    numNode = sizeOfTree(root2);

    // Take auxiliary array for storing
    // The inorder traversal of BST2
    int inOrder2[numNode + 1];
    int index2 = 0;

    // Function call for storing
    // inorder traversal of BST1
    storeInorder(root1, inOrder1,
                 index1);

    // Function call for storing
    // inorder traversal of BST1
    storeInorder(root2, inOrder2,
                 index2);

    // Utility function call to count
    // the pair
    printPairUtil(inOrder1, inOrder2,
                  index1, index2 - 1, k);
}

// Driver code
int main()
{

    /* Formation of BST 1
             5
           /   \     
          3     7    
         / \   / \   
         2  4  6  8 
    */

    struct node* root1 = NULL;
    root1 = insert(root1, 5);
    insert(root1, 3);
    insert(root1, 2);
    insert(root1, 4);
    insert(root1, 7);
    insert(root1, 6);
    insert(root1, 8);

    /* Formation of BST 2
            10
           /   \     
          6     15    
         / \   / \   
        3   8 11  18 
    */

    struct node* root2 = NULL;
    root2 = insert(root2, 10);
    insert(root2, 6);
    insert(root2, 15);
    insert(root2, 3);
    insert(root2, 8);
    insert(root2, 11);
    insert(root2, 18);

    int x = 20;

    // Print pairs
    printPairs(root1, root2, x);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to print pairs
// from two BSTs whose sum is greater
// the given value x
class GFG{

static class RefInteger
{
    Integer value;

    public RefInteger(Integer value)
    {
        this.value = value;
    }
}

// Structure of each Node of BST
static class Node
{
    int key;
    Node left, right;
};

// Function to create a new BST Node
static Node newNode(int item)
{
    Node temp = new Node();
    temp.key = item;
    temp.left = temp.right = null;
    return temp;
}

// A utility function to insert a
// new Node with given key in BST
static Node insert(Node Node, int key)
{

    // If the tree is empty,
    // return a new Node
    if (Node == null)
        return newNode(key);

    // Otherwise, recur down the tree
    if (key < Node.key)
        Node.left = insert(Node.left, key);
    else if (key > Node.key)
        Node.right = insert(Node.right, key);

    // Return the (unchanged) Node pointer
    return Node;
}

// Function to return the size of
// the tree
static int sizeOfTree(Node root)
{
    if (root == null)
    {
        return 0;
    }

    // Calculate left size recursively
    int left = sizeOfTree(root.left);

    // Calculate right size recursively
    int right = sizeOfTree(root.right);

    // Return total size recursively
    return (left + right + 1);
}

// Function to store inorder
// traversal of BST
static void storeInorder(Node root, int inOrder[],
                         RefInteger index)
{

    // Base condition
    if (root == null)
    {
        return;
    }

    // Left recursive call
    storeInorder(root.left, inOrder, index);

    // Store elements in inorder array
    inOrder[index.value++] = root.key;

    // Right recursive call
    storeInorder(root.right, inOrder, index);
}

// Function to print the pairs
static void print(int inOrder1[], int i,
                  int index1, int value)
{
    while (i < index1)
    {
        System.out.println("(" + inOrder1[i] +
                           ", " + value + ")");
        i++;
    }
}

// Utility function to check the
// pair of BSTs whose sum is
// greater than given value x
static void printPairUtil(int inOrder1[],
                          int inOrder2[],
                          int index1, int j,
                          int k)
{
    int i = 0;

    while (i < index1 && j >= 0)
    {
        if (inOrder1[i] + inOrder2[j] > k)
        {
            print(inOrder1, i, index1,
                  inOrder2[j]);

            j--;
        }
        else
        {
            i++;
        }
    }
}

// Function to check the pair of
// BSTs whose sum is greater than
// given value x
static void printPairs(Node root1,
                       Node root2, int k)
{

    // Store the size of BST1
    int numNode = sizeOfTree(root1);

    // Take auxiliary array for storing
    // The inorder traversal of BST1
    int[] inOrder1 = new int[numNode + 1];
    RefInteger index1 = new RefInteger(0);

    // Store the size of BST2
    numNode = sizeOfTree(root2);

    // Take auxiliary array for storing
    // The inorder traversal of BST2
    int[] inOrder2 = new int[numNode + 1];
    RefInteger index2 = new RefInteger(0);

    // Function call for storing
    // inorder traversal of BST1
    storeInorder(root1, inOrder1, index1);

    // Function call for storing
    // inorder traversal of BST1
    storeInorder(root2, inOrder2, index2);

    // Utility function call to count
    // the pair
    printPairUtil(inOrder1, inOrder2,
                  index1.value,
                  index2.value - 1, k);
}

// Driver code
public static void main(String[] args)
{

    /* Formation of BST 1
         5
       /   \     
      3     7    
     / \   / \   
    2  4  6   8 
    */

    Node root1 = null;
    root1 = insert(root1, 5);
    insert(root1, 3);
    insert(root1, 2);
    insert(root1, 4);
    insert(root1, 7);
    insert(root1, 6);
    insert(root1, 8);

    /* Formation of BST 2
        10
       /   \     
      6     15    
     / \   / \   
    3   8 11  18 
    */

    Node root2 = null;
    root2 = insert(root2, 10);
    insert(root2, 6);
    insert(root2, 15);
    insert(root2, 3);
    insert(root2, 8);
    insert(root2, 11);
    insert(root2, 18);

    int x = 20;

    // Print pairs
    printPairs(root1, root2, x);
}
}

// This code is contributed by sanjeev2552
```

## 蟒蛇 3

```
# Python3 implementation to print pairs
# from two BSTs whose sum is greater
# the given value x
index = 0

# Structure of each node of BST
class newNode:

    def __init__(self, item):

        self.key = item
        self.left = None
        self.right = None

# A utility function to insert a
# new node with given key in BST
def insert(node, key):

    # If the tree is empty,
    # return a new node
    if (node == None):
        return newNode(key)

    # Otherwise, recur down the tree
    if (key < node.key):
        node.left = insert(node.left, key)
    elif (key > node.key):
        node.right = insert(node.right, key)

    # Return the (unchanged) node pointer
    return node

# Function to return the size of
# the tree
def sizeOfTree(root):

    if (root == None):
        return 0

    # Calculate left size recursively
    left = sizeOfTree(root.left)

    # Calculate right size recursively
    right = sizeOfTree(root.right)

    # Return total size recursively
    return (left + right + 1)

# Function to store inorder
# traversal of BST
def storeInorder(root, inOrder):

    global index

    # Base condition
    if (root == None):
        return

    # Left recursive call
    storeInorder(root.left, inOrder)

    # Store elements in inorder array
    inOrder[index] = root.key
    index += 1

    # Right recursive call
    storeInorder(root.right, inOrder)

# Function to print the pairs
def print1(inOrder1, i, index1, value):

    while (i < index1):
        print("(", inOrder1[i], ",", value, ")")
        i += 1

# Utility function to check the
# pair of BSTs whose sum is
# greater than given value x
def printPairUtil(inOrder1, inOrder2,
                  index1, j, k):

    i = 0

    while (i < index1 and j >= 0):
        if (inOrder1[i] + inOrder2[j] > k):
            print1(inOrder1, i, index1, inOrder2[j])
            j -= 1
        else:
            i += 1

# Function to check the
# pair of BSTs whose sum is
# greater than given value x
def printPairs(root1, root2, k):

    global index

    # Store the size of BST1
    numNode = sizeOfTree(root1)

    # Take auxiliary array for storing
    # The inorder traversal of BST1
    inOrder1 = [0 for i in range(numNode + 1)]
    index1 = 0

    # Store the size of BST2
    numNode = sizeOfTree(root2)

    # Take auxiliary array for storing
    # The inorder traversal of BST2
    inOrder2 = [0 for i in range(numNode + 1)]
    index2 = 0

    # Function call for storing
    # inorder traversal of BST1
    index = 0
    storeInorder(root1, inOrder1)
    temp1 = index

    # Function call for storing
    # inorder traversal of BST1
    index = 0
    storeInorder(root2, inOrder2)
    temp2 = index

    # Utility function call to count
    # the pair
    printPairUtil(inOrder1, inOrder2,
                  temp1, temp2 - 1, k)

# Driver code
if __name__ == '__main__':

    ''' Formation of BST 1
             5
           /   \      
          3     7     
         / \   / \    
         2  4  6  8  
    '''

    root1 = None
    root1 = insert(root1, 5)
    insert(root1, 3)
    insert(root1, 2)
    insert(root1, 4)
    insert(root1, 7)
    insert(root1, 6)
    insert(root1, 8)

    '''Formation of BST 2
            10
           /   \      
          6     15     
         / \   / \    
        3   8 11  18  
    '''
    root2 = None
    root2 = insert(root2, 10)
    insert(root2, 6)
    insert(root2, 15)
    insert(root2, 3)
    insert(root2, 8)
    insert(root2, 11)
    insert(root2, 18)

    x = 20

    # Print pairs
    printPairs(root1, root2, x)

# This code is contributed by ipg2016107
```

## C#

```
// C# implementation to print pairs
// from two BSTs whose sum is greater
// the given value x

using System;

class GFG{

public class Refint
{
    public int value;

    public Refint(int value)
    {
        this.value = value;
    }
}

// Structure of each Node of BST
public class Node
{
    public int key;
    public Node left, right;
};

// Function to create a new BST Node
static Node newNode(int item)
{
    Node temp = new Node();
    temp.key = item;
    temp.left = temp.right = null;
    return temp;
}

// A utility function to insert a
// new Node with given key in BST
static Node insert(Node Node, int key)
{

    // If the tree is empty,
    // return a new Node
    if (Node == null)
        return newNode(key);

    // Otherwise, recur down the tree
    if (key < Node.key)
        Node.left = insert(Node.left, key);
    else if (key > Node.key)
        Node.right = insert(Node.right, key);

    // Return the (unchanged) Node pointer
    return Node;
}

// Function to return the size of
// the tree
static int sizeOfTree(Node root)
{
    if (root == null)
    {
        return 0;
    }

    // Calculate left size recursively
    int left = sizeOfTree(root.left);

    // Calculate right size recursively
    int right = sizeOfTree(root.right);

    // Return total size recursively
    return (left + right + 1);
}

// Function to store inorder
// traversal of BST
static void storeInorder(Node root, int []inOrder,
                         Refint index)
{

    // Base condition
    if (root == null)
    {
        return;
    }

    // Left recursive call
    storeInorder(root.left, inOrder, index);

    // Store elements in inorder array
    inOrder[index.value++] = root.key;

    // Right recursive call
    storeInorder(root.right, inOrder, index);
}

// Function to print the pairs
static void print(int []inOrder1, int i,
                  int index1, int value)
{
    while (i < index1)
    {

        Console.WriteLine("(" + inOrder1[i] +
                           ", " + value + ")");
        i++;
    }
}

// Utility function to check the
// pair of BSTs whose sum is
// greater than given value x
static void printPairUtil(int []inOrder1,
                          int []inOrder2,
                          int index1, int j,
                          int k)
{
    int i = 0;

    while (i < index1 && j >= 0)
    {
        if (inOrder1[i] + inOrder2[j] > k)
        {
            print(inOrder1, i, index1,
                  inOrder2[j]);

            j--;
        }
        else
        {
            i++;
        }
    }
}

// Function to check the pair of
// BSTs whose sum is greater than
// given value x
static void printPairs(Node root1,
                       Node root2, int k)
{

    // Store the size of BST1
    int numNode = sizeOfTree(root1);

    // Take auxiliary array for storing
    // The inorder traversal of BST1
    int[] inOrder1 = new int[numNode + 1];
    Refint index1 = new Refint(0);

    // Store the size of BST2
    numNode = sizeOfTree(root2);

    // Take auxiliary array for storing
    // The inorder traversal of BST2
    int[] inOrder2 = new int[numNode + 1];
    Refint index2 = new Refint(0);

    // Function call for storing
    // inorder traversal of BST1
    storeInorder(root1, inOrder1, index1);

    // Function call for storing
    // inorder traversal of BST1
    storeInorder(root2, inOrder2, index2);

    // Utility function call to count
    // the pair
    printPairUtil(inOrder1, inOrder2,
                  index1.value,
                  index2.value - 1, k);
}

// Driver code
public static void Main(string[] args)
{

    /* Formation of BST 1
         5
       /   \     
      3     7    
     / \   / \   
    2  4  6   8 
    */

    Node root1 = null;
    root1 = insert(root1, 5);
    insert(root1, 3);
    insert(root1, 2);
    insert(root1, 4);
    insert(root1, 7);
    insert(root1, 6);
    insert(root1, 8);

    /* Formation of BST 2
        10
       /   \     
      6     15    
     / \   / \   
    3   8 11  18 
    */

    Node root2 = null;
    root2 = insert(root2, 10);
    insert(root2, 6);
    insert(root2, 15);
    insert(root2, 3);
    insert(root2, 8);
    insert(root2, 11);
    insert(root2, 18);

    int x = 20;

    // Print pairs
    printPairs(root1, root2, x);
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

    // JavaScript implementation to print pairs
    // from two BSTs whose sum is greater
    // the given value x

    class Refint
    {
        constructor(value)
        {
            this.value = value;
        }
    }

    // Structure of each Node of BST
    class Node
    {
        constructor(item) {
           this.left = null;
           this.right = null;
           this.key = item;
        }
    }

    // Function to create a new BST Node
    function newNode(item)
    {
        let temp = new Node(item);
        return temp;
    }

    // A utility function to insert a
    // new Node with given key in BST
    function insert(Node, key)
    {

        // If the tree is empty,
        // return a new Node
        if (Node == null)
            return newNode(key);

        // Otherwise, recur down the tree
        if (key < Node.key)
            Node.left = insert(Node.left, key);
        else if (key > Node.key)
            Node.right = insert(Node.right, key);

        // Return the (unchanged) Node pointer
        return Node;
    }

    // Function to return the size of
    // the tree
    function sizeOfTree(root)
    {
        if (root == null)
        {
            return 0;
        }

        // Calculate left size recursively
        let left = sizeOfTree(root.left);

        // Calculate right size recursively
        let right = sizeOfTree(root.right);

        // Return total size recursively
        return (left + right + 1);
    }

    // Function to store inorder
    // traversal of BST
    function storeInorder(root, inOrder, index)
    {

        // Base condition
        if (root == null)
        {
            return;
        }

        // Left recursive call
        storeInorder(root.left, inOrder, index);

        // Store elements in inorder array
        inOrder[index.value++] = root.key;

        // Right recursive call
        storeInorder(root.right, inOrder, index);
    }

    // Function to print the pairs
    function print(inOrder1, i, index1, value)
    {
        while (i < index1)
        {

            document.write("(" + inOrder1[i] +
                               ", " + value + ")" + "</br>");
            i++;
        }
    }

    // Utility function to check the
    // pair of BSTs whose sum is
    // greater than given value x
    function printPairUtil(inOrder1, inOrder2, index1, j, k)
    {
        let i = 0;

        while (i < index1 && j >= 0)
        {
            if (inOrder1[i] + inOrder2[j] > k)
            {
                print(inOrder1, i, index1,
                      inOrder2[j]);

                j--;
            }
            else
            {
                i++;
            }
        }
    }

    // Function to check the pair of
    // BSTs whose sum is greater than
    // given value x
    function printPairs(root1, root2, k)
    {

        // Store the size of BST1
        let numNode = sizeOfTree(root1);

        // Take auxiliary array for storing
        // The inorder traversal of BST1
        let inOrder1 = new Array(numNode + 1);
        let index1 = new Refint(0);

        // Store the size of BST2
        numNode = sizeOfTree(root2);

        // Take auxiliary array for storing
        // The inorder traversal of BST2
        let inOrder2 = new Array(numNode + 1);
        let index2 = new Refint(0);

        // Function call for storing
        // inorder traversal of BST1
        storeInorder(root1, inOrder1, index1);

        // Function call for storing
        // inorder traversal of BST1
        storeInorder(root2, inOrder2, index2);

        // Utility function call to count
        // the pair
        printPairUtil(inOrder1, inOrder2,
                      index1.value,
                      index2.value - 1, k);
    }

    /* Formation of BST 1
         5
       /   \    
      3     7   
     / \   / \  
    2  4  6   8
    */

    let root1 = null;
    root1 = insert(root1, 5);
    insert(root1, 3);
    insert(root1, 2);
    insert(root1, 4);
    insert(root1, 7);
    insert(root1, 6);
    insert(root1, 8);

    /* Formation of BST 2
        10
       /   \    
      6     15   
     / \   / \  
    3   8 11  18
    */

    let root2 = null;
    root2 = insert(root2, 10);
    insert(root2, 6);
    insert(root2, 15);
    insert(root2, 3);
    insert(root2, 8);
    insert(root2, 11);
    insert(root2, 18);

    let x = 20;

    // Print pairs
    printPairs(root1, root2, x);

</script>
```

**Output:** 

```
(3, 18)
(4, 18)
(5, 18)
(6, 18)
(7, 18)
(8, 18)
(6, 15)
(7, 15)
(8, 15)
```