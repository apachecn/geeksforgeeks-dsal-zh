# 移除给定范围内的 BST 键

> 原文:[https://www . geesforgeks . org/remove-BST-keys-in-a-给定范围/](https://www.geeksforgeeks.org/remove-bst-keys-in-a-given-range/)

给定二叉查找树(BST)和范围[最小，最大]，移除给定范围内的所有键。修改后的树也应该是 BST。例如，考虑以下 BST 和范围[50，70]。

```
             50
          /     \
         30      70
        /  \    /  \
      20   40  60   80 

The given BST should be transformed to this:
            80
          /
         30
        /  \
      20   40
```

每个节点都有两种可能的情况。
1)节点的键在给定范围内。
2)节点的密钥超出范围。

我们不需要为案例 2 做任何事。在案例 1 中，我们需要移除该节点，并更改以该节点为根的子树的根。
想法是以后置的方式固定树。当我们访问一个节点时，我们确保它的左右子树已经固定。当我们在范围内找到一个节点时，我们调用正常的 BST 删除函数来删除该节点。

下面是上述方法的实现。

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>

using namespace std;

class BSTnode {
public:
    int data;
    BSTnode *left, *right;
    BSTnode(int data)
    {
        this->data = data;
        this->left = this->right = NULL;
    }
};

// A Utility function to find leftMost node
BSTnode* leftMost(BSTnode* root)
{
    if (!root)
        return NULL;
    while (root->left)
        root = root->left;
    return root;
}

// A Utility function to delete the give node
BSTnode* deleteNode(BSTnode* root)
{
    // node with only one chile or no child
    if (!root->left) {
        BSTnode* child = root->right;
        root = NULL;
        return child;
    }
    else if (!root->right) {
        BSTnode* child = root->left;
        root = NULL;
        return child;
    }

    // node with two children: get inorder successor
    // in the right subtree
    BSTnode* next = leftMost(root->right);

    // copy the inorder successor's content to this node
    root->data = next->data;

    // delete the inorder successor
    root->right = deleteNode(root->right);

    return root;
}

// function to find node in given range and delete
// it in preorder manner
BSTnode* removeRange(BSTnode* node, int low, int high)
{

    // Base case
    if (!node)
        return NULL;

    // First fix the left and right subtrees of node
    node->left = removeRange(node->left, low, high);
    node->right = removeRange(node->right, low, high);

    // Now fix the node.
    // if given node is in Range then delete it
    if (node->data >= low && node->data <= high)
        return deleteNode(node);

    // Root is out of range
    return node;
}

// Utility function to traverse the binary tree
// after conversion
void inorder(BSTnode* root)
{
    if (root) {
        inorder(root->left);
        cout << root->data << ' ';
        inorder(root->right);
    }
}

// Driver Program to test above functions
int main()
{
    /* Let us create following BST
             50
          /     \
         30      70
        /  \    /  \
      20   40  60   80 */
    BSTnode* root = new BSTnode(50);
    root->left = new BSTnode(30);
    root->right = new BSTnode(70);
    root->left->right = new BSTnode(40);
    root->right->right = new BSTnode(80);
    root->right->left = new BSTnode(60);
    root->left->left = new BSTnode(20);

    cout << "Inorder Before deletion: ";
    inorder(root);

    root = removeRange(root, 50, 70);

    cout << "\nInorder After deletion: ";
    inorder(root);

    cout << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;
class Solution {

    static class BSTnode {

        int data;
        BSTnode left, right;
        BSTnode(int data)
        {
            this.data = data;
            this.left = this.right = null;
        }
    }

    // A Utility function to find leftMost node
    static BSTnode leftMost(BSTnode root)
    {
        if (root == null)
            return null;
        while (root.left != null)
            root = root.left;
        return root;
    }

    // A Utility function to delete the give node
    static BSTnode deleteNode(BSTnode root)
    {
        // node with only one chile or no child
        if (root.left == null) {
            BSTnode child = root.right;
            root = null;
            return child;
        }
        else if (root.right == null) {
            BSTnode child = root.left;
            root = null;
            return child;
        }

        // node with two children: get inorder successor
        // in the right subtree
        BSTnode next = leftMost(root.right);

        // copy the inorder successor's content to this node
        root.data = next.data;

        // delete the inorder successor
        root.right = deleteNode(root.right);

        return root;
    }

    // function to find node in given range and delete
    // it in preorder manner
    static BSTnode removeRange(BSTnode node, int low, int high)
    {

        // Base case
        if (node == null)
            return null;

        // First fix the left and right subtrees of node
        node.left = removeRange(node.left, low, high);
        node.right = removeRange(node.right, low, high);

        // Now fix the node.
        // if given node is in Range then delete it
        if (node.data >= low && node.data <= high)
            return deleteNode(node);

        // Root is out of range
        return node;
    }

    // Utility function to traverse the binary tree
    // after conversion
    static void inorder(BSTnode root)
    {
        if (root != null) {
            inorder(root.left);
            System.out.print(root.data + " ");
            inorder(root.right);
        }
    }

    // Driver Program to test above functions
    public static void main(String args[])
    {
        /* Let us create following BST
             50
          /     \
         30      70
        /  \    /  \
      20   40  60   80 */
        BSTnode root = new BSTnode(50);
        root.left = new BSTnode(30);
        root.right = new BSTnode(70);
        root.left.right = new BSTnode(40);
        root.right.right = new BSTnode(80);
        root.right.left = new BSTnode(60);
        root.left.left = new BSTnode(20);

        System.out.print("Inorder Before deletion: ");
        inorder(root);

        root = removeRange(root, 50, 70);

        System.out.print("\nInorder After deletion: ");
        inorder(root);
    }
}
// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 implementation of the above approach
class BSTnode:

    def __init__(self, data):

        self.data = data
        self.left = None
        self.right = None

# A Utility function to find leftMost node
def leftMost(root):

    if (root == None):
        return None

    while (root.left):
        root = root.left

    return root

# A Utility function to delete the give node
def deleteNode(root):

    # Node with only one chile or no child
    if (root.left == None):
        child = root.right
        root = None
        return child

    elif (root.right == None):
        child = root.left
        root = None
        return child

    # Node with two children: get
    # inorder successor in the
    # right subtree
    next = leftMost(root.right)

    # Copy the inorder successor's
    # content to this node
    root.data = next.data

    # Delete the inorder successor
    root.right = deleteNode(root.right)

    return root

# Function to find node in given range
# and delete it in preorder manner
def removeRange(node, low, high):

    # Base case
    if (node == None):
        return None

    # First fix the left and right subtrees of node
    node.left = removeRange(node.left, low, high)
    node.right = removeRange(node.right, low, high)

    # Now fix the node. If given node
    # is in Range then delete it
    if (node.data >= low and node.data <= high):
        return deleteNode(node)

    # Root is out of range
    return node

# Utility function to traverse the
# binary tree after conversion
def inorder(root):

    if (root):
        inorder(root.left)
        print(root.data, end = " ")
        inorder(root.right)

# Driver code
if __name__ == '__main__':

    '''
    Let us create following BST
             50
          /     \
         30      70
        /  /    /  \
      20   40  60   80
    '''
    root = BSTnode(50)
    root.left = BSTnode(30)
    root.right = BSTnode(70)
    root.left.right = BSTnode(40)
    root.right.right = BSTnode(80)
    root.right.left = BSTnode(60)
    root.left.left = BSTnode(20)

    print("Inorder Before deletion:", end = "")
    inorder(root)

    root = removeRange(root, 50, 70)

    print("\nInorder After deletion:", end = "")
    inorder(root)

# This code is contributed by bgangwar59
```

## C#

```
// C# implementation of the above approach
using System;

class GFG {

    public class BSTnode {

        public int data;
        public BSTnode left, right;
        public BSTnode(int data)
        {
            this.data = data;
            this.left = this.right = null;
        }
    }

    // A Utility function to find leftMost node
    static BSTnode leftMost(BSTnode root)
    {
        if (root == null)
            return null;
        while (root.left != null)
            root = root.left;
        return root;
    }

    // A Utility function to delete the give node
    static BSTnode deleteNode(BSTnode root)
    {
        // node with only one chile or no child
        if (root.left == null) {
            BSTnode child = root.right;
            root = null;
            return child;
        }
        else if (root.right == null) {
            BSTnode child = root.left;
            root = null;
            return child;
        }

        // node with two children: get inorder successor
        // in the right subtree
        BSTnode next = leftMost(root.right);

        // copy the inorder successor's content to this node
        root.data = next.data;

        // delete the inorder successor
        root.right = deleteNode(root.right);

        return root;
    }

    // function to find node in given range and delete
    // it in preorder manner
    static BSTnode removeRange(BSTnode node, int low, int high)
    {

        // Base case
        if (node == null)
            return null;

        // First fix the left and right subtrees of node
        node.left = removeRange(node.left, low, high);
        node.right = removeRange(node.right, low, high);

        // Now fix the node.
        // if given node is in Range then delete it
        if (node.data >= low && node.data <= high)
            return deleteNode(node);

        // Root is out of range
        return node;
    }

    // Utility function to traverse the binary tree
    // after conversion
    static void inorder(BSTnode root)
    {
        if (root != null) {
            inorder(root.left);
            Console.Write(root.data + " ");
            inorder(root.right);
        }
    }

    // Driver code
    public static void Main(String[] args)
    {
        /* Let us create following BST
            50
        /     \
        30     70
        / \ / \
    20 40 60 80 */
        BSTnode root = new BSTnode(50);
        root.left = new BSTnode(30);
        root.right = new BSTnode(70);
        root.left.right = new BSTnode(40);
        root.right.right = new BSTnode(80);
        root.right.left = new BSTnode(60);
        root.left.left = new BSTnode(20);

        Console.Write("Inorder Before deletion: ");
        inorder(root);

        root = removeRange(root, 50, 70);

        Console.Write("\nInorder After deletion: ");
        inorder(root);
    }
}

// This code contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript implementation of the
// above approach
class BSTnode
{
    constructor(data)
    {
        this.left = null;
        this.right = null;
        this.data = data;
    }
}

// A Utility function to find leftMost node
function leftMost(root)
{
    if (root == null)
        return null;
    while (root.left != null)
        root = root.left;

    return root;
}

// A Utility function to delete the give node
function deleteNode(root)
{

    // Node with only one chile or no child
    if (root.left == null)
    {
        let child = root.right;
        root = null;
        return child;
    }
    else if (root.right == null)
    {
        let child = root.left;
        root = null;
        return child;
    }

    // Node with two children: get inorder
    // successor in the right subtree
    let next = leftMost(root.right);

    // Copy the inorder successor's
    // content to this node
    root.data = next.data;

    // Delete the inorder successor
    root.right = deleteNode(root.right);

    return root;
}

// Function to find node in given range
// and delete it in preorder manner
function removeRange(node, low, high)
{

    // Base case
    if (node == null)
        return null;

    // First fix the left and right subtrees of node
    node.left = removeRange(node.left, low, high);
    node.right = removeRange(node.right, low, high);

    // Now fix the node.
    // if given node is in Range then delete it
    if (node.data >= low && node.data <= high)
        return deleteNode(node);

    // Root is out of range
    return node;
}

// Utility function to traverse the binary
// tree after conversion
function inorder(root)
{
    if (root != null)
    {
        inorder(root.left);
        document.write(root.data + " ");
        inorder(root.right);
    }
}

// Driver code

/* Let us create following BST
         50
      /     \
     30      70
    /  \    /  \
  20   40  60   80 */
let root = new BSTnode(50);
root.left = new BSTnode(30);
root.right = new BSTnode(70);
root.left.right = new BSTnode(40);
root.right.right = new BSTnode(80);
root.right.left = new BSTnode(60);
root.left.left = new BSTnode(20);

document.write("Inorder Before deletion: ");
inorder(root);

root = removeRange(root, 50, 70);

document.write("</br>" + "Inorder After deletion: ");
inorder(root);

// This code is contributed by divyeshrabadiya07

</script>
```

**Output:** 

```
Inorder Before deletion: 20 30 40 50 60 70 80 
Inorder After deletion: 20 30 40 80
```