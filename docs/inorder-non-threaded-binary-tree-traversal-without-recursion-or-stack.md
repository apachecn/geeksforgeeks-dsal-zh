# 无递归或栈的有序无线程二叉树遍历

> 原文:[https://www . geesforgeks . org/in order-非线程-二叉树-遍历-无递归-或-栈/](https://www.geeksforgeeks.org/inorder-non-threaded-binary-tree-traversal-without-recursion-or-stack/)

我们已经讨论了[基于线程的莫里斯遍历](https://www.geeksforgeeks.org/inorder-tree-traversal-without-recursion-and-without-stack/)。如果我们有可用的父指针，我们可以在没有线程的情况下进行有序遍历吗？

```
Input: Root of Below Tree [Every node of 
       tree has parent pointer also]
        10
      /    \
     5     100
           /  \
          80  120 
Output: 5 10 80 100 120
The code should not extra space (No Recursion
and stack)
```

在有序遍历中，我们遵循“左根右”。我们可以使用左右指针来移动到儿童。一旦节点被访问，我们也需要移动到父节点。例如，在上面的树中，我们需要在打印 5 之后移动到 10。为此，我们使用父指针。下面是算法。

```
1\. Initialize current node as root
2\. Initialize a flag: leftdone = false;
3\. Do following while root is not NULL
     a) If leftdone is false, set current node as leftmost
        child of node. 
     b) Mark leftdone as true and print current node.
     c) If right child of current nodes exists, set current
        as right child and set leftdone as false.
     d) Else If parent exists, If current node is left child
        of its parent, set current node as parent. 
        If current node is right child, keep moving to ancestors
        using parent pointer while current node is right child
        of its parent.  
     e) Else break (We have reached back to root)
```

**插图:**

```
Let us consider below tree for illustration.
        10
      /    \
     5     100
           /  \
          80  120 

Initialize: Current node = 10, leftdone = false

Since leftdone is false, we move to 5 (3.a), print it
and set leftdone = true.

Now we move to parent of 5 (3.d). Node 10 is 
printed because leftdone is true.

We move to right of 10 and set leftdone as false (3.c)

Now current node is 100\. Since leftdone is false, we move
to 80 (3.a) and set leftdone as true.  We print current 
node 80 and move back to parent 100 (3.d).  Since leftdone
is true, we print current node 100\. 

Right of 100 exists, so we move to 120 (3.c).   We print
current node 120.

Since 120 is right child of its parent we keep moving to parent
while parent is right child of its parent.  We reach root. So
we break the loop and stop
```

下面是上述算法的实现。请注意，该实现使用二叉查找树而不是二叉树。我们也可以对二叉树使用同样的函数**inoder()**。在下面的代码中使用二叉查找树的原因是，很容易用父指针构造一个二叉查找树，并且很容易测试结果(在 BST 中，有序遍历总是被排序的)。

## C++

```
// C++ program to print inorder traversal of a Binary Search
// Tree (BST) without recursion and stack
#include <bits/stdc++.h>
using namespace std;

// BST Node
struct Node
{
    Node *left, *right, *parent;
    int key;
};

// A utility function to create a new BST node
Node *newNode(int item)
{
    Node *temp = new Node;
    temp->key = item;
    temp->parent = temp->left = temp->right = NULL;
    return temp;
}

/* A utility function to insert a new node with
   given key in BST */
Node *insert(Node *node, int key)
{
    /* If the tree is empty, return a new node */
    if (node == NULL) return newNode(key);

    /* Otherwise, recur down the tree */
    if (key < node->key)
    {
        node->left  = insert(node->left, key);
        node->left->parent = node;
    }
    else if (key > node->key)
    {
        node->right = insert(node->right, key);
        node->right->parent = node;
    }

    /* return the (unchanged) node pointer */
    return node;
}

// Function to print inorder traversal using parent
// pointer
void inorder(Node *root)
{
    bool leftdone = false;

    // Start traversal from root
    while (root)
    {
        // If left child is not traversed, find the
        // leftmost child
        if (!leftdone)
        {
            while (root->left)
                root = root->left;
        }

        // Print root's data
        printf("%d ", root->key);

        // Mark left as done
        leftdone = true;

        // If right child exists
        if (root->right)
        {
            leftdone = false;
            root = root->right;
        }

        // If right child doesn't exist, move to parent
        else if (root->parent)
        {
            // If this node is right child of its parent,
            // visit parent's parent first
            while (root->parent &&
                   root == root->parent->right)
                root = root->parent;
            if (!root->parent)
                break;
            root = root->parent;
        }
        else break;
    }
}

int main(void)
{
    Node * root = NULL;

    root = insert(root, 24);
    root = insert(root, 27);
    root = insert(root, 29);
    root = insert(root, 34);
    root = insert(root, 14);
    root = insert(root, 4);
    root = insert(root, 10);
    root = insert(root, 22);
    root = insert(root, 13);
    root = insert(root, 3);
    root = insert(root, 2);
    root = insert(root, 6);

    printf("Inorder traversal is \n");
    inorder(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/* Java program to print inorder traversal of a Binary Search Tree
   without recursion and stack */

// BST node
class Node
{
    int key;
    Node left, right, parent;

    public Node(int key)
    {
        this.key = key;
        left = right = parent = null;
    }
}

class BinaryTree
{
    Node root;

    /* A utility function to insert a new node with
       given key in BST */
    Node insert(Node node, int key)
    {
        /* If the tree is empty, return a new node */
        if (node == null)
            return new Node(key);

        /* Otherwise, recur down the tree */
        if (key < node.key)
        {
            node.left = insert(node.left, key);
            node.left.parent = node;
        }
        else if (key > node.key)
        {
            node.right = insert(node.right, key);
            node.right.parent = node;
        }

        /* return the (unchanged) node pointer */
        return node;
    }

    // Function to print inorder traversal using parent
    // pointer
    void inorder(Node root)
    {
        boolean leftdone = false;

        // Start traversal from root
        while (root != null)
        {
            // If left child is not traversed, find the
            // leftmost child
            if (!leftdone)
            {
                while (root.left != null)
                {
                    root = root.left;
                }
            }

            // Print root's data
            System.out.print(root.key + " ");

            // Mark left as done
            leftdone = true;

            // If right child exists
            if (root.right != null)
            {
                leftdone = false;
                root = root.right;
            }

            // If right child doesn't exist, move to parent
            else if (root.parent != null)
            {
                // If this node is right child of its parent,
                // visit parent's parent first
                while (root.parent != null
                        && root == root.parent.right)
                    root = root.parent;

                if (root.parent == null)
                    break;
                root = root.parent;
            }
            else
                break;
        }
    }

    public static void main(String[] args)
    {
        BinaryTree tree = new BinaryTree();
        tree.root = tree.insert(tree.root, 24);
        tree.root = tree.insert(tree.root, 27);
        tree.root = tree.insert(tree.root, 29);
        tree.root = tree.insert(tree.root, 34);
        tree.root = tree.insert(tree.root, 14);
        tree.root = tree.insert(tree.root, 4);
        tree.root = tree.insert(tree.root, 10);
        tree.root = tree.insert(tree.root, 22);
        tree.root = tree.insert(tree.root, 13);
        tree.root = tree.insert(tree.root, 3);
        tree.root = tree.insert(tree.root, 2);
        tree.root = tree.insert(tree.root, 6);

        System.out.println("Inorder traversal is ");
        tree.inorder(tree.root);
    }
}
// This code has been contributed by Mayank Jaiswal(mayank_24)
```

## 蟒蛇 3

```
# Python3 program to print inorder traversal of a
# Binary Search Tree (BST) without recursion and stack

# A utility function to create a new BST node
class newNode:
    def __init__(self, item):
        self.key = item
        self.parent = self.left = self.right = None

# A utility function to insert a new
# node with given key in BST
def insert(node, key):

    # If the tree is empty, return a new node
    if node == None:
        return newNode(key)

    # Otherwise, recur down the tree
    if key < node.key:
        node.left = insert(node.left, key)
        node.left.parent = node
    elif key > node.key:
        node.right = insert(node.right, key)
        node.right.parent = node

    # return the (unchanged) node pointer
    return node

# Function to print inorder traversal
# using parent pointer
def inorder(root):
    leftdone = False

    # Start traversal from root
    while root:

        # If left child is not traversed,
        # find the leftmost child
        if leftdone == False:
            while root.left:
                root = root.left

        # Print root's data
        print(root.key, end = " ")

        # Mark left as done
        leftdone = True

        # If right child exists
        if root.right:
            leftdone = False
            root = root.right

        # If right child doesn't exist, move to parent
        elif root.parent:

            # If this node is right child of its
            # parent, visit parent's parent first
            while root.parent and root == root.parent.right:
                root = root.parent
            if root.parent == None:
                break
            root = root.parent
        else:
            break

# Driver Code
if __name__ == '__main__':
    root = None

    root = insert(root, 24)
    root = insert(root, 27)
    root = insert(root, 29)
    root = insert(root, 34)
    root = insert(root, 14)
    root = insert(root, 4)
    root = insert(root, 10)
    root = insert(root, 22)
    root = insert(root, 13)
    root = insert(root, 3)
    root = insert(root, 2)
    root = insert(root, 6)

    print("Inorder traversal is ")
    inorder(root)

# This code is contributed by PranchalK
```

## C#

```
// C# program to print inorder traversal
// of a Binary Search Tree without
// recursion and stack
using System;

// BST node
class Node
{
    public int key;
    public Node left, right, parent;

    public Node(int key)
    {
        this.key = key;
        left = right = parent = null;
    }
}

class BinaryTree
{
Node root;

/* A utility function to insert a
new node with given key in BST */
Node insert(Node node, int key)
{
    /* If the tree is empty,
       return a new node */
    if (node == null)
        return new Node(key);

    /* Otherwise, recur down the tree */
    if (key < node.key)
    {
        node.left = insert(node.left, key);
        node.left.parent = node;
    }
    else if (key > node.key)
    {
        node.right = insert(node.right, key);
        node.right.parent = node;
    }

    /* return the (unchanged) node pointer */
    return node;
}

// Function to print inorder traversal
// using parent pointer
void inorder(Node root)
{
    Boolean leftdone = false;

    // Start traversal from root
    while (root != null)
    {
        // If left child is not traversed,
        // find the leftmost child
        if (!leftdone)
        {
            while (root.left != null)
            {
                root = root.left;
            }
        }

        // Print root's data
        Console.Write(root.key + " ");

        // Mark left as done
        leftdone = true;

        // If right child exists
        if (root.right != null)
        {
            leftdone = false;
            root = root.right;
        }

        // If right child doesn't exist,
        // move to parent
        else if (root.parent != null)
        {
            // If this node is right child
            // of its parent, visit parent's
            // parent first
            while (root.parent != null &&
                   root == root.parent.right)
                root = root.parent;

            if (root.parent == null)
                break;
            root = root.parent;
        }
        else
            break;
    }
}

// Driver Code
static public void Main(String[] args)
{
    BinaryTree tree = new BinaryTree();
    tree.root = tree.insert(tree.root, 24);
    tree.root = tree.insert(tree.root, 27);
    tree.root = tree.insert(tree.root, 29);
    tree.root = tree.insert(tree.root, 34);
    tree.root = tree.insert(tree.root, 14);
    tree.root = tree.insert(tree.root, 4);
    tree.root = tree.insert(tree.root, 10);
    tree.root = tree.insert(tree.root, 22);
    tree.root = tree.insert(tree.root, 13);
    tree.root = tree.insert(tree.root, 3);
    tree.root = tree.insert(tree.root, 2);
    tree.root = tree.insert(tree.root, 6);

    Console.WriteLine("Inorder traversal is ");
    tree.inorder(tree.root);
}
}

// This code is contributed by Arnab Kundu
```

## java 描述语言

```
<script>
/* javascript program to print inorder traversal of a Binary Search Tree
   without recursion and stack */

// BST node
class Node {

    constructor(key) {
        this.key = key;
        this.left = this.right = this.parent = null;
    }
}

var root = null;

    /*
     * A utility function to insert a new node with given key in BST
     */
    function insert(node , key) {
        /* If the tree is empty, return a new node */
        if (node == null)
            return new Node(key);

        /* Otherwise, recur down the tree */
        if (key < node.key) {
            node.left = insert(node.left, key);
            node.left.parent = node;
        } else if (key > node.key) {
            node.right = insert(node.right, key);
            node.right.parent = node;
        }

        /* return the (unchanged) node pointer */
        return node;
    }

    // Function to print inorder traversal using parent
    // pointer
    function inorder(root) {
        var leftdone = false;

        // Start traversal from root
        while (root != null) {
            // If left child is not traversed, find the
            // leftmost child
            if (!leftdone) {
                while (root.left != null) {
                    root = root.left;
                }
            }

            // Print root's data
            document.write(root.key + " ");

            // Mark left as done
            leftdone = true;

            // If right child exists
            if (root.right != null) {
                leftdone = false;
                root = root.right;
            }

            // If right child doesn't exist, move to parent
            else if (root.parent != null) {
                // If this node is right child of its parent,
                // visit parent's parent first
                while (root.parent != null && root == root.parent.right)
                    root = root.parent;

                if (root.parent == null)
                    break;
                root = root.parent;
            } else
                break;
        }
    }

        root = insert(root, 24);
        root = insert(root, 27);
        root = insert(root, 29);
        root = insert(root, 34);
        root = insert(root, 14);
        root = insert(root, 4);
        root = insert(root, 10);
        root = insert(root, 22);
        root = insert(root, 13);
        root = insert(root, 3);
        root = insert(root, 2);
        root = insert(root, 6);

        document.write("Inorder traversal is ");
        inorder(root);

// This code contributed by aashish1995
</script>
```

**输出:**

```
Inorder traversal is 
2 3 4 6 10 13 14 22 24 27 29 34
```

本文由**日希·奇伯**供稿。如果你发现任何不正确的地方，请写评论，或者你想分享更多关于上面讨论的话题的信息