# 修改二叉树，仅使用右指针进行前序遍历

> 原文:[https://www . geesforgeks . org/modify-二叉树-get-preorder-遍历-使用右指针/](https://www.geeksforgeeks.org/modify-binary-tree-get-preorder-traversal-using-right-pointers/)

给定一棵二叉树。以这样一种方式修改它，在修改之后，您可以只使用正确的指针对它进行一次前序遍历。在修改过程中，您可以使用右指针和左指针。
示例:

```
Input :    10
          /   \
        8      2
      /  \    
    3     5  
Output :    10
              \
               8
                \ 
                 3
                  \
                   5
                    \
                     2
Explanation : The preorder traversal
of given binary tree is 10 8 3 5 2.
```

**方法 1(递归)**
需要使根的右指针指向左子树。
如果节点刚刚离开子节点，那么只需将子节点向右移动，即可完成对该节点的处理。
如果也有一个右子树，那么应该是原左子树最右边的**右子树。**
上面的函数用在代码中处理一个节点，然后返回变换后的子树最右边的节点。

## C++

```
// C code to modify binary tree for
// traversal using only right pointer
#include <bits/stdc++.h>

using namespace std;

// A binary tree node has data,
// left child and right child
struct Node {
    int data;
    struct Node* left;
    struct Node* right;
};

// function that allocates a new node
// with the given data and NULL left
// and right pointers.
struct Node* newNode(int data)
{
    struct Node* node = new struct Node;
    node->data = data;
    node->left = NULL;
    node->right = NULL;
    return (node);
}

// Function to modify tree
struct Node* modifytree(struct Node* root)
{
    struct Node* right = root->right;
    struct Node* rightMost = root;

    // if the left tree exists
    if (root->left) {

        // get the right-most of the
        // original left subtree
        rightMost = modifytree(root->left);

        // set root right to left subtree
        root->right = root->left;
        root->left = NULL;
    }

    // if the right subtree does
    // not exists we are done!
    if (!right)
        return rightMost;

    // set right pointer of right-most
    // of the original left subtree
    rightMost->right = right;

    // modify the rightsubtree
    rightMost = modifytree(right);
    return rightMost;
}

// printing using right pointer only
void printpre(struct Node* root)
{
    while (root != NULL) {
        cout << root->data << " ";
        root = root->right;
    }
}

// Driver program to test above functions
int main()
{
    /* Constructed binary tree is
         10
        / \
       8   2
      / \ 
     3   5     */
    struct Node* root = newNode(10);
    root->left = newNode(8);
    root->right = newNode(2);
    root->left->left = newNode(3);
    root->left->right = newNode(5);

    modifytree(root);
    printpre(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to modify binary tree for
// traversal using only right pointer
class GFG
{

// A binary tree node has data,
// left child and right child
static class Node
{
    int data;
    Node left;
    Node right;
};

// function that allocates a new node
// with the given data and null left
// and right pointers.
static Node newNode(int data)
{
    Node node = new Node();
    node.data = data;
    node.left = null;
    node.right = null;
    return (node);
}

// Function to modify tree
static Node modifytree( Node root)
{
    Node right = root.right;
    Node rightMost = root;

    // if the left tree exists
    if (root.left != null)
    {

        // get the right-most of the
        // original left subtree
        rightMost = modifytree(root.left);

        // set root right to left subtree
        root.right = root.left;
        root.left = null;
    }

    // if the right subtree does
    // not exists we are done!
    if (right == null)
        return rightMost;

    // set right pointer of right-most
    // of the original left subtree
    rightMost.right = right;

    // modify the rightsubtree
    rightMost = modifytree(right);
    return rightMost;
}

// printing using right pointer only
static void printpre( Node root)
{
    while (root != null)
    {
        System.out.print( root.data + " ");
        root = root.right;
    }
}

// Driver cde
public static void main(String args[])
{
    /* Constructed binary tree is
        10
        / \
    8 2
    / \
    3 5 */
    Node root = newNode(10);
    root.left = newNode(8);
    root.right = newNode(2);
    root.left.left = newNode(3);
    root.left.right = newNode(5);

    modifytree(root);
    printpre(root);
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python code to modify binary tree for
# traversal using only right pointer

class newNode():

    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# Function to modify tree
def modifytree(root):

    right = root.right
    rightMost = root

    # if the left tree exists
    if (root.left):

        # get the right-most of the
        # original left subtree
        rightMost = modifytree(root.left)

        # set root right to left subtree
        root.right = root.left
        root.left = None

    # if the right subtree does
    # not exists we are done!
    if (not right):
        return rightMost

    # set right pointer of right-most
    # of the original left subtree
    rightMost.right = right

    # modify the rightsubtree
    rightMost = modifytree(right)
    return rightMost

# printing using right pointer only
def printpre(root):

    while (root != None):
        print(root.data,end=" ")
        root = root.right

# Driver code
if __name__ == '__main__':
    """ Constructed binary tree is
    10
        / \
    8 2
    / \
    3 5     """
    root = newNode(10)
    root.left = newNode(8)
    root.right = newNode(2)
    root.left.left = newNode(3)
    root.left.right = newNode(5)

    modifytree(root)
    printpre(root)

# This code is contributed by SHUBHAMSINGH10
```

## C#

```
// C# code to modify binary tree for
// traversal using only right pointer
using System;

class GFG
{

// A binary tree node has data,
// left child and right child
public class Node
{
    public int data;
    public Node left;
    public Node right;
};

// function that allocates a new node
// with the given data and null left
// and right pointers.
static Node newNode(int data)
{
    Node node = new Node();
    node.data = data;
    node.left = null;
    node.right = null;
    return (node);
}

// Function to modify tree
static Node modifytree( Node root)
{
    Node right = root.right;
    Node rightMost = root;

    // if the left tree exists
    if (root.left != null)
    {

        // get the right-most of the
        // original left subtree
        rightMost = modifytree(root.left);

        // set root right to left subtree
        root.right = root.left;
        root.left = null;
    }

    // if the right subtree does
    // not exists we are done!
    if (right == null)
        return rightMost;

    // set right pointer of right-most
    // of the original left subtree
    rightMost.right = right;

    // modify the rightsubtree
    rightMost = modifytree(right);
    return rightMost;
}

// printing using right pointer only
static void printpre( Node root)
{
    while (root != null)
    {
        Console.Write( root.data + " ");
        root = root.right;
    }
}

// Driver cde
public static void Main(String []args)
{
    /* Constructed binary tree is
        10
        / \
    8 2
    / \
    3 5 */
    Node root = newNode(10);
    root.left = newNode(8);
    root.right = newNode(2);
    root.left.left = newNode(3);
    root.left.right = newNode(5);

    modifytree(root);
    printpre(root);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

    // JavaScript code to modify binary tree for
    // traversal using only right pointer

    // A binary tree node has data,
    // left child and right child
    class Node
    {
        constructor(data) {
           this.left = null;
           this.right = null;
           this.data = data;
        }
    }

    // function that allocates a new node
    // with the given data and null left
    // and right pointers.
    function newNode(data)
    {
        let node = new Node(data);
        return (node);
    }

    // Function to modify tree
    function modifytree(root)
    {
        let right = root.right;
        let rightMost = root;

        // if the left tree exists
        if (root.left != null)
        {

            // get the right-most of the
            // original left subtree
            rightMost = modifytree(root.left);

            // set root right to left subtree
            root.right = root.left;
            root.left = null;
        }

        // if the right subtree does
        // not exists we are done!
        if (right == null)
            return rightMost;

        // set right pointer of right-most
        // of the original left subtree
        rightMost.right = right;

        // modify the rightsubtree
        rightMost = modifytree(right);
        return rightMost;
    }

    // printing using right pointer only
    function printpre(root)
    {
        while (root != null)
        {
            document.write( root.data + " ");
            root = root.right;
        }
    }

    /* Constructed binary tree is
        10
        / \
        8 2
        / \
        3 5 */
    let root = newNode(10);
    root.left = newNode(8);
    root.right = newNode(2);
    root.left.left = newNode(3);
    root.left.right = newNode(5);

    modifytree(root);
    printpre(root);

</script>
```

**Output:** 

```
10 8 3 5 2 
```