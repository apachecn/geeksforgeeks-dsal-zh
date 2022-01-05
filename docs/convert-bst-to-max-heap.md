# 将 BST 转换为最大堆

> 原文:[https://www.geeksforgeeks.org/convert-bst-to-max-heap/](https://www.geeksforgeeks.org/convert-bst-to-max-heap/)

给定一个也是完全二叉树的[二叉查找树](https://www.geeksforgeeks.org/binary-search-tree-data-structure/)。问题是在一个节点的左子树中的所有值都应该小于该节点的右子树中的所有值的条件下，将一个给定的 BST 转换成一个特殊的 Max Heap。此条件应用于如此转换的最大堆中的所有节点。
示例:

```
Input :          4
               /   \
              2     6
            /  \   /  \
           1   3  5    7  

Output :       7
             /   \
            3     6
          /   \  /   \
         1    2 4     5
The given BST has been transformed into a
Max Heap.
All the nodes in the Max Heap satisfies the given
condition, that is, values in the left subtree of
a node should be less than the values in the right
subtree of the node. 
```

**先决条件** : [二叉查找树](https://www.geeksforgeeks.org/binary-search-tree-data-structure/) | [堆](https://www.geeksforgeeks.org/heap-data-structure/)
接近 T9】1。创建一个大小为 n 的数组 **arr[]** ，其中 n 是给定 BST 中的节点数。
2。执行 BST 的有序遍历，并按照排序后的
顺序复制 **arr[]** 中的节点值。
3。现在执行树的后置遍历。
4。在后序遍历过程中遍历根时，将数组**中的值逐个复制到节点中。** 

## C++

```
// C++ implementation to convert a given
// BST to Max Heap
#include <bits/stdc++.h>
using namespace std;

struct Node {
    int data;
    Node *left, *right;
};

/* Helper function that allocates a new node
with the given data and NULL left and right
pointers. */
struct Node* getNode(int data)
{
    struct Node* newNode = new Node;
    newNode->data = data;
    newNode->left = newNode->right = NULL;
    return newNode;
}

// Function prototype for postorder traversal
// of the given tree
void postorderTraversal(Node*);

// Function for the inorder traversal of the tree
// so as to store the node values in 'arr' in
// sorted order
void inorderTraversal(Node* root, vector<int>& arr)
{
    if (root == NULL)
        return;

    // first recur on left subtree
    inorderTraversal(root->left, arr);

    // then copy the data of the node
    arr.push_back(root->data);

    // now recur for right subtree
    inorderTraversal(root->right, arr);
}

void BSTToMaxHeap(Node* root, vector<int> &arr, int* i)
{
    if (root == NULL)
        return;

    // recur on left subtree
    BSTToMaxHeap(root->left, arr, i);

    // recur on right subtree
    BSTToMaxHeap(root->right, arr, i);

    // copy data at index 'i' of 'arr' to
    // the node
    root->data = arr[++*i];
}

// Utility function to convert the given BST to
// MAX HEAP
void convertToMaxHeapUtil(Node* root)
{
    // vector to store the data of all the
    // nodes of the BST
    vector<int> arr;
    int i = -1;

    // inorder traversal to populate 'arr'
    inorderTraversal(root, arr);

    // BST to MAX HEAP conversion
    BSTToMaxHeap(root, arr, &i);
}

// Function to Print Postorder Traversal of the tree
void postorderTraversal(Node* root)
{
    if (!root)
        return;

    // recur on left subtree
    postorderTraversal(root->left);

    // then recur on right subtree
    postorderTraversal(root->right);

    // print the root's data
    cout << root->data << " ";
}

// Driver Code
int main()
{
    // BST formation
    struct Node* root = getNode(4);
    root->left = getNode(2);
    root->right = getNode(6);
    root->left->left = getNode(1);
    root->left->right = getNode(3);
    root->right->left = getNode(5);
    root->right->right = getNode(7);

    convertToMaxHeapUtil(root);
    cout << "Postorder Traversal of Tree:" << endl;
    postorderTraversal(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to convert a given
// BST to Max Heap
import java.util.*;

class GFG
{

static int i;
static class Node
{
    int data;
    Node left, right;
};

/* Helper function that allocates a new node
with the given data and null left and right
pointers. */
static Node getNode(int data)
{
    Node newNode = new Node();
    newNode.data = data;
    newNode.left = newNode.right = null;
    return newNode;
}

// Function for the inorder traversal of the tree
// so as to store the node values in 'arr' in
// sorted order
static void inorderTraversal(Node root, Vector<Integer> arr)
{
    if (root == null)
        return;

    // first recur on left subtree
    inorderTraversal(root.left, arr);

    // then copy the data of the node
    arr.add(root.data);

    // now recur for right subtree
    inorderTraversal(root.right, arr);
}

static void BSTToMaxHeap(Node root, Vector<Integer> arr)
{
    if (root == null)
        return;

    // recur on left subtree
    BSTToMaxHeap(root.left, arr);

    // recur on right subtree
    BSTToMaxHeap(root.right, arr);

    // copy data at index 'i' of 'arr' to
    // the node
    root.data = arr.get(i++);
}

// Utility function to convert the given BST to
// MAX HEAP
static void convertToMaxHeapUtil(Node root)
{
    // vector to store the data of all the
    // nodes of the BST
    Vector<Integer> arr = new Vector<Integer>();
    int i = -1;

    // inorder traversal to populate 'arr'
    inorderTraversal(root, arr);

    // BST to MAX HEAP conversion
    BSTToMaxHeap(root, arr);
}

// Function to Print Postorder Traversal of the tree
static void postorderTraversal(Node root)
{
    if (root == null)
        return;

    // recur on left subtree
    postorderTraversal(root.left);

    // then recur on right subtree
    postorderTraversal(root.right);

    // print the root's data
    System.out.print(root.data + " ");
}

// Driver Code
public static void main(String[] args)
{
    // BST formation
    Node root = getNode(4);
    root.left = getNode(2);
    root.right = getNode(6);
    root.left.left = getNode(1);
    root.left.right = getNode(3);
    root.right.left = getNode(5);
    root.right.right = getNode(7);

    convertToMaxHeapUtil(root);
    System.out.print("Postorder Traversal of Tree:" +"\n");
    postorderTraversal(root);

}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation to convert a given
# BST to Max Heap
i = 0
class Node:
    def __init__(self):
        self.data = 0
        self.left = None
        self.right = None

# Helper function that allocates a new node
# with the given data and None left and right
# pointers.
def getNode(data):

    newNode = Node()
    newNode.data = data
    newNode.left = newNode.right = None
    return newNode

arr = []

# Function for the inorder traversal of the tree
# so as to store the node values in 'arr' in
# sorted order
def inorderTraversal( root):

    if (root == None):
        return arr

    # first recur on left subtree
    inorderTraversal(root.left)

    # then copy the data of the node
    arr.append(root.data)

    # now recur for right subtree
    inorderTraversal(root.right)

def BSTToMaxHeap(root):

    global i
    if (root == None):
        return None

    # recur on left subtree
    root.left = BSTToMaxHeap(root.left)

    # recur on right subtree
    root.right = BSTToMaxHeap(root.right)

    # copy data at index 'i' of 'arr' to
    # the node
    root.data = arr[i]
    i = i + 1
    return root

# Utility function to convert the given BST to
# MAX HEAP
def convertToMaxHeapUtil( root):
    global i

    # vector to store the data of all the
    # nodes of the BST
    i = 0

    # inorder traversal to populate 'arr'
    inorderTraversal(root)

    # BST to MAX HEAP conversion
    root = BSTToMaxHeap(root)
    return root

# Function to Print Postorder Traversal of the tree
def postorderTraversal(root):

    if (root == None):
        return

    # recur on left subtree
    postorderTraversal(root.left)

    # then recur on right subtree
    postorderTraversal(root.right)

    # print the root's data
    print(root.data ,end= " ")

# Driver Code

# BST formation
root = getNode(4)
root.left = getNode(2)
root.right = getNode(6)
root.left.left = getNode(1)
root.left.right = getNode(3)
root.right.left = getNode(5)
root.right.right = getNode(7)

root = convertToMaxHeapUtil(root)
print("Postorder Traversal of Tree:" )
postorderTraversal(root)

# This code is contributed by Arnab Kundu
```

## java 描述语言

```
<script>
// Javascript implementation to convert a given
// BST to Max Heap

let i = 0;

class Node
{
    constructor()
    {
        this.data = 0;
        this.left = this.right = null;
    }
}

/* Helper function that allocates a new node
   with the given data and null left and right
   pointers. */
function getNode(data)
{
    let newNode = new Node();
    newNode.data = data;
    newNode.left = newNode.right = null;
    return newNode;
}

// Function for the inorder traversal of the tree
// so as to store the node values in 'arr' in
// sorted order
function inorderTraversal(root, arr)
{
    if (root == null)
        return;

    // first recur on left subtree
    inorderTraversal(root.left, arr);

    // then copy the data of the node
    arr.push(root.data);

    // now recur for right subtree
    inorderTraversal(root.right, arr);
}

function BSTToMaxHeap(root,arr)
{

    if (root == null)
        return;

    // recur on left subtree
    BSTToMaxHeap(root.left, arr);

    // recur on right subtree
    BSTToMaxHeap(root.right, arr);

    // copy data at index 'i' of 'arr' to
    // the node

    root.data = arr[i++];

}

// Utility function to convert the given BST to
// MAX HEAP
function convertToMaxHeapUtil(root)
{
    // vector to store the data of all the
    // nodes of the BST
    let arr = [];

    // inorder traversal to populate 'arr'
    inorderTraversal(root, arr);

    // BST to MAX HEAP conversion
    BSTToMaxHeap(root, arr);

}

// Function to Print Postorder Traversal of the tree
function postorderTraversal(root)
{
    if (root == null)
        return;

    // recur on left subtree
    postorderTraversal(root.left);

    // then recur on right subtree
    postorderTraversal(root.right);

    // print the root's data
    document.write(root.data + " ");
}

// Driver Code
// BST formation
let root = getNode(4);
root.left = getNode(2);
root.right = getNode(6);
root.left.left = getNode(1);
root.left.right = getNode(3);
root.right.left = getNode(5);
root.right.right = getNode(7);

convertToMaxHeapUtil(root);
document.write("Postorder Traversal of Tree:" +"\n");
postorderTraversal(root);

// This code is contributed by rag2127
</script>
```

**输出:**

```
Postorder Traversal of Tree:
1 2 3 4 5 6 7 
```

**时间复杂度** : O(n)
**辅助空间** : O(n)
其中，n 为树中节点数