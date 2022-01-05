# 通过将每个节点替换为其前序前驱和后继的总和来修改二叉树

> 原文:[https://www . geeksforgeeks . org/modify-二叉树-通过将每个节点替换为其前序-前序-后序之和/](https://www.geeksforgeeks.org/modify-binary-tree-by-replacing-each-node-with-the-sum-of-its-preorder-predecessor-and-successor/)

给定一个由 **N** 节点组成的[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)，任务是用其[前序前身](https://www.geeksforgeeks.org/preorder-predecessor-node-binary-tree/)和[前序后继](https://www.geeksforgeeks.org/preorder-successor-node-binary-tree/)之和替换二叉树中的每个节点。

**示例:**

> **输入:**
>  ****/*3 4*****
> 
> *   ******对于节点 2:** 前序前置任务= 0(因为前序前置任务不存在)，前序后续任务= 3。总和= 3。****
> *   ******对于节点 3:** 前序前驱= 2，前序后继= 6。总和= 8。****
> *   ******对于节点 6:** 前序前驱= 3，前序后继= 5。总和= 8。****
> *   ******对于节点 5:** 前序前置= 6，前序后续= 4。总和= 10。****
> *   ******对于节点 4:** 前序前置= 5，前序后续= 7。总和= 12。****
> *   ******对于节点 7:** 前序前置= 4，前序后续= 8。总和= 12。****
> *   ******对于节点 8:** 前序前置任务= 7，前序后续任务= 0(因为前序后续任务不存在)。总和= 7。****
> 
> ******输入:***
> ***1*** ***/\*
> *2 3*
> ***输出:***
> ***2*** ***/\*
> 4 2*******

*********方法:**给定的问题可以通过将树的[前序遍历存储在辅助](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)中，然后用[前序前置](https://www.geeksforgeeks.org/preorder-predecessor-node-binary-tree/)和[前序后继](https://www.geeksforgeeks.org/preorder-successor-node-binary-tree/)的和替换每个节点来解决。按照以下步骤解决问题:*******

*   *****声明一个函数，说 **replaceNode(root，A[]，idx)** 到[在树](https://www.geeksforgeeks.org/check-if-a-given-array-can-represent-preorder-traversal-of-binary-search-tree/)上执行前序遍历，起始索引为 **i** ，执行如下步骤:

    *   如果根节点为**空**，则[从功能](https://www.geeksforgeeks.org/return-statement-in-c-cpp-with-examples/)返回。
    *   将当前节点的值替换为**V[I–1]+V[I+1]**对于元素 **V[i]** ，值**V[I–1]**和 **V[i + 1]** 分别为其[前序前置](https://www.geeksforgeeks.org/preorder-predecessor-node-binary-tree/)和[前序后续](https://www.geeksforgeeks.org/preorder-successor-node-binary-tree/)。
    *   递归调用函数 **replaceNode(根- >左，A[]，idx + 1)** 和 **replaceNode(根- >右，A[]，idx + 1)** 。***** 
*   *****初始化一个[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/) **V** ，它存储给定树的[前序遍历。](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)*****
*   *****将 **0** 存储在索引 **0** 中，因为[最左侧叶节点](https://www.geeksforgeeks.org/print-leftmost-and-rightmost-nodes-of-a-binary-tree/)的预订前身不存在。*****
*   *****[对给定的树](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)执行预序遍历，并将预序遍历存储在向量 **V** 中。*****
*   *****将 **0** 存储在向量的[端，作为不存在的](https://www.geeksforgeeks.org/vectorbegin-vectorend-c-stl/)[最右边叶节点](https://www.geeksforgeeks.org/print-leftmost-and-rightmost-nodes-of-a-binary-tree/)的预订后继节点。*****
*   *****调用函数 **replaceNode(根，A[]，1)** 用需要的和替换每个节点。*****
*   *****完成以上步骤后，[打印修改树](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)的预订单。*****

*****下面是上述方法的实现:*****

## *****C++*****

```
*****// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Node of a binary tree
struct Node {
    int data;
    struct Node *left, *right;
};

// Function to generate a new node
struct Node* getnew(int data)
{
    // Allocate node
    struct Node* newnode
        = (struct Node*)malloc(
            sizeof(struct Node));

    // Assign the data value
    newnode->data = data;
    newnode->left = newnode->right = NULL;

    return newnode;
}

// Function to store Preorder Traversal
// of the binary tree in the vector V
void StorePreorderTraversal(
    struct Node* root, vector<int>& v)
{
    // If root is NULL, then return
    if (root == NULL)
        return;

    // Store the root's data in V
    v.push_back(root->data);

    // Recur on the left subtree
    StorePreorderTraversal(
        root->left, v);

    // Recur on right subtree
    StorePreorderTraversal(
        root->right, v);
}

// Function to replace each node of a
// Binary Tree with the sum of its
// preorder predecessor and successor
void ReplaceNodeWithSum(struct Node* root,
                        vector<int>& v,
                        int& i)
{
    // If root does not exist
    if (root == NULL)
        return;

    // Update the data present in the
    // root by the sum of its preorder
    // predecessor and successor
    root->data = v[i - 1] + v[i + 1];

    // Increment index 'i'
    i++;

    // Recur on the left subtree
    ReplaceNodeWithSum(root->left,
                       v, i);

    // Recur on the right subtree
    ReplaceNodeWithSum(root->right,
                       v, i);
}

// Utility function to replace each
// node of a binary tree with the
// sum of its preorder predecessor
// and successor
void ReplaceNodeWithSumUtil(
    struct Node* root)
{
    // If tree is empty, then return
    if (root == NULL)
        return;

    vector<int> v;

    // Stores the value of preorder
    // predecessor for root node
    v.push_back(0);

    // Store the preorder
    // traversal of the tree in V
    StorePreorderTraversal(root, v);

    // Store the value of preorder
    // successor for rightmost leaf
    v.push_back(0);

    // Replace each node
    // with the required sum
    int i = 1;

    // Function call to update
    // the values of the node
    ReplaceNodeWithSum(root, v, i);
}

// Function to print the preorder
// traversal of a binary tree
void PreorderTraversal(
    struct Node* root)
{
    // If root is NULL
    if (root == NULL)
        return;

    // Print the data of node
    cout << root->data << " ";

    // Recur on the left subtree
    PreorderTraversal(root->left);

    // Recur on the right subtree
    PreorderTraversal(root->right);
}

// Driver Code
int main()
{
    // Binary Tree
    struct Node* root = getnew(2);
    root->left = getnew(3);
    root->right = getnew(4);
    root->left->left = getnew(6);
    root->left->right = getnew(5);
    root->right->left = getnew(7);
    root->right->right = getnew(8);

    // Print the preorder traversal
    // of the original tree
    cout << "Preorder Traversal before"
         << " modification of tree: ";
    PreorderTraversal(root);

    ReplaceNodeWithSumUtil(root);

    // Print the preorder traversal
    // of the modified tree
    cout << "\nPreorder Traversal after "
         << "modification of tree: ";
    PreorderTraversal(root);

    return 0;
}*****
```

## *****Java 语言(一种计算机语言，尤用于创建网站)*****

```
*****// Java program for the above approach
import java.util.Vector;

class GFG{

// Node of a binary tree
static class Node
{
    int data;
    Node left, right;
}

// INT class
static class INT
{
    int data;
}

// Function to get a new node
// of a binary tree
static Node getNode(int data)
{

    // Allocate node
    Node new_node = new Node();

    // Put in the data;
    new_node.data = data;
    new_node.left = new_node.right = null;

    return new_node;
}

// Function to print the preorder traversal
// of a binary tree
static void preorderTraversal(Node root)
{

    // If root is null
    if (root == null)
        return;

    // First print the data of node
    System.out.print(root.data + " ");

    // Then recur on left subtree
    preorderTraversal(root.left);

    // Now recur on right subtree
    preorderTraversal(root.right);
}

// Function to replace each node with the sum of its
// preorder predecessor and successor
static void replaceNodeWithSum(Node root,
                               Vector<Integer> V, INT i)
{

    // If root is null
    if (root == null)
        return;

    // Replace node's data with the sum of its
    // preorder predecessor and successor
    root.data = V.get(i.data - 1) +
                V.get(i.data + 1);

    // Move 'i' to point to the next 'V' element
    i.data++;

    // First recur on left child
    replaceNodeWithSum(root.left, V, i);

    // Now recur on right child
    replaceNodeWithSum(root.right, V, i);
}

// Function to store the preorder traversal
// of the binary tree in V
static void storePreorderTraversal(Node root,
                                   Vector<Integer> V)
{

    // If root is null
    if (root == null)
        return;

    // Then store the root's data in 'V'
    V.add(root.data);

    // First recur on left child
    storePreorderTraversal(root.left, V);

    // Now recur on right child
    storePreorderTraversal(root.right, V);
}

// Utility function to replace each node in binary
// tree with the sum of its preorder predecessor
// and successor
static void replaceNodeWithSumUtil(Node root)
{

    // If tree is empty
    if (root == null)
        return;

    Vector<Integer> V = new Vector<Integer>();

    // Store the value of preorder predecessor
    // for the leftmost leaf
    V.add(0);

    // Store the preorder traversal of the tree in V
    storePreorderTraversal(root, V);

    // Store the value of preorder successor
    // for the rightmost leaf
    V.add(0);

    // Replace each node with the required sum
    INT i = new INT();

    i.data = 1;

    replaceNodeWithSum(root, V, i);
}

// Driver code
public static void main(String[] args)
{

    // Binary tree formation
    Node root = getNode(2);
    root.left = getNode(3);
    root.right = getNode(4);
    root.left.left = getNode(6);
    root.left.right = getNode(5);
    root.right.left = getNode(7);
    root.right.right = getNode(8);

    // Print the preorder traversal of the original tree
    System.out.print("Preorder Transversal before " +
                     "modification of tree:\n");
    preorderTraversal(root);

    replaceNodeWithSumUtil(root);

    // Print the preorder traversal of the modification
    // tree
    System.out.print("\nPreorder Transversal after " +
                     "modification of tree:\n");
    preorderTraversal(root);
}
}

// This code is contributed by abhinavjain194*****
```

## *****蟒蛇 3*****

```
*****# Python3 program for the above approach

# Node of a binary tree
class Node:

    def __init__(self, d):

        self.data = d
        self.left = None
        self.right = None

# Function to store Preorder Traversal
# of the binary tree in the vector V
def StorePreorderTraversal(root):

    global v

    # If root is NULL, then return
    if (root == None):
        return

    # Store the root's data in V
    v.append(root.data)

    # Recur on the left subtree
    StorePreorderTraversal(root.left)

    # Recur on right subtree
    StorePreorderTraversal(root.right)

# Function to replace each node of a
# Binary Tree with the sum of its
# preorder predecessor and successor
def ReplaceNodeWithSum(root):

    global v, i

    # If root does not exist
    if (root == None):
        return

    # Update the data present in the
    # root by the sum of its preorder
    # predecessor and successor
    root.data = v[i - 1] + v[i + 1]

    # Increment index 'i'
    i += 1

    # Recur on the left subtree
    ReplaceNodeWithSum(root.left)

    # Recur on the right subtree
    ReplaceNodeWithSum(root.right)

# Utility function to replace each
# node of a binary tree with the
# sum of its preorder predecessor
# and successor
def ReplaceNodeWithSumUtil(root):

    global v, i

    # If tree is empty, then return
    if (root == None):
        return

    v.clear()

    # Stores the value of preorder
    # predecessor for root node
    v.append(0)

    # Store the preorder
    # traversal of the tree in V
    StorePreorderTraversal(root)

    # Store the value of preorder
    # successor for rightmost leaf
    v.append(0)

    # Replace each node
    # with the required sum
    i = 1

    # Function call to update
    # the values of the node
    ReplaceNodeWithSum(root)

# Function to print the preorder
# traversal of a binary tree
def PreorderTraversal(root):

    # If root is NULL
    if (root == None):
        return

    # Print the data of node
    print(root.data, end = " ")

    # Recur on the left subtree
    PreorderTraversal(root.left)

    # Recur on the right subtree
    PreorderTraversal(root.right)

# Driver Code
if __name__ == '__main__':

    # Binary Tree
    v, i = [], 0
    root = Node(2)
    root.left = Node(3)
    root.right = Node(4)
    root.left.left = Node(6)
    root.left.right = Node(5)
    root.right.left = Node(7)
    root.right.right = Node(8)

    # Print the preorder traversal
    # of the original tree
    print("Preorder Traversal before "
          "modification of tree: ", end = "")

    PreorderTraversal(root)

    ReplaceNodeWithSumUtil(root)

    # Print the preorder traversal
    # of the modified tree
    print("\nPreorder Traversal after "
          "modification of tree: ", end = "")

    PreorderTraversal(root)

# This code is contributed by mohit kumar 29*****
```

## *****C#*****

```
*****// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG {

    // TreeNode class
    class Node {
        public int data;
        public Node left, right;
    };

    static int i;

    // Function to get a new node
    // of a binary tree
    static Node getNode(int data)
    {

        // Allocate node
        Node new_node = new Node();

        // Put in the data;
        new_node.data = data;
        new_node.left = new_node.right = null;

        return new_node;
    }

    // Function to print the preorder traversal
    // of a binary tree
    static void preorderTraversal(Node root)
    {

        // If root is null
        if (root == null)
            return;

        // First print the data of node
        Console.Write(root.data + " ");

        // Then recur on left subtree
        preorderTraversal(root.left);

        // Now recur on right subtree
        preorderTraversal(root.right);
    }

    // Function to replace each node with the sum of its
    // preorder predecessor and successor
    static void replaceNodeWithSum(Node root, List<int> V)
    {

        // If root is null
        if (root == null)
            return;

        // Replace node's data with the sum of its
        // preorder predecessor and successor
        root.data = V[i - 1] + V[i + 1];

        // Move 'i' to point to the next 'V' element
        i++;

        // First recur on left child
        replaceNodeWithSum(root.left, V);

        // Now recur on right child
        replaceNodeWithSum(root.right, V);
    }

    // Function to store the preorder traversal
    // of the binary tree in V
    static void storePreorderTraversal(Node root, List<int> V)
    {

        // If root is null
        if (root == null)
            return;

        // Then store the root's data in 'V'
        V.Add(root.data);

        // First recur on left child
        storePreorderTraversal(root.left, V);

        // Now recur on right child
        storePreorderTraversal(root.right, V);
    }

    // Utility function to replace each node in binary
    // tree with the sum of its preorder predecessor
    // and successor
    static void replaceNodeWithSumUtil(Node root)
    {

        // If tree is empty
        if (root == null)
            return;

        List<int> V = new List<int>();

        // Store the value of preorder predecessor
        // for the leftmost leaf
        V.Add(0);

        // Store the preorder traversal of the tree in V
        storePreorderTraversal(root, V);

        // Store the value of preorder successor
        // for the rightmost leaf
        V.Add(0);

        // Replace each node with the required sum
        i = 1;

        replaceNodeWithSum(root, V);
    }

  static void Main() {
    // Binary tree formation
    Node root = getNode(2);
    root.left = getNode(3);
    root.right = getNode(4);
    root.left.left = getNode(6);
    root.left.right = getNode(5);
    root.right.left = getNode(7);
    root.right.right = getNode(8);

    // Print the preorder traversal of the original tree
    Console.Write("Preorder Transversal before " +
                     "modification of tree: ");
    preorderTraversal(root);

    replaceNodeWithSumUtil(root);

    // Print the preorder traversal of the modification
    // tree
    Console.Write("\nPreorder Transversal after " +
                     "modification of tree: ");
    preorderTraversal(root);
  }
}*****
```

## *****java 描述语言*****

```
*****<script>
    // Javascript program for the above approach

    class Node
    {
        constructor(data) {
           this.left = null;
           this.right = null;
           this.data = data;
        }
    }

    // Function to get a new node
    // of a binary tree
    function getNode(data)
    {

        // Allocate node
        let new_node = new Node(data);
        return new_node;
    }

    // Function to print the preorder traversal
    // of a binary tree
    function preorderTraversal(root)
    {

        // If root is null
        if (root == null)
            return;

        // First print the data of node
        document.write(root.data + " ");

        // Then recur on left subtree
        preorderTraversal(root.left);

        // Now recur on right subtree
        preorderTraversal(root.right);
    }

    // Function to replace each node with the sum of its
    // preorder predecessor and successor
    function replaceNodeWithSum(root, V)
    {

        // If root is null
        if (root == null)
            return;

        // Replace node's data with the sum of its
        // preorder predecessor and successor
        root.data = V[data - 1] +
                    V[data + 1];

        // Move 'i' to point to the next 'V' element
        data++;

        // First recur on left child
        replaceNodeWithSum(root.left, V);

        // Now recur on right child
        replaceNodeWithSum(root.right, V);
    }

    // Function to store the preorder traversal
    // of the binary tree in V
    function storePreorderTraversal(root, V)
    {

        // If root is null
        if (root == null)
            return;

        // Then store the root's data in 'V'
        V.push(root.data);

        // First recur on left child
        storePreorderTraversal(root.left, V);

        // Now recur on right child
        storePreorderTraversal(root.right, V);
    }

    // Utility function to replace each node in binary
    // tree with the sum of its preorder predecessor
    // and successor
    function replaceNodeWithSumUtil(root)
    {

        // If tree is empty
        if (root == null)
            return;

        let V = [];

        // Store the value of preorder predecessor
        // for the leftmost leaf
        V.push(0);

        // Store the preorder traversal of the tree in V
        storePreorderTraversal(root, V);

        // Store the value of preorder successor
        // for the rightmost leaf
        V.push(0);

        data = 1;

        replaceNodeWithSum(root, V);
    }

    // Binary tree formation
    let root = getNode(2);
    root.left = getNode(3);
    root.right = getNode(4);
    root.left.left = getNode(6);
    root.left.right = getNode(5);
    root.right.left = getNode(7);
    root.right.right = getNode(8);

    // Print the preorder traversal of the original tree
    document.write("Preorder Transversal before " +
                     "modification of tree : ");
    preorderTraversal(root);

    replaceNodeWithSumUtil(root);

    // Print the preorder traversal of the modification
    // tree
    document.write("</br>" + "Preorder Transversal after " +
                     "modification of tree : ");
    preorderTraversal(root);

</script>*****
```

*******Output:** 

```
Preorder Traversal before modification of tree: 2 3 6 5 4 7 8 
Preorder Traversal after modification of tree: 3 8 8 10 12 12 7
```***** 

********时间复杂度:**O(N)*
T5**辅助空间:** O(N)*****