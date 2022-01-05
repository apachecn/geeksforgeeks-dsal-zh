# 二叉树中距离给定节点最近的叶子

> 原文:[https://www . geeksforgeeks . org/离给定二叉树节点最近的叶子/](https://www.geeksforgeeks.org/closest-leaf-to-a-given-node-in-binary-tree/)

给定一棵二叉树和其中的一个节点 **x** ，求二叉树中最靠近 **x** 的叶子的距离。如果给定的节点本身是叶子，那么距离是 0。
**例:**

```
Input: Root of below tree
       And x = pointer to node 13
          10
       /     \
     12       13
             /     
           14      
Output 1
Distance 1\. Closest leaf is 14.

Input: Root of below tree
       And x = pointer to node 13
          10
       /     \
     12       13
           /     \
         14       15    
        /   \     /  \
       21   22   23   24
       /\   /\   /\   /\
      1 2  3 4  5 6  7  8

Output 2
Closest leaf is 12 through 10.
```

**我们强烈建议你尽量减少浏览器，先自己试试这个。**
想法是首先遍历以给定节点为根的子树，找到这个子树中最近的叶子。储存这个距离。现在从根开始遍历树。如果给定的节点 x 在根的左子树中，则在右子树中找到最近的叶子，否则在左子树中找到最近的左边。下面是这个想法的实现。

## C++

```
/* Find closest leaf to the given node x in a tree */
#include<bits/stdc++.h>
using namespace std;

// A Tree node
struct Node
{
    int key;
    struct Node* left, *right;
};

// Utility function to create a new node
Node* newNode(int key)
{
    Node* temp = new Node;
    temp->key = key;
    temp->left = temp->right = NULL;
    return (temp);
}

// This function finds closest leaf to root.  This distance
// is stored at *minDist.
void findLeafDown(Node *root, int lev, int *minDist)
{
    // base case
    if (root == NULL)
        return ;

    // If this is a leaf node, then check if it is closer
    // than the closest so far
    if (root->left == NULL && root->right == NULL)
    {
        if (lev < (*minDist))
            *minDist = lev;
        return;
    }

    // Recur for left and right subtrees
    findLeafDown(root->left, lev+1, minDist);
    findLeafDown(root->right, lev+1, minDist);
}

// This function finds if there is closer leaf to x through
// parent node.
int findThroughParent(Node * root, Node *x, int *minDist)
{
    // Base cases
    if (root == NULL) return -1;
    if (root == x) return 0;

    // Search x in left subtree of root
    int l = findThroughParent(root->left, x,  minDist);

    // If left subtree has x
    if (l != -1)
    {
        // Find closest leaf in right subtree
        findLeafDown(root->right, l+2, minDist);
        return l+1;
    }

    // Search x in right subtree of root
    int r = findThroughParent(root->right, x, minDist);

    // If right subtree has x
    if (r != -1)
    {
        // Find closest leaf in left subtree
        findLeafDown(root->left, r+2, minDist);
        return r+1;
    }

    return -1;
}

// Returns minimum distance of a leaf from given node x
int minimumDistance(Node *root, Node *x)
{
    // Initialize result (minimum distance from a leaf)
    int minDist = INT_MAX;

    // Find closest leaf down to x
    findLeafDown(x, 0, &minDist);

    // See if there is a closer leaf through parent
    findThroughParent(root, x, &minDist);

    return minDist;
}

// Driver program
int main ()
{
    // Let us create Binary Tree shown in above example
    Node *root  = newNode(1);
    root->left  = newNode(12);
    root->right = newNode(13);

    root->right->left   = newNode(14);
    root->right->right  = newNode(15);

    root->right->left->left   = newNode(21);
    root->right->left->right  = newNode(22);
    root->right->right->left  = newNode(23);
    root->right->right->right = newNode(24);

    root->right->left->left->left  = newNode(1);
    root->right->left->left->right = newNode(2);
    root->right->left->right->left  = newNode(3);
    root->right->left->right->right = newNode(4);
    root->right->right->left->left  = newNode(5);
    root->right->right->left->right = newNode(6);
    root->right->right->right->left = newNode(7);
    root->right->right->right->right = newNode(8);

    Node *x = root->right;

    cout << "The closest leaf to the node with value "
         << x->key << " is at a distance of "
         << minimumDistance(root, x) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find closest leaf to given node x in a tree

// A binary tree node
class Node
{
    int key;
    Node left, right;

    public Node(int key)
    {
        this.key = key;
        left = right = null;
    }
}

class Distance
{
    int minDis = Integer.MAX_VALUE;
}

class BinaryTree
{
    Node root;

    // This function finds closest leaf to root.  This distance
    // is stored at *minDist.
    void findLeafDown(Node root, int lev, Distance minDist)
    {

        // base case
        if (root == null)
            return;

        // If this is a leaf node, then check if it is closer
        // than the closest so far
        if (root.left == null && root.right == null)
        {
            if (lev < (minDist.minDis))
                minDist.minDis = lev;

            return;
        }

        // Recur for left and right subtrees
        findLeafDown(root.left, lev + 1, minDist);
        findLeafDown(root.right, lev + 1, minDist);
    }

    // This function finds if there is closer leaf to x through
    // parent node.
    int findThroughParent(Node root, Node x, Distance minDist)
    {
        // Base cases
        if (root == null)
            return -1;

        if (root == x)
            return 0;

        // Search x in left subtree of root
        int l = findThroughParent(root.left, x, minDist);

        // If left subtree has x
        if (l != -1)
        {   
            // Find closest leaf in right subtree
            findLeafDown(root.right, l + 2, minDist);
            return l + 1;
        }

        // Search x in right subtree of root
        int r = findThroughParent(root.right, x, minDist);

        // If right subtree has x
        if (r != -1)
        {
            // Find closest leaf in left subtree
            findLeafDown(root.left, r + 2, minDist);
            return r + 1;
        }

        return -1;
    }

    // Returns minimum distance of a leaf from given node x
    int minimumDistance(Node root, Node x)
    {
        // Initialize result (minimum distance from a leaf)
        Distance d = new Distance();

        // Find closest leaf down to x
        findLeafDown(x, 0, d);

        // See if there is a closer leaf through parent
        findThroughParent(root, x, d);

        return d.minDis;
    }

    // Driver program
    public static void main(String[] args)
    {
        BinaryTree tree = new BinaryTree();

        // Let us create Binary Tree shown in above example
        tree.root = new Node(1);
        tree.root.left = new Node(12);
        tree.root.right = new Node(13);

        tree.root.right.left = new Node(14);
        tree.root.right.right = new Node(15);

        tree.root.right.left.left = new Node(21);
        tree.root.right.left.right = new Node(22);
        tree.root.right.right.left = new Node(23);
        tree.root.right.right.right = new Node(24);

        tree.root.right.left.left.left = new Node(1);
        tree.root.right.left.left.right = new Node(2);
        tree.root.right.left.right.left = new Node(3);
        tree.root.right.left.right.right = new Node(4);
        tree.root.right.right.left.left = new Node(5);
        tree.root.right.right.left.right = new Node(6);
        tree.root.right.right.right.left = new Node(7);
        tree.root.right.right.right.right = new Node(8);

        Node x = tree.root.right;

        System.out.println("The closest leaf to node with value "
                + x.key + " is at a distance of "
                + tree.minimumDistance(tree.root, x));
    }
}

// This code has been contributed by mayank_24
```

## 蟒蛇 3

```
# Find closest leaf to the given
# node x in a tree

# Utility class to create a new node
class newNode:
    def __init__(self, key):
        self.key = key
        self.left = self.right = None

# This function finds closest leaf to
# root. This distance is stored at *minDist.
def findLeafDown(root, lev, minDist):

    # base case
    if (root == None):
        return

    # If this is a leaf node, then check if
    # it is closer than the closest so far
    if (root.left == None and
        root.right == None):
        if (lev < (minDist[0])):
            minDist[0] = lev
        return

    # Recur for left and right subtrees
    findLeafDown(root.left, lev + 1, minDist)
    findLeafDown(root.right, lev + 1, minDist)

# This function finds if there is
# closer leaf to x through parent node.
def findThroughParent(root, x, minDist):

    # Base cases
    if (root == None):
        return -1
    if (root == x):
        return 0

    # Search x in left subtree of root
    l = findThroughParent(root.left, x,
                               minDist)

    # If left subtree has x
    if (l != -1):

        # Find closest leaf in right subtree
        findLeafDown(root.right, l + 2, minDist)
        return l + 1

    # Search x in right subtree of root
    r = findThroughParent(root.right, x, minDist)

    # If right subtree has x
    if (r != -1):

        # Find closest leaf in left subtree
        findLeafDown(root.left, r + 2, minDist)
        return r + 1

    return -1

# Returns minimum distance of a leaf
# from given node x
def minimumDistance(root, x):

    # Initialize result (minimum
    # distance from a leaf)
    minDist = [999999999999]

    # Find closest leaf down to x
    findLeafDown(x, 0, minDist)

    # See if there is a closer leaf
    # through parent
    findThroughParent(root, x, minDist)

    return minDist[0]

# Driver Code
if __name__ == '__main__':

    # Let us create Binary Tree shown
    # in above example
    root = newNode(1)
    root.left = newNode(12)
    root.right = newNode(13)

    root.right.left = newNode(14)
    root.right.right = newNode(15)

    root.right.left.left = newNode(21)
    root.right.left.right = newNode(22)
    root.right.right.left = newNode(23)
    root.right.right.right = newNode(24)

    root.right.left.left.left = newNode(1)
    root.right.left.left.right = newNode(2)
    root.right.left.right.left = newNode(3)
    root.right.left.right.right = newNode(4)
    root.right.right.left.left = newNode(5)
    root.right.right.left.right = newNode(6)
    root.right.right.right.left = newNode(7)
    root.right.right.right.right = newNode(8)

    x = root.right

    print("The closest leaf to the node with value",
           x.key, "is at a distance of",
           minimumDistance(root, x))

# This code is contributed by PranchalK
```

## C#

```
using System;

// C# program to find closest leaf to given node x in a tree

// A binary tree node
public class Node
{
    public int key;
    public Node left, right;

    public Node(int key)
    {
        this.key = key;
        left = right = null;
    }
}

public class Distance
{
    public int minDis = int.MaxValue;
}

public class BinaryTree
{
    public Node root;

    // This function finds closest leaf to root.  This distance
    // is stored at *minDist.
    public virtual void findLeafDown(Node root, int lev, Distance minDist)
    {

        // base case
        if (root == null)
        {
            return;
        }

        // If this is a leaf node, then check if it is closer
        // than the closest so far
        if (root.left == null && root.right == null)
        {
            if (lev < (minDist.minDis))
            {
                minDist.minDis = lev;
            }

            return;
        }

        // Recur for left and right subtrees
        findLeafDown(root.left, lev + 1, minDist);
        findLeafDown(root.right, lev + 1, minDist);
    }

    // This function finds if there is closer leaf to x through 
    // parent node.
    public virtual int findThroughParent(Node root, Node x, Distance minDist)
    {
        // Base cases
        if (root == null)
        {
            return -1;
        }

        if (root == x)
        {
            return 0;
        }

        // Search x in left subtree of root
        int l = findThroughParent(root.left, x, minDist);

        // If left subtree has x
        if (l != -1)
        {
            // Find closest leaf in right subtree
            findLeafDown(root.right, l + 2, minDist);
            return l + 1;
        }

        // Search x in right subtree of root
        int r = findThroughParent(root.right, x, minDist);

        // If right subtree has x
        if (r != -1)
        {
            // Find closest leaf in left subtree
            findLeafDown(root.left, r + 2, minDist);
            return r + 1;
        }

        return -1;
    }

    // Returns minimum distance of a leaf from given node x
    public virtual int minimumDistance(Node root, Node x)
    {
        // Initialize result (minimum distance from a leaf)
        Distance d = new Distance();

        // Find closest leaf down to x
        findLeafDown(x, 0, d);

        // See if there is a closer leaf through parent
        findThroughParent(root, x, d);

        return d.minDis;
    }

    // Driver program
    public static void Main(string[] args)
    {
        BinaryTree tree = new BinaryTree();

        // Let us create Binary Tree shown in above example
        tree.root = new Node(1);
        tree.root.left = new Node(12);
        tree.root.right = new Node(13);

        tree.root.right.left = new Node(14);
        tree.root.right.right = new Node(15);

        tree.root.right.left.left = new Node(21);
        tree.root.right.left.right = new Node(22);
        tree.root.right.right.left = new Node(23);
        tree.root.right.right.right = new Node(24);

        tree.root.right.left.left.left = new Node(1);
        tree.root.right.left.left.right = new Node(2);
        tree.root.right.left.right.left = new Node(3);
        tree.root.right.left.right.right = new Node(4);
        tree.root.right.right.left.left = new Node(5);
        tree.root.right.right.left.right = new Node(6);
        tree.root.right.right.right.left = new Node(7);
        tree.root.right.right.right.right = new Node(8);

        Node x = tree.root.right;

        Console.WriteLine("The closest leaf to node with value " + x.key + " is at a distance of " + tree.minimumDistance(tree.root, x));
    }
}

 //  This code is contributed by Shrikant13
```

## java 描述语言

```
<script>
// javascript program to find closest leaf to given node x in a tree

// A binary tree node
class Node {
    constructor(key) {
        this.key = key;
        this.left = this.right = null;
    }
}

class Distance {
constructor(){
    this.minDis = Number.MAX_VALUE;
    }
}

    var root;

    // This function finds closest leaf to root. This distance
    // is stored at *minDist.
    function findLeafDown( root , lev,  minDist) {

        // base case
        if (root == null)
            return;

        // If this is a leaf node, then check if it is closer
        // than the closest so far
        if (root.left == null && root.right == null) {
            if (lev < (minDist.minDis))
                minDist.minDis = lev;

            return;
        }

        // Recur for left and right subtrees
        findLeafDown(root.left, lev + 1, minDist);
        findLeafDown(root.right, lev + 1, minDist);
    }

    // This function finds if there is closer leaf to x through
    // parent node.
    function findThroughParent( root,  x,  minDist) {
        // Base cases
        if (root == null)
            return -1;

        if (root == x)
            return 0;

        // Search x in left subtree of root
        var l = findThroughParent(root.left, x, minDist);

        // If left subtree has x
        if (l != -1) {
            // Find closest leaf in right subtree
            findLeafDown(root.right, l + 2, minDist);
            return l + 1;
        }

        // Search x in right subtree of root
        var r = findThroughParent(root.right, x, minDist);

        // If right subtree has x
        if (r != -1) {
            // Find closest leaf in left subtree
            findLeafDown(root.left, r + 2, minDist);
            return r + 1;
        }

        return -1;
    }

    // Returns minimum distance of a leaf from given node x
    function minimumDistance( root,  x) {
        // Initialize result (minimum distance from a leaf)
         d = new Distance();

        // Find closest leaf down to x
        findLeafDown(x, 0, d);

        // See if there is a closer leaf through parent
        findThroughParent(root, x, d);

        return d.minDis;
    }

    // Driver program

        // Let us create Binary Tree shown in above example
        root = new Node(1);
        root.left = new Node(12);
        root.right = new Node(13);

        root.right.left = new Node(14);
        root.right.right = new Node(15);

        root.right.left.left = new Node(21);
        root.right.left.right = new Node(22);
        root.right.right.left = new Node(23);
        root.right.right.right = new Node(24);

        root.right.left.left.left = new Node(1);
        root.right.left.left.right = new Node(2);
        root.right.left.right.left = new Node(3);
        root.right.left.right.right = new Node(4);
        root.right.right.left.left = new Node(5);
        root.right.right.left.right = new Node(6);
        root.right.right.right.left = new Node(7);
        root.right.right.right.right = new Node(8);

        x = root.right;

        document.write("The closest leaf to node with value "
        + x.key + " is at a distance of "
                + minimumDistance(root, x));

// This code contributed by umadevi9616
</script>
```

**输出:**

```
The closest leaf to the node with value 13 is at a distance of 2
```

上述解决方案的时间复杂度为 0(n)，因为它最多遍历给定的二叉树两次。
本文由 [Ekta Goel](https://www.linkedin.com/in/ekta-goel-3a612a75?authType=NAME_SEARCH&authToken=n5Y7&locale=en_US&trk=tyah&trkInfo=clickedVertical%3Amynetwork%2CclickedEntityId%3A266060718%2CauthType%3ANAME_SEARCH%2Cidx%3A1-1-1%2CtarId%3A1453641087830%2Ctas%3AEkta%20Go) 供稿。如果发现有不正确的地方，请写评论，或者想分享更多关于以上讨论话题的信息