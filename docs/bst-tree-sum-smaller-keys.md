# 用所有较小的键之和将 BST 转换为一棵树

> 原文:[https://www.geeksforgeeks.org/bst-tree-sum-smaller-keys/](https://www.geeksforgeeks.org/bst-tree-sum-smaller-keys/)

给定一个二叉查找树(BST)，将其转换为二叉树，这样原始 BST 的每个键都被更改为键加上 BST 中所有较小键的总和。
给定一个有 N 个节点的 BST，我们必须转换成二叉树

上面给出了 **N=5** 个节点的 BST。节点处的值为转换后的 **9、6、15、3、21**
二叉树

转换后的二叉树，节点处的值为 **18，9，33，3，54**

**解决方案:**我们将执行一个常规的有序遍历，其中我们跟踪访问的节点的总和。让这个总和成为*总和*。正在访问的节点，将该节点的键添加到*和*中，即*和=和+节点- >键*。将当前节点的键改为*和*，即*节点- >键=和*。
当顺序遍历一个 BST 时，对于当前被访问的每个键，所有已经被访问的键都是较小的键。

## C++

```
// Program to change a BST to Binary Tree such 
// that key of a Node becomes original key plus 
// sum of all smaller keys in BST
#include <bits/stdc++.h>

/* A BST Node has key, left child and 
   right child */
struct Node {
    int key;
    struct Node* left;
    struct Node* right;
};

/* Helper function that allocates a new 
   node with the given key and NULL left
   and right pointers.*/
struct Node* newNode(int key)
{
    struct Node* node = new Node;
    node->key = key;
    node->left = NULL;
    node->right = NULL;
    return (node);
}

// A recursive function that traverses the
// given BST in inorder and for every key,
// adds all smaller keys to it
void addSmallerUtil(struct Node* root, int* sum)
{
    // Base Case
    if (root == NULL)
        return;

    // Recur for left subtree first so that
    // sum of all smaller Nodes is stored
    addSmallerUtil(root->left, sum);

    // Update the value at sum
    *sum = *sum + root->key;

    // Update key of this Node
    root->key = *sum;

    // Recur for right subtree so that
    // the updated sum is added
    // to greater Nodes
    addSmallerUtil(root->right, sum);
}

// A wrapper over addSmallerUtil(). It 
// initializes sum and calls addSmallerUtil() 
// to recursively update and use value of
void addSmaller(struct Node* root)
{
    int sum = 0;
    addSmallerUtil(root, &sum);
}

// A utility function to print inorder 
// traversal of Binary Tree
void printInorder(struct Node* node)
{
    if (node == NULL)
        return;
    printInorder(node->left);
    printf("%d ", node->key);
    printInorder(node->right);
}

// Driver program to test above function
int main()
{
    /* Create following BST
            9
            / \
        6     15 */
    Node* root = newNode(9);
    root->left = newNode(6);
    root->right = newNode(15);

    printf(" Original BST\n");
    printInorder(root);

    addSmaller(root);

    printf("\n BST To Binary Tree\n");
    printInorder(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to convert BST to binary tree 
// such that sum of all smaller keys is added 
// to every key

class Node {

    int data;
    Node left, right;

    Node(int d)
    {
        data = d;
        left = right = null;
    }
}

class Sum {

    int addvalue = 0;
}

class BSTtoBinaryTree {

    static Node root;
    Sum add = new Sum();

    // A recursive function that traverses 
    // the given BST in inorder and for every 
    // key, adds all smaller keys to it
    void addSmallerUtil(Node node, Sum sum)
    {

        // Base Case
        if (node == null) {
            return;
        }

        // Recur for left subtree first so that
        //  sum of all smaller Nodes is stored at sum
        addSmallerUtil(node.left, sum);

        // Update the value at sum
        sum.addvalue = sum.addvalue + node.data;

        // Update key of this Node
        node.data = sum.addvalue;

        // Recur for right subtree so that the 
        // updated sum is added to greater Nodes
        addSmallerUtil(node.right, sum);
    }

    // A wrapper over addSmallerUtil().  It 
    // initializes addvalue and calls
    // addSmallerUtil() to recursively update 
    // and use value of addvalue
    Node addSmaller(Node node)
    {
        addSmallerUtil(node, add);
        return node;
    }

    // A utility function to print inorder
    // traversal of Binary Tree
    void printInorder(Node node)
    {
        if (node == null) {
            return;
        }
        printInorder(node.left);
        System.out.print(node.data + " ");
        printInorder(node.right);
    }

    // Driver program to test the above functions
    public static void main(String[] args)
    {
        BSTtoBinaryTree tree = new BSTtoBinaryTree();
        tree.root = new Node(9);
        tree.root.left = new Node(6);
        tree.root.right = new Node(15);

        System.out.println("Original BST");
        tree.printInorder(root);
        Node Node = tree.addSmaller(root);
        System.out.println("");
        System.out.println("BST To Binary Tree");
        tree.printInorder(Node);
    }
}
```

## 蟒蛇 3

```
# Program to change a BST to Binary Tree
# such that key of a Node becomes original 
# key plus sum of all smaller keys in BST

# A BST node has key, left child 
# and right child */
class Node: 

    # Constructor to create a new node 
    def __init__(self, data): 
        self.key = data 
        self.left = None
        self.right = None

# A recursive function that traverses the 
# given BST in inorder and for every key,
# adds all smaller keys to it 
def addSmallerUtil(root, Sum):

    # Base Case 
    if root == None: 
        return

    # Recur for left subtree first so that 
    # sum of all smaller Nodes is stored 
    addSmallerUtil(root.left, Sum) 

    # Update the value at sum 
    Sum[0] = Sum[0] + root.key 

    # Update key of this Node 
    root.key = Sum[0] 

    # Recur for right subtree so 
    # that the updated sum is 
    # added to greater Nodes 
    addSmallerUtil(root.right, Sum)

# A wrapper over addSmallerUtil(). It
# initializes sum and calls addSmallerUtil() 
# to recursively update and use value of
def addSmaller(root):
    Sum = [0] 
    addSmallerUtil(root, Sum)

# A utility function to print
# inorder traversal of Binary Tree 
def printInorder(node):
    if node == None: 
        return
    printInorder(node.left) 
    print(node.key, end = " ")
    printInorder(node.right)

# Driver Code
if __name__ == '__main__':

    # Create following BST 
    #         9 
    #     / \ 
    #     6     15 
    root = Node(9) 
    root.left = Node(6) 
    root.right = Node(15) 

    print("Original BST") 
    printInorder(root)
    print()
    addSmaller(root) 

    print("BST To Binary Tree") 
    printInorder(root) 

# This code is contributed by PranchalK
```

## C#

```
using System;

// C#  program to convert BST to binary tree  
// such that sum of all smaller keys is added  
// to every key 

public class Node
{

    public int data;
    public Node left, right;

    public Node(int d)
    {
        data = d;
        left = right = null;
    }
}

public class Sum
{

    public int addvalue = 0;
}

public class BSTtoBinaryTree
{

    public static Node root;
    public Sum add = new Sum();

    // A recursive function that traverses  
    // the given BST in inorder and for every  
    // key, adds all smaller keys to it 
    public virtual void addSmallerUtil(Node node, Sum sum)
    {

        // Base Case 
        if (node == null)
        {
            return;
        }

        // Recur for left subtree first so that 
        //  sum of all smaller Nodes is stored at sum 
        addSmallerUtil(node.left, sum);

        // Update the value at sum 
        sum.addvalue = sum.addvalue + node.data;

        // Update key of this Node 
        node.data = sum.addvalue;

        // Recur for right subtree so that the  
        // updated sum is added to greater Nodes 
        addSmallerUtil(node.right, sum);
    }

    // A wrapper over addSmallerUtil().  It  
    // initializes addvalue and calls 
    // addSmallerUtil() to recursively update  
    // and use value of addvalue 
    public virtual Node addSmaller(Node node)
    {
        addSmallerUtil(node, add);
        return node;
    }

    // A utility function to print inorder 
    // traversal of Binary Tree 
    public virtual void printInorder(Node node)
    {
        if (node == null)
        {
            return;
        }
        printInorder(node.left);
        Console.Write(node.data + " ");
        printInorder(node.right);
    }

    // Driver program to test the above functions 
    public static void Main(string[] args)
    {
        BSTtoBinaryTree tree = new BSTtoBinaryTree();
        BSTtoBinaryTree.root = new Node(9);
        BSTtoBinaryTree.root.left = new Node(6);
        BSTtoBinaryTree.root.right = new Node(15);

        Console.WriteLine("Original BST");
        tree.printInorder(root);
        Node Node = tree.addSmaller(root);
        Console.WriteLine("");
        Console.WriteLine("BST To Binary Tree");
        tree.printInorder(Node);
    }
}

  // This code is contributed by Shrikant13
```

## java 描述语言

```
<script>

// Javascript  program to convert BST to binary tree  
// such that sum of all smaller keys is added  
// to every key 
class Node
{

    constructor(d)
    {
        this.data = d;
        this.left = null;
        this.right = null;
    }
}

class Sum
{
    constructor()
    {
        this.addvalue = 0;
    }
}

var root = null;
var add = new Sum();

// A recursive function that traverses  
// the given BST in inorder and for every  
// key, adds all smaller keys to it 
function addSmallerUtil(node, sum)
{
    // Base Case 
    if (node == null)
    {
        return;
    }

    // Recur for left subtree first so that 
    //  sum of all smaller Nodes is stored at sum 
    addSmallerUtil(node.left, sum);

    // Update the value at sum 
    sum.addvalue = sum.addvalue + node.data;

    // Update key of this Node 
    node.data = sum.addvalue;

    // Recur for right subtree so that the  
    // updated sum is added to greater Nodes 
    addSmallerUtil(node.right, sum);
}

// A wrapper over addSmallerUtil().  It  
// initializes addvalue and calls 
// addSmallerUtil() to recursively update  
// and use value of addvalue 
function addSmaller(node)
{
    addSmallerUtil(node, add);
    return node;
}

// A utility function to print inorder 
// traversal of Binary Tree 
function printInorder(node)
{
    if (node == null)
    {
        return;
    }
    printInorder(node.left);
    document.write(node.data + " ");
    printInorder(node.right);
}

// Driver program to test the above functions 
root = new Node(9);
root.left = new Node(6);
root.right = new Node(15);
document.write("Original BST<br>");
printInorder(root);
var node = addSmaller(root);
document.write("<br>");
document.write("BST To Binary Tree<br>");
printInorder(node);

// This code is contributed by itsok.
</script>
```

**输出:**

```
Original BST
6 9 15 
BST To Binary Tree
6 15 30 
```