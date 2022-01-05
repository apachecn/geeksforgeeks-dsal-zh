# 改变二叉树，使每个节点都存储左子树中所有节点的总和

> 原文:[https://www . geeksforgeeks . org/change-a-二叉树-以便每个节点都存储左子树中所有节点的总和/](https://www.geeksforgeeks.org/change-a-binary-tree-so-that-every-node-stores-sum-of-all-nodes-in-left-subtree/)

给定一棵二叉树，将每个节点中的值更改为左子树中节点的所有值的总和，包括它自己的值。
**例:**

```
Input : 
     1
   /   \
 2      3

Output :
    3
  /   \
 2     3

Input
       1
      / \
     2   3
    / \   \
   4   5   6
Output:
      12
     / \
    6   3
   / \   \
  4   5   6
```

**我们强烈建议你尽量减少浏览器，先自己试试这个。**
想法是以自下而上的方式遍历给定的树。对于每个节点，递归计算左右子树中节点的和。将左子树中的节点和添加到当前节点，并返回当前子树下的节点和。
以下是以上思路的实现。

## C++

```
// C++ program to store sum of nodes
// in left subtree in every node
#include<bits/stdc++.h>

using namespace std;

// A tree node
class node
{
    public:
    int data;
    node* left, *right;

    /* Constructor that allocates a new node with the
    given data and NULL left and right pointers. */
    node(int data)
    {
        this->data = data;
        this->left = NULL;
        this->right = NULL;
    }
};

// Function to modify a Binary Tree
// so that every node stores sum of
// values in its left child including
// its own value
int updatetree(node *root)
{
    // Base cases
    if (!root)
        return 0;
    if (root->left == NULL && root->right == NULL)
        return root->data;

    // Update left and right subtrees
    int leftsum = updatetree(root->left);
    int rightsum = updatetree(root->right);

    // Add leftsum to current node
    root->data += leftsum;

    // Return sum of values under root
    return root->data + rightsum;
}

// Utility function to do inorder traversal
void inorder(node* node)
{
    if (node == NULL)
        return;
    inorder(node->left);
    cout<<node->data<<" ";
    inorder(node->right);
}

// Driver code
int main()
{
    /* Let us construct below tree
                1
            / \
            2 3
            / \ \
            4 5 6 */
    struct node *root = new node(1);
    root->left     = new node(2);
    root->right = new node(3);
    root->left->left = new node(4);
    root->left->right = new node(5);
    root->right->right = new node(6);

    updatetree(root);

    cout << "Inorder traversal of the modified tree is: \n";
    inorder(root);
    return 0;
}

// This code is contributed by rathbhupendra
```

## C

```
// C program to store  sum of nodes in left subtree in every
// node
#include<bits/stdc++.h>
using namespace std;

// A tree node
struct node
{
    int data;
    struct node* left,  *right;
};

// Function to modify a Binary Tree so that every node
// stores sum of values in its left child including its
// own value
int updatetree(node *root)
{
    // Base cases
    if (!root)
        return 0;
    if (root->left == NULL && root->right == NULL)
        return root->data;

    // Update left and right subtrees
    int leftsum  = updatetree(root->left);
    int rightsum = updatetree(root->right);

    // Add leftsum to current node
    root->data += leftsum;

    // Return sum of values under root
    return root->data + rightsum;
}

// Utility function to do inorder traversal
void inorder(struct node* node)
{
    if (node == NULL)
        return;
    inorder(node->left);
    printf("%d ", node->data);
    inorder(node->right);
}

// Utility function to create a new node
struct node* newNode(int data)
{
    struct node* node =
        (struct node*)malloc(sizeof(struct node));
    node->data = data;
    node->left = NULL;
    node->right = NULL;
    return(node);
}

// Driver program
int main()
{
    /* Let us construct below tree
                1
               / \
              2   3
             / \   \
            4   5   6    */
    struct node *root  = newNode(1);
    root->left         = newNode(2);
    root->right        = newNode(3);
    root->left->left   = newNode(4);
    root->left->right  = newNode(5);
    root->right->right = newNode(6);

    updatetree(root);

    cout << "Inorder traversal of the modified tree is \n";
    inorder(root);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to store sum of nodes in left subtree in every
// node
class GfG {

// A tree node
static class node
{
    int data;
    node left, right;
}

// Function to modify a Binary Tree so that every node
// stores sum of values in its left child including its
// own value
static int updatetree(node root)
{
    // Base cases
    if (root == null)
        return 0;
    if (root.left == null && root.right == null)
        return root.data;

    // Update left and right subtrees
    int leftsum = updatetree(root.left);
    int rightsum = updatetree(root.right);

    // Add leftsum to current node
    root.data += leftsum;

    // Return sum of values under root
    return root.data + rightsum;
}

// Utility function to do inorder traversal
static void inorder(node node)
{
    if (node == null)
        return;
    inorder(node.left);
    System.out.print(node.data + " ");
    inorder(node.right);
}

// Utility function to create a new node
static node newNode(int data)
{
    node node = new node();
    node.data = data;
    node.left = null;
    node.right = null;
    return(node);
}

// Driver program
public static void main(String[] args)
{
    /* Let us construct below tree
                1
            / \
            2 3
            / \ \
            4 5 6 */
    node root = newNode(1);
    root.left         = newNode(2);
    root.right     = newNode(3);
    root.left.left = newNode(4);
    root.left.right = newNode(5);
    root.right.right = newNode(6);

    updatetree(root);

    System.out.println("Inorder traversal of the modified tree is");
    inorder(root);
}
}
```

## 蟒蛇 3

```
# Python3 program to store sum of nodes
# in left subtree in every node

# Binary Tree Node

# utility that allocates a new Node
# with the given key
class newNode:

    # Construct to create a new node
    def __init__(self, key):
        self.data = key
        self.left = None
        self.right = None

# Function to modify a Binary Tree so
# that every node stores sum of values
# in its left child including its own value
def updatetree(root):

    # Base cases
    if (not root):
        return 0
    if (root.left == None and
        root.right == None) :
        return root.data

    # Update left and right subtrees
    leftsum = updatetree(root.left)
    rightsum = updatetree(root.right)

    # Add leftsum to current node
    root.data += leftsum

    # Return sum of values under root
    return root.data + rightsum

# Utility function to do inorder traversal
def inorder(node) :

    if (node == None) :
        return
    inorder(node.left)
    print(node.data, end = " ")
    inorder(node.right)

# Driver Code
if __name__ == '__main__':

    """ Let us con below tree
                    1
                / \
                2 3
                / \ \
                4 5 6 """
    root = newNode(1)
    root.left = newNode(2)
    root.right = newNode(3)
    root.left.left = newNode(4)
    root.left.right = newNode(5)
    root.right.right = newNode(6)

    updatetree(root)

    print("Inorder traversal of the modified tree is")
    inorder(root)

# This code is contributed by
# Shubham Singh(SHUBHAMSINGH10)
```

## C#

```
// C# program to store sum of nodes in left 
// subtree in every node
using System;

class GfG
{

// A tree node
class node
{
    public int data;
    public node left, right;
}

// Function to modify a Binary Tree so
// that every node stores sum of values
// in its left child including its own value
static int updatetree(node root)
{
    // Base cases
    if (root == null)
        return 0;
    if (root.left == null && root.right == null)
        return root.data;

    // Update left and right subtrees
    int leftsum = updatetree(root.left);
    int rightsum = updatetree(root.right);

    // Add leftsum to current node
    root.data += leftsum;

    // Return sum of values under root
    return root.data + rightsum;
}

// Utility function to do inorder traversal
static void inorder(node node)
{
    if (node == null)
        return;
    inorder(node.left);
    Console.Write(node.data + " ");
    inorder(node.right);
}

// Utility function to create a new node
static node newNode(int data)
{
    node node = new node();
    node.data = data;
    node.left = null;
    node.right = null;
    return(node);
}

// Driver code
public static void Main()
{
    /* Let us construct below tree
                1
            / \
            2 3
            / \ \
            4 5 6 */
    node root = newNode(1);
    root.left = newNode(2);
    root.right = newNode(3);
    root.left.left = newNode(4);
    root.left.right = newNode(5);
    root.right.right = newNode(6);

    updatetree(root);

    Console.WriteLine("Inorder traversal of the modified tree is");
    inorder(root);
}
}

/* This code is contributed by Rajput-Ji*/
```

## java 描述语言

```
<script>

// Javascript program to store sum of nodes in left 
// subtree in every node

// A tree node
class node
{
  constructor()
  {
    this.data = 0;
    this.left = null;
    this.right = null;
  }
}

// Function to modify a Binary Tree so
// that every node stores sum of values
// in its left child including its own value
function updatetree(root)
{
    // Base cases
    if (root == null)
        return 0;
    if (root.left == null && root.right == null)
        return root.data;

    // Update left and right subtrees
    var leftsum = updatetree(root.left);
    var rightsum = updatetree(root.right);

    // Add leftsum to current node
    root.data += leftsum;

    // Return sum of values under root
    return root.data + rightsum;
}

// Utility function to do inorder traversal
function inorder(node)
{
    if (node == null)
        return;
    inorder(node.left);
    document.write(node.data + " ");
    inorder(node.right);
}

// Utility function to create a new node
function newNode(data)
{
    var nod = new node();
    nod.data = data;
    nod.left = null;
    nod.right = null;
    return(nod);
}

// Driver code
/* Let us construct below tree
            1
        / \
        2 3
        / \ \
        4 5 6 */
var root = newNode(1);
root.left = newNode(2);
root.right = newNode(3);
root.left.left = newNode(4);
root.left.right = newNode(5);
root.right.right = newNode(6);
updatetree(root);
document.write("Inorder traversal of the modified tree is<br>");
inorder(root);

// This code is contributed by rrrtnx.
</script>
```

**输出:**

```
Inorder traversal of the modified tree is
4 6 5 12 3 6
```

**时间复杂度:** O(n)

https://www.youtube.com/watch?v=EkmG

-fkrbq〔t0〕

感谢 Gaurav Ahrirwar 提出这个解决方案。
发现有不正确的地方请写评论，或者想分享更多以上讨论话题的信息