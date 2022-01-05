# 检查对称二叉树(迭代方法)

> 原文:[https://www . geesforgeks . org/check-对称-二叉树-迭代-方法/](https://www.geeksforgeeks.org/check-symmetric-binary-tree-iterative-approach/)

给定一棵二叉树，检查它是否是自身的镜像而不递归。

**示例:**

```
Input :   

     1
   /   \
  2     2
 / \   / \
3   4 4   3

Output : Symmetric

Input :    

    1
   / \
  2   2
   \   \
   3    3

Output : Not Symmetric
```

我们在下面的帖子中讨论了递归方法来解决这个问题:
[【对称树(自身的镜像)](https://www.geeksforgeeks.org/symmetric-tree-tree-which-is-mirror-image-of-itself/)
在这篇帖子中，讨论了迭代方法。我们在这里使用队列。注意，对于对称的，每个层次的元素都是回文的。在例 2 中，在叶水平上，元素是不回文的。
换句话说，
1。左子树的左子=右子树的右子。
2。左子树的右子树=右子树的左子树。
如果我们在队列中先插入左子树的左子，再插入右子树的右子，我们只需要保证这些是相等的。
同样，如果我们在队列中插入左子树的右子树，然后是右子树的左子树，我们再次需要确保这些是相等的。

以下是基于上述思想的实现。

## C++

```
// C++ program to check if a given Binary
// Tree is symmetric or not
#include<bits/stdc++.h>
using namespace std;

// A Binary Tree Node
struct Node
{
    int key;
    struct Node* left, *right;
};

// Utility function to create new Node
Node *newNode(int key)
{
    Node *temp = new Node;
    temp->key = key;
    temp->left = temp->right = NULL;
    return (temp);
}

// Returns true if a tree is symmetric
// i.e. mirror image of itself
bool isSymmetric(struct Node* root)
{
    if(root == NULL)
        return true;

    // If it is a single tree node, then
    // it is a symmetric tree.
    if(!root->left && !root->right)
        return true;

    queue <Node*> q;

    // Add root to queue two times so that
    // it can be checked if either one child
    // alone is NULL or not.
    q.push(root);
    q.push(root);

    // To store two nodes for checking their
    // symmetry.
    Node* leftNode, *rightNode;

    while(!q.empty()){

        // Remove first two nodes to check
        // their symmetry.
        leftNode = q.front();
        q.pop();

        rightNode = q.front();
        q.pop();

        // if both left and right nodes
        // exist, but have different
        // values--> inequality, return false
        if(leftNode->key != rightNode->key){
        return false;
        }

        // Push left child of left subtree node
        // and right child of right subtree
        // node in queue.
        if(leftNode->left && rightNode->right){
            q.push(leftNode->left);
            q.push(rightNode->right);
        }

        // If only one child is present alone
        // and other is NULL, then tree
        // is not symmetric.
        else if (leftNode->left || rightNode->right)
        return false;

        // Push right child of left subtree node
        // and left child of right subtree node
        // in queue.
        if(leftNode->right && rightNode->left){
            q.push(leftNode->right);
            q.push(rightNode->left);
        }

        // If only one child is present alone
        // and other is NULL, then tree
        // is not symmetric.
        else if(leftNode->right || rightNode->left)
        return false;
    }

    return true;
}

// Driver program
int main()
{
    // Let us construct the Tree shown in
    // the above figure
    Node *root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(2);
    root->left->left = newNode(3);
    root->left->right = newNode(4);
    root->right->left = newNode(4);
    root->right->right = newNode(3);

    if(isSymmetric(root))
        cout << "The given tree is Symmetric";
    else
        cout << "The given tree is not Symmetric";
    return 0;
}

// This code is contributed by Nikhil jindal.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Iterative Java program to check if
// given binary tree symmetric
import java.util.* ;

public class BinaryTree
{
    Node root;
    static class Node
    {
        int val;
        Node left, right;
        Node(int v)
        {
            val = v;
            left = null;
            right = null;
        }
    }

    /* constructor to initialise the root */
    BinaryTree(Node r) { root = r; }

    /* empty constructor */
    BinaryTree()  {  }

    /* function to check if the tree is Symmetric */
    public boolean isSymmetric(Node root)
    {
        /* This allows adding null elements to the queue */
        Queue<Node> q = new LinkedList<Node>();

        /* Initially, add left and right nodes of root */
        q.add(root.left);
        q.add(root.right);

        while (!q.isEmpty())
        {
            /* remove the front 2 nodes to
              check for equality */
            Node tempLeft = q.remove();
            Node tempRight = q.remove();

            /* if both are null, continue and check
               for further elements */
            if (tempLeft==null && tempRight==null)
                continue;

            /* if only one is null---inequality, return false */
            if ((tempLeft==null && tempRight!=null) ||
                (tempLeft!=null && tempRight==null))
                return false;

            /* if both left and right nodes exist, but
               have different values-- inequality,
               return false*/
            if (tempLeft.val != tempRight.val)
                return false;

            /* Note the order of insertion of elements
               to the queue :
               1) left child of left subtree
               2) right child of right subtree
               3) right child of left subtree
               4) left child of right subtree */
            q.add(tempLeft.left);
            q.add(tempRight.right);
            q.add(tempLeft.right);
            q.add(tempRight.left);
        }

        /* if the flow reaches here, return true*/
        return true;
    }

    /* driver function to test other functions */
    public static void main(String[] args)
    {
        Node n = new Node(1);
        BinaryTree bt = new BinaryTree(n);
        bt.root.left = new Node(2);
        bt.root.right = new Node(2);
        bt.root.left.left = new Node(3);
        bt.root.left.right = new Node(4);
        bt.root.right.left = new Node(4);
        bt.root.right.right = new Node(3);

        if (bt.isSymmetric(bt.root))
            System.out.println("The given tree is Symmetric");
        else
            System.out.println("The given tree is not Symmetric");
    }
}
```

## 蟒蛇 3

```
# Python3 program to program to check if a
# given Binary Tree is symmetric or not

# Helper function that allocates a new
# node with the given data and None
# left and right pairs.                                    
class newNode:

    # Constructor to create a new node
    def __init__(self, key):
        self.key = key
        self.left = None
        self.right = None

# function to check if a given
# Binary Tree is symmetric or not
def isSymmetric( root) :

    # if tree is empty
    if (root == None) :
        return True

    # If it is a single tree node,
    # then it is a symmetric tree.
    if(not root.left and not root.right):
        return True

    q = []    

    # Add root to queue two times so that
    # it can be checked if either one
    # child alone is NULL or not.
    q.append(root)
    q.append(root)

    # To store two nodes for checking
    # their symmetry.
    leftNode = 0
    rightNode = 0

    while(not len(q)):

        # Remove first two nodes to
        # check their symmetry.
        leftNode = q[0]
        q.pop(0)

        rightNode = q[0]
        q.pop(0)

        # if both left and right nodes
        # exist, but have different
        # values-. inequality, return False
        if(leftNode.key != rightNode.key):
            return False

        # append left child of left subtree
        # node and right child of right 
        # subtree node in queue.
        if(leftNode.left and rightNode.right) :
            q.append(leftNode.left)
            q.append(rightNode.right)

        # If only one child is present
        # alone and other is NULL, then
        # tree is not symmetric.
        elif (leftNode.left or rightNode.right) :
            return False

        # append right child of left subtree
        # node and left child of right subtree
        # node in queue.
        if(leftNode.right and rightNode.left):
            q.append(leftNode.right)
            q.append(rightNode.left)

        # If only one child is present
        # alone and other is NULL, then
        # tree is not symmetric.
        elif(leftNode.right or rightNode.left):
            return False

    return True

# Driver Code
if __name__ == '__main__':

    # Let us construct the Tree
    # shown in the above figure
    root = newNode(1)
    root.left = newNode(2)
    root.right = newNode(2)
    root.left.left = newNode(3)
    root.left.right = newNode(4)
    root.right.left = newNode(4)
    root.right.right = newNode(3)
    if (isSymmetric(root)) :
        print("The given tree is Symmetric")
    else:
        print("The given tree is not Symmetric")

# This code is contributed by
# Shubham Singh(SHUBHAMSINGH10)
```

## C#

```
// Iterative C# program to check if
// given binary tree symmetric
using System;
using System.Collections.Generic;

public class BinaryTree
{
    public Node root;
    public class Node
    {
        public int val;
        public Node left, right;
        public Node(int v)
        {
            val = v;
            left = null;
            right = null;
        }
    }

    /* constructor to initialise the root */
    BinaryTree(Node r) { root = r; }

    /* empty constructor */
    BinaryTree() { }

    /* function to check if the tree is Symmetric */
    public bool isSymmetric(Node root)
    {
        /* This allows adding null elements to the queue */
        Queue<Node> q = new Queue<Node>();

        /* Initially, add left and right nodes of root */
        q.Enqueue(root.left);
        q.Enqueue(root.right);

        while (q.Count!=0)
        {
            /* remove the front 2 nodes to
            check for equality */
            Node tempLeft = q.Dequeue();
            Node tempRight = q.Dequeue();

            /* if both are null, continue and check
            for further elements */
            if (tempLeft==null && tempRight==null)
                continue;

            /* if only one is null---inequality, return false */
            if ((tempLeft==null && tempRight!=null) ||
                (tempLeft!=null && tempRight==null))
                return false;

            /* if both left and right nodes exist, but
            have different values-- inequality,
            return false*/
            if (tempLeft.val != tempRight.val)
                return false;

            /* Note the order of insertion of elements
            to the queue :
            1) left child of left subtree
            2) right child of right subtree
            3) right child of left subtree
            4) left child of right subtree */
            q.Enqueue(tempLeft.left);
            q.Enqueue(tempRight.right);
            q.Enqueue(tempLeft.right);
            q.Enqueue(tempRight.left);
        }

        /* if the flow reaches here, return true*/
        return true;
    }

    /* driver code */
    public static void Main(String[] args)
    {
        Node n = new Node(1);
        BinaryTree bt = new BinaryTree(n);
        bt.root.left = new Node(2);
        bt.root.right = new Node(2);
        bt.root.left.left = new Node(3);
        bt.root.left.right = new Node(4);
        bt.root.right.left = new Node(4);
        bt.root.right.right = new Node(3);

        if (bt.isSymmetric(bt.root))
            Console.WriteLine("The given tree is Symmetric");
        else
            Console.WriteLine("The given tree is not Symmetric");
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Iterative Javascript program to check if
// given binary tree symmetric
var root = null;

class Node
{
    constructor(v)
    {
        this.val = v;
        this.left = null;
        this.right = null;
    }
}

/* Function to check if the tree is Symmetric */
function isSymmetric(root)
{

    /* This allows adding null
    elements to the queue */
    var q = [];

    /* Initially, add left and
    right nodes of root */
    q.push(root.left);
    q.push(root.right);

    while (q.length != 0)
    {

        /* Remove the front 2 nodes to
        check for equality */
        var tempLeft = q[0];
        q.shift();
        var tempRight = q[0];
        q.shift();

        /* If both are null, continue and check
        for further elements */
        if (tempLeft == null && tempRight == null)
            continue;

        /* If only one is null---inequality, return false */
        if ((tempLeft == null && tempRight != null) ||
            (tempLeft != null && tempRight == null))
            return false;

        /* If both left and right nodes exist, but
        have different values-- inequality,
        return false*/
        if (tempLeft.val != tempRight.val)
            return false;

        /* Note the order of insertion of elements
        to the queue :
        1) left child of left subtree
        2) right child of right subtree
        3) right child of left subtree
        4) left child of right subtree */
        q.push(tempLeft.left);
        q.push(tempRight.right);
        q.push(tempLeft.right);
        q.push(tempRight.left);
    }

    /* If the flow reaches here, return true*/
    return true;
}

// Driver code
var n = new Node(1);
root = n;
root.left = new Node(2);
root.right = new Node(2);
root.left.left = new Node(3);
root.left.right = new Node(4);
root.right.left = new Node(4);
root.right.right = new Node(3);

if (isSymmetric(root))
    document.write("The given tree is Symmetric");
else
    document.write("The given tree is not Symmetric");

// This code is contributed by noob2000

</script>
```

**输出:**

```
The given tree is Symmetric
```

本文由**萨罗尼·巴韦贾**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。