# 根据 K 值

将一个 BST 拆分为两个平衡的 BST

> 原文:[https://www . geesforgeks . org/split-a-BST-in-two-balanced-BST-bast-on-a-value-k/](https://www.geeksforgeeks.org/split-a-bst-into-two-balanced-bsts-based-on-a-value-k/)

给定一个[二叉查找树](https://www.geeksforgeeks.org/binary-search-tree-set-1-search-and-insertion/)和一个整数 **K** ，我们必须将树拆分为两个 [**平衡的二叉查找树**](https://www.geeksforgeeks.org/convert-normal-bst-balanced-bst/) ，其中 BST-1 由所有小于 K 的节点组成，BST-2 由所有大于或等于 K 的节点组成
**注意:**节点的排列可以是任何东西，但两个 BST 都应该是平衡的。
**示例:**

```
Input:
         40                            
        /   \    
      20     50     
     /  \      \               
    10   35     60
        /      /   
      25      55 
K = 35
Output:
First BST: 10 20 25
Second BST: 35 40 50 55 60
Explanation:
After splitting above BST
about given value K = 35
First Balanced Binary Search Tree is 
         20                            
        /   \    
      10     25 
Second Balanced Binary Search Tree is
         50                            
        /   \    
      35     55     
        \      \               
         40     60
OR
         40                            
        /   \    
      35     55     
            /   \               
           50    60

Input:
         100                            
        /   \    
      20     500     
     /  \                     
    10   30     
           \      
            40 
K = 50
Output:
First BST: 10 20 30 40
Second BST: 100 500
Explanation:
After splitting above BST 
about given value K = 50
First Balanced Binary Search Tree is 
         20                            
        /   \    
      10     30 
                \
                 40
Second Balanced Binary Search Tree is
         100                            
            \    
             500     

```

**进场:**

1.  首先将[存储在一个](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)[数组](https://www.geeksforgeeks.org/array-data-structure/)中，以便遍历给定的 BST
2.  然后，在给定值 K 左右拆分这个数组
3.  现在[通过第一个分割部分构建第一个平衡的 BST](https://www.geeksforgeeks.org/sorted-array-to-balanced-bst/) ，通过第二个分割部分构建第二个 BST，使用本文[中使用的方法](https://www.geeksforgeeks.org/sorted-array-to-balanced-bst/)。

以下是上述方法的实现:

## C++

```
// C++ program to split a BST into
// two balanced BSTs based on a value K

#include <iostream>
using namespace std;

// Structure of each node of BST
struct node {
    int key;
    struct node *left, *right;
};

// A utility function to
// create a new BST node
node* newNode(int item)
{
    node* temp = new node();
    temp->key = item;
    temp->left = temp->right = NULL;
    return temp;
}

// A utility function to insert a new
// node with given key in BST
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

    // return the (unchanged) node pointer
    return node;
}

// Function to return the size
// of the tree
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
                 inOrder, index);

    // Store elements in inorder array
    inOrder[index++] = root->key;

    // Right recursive call
    storeInorder(root->right,
                 inOrder, index);
}

// Function to return the splitting
// index of the array
int getSplittingIndex(int inOrder[],
                      int index, int k)
{
    for (int i = 0; i < index; i++) {
        if (inOrder[i] >= k) {
            return i - 1;
        }
    }
    return index - 1;
}

// Function to create the Balanced
// Binary search tree
node* createBST(int inOrder[],
                int start, int end)
{
    // Base Condition
    if (start > end) {
        return NULL;
    }

    // Calculate the mid of the array
    int mid = (start + end) / 2;
    node* t = newNode(inOrder[mid]);

    // Recursive call for left child
    t->left = createBST(inOrder,
                        start, mid - 1);

    // Recursive call for right child
    t->right = createBST(inOrder,
                         mid + 1, end);

    // Return newly created Balanced
    // Binary Search Tree
    return t;
}

// Function to traverse the tree
// in inorder fashion
void inorderTrav(node* root)
{
    if (root == NULL)
        return;
    inorderTrav(root->left);
    cout << root->key << " ";
    inorderTrav(root->right);
}

// Function to split the BST
// into two Balanced BST
void splitBST(node* root, int k)
{

    // Print the original BST
    cout << "Original BST : ";
    if (root != NULL) {
        inorderTrav(root);
    }
    else {
        cout << "NULL";
    }
    cout << endl;

    // Store the size of BST1
    int numNode = sizeOfTree(root);

    // Take auxiliary array for storing
    // The inorder traversal of BST1
    int inOrder[numNode + 1];
    int index = 0;

    // Function call for storing
    // inorder traversal of BST1
    storeInorder(root, inOrder, index);

    // Function call for getting
    // splitting index
    int splitIndex
        = getSplittingIndex(inOrder,
                            index, k);

    node* root1 = NULL;
    node* root2 = NULL;

    // Creation of first Balanced
    // Binary Search Tree
    if (splitIndex != -1)
        root1 = createBST(inOrder, 0,
                          splitIndex);

    // Creation of Second Balanced
    // Binary Search Tree
    if (splitIndex != (index - 1))
        root2 = createBST(inOrder,
                          splitIndex + 1,
                          index - 1);

    // Print two Balanced BSTs
    cout << "First BST : ";
    if (root1 != NULL) {
        inorderTrav(root1);
    }
    else {
        cout << "NULL";
    }
    cout << endl;

    cout << "Second BST : ";
    if (root2 != NULL) {
        inorderTrav(root2);
    }
    else {
        cout << "NULL";
    }
}

// Driver code
int main()
{
    /*  BST
             5
           /   \     
          3     7    
         / \   / \   
         2  4  6  8 
    */
    struct node* root = NULL;
    root = insert(root, 5);
    insert(root, 3);
    insert(root, 2);
    insert(root, 4);
    insert(root, 7);
    insert(root, 6);
    insert(root, 8);

    int k = 5;

    // Function to split BST
    splitBST(root, k);

    return 0;
}
```

## 蟒蛇 3

```
# Python 3 program to split a
# BST into two balanced BSTs
# based on a value K
index = 0

# Structure of each node of BST
class newNode:
    def __init__(self, item):

        # A utility function to
        # create a new BST node
        self.key = item
        self.left = None
        self.right = None

# A utility function to insert
# a new node with given key
# in BST
def insert(node, key):

    # If the tree is empty,
    # return a new node
    if (node == None):
        return newNode(key)

    # Otherwise, recur down
    # the tree
    if (key < node.key):
        node.left = insert(node.left,
                           key)
    elif (key > node.key):
        node.right = insert(node.right,
                            key)

    # return the (unchanged)
    # node pointer
    return node

# Function to return the
# size of the tree
def sizeOfTree(root):

    if (root == None):
        return 0

    # Calculate left size
    # recursively
    left = sizeOfTree(root.left)

    # Calculate right size
    # recursively
    right = sizeOfTree(root.right)

    # Return total size
    # recursively
    return (left + right + 1)

# Function to store inorder
# traversal of BST
def storeInorder(root, inOrder):

    global index
    # Base condition
    if (root == None):
        return

    # Left recursive call
    storeInorder(root.left,
                 inOrder)

    # Store elements in
    # inorder array
    inOrder[index] = root.key
    index += 1

    # Right recursive call
    storeInorder(root.right,
                 inOrder)

# Function to return the
# splitting index of the
# array
def getSplittingIndex(inOrder,
                      index, k):

    for i in range(index):
        if (inOrder[i] >= k):
            return i - 1
    return index - 1

# Function to create the
# Balanced Binary search
# tree
def createBST(inOrder,
              start, end):

    # Base Condition
    if (start > end):
        return None

    # Calculate the mid of
    # the array
    mid = (start + end) // 2
    t = newNode(inOrder[mid])

    # Recursive call for
    # left child
    t.left = createBST(inOrder,
                       start,
                       mid - 1)

    # Recursive call for
    # right child
    t.right = createBST(inOrder,
                        mid + 1, end)

    # Return newly created
    # Balanced Binary Search
    # Tree
    return t

# Function to traverse
# the tree in inorder
# fashion
def inorderTrav(root):

    if (root == None):
        return

    inorderTrav(root.left)
    print(root.key, end = " ")
    inorderTrav(root.right)

# Function to split the BST
# into two Balanced BST
def splitBST(root, k):

    global index

    # Print the original BST
    print("Original BST : ")
    if (root != None):
        inorderTrav(root)
        print("\n", end = "")
    else:
        print("NULL")

    # Store the size of BST1
    numNode = sizeOfTree(root)

    # Take auxiliary array for
    # storing The inorder traversal
    # of BST1
    inOrder = [0 for i in range(numNode + 1)]
    index = 0

    # Function call for storing
    # inorder traversal of BST1
    storeInorder(root, inOrder)

    # Function call for getting
    # splitting index
    splitIndex = getSplittingIndex(inOrder,
                                   index, k)

    root1 = None
    root2 = None

    # Creation of first Balanced
    # Binary Search Tree
    if (splitIndex != -1):
        root1 = createBST(inOrder,
                          0, splitIndex)

    # Creation of Second Balanced
    # Binary Search Tree
    if (splitIndex != (index - 1)):
        root2 = createBST(inOrder,
                          splitIndex + 1,
                          index - 1)

    # Print two Balanced BSTs
    print("First BST : ")
    if (root1 != None):
        inorderTrav(root1)
        print("\n", end = "")
    else:
        print("NULL")

    print("Second BST : ")
    if (root2 != None):
        inorderTrav(root2)
        print("\n", end = "")
    else:
        print("NULL")

# Driver code
if __name__ == '__main__':

    '''/*  BST
             5
           /   /     
          3     7    
         / /   / /   
         2  4  6  8 
    */'''
    root = None
    root = insert(root, 5)
    insert(root, 3)
    insert(root, 2)
    insert(root, 4)
    insert(root, 7)
    insert(root, 6)
    insert(root, 8)

    k = 5

    # Function to split BST
    splitBST(root, k)

# This code is contributed by Chitranayal
```

**Output:** 

```
Original BST : 2 3 4 5 6 7 8 
First BST : 2 3 4 
Second BST : 5 6 7 8

```