# 在二叉树中下沉偶数节点

> 原文:[https://www . geeksforgeeks . org/sink-二叉树偶数节点/](https://www.geeksforgeeks.org/sink-even-nodes-in-binary-tree/)

给定具有奇数和偶数元素的二叉树，接收其所有偶数值的节点，使得具有偶数值的节点不能是具有奇数值的节点的父节点。

给定的树可以有多个输出，我们需要打印其中一个。转换树总是可能的(注意，具有奇数节点和所有偶数节点的节点都遵循该规则)

**示例:**

```
Input: 
       1
     /    \
    5       8
  /  \     /  \
 2    4   9    10
Output: 
1 
5 9 
2 4 8 10

Level order traversal after
sinking all the nodes

Input: 
  4
 /  \
2    1
Output: 
4
2 1
```

```
Explanation: 
In the first case
Given tree
       4
    /    \
   2      1

There are two trees possible
       1            1
    /    \   OR   /   \
   2      4      4     2 

In the second example also,
Given tree
       1
     /    \
    5       8
  /  \     /  \
 2    4   9    10

There are more than one tree
that can satisfy the condition
      1                 1
   /    \            /    \     
  5       9    OR   5      9   
 /  \    /  \      /  \   / \   
2   4  8   10    4    2  8  10
```

**进场:**

*   基本上，需要将节点的偶数值与其后代之一的奇数值交换。
*   这个想法是以后置的方式遍历树。
*   由于我们以后置顺序处理，对于遇到的每个偶数节点，其左右子树已经平衡(下沉)。
*   检查它是否是一个偶数节点，它的左或右子节点是否有一个奇数值。如果找到了奇数，将节点的数据与奇数子节点的数据交换，并调用奇数子节点上的过程来平衡子树。
*   如果两个孩子都有平等的价值观，那就意味着他们所有的后代都是平等的。

下面是这个想法的实现:

## 计算机编程语言

```
# Python3 program to sink even nodes
# to the bottom of binary tree

# A binary tree node
# Helper function to allocates a new node
class newnode:

    # Constructor to create a new node
    def __init__(self, key):
        self.data = key
        self.left = None
        self.right = None

# Helper function to check
# if node is leaf node
def isLeaf(root):
    return (root.left == None and
            root.right == None)

# A recursive method to sink a tree with even root
# This method assumes that the subtrees are
# already sinked. This method is similar to
# Heapify of Heap-Sort
def sink(root):

    # If None or is a leaf, do nothing
    if (root == None or isLeaf(root)):
        return

    # if left subtree exists and
    # left child is even
    if (root.left and (root.left.data & 1)):

        # swap root's data with left child
        # and fix left subtree
        root.data, root.left.data = root.left.data, root.data
        sink(root.left)

    # if right subtree exists and
    # right child is even
    elif(root.right and (root.right.data & 1)):

        # swap root's data with right child
        # and fix right subtree
        root.data, root.right.data = root.right.data, root.data
        sink(root.right)

# Function to sink all even nodes to
# the bottom of binary tree. It does
# a postorder traversal and calls sink()
# if any even node is found
def sinkevenNodes(root):

    # If None or is a leaf, do nothing
    if (root == None or isLeaf(root)):
        return

    # Process left and right subtrees
    # before this node
    sinkevenNodes(root.left)
    sinkevenNodes(root.right)

    # If root is even, sink it
    if not (root.data & 1):
        sink(root)

# Helper function to do Level Order Traversal
# of Binary Tree level by level. This function
# is used here only for showing modified tree.
def printLevelOrder(root):
    q = []
    q.append(root)

    # Do Level order traversal
    while (len(q)):

        nodeCount = len(q)

        # Print one level at a time
        while (nodeCount):
            node = q[0]
            print(node.data, end = " ")
            q.pop(0)
            if (node.left != None):
                q.append(node.left)
            if (node.right != None):
                q.append(node.right)
            nodeCount -= 1

        # Line separator for levels
        print()

# Driver Code
""" Constructed binary tree is
            1
        / \
        5 8
        / \ / \
    2 4 9 10     """
root = newnode(1)
root.left = newnode(5)
root.right = newnode(8)
root.left.left = newnode(2)
root.left.right = newnode(4)
root.right.left = newnode(9)
root.right.right = newnode(10)

sinkevenNodes(root)

printLevelOrder(root)

# This code is contributed by SHUBHAMSINGH10
```

## java 描述语言

```
<script>

// Program to sink even nodes
// to the bottom of binary tree

// A binary tree node
class Node {

    constructor()
    {
        this.data = 0;
        this.left = null;
        this.right = null;
    }
};

// Helper function to allocates
// a new node
function newnode(data)
{
    var node = new Node;
    node.data = data;
    return node;
}

// Helper function to check
// if node is leaf node
function isLeaf(root)
{
    return (root.left == null
            && root.right == null);
}

// A recursive method to sink
// a tree with odd root

// This method assumes that the
// subtrees are already sinked.
// This method is similar to
// Heapify of Heap-Sort
function sink(root)
{
    // If null or is a leaf, do nothing
    if (root == null || isLeaf(root))
        return;

    // If left subtree exists
    // and left child is odd
    if (root.left
        && (root.left.data & 1)) {

        // Swap root's data with left
        // child and fix left subtree
        [root.data,
             root.left.data] = [root.left.data, root.data];
        sink(root.left);
    }

    // If right subtree exists
    // and right child is odd
    else if (root.right
             && (root.right.data & 1)) {

        // Swap root's data with right
        // child and fix right subtree
        [root.data,
             root.right.data] = [root.right.data, root.data];
        sink(root.right);
    }
}

// Function to sink all even
// nodes to the bottom of
// binary tree. It does a
// postorder traversal and
// calls sink()
// if any even node is found
function sinkevenNodes( root)
{
    // If null or is a
    // leaf, do nothing
    if (root == null || isLeaf(root))
        return;

    // Process left and right
    // subtrees before this node
    sinkevenNodes(root.left);
    sinkevenNodes(root.right);

    // If root is even, sink it
    if (!(root.data & 1))
        sink(root);
}

// Helper function to do Level
// Order Traversal of Binary Tree
// level by level. This function
// is used here only for showing
// modified tree.
function printLevelOrder(root)
{
    var q = [];
    q.push(root);

    // Do Level order traversal
    while (q.length!=0) {
        var nodeCount = q.length;

        // Print one level at a time
        while (nodeCount) {

            var node = q[0];

            document.write(node.data + " ");

            q.shift();

            // If the node has a left
            // child then push into queue
            if (node.left != null)
                q.push(node.left);

            // If the node has a right
            // child then push into queue
            if (node.right != null)
                q.push(node.right);

            nodeCount--;
        }

        // Line separator for levels
        document.write("<br>");
    }
}

// Driver code

    /* Constructed binary tree is
        1
      /  \
     5    8
    / \  / \
   2  4 9  10     */

    var root = newnode(1);
    root.left = newnode(5);
    root.right = newnode(8);
    root.left.left = newnode(2);
    root.left.right = newnode(4);
    root.right.left = newnode(9);
    root.right.right = newnode(10);

    // Calling function to perform
    // sink operation
    sinkevenNodes(root);

    // Printing the updated tree
    // using level order traversal
    printLevelOrder(root);

</script>
```

**Output:** 

```
1 
5 9 
2 4 8 10
```