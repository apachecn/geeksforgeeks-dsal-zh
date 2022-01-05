# 对称树(自身镜像)

> 原文:[https://www . geesforgeks . org/symmetric-tree-tree-这是自身的镜像/](https://www.geeksforgeeks.org/symmetric-tree-tree-which-is-mirror-image-of-itself/)

给定一棵二叉树，检查它是否是自身的镜像。

**例如，**这个二叉树是对称的:

```
     1
   /   \
  2     2
 / \   / \
3   4 4   3

But the following is not:
    1
   / \
  2   2
   \   \
   3    3
```

其思想是编写一个递归函数 isMirror()，该函数以两棵树作为参数，如果树是镜像，则返回 true，如果树不是镜像，则返回 false。isMirror()函数递归检查根下的两个根和子树。

下面是上述算法的实现。

## C++14

```
// C++ program to check if a given 
// Binary Tree is symmetric or not
#include <bits/stdc++.h>
using namespace std;

// A Binary Tree Node
struct Node 
{
    int key;
    struct Node *left, *right;
};

// Utility function to create new Node
Node* newNode(int key)
{
    Node* temp = new Node;
    temp->key = key;
    temp->left = temp->right = NULL;
    return (temp);
}

// Returns true if trees 
// with roots as root1 and root2 are mirror
bool isMirror(struct Node* root1, struct Node* root2)
{
    // If both trees are empty, 
    // then they are mirror images
    if (root1 == NULL && root2 == NULL)
        return true;

    // For two trees to be mirror 
    // images, the following
    // three conditions must be true 
    // 1 - Their root node's
    // key must be same 2 - left 
    // subtree of left tree and right subtree
    // of right tree have to be mirror images
    // 3 - right subtree of left tree and left subtree
    // of right tree have to be mirror images
    if (root1 && root2 && root1->key == root2->key)
        return isMirror(root1->left, root2->right)
               && isMirror(root1->right, root2->left);

    // if none of above conditions is true then root1
    // and root2 are not mirror images
    return false;
}

// Returns true if a tree is 
// symmetric i.e. mirror image of itself
bool isSymmetric(struct Node* root)
{
    // Check if tree is mirror of itself
    return isMirror(root, root);
}

// Driver code
int main()
{
    // Let us construct the Tree shown in the above figure
    Node* root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(2);
    root->left->left = newNode(3);
    root->left->right = newNode(4);
    root->right->left = newNode(4);
    root->right->right = newNode(3);

    if(isSymmetric(root))
      cout<<"Symmetric";
    else
      cout<<"Not symmetric"; 
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check is 
// binary tree is symmetric or not
class Node {
    int key;
    Node left, right;

    Node(int item)
    {
        key = item;
        left = right = null;
    }
}

class BinaryTree {
    Node root;

    // returns true if trees
    //  with roots as root1 and root2are mirror
    boolean isMirror(Node node1, Node node2)
    {
        // if both trees are empty,
        //  then they are mirror image
        if (node1 == null && node2 == null)
            return true;

        // For two trees to be mirror images, the following
        // three conditions must be true 1 - Their root
        // node's key must be same 2 - left subtree of left
        // tree and right subtree
        //      of right tree have to be mirror images
        // 3 - right subtree of left tree and left subtree
        //      of right tree have to be mirror images
        if (node1 != null && node2 != null
            && node1.key == node2.key)
            return (isMirror(node1.left, node2.right)
                    && isMirror(node1.right, node2.left));

        // if none of the above conditions is true then
        // root1 and root2 are not mirror images
        return false;
    }

    // returns true if the tree is symmetric i.e
    // mirror image of itself
    boolean isSymmetric()
    {
        // check if tree is mirror of itself
        return isMirror(root, root);
    }

    // Driver code
    public static void main(String args[])
    {
        BinaryTree tree = new BinaryTree();
        tree.root = new Node(1);
        tree.root.left = new Node(2);
        tree.root.right = new Node(2);
        tree.root.left.left = new Node(3);
        tree.root.left.right = new Node(4);
        tree.root.right.left = new Node(4);
        tree.root.right.right = new Node(3);
        boolean output = tree.isSymmetric();
        if (output == true)
            System.out.println("Symmetric");
        else
            System.out.println("Not symmetric");
    }
}

// This code has been contributed by Mayank Jaiswal
```

## 计算机编程语言

```
# Python program to check if a 
# given Binary Tree is symmetric or not

# Node structure

class Node:

    # Utility function to create new node
    def __init__(self, key):
        self.key = key
        self.left = None
        self.right = None

# Returns True if trees 
#with roots as root1 and root 2  are mirror

def isMirror(root1, root2):
    # If both trees are empty, then they are mirror images
    if root1 is None and root2 is None:
        return True

    """ For two trees to be mirror images, 
        the following three conditions must be true
        1 - Their root node's key must be same
        2 - left subtree of left tree and right subtree
          of the right tree have to be mirror images
        3 - right subtree of left tree and left subtree
           of right tree have to be mirror images
    """
    if (root1 is not None and root2 is not None):
        if root1.key == root2.key:
            return (isMirror(root1.left, root2.right)and
                    isMirror(root1.right, root2.left))

    # If none of the above conditions is true then root1
    # and root2 are not mirror images
    return False

def isSymmetric(root):

    # Check if tree is mirror of itself
    return isMirror(root, root)

# Driver Code
# Let's construct the tree show in the above figure
root = Node(1)
root.left = Node(2)
root.right = Node(2)
root.left.left = Node(3)
root.left.right = Node(4)
root.right.left = Node(4)
root.right.right = Node(3)
print "Symmetric" if isSymmetric(root) == True else "Not symmetric"

# This code is contributed by Nikhil Kumar Singh(nickzuck_007)
```

## C#

```
// C# program to check is binary
// tree is symmetric or not
using System;

class Node {
    public int key;
    public Node left, right;

    public Node(int item)
    {
        key = item;
        left = right = null;
    }
}

class GFG {
    Node root;

    // returns true if trees with roots
    // as root1 and root2 are mirror
    Boolean isMirror(Node node1, Node node2)
    {
        // if both trees are empty,
        // then they are mirror image
        if (node1 == null && node2 == null)
            return true;

        // For two trees to be mirror images,
        // the following three conditions must be true
        // 1 - Their root node's key must be same
        // 2 - left subtree of left tree and right 
        // subtree of right tree have to be mirror images
        // 3 - right subtree of left tree and left subtree
        // of right tree have to be mirror images
        if (node1 != null && node2 != null
            && node1.key == node2.key)
            return (isMirror(node1.left, node2.right)
                    && isMirror(node1.right, node2.left));

        // if none of the above conditions
        // is true then root1 and root2 are
        // mirror images
        return false;
    }

    // returns true if the tree is symmetric
    // i.e mirror image of itself
    Boolean isSymmetric()
    {
        // check if tree is mirror of itself
        return isMirror(root, root);
    }

    // Driver Code
    static public void Main(String[] args)
    {
        GFG tree = new GFG();
        tree.root = new Node(1);
        tree.root.left = new Node(2);
        tree.root.right = new Node(2);
        tree.root.left.left = new Node(3);
        tree.root.left.right = new Node(4);
        tree.root.right.left = new Node(4);
        tree.root.right.right = new Node(3);
        Boolean output = tree.isSymmetric();
        if (output == true)
            Console.WriteLine("Symmetric");
        else
            Console.WriteLine("Not symmetric");
    }
}

// This code is contributed by Arnab Kundu
```

## java 描述语言

```
<script>

// Javascript program to check is binary
// tree is symmetric or not

class Node {

  constructor(item)
  {
    this.key = item;
    this.left = null;
    this.right = null;
  }
}

var root = null;

// returns true if trees with roots
// as root1 and root2 are mirror
function isMirror(node1, node2)
{
    // if both trees are empty,
    // then they are mirror image
    if (node1 == null && node2 == null)
        return true;

    // For two trees to be mirror images,
    // the following three conditions must be true
    // 1 - Their root node's key must be same
    // 2 - left subtree of left tree and right 
    // subtree of right tree have to be mirror images
    // 3 - right subtree of left tree and left subtree
    // of right tree have to be mirror images
    if (node1 != null && node2 != null
        && node1.key == node2.key)
        return (isMirror(node1.left, node2.right)
                && isMirror(node1.right, node2.left));

    // if none of the above conditions
    // is true then root1 and root2 are
    // mirror images
    return false;
}

// returns true if the tree is symmetric
// i.e mirror image of itself
function isSymmetric()
{

    // check if tree is mirror of itself
    return isMirror(root, root);
}

// Driver Code
root = new Node(1);
root.left = new Node(2);
root.right = new Node(2);
root.left.left = new Node(3);
root.left.right = new Node(4);
root.right.left = new Node(4);
root.right.right = new Node(3);
var output = isSymmetric();
if (output == true)
    document.write("Symmetric");
else
    document.write("Not symmetric");

// This code is contributed by rrrtnx.
</script>
```

**Output**

```
Symmetric
```

**时间复杂度:** O(N)

**辅助空间:** O(h)其中 h 为树的最大高度

？list = plqm7 alhxfyshcxd 7 r1j 0k y9 ZG _ gbb1 dbk
[检查对称二叉树(迭代方法)](https://www.geeksforgeeks.org/check-symmetric-binary-tree-iterative-approach/)
本文由**穆尼尔·艾哈迈德供稿。**发现有不正确的地方请写评论，或者想分享更多以上讨论话题的信息