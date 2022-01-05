# 求同级叶片数据之和的乘积

> 原文:[https://www . geeksforgeeks . org/find-在正常水平下所有树叶数据总和的乘法/](https://www.geeksforgeeks.org/find-multiplication-of-sums-of-data-of-all-leaves-at-sane-levels/)

给定一个二叉树，返回以下值。
1)对于每个级别，如果该级别有叶子，则计算所有叶子的总和。否则，忽略它。
2)返回所有和的乘法。
**例:**

```
Input: Root of below tree
         2
       /   \
      7     5
             \
              9
Output: 63
First levels doesn't have leaves. Second level
has one leaf 7 and third level also has one 
leaf 9\.  Therefore result is 7*9 = 63

Input: Root of below tree
         2
       /   \
     7      5
    / \      \
   8   6      9
      / \    /  \
     1  11  4    10 

Output: 208
First two levels don't have leaves. Third
level has single leaf 8\. Last level has four
leaves 1, 11, 4 and 10\. Therefore result is 
8 * (1 + 11 + 4 + 10)  
```

**我们强烈建议你尽量减少浏览器，先自己试试这个。**
一个**简单的解决方案**是从上到下递归计算所有级别的叶和。然后乘以有叶子的层次的和。该解决方案的时间复杂度为 0(n<sup>2</sup>)。
一个**有效的解决方案**是使用基于队列的级别顺序遍历。遍历时，分别处理所有不同的级别。对于每个已处理的级别，检查它是否有叶。如果有，则计算叶节点的和。最后返回所有和的乘积。

## C++

```
/* Iterative C++ program to find sum of data of all leaves
   of a binary tree on same level and then multiply sums
   obtained of all levels. */
#include <bits/stdc++.h>
using namespace std;

// A Binary Tree Node
struct Node {
    int data;
    struct Node *left, *right;
};

// helper function to check if a Node is leaf of tree
bool isLeaf(Node* root)
{
    return (!root->left && !root->right);
}

/* Calculate sum of all leaf Nodes at each level and returns
   multiplication of sums */
int sumAndMultiplyLevelData(Node* root)
{
    // Tree is empty
    if (!root)
        return 0;

    int mul = 1; /* To store result */

    // Create an empty queue for level order traversal
    queue<Node*> q;

    // Enqueue Root and initialize height
    q.push(root);

    // Do level order traversal of tree
    while (1) {
        // NodeCount (queue size) indicates number of Nodes
        // at current level.
        int NodeCount = q.size();

        // If there are no Nodes at current level, we are done
        if (NodeCount == 0)
            break;

        // Initialize leaf sum for current level
        int levelSum = 0;

        // A boolean variable to indicate if found a leaf
        // Node at current level or not
        bool leafFound = false;

        // Dequeue all Nodes of current level and Enqueue all
        // Nodes of next level
        while (NodeCount > 0) {
            // Process next Node  of current level
            Node* Node = q.front();

            /* if Node is a leaf, update sum at the level */
            if (isLeaf(Node)) {
                leafFound = true;
                levelSum += Node->data;
            }
            q.pop();

            // Add children of Node
            if (Node->left != NULL)
                q.push(Node->left);
            if (Node->right != NULL)
                q.push(Node->right);
            NodeCount--;
        }

        // If we found at least one leaf, we multiply
        // result with level sum.
        if (leafFound)
            mul *= levelSum;
    }

    return mul; // Return result
}

// Utility function to create a new tree Node
Node* newNode(int data)
{
    Node* temp = new Node;
    temp->data = data;
    temp->left = temp->right = NULL;
    return temp;
}

// Driver program to test above functions
int main()
{
    Node* root = newNode(2);
    root->left = newNode(7);
    root->right = newNode(5);
    root->left->right = newNode(6);
    root->left->left = newNode(8);
    root->left->right->left = newNode(1);
    root->left->right->right = newNode(11);
    root->right->right = newNode(9);
    root->right->right->left = newNode(4);
    root->right->right->right = newNode(10);

    cout << "Final product value = "
         << sumAndMultiplyLevelData(root) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/* Iterative Java program to find sum of data of all leaves
   of a binary tree on same level and then multiply sums
   obtained of all levels. */

/* importing the necessary class */
import java.util.LinkedList;
import java.util.Queue;
import java.util.Stack;

/* Class containing left and right child of current
 node and key value*/
class Node {

    int data;
    Node left, right;

    public Node(int item)
    {
        data = item;
        left = right = null;
    }
}

class BinaryTree {

    Node root;

    // helper function to check if a Node is leaf of tree
    boolean isLeaf(Node node)
    {
        return ((node.left == null) && (node.right == null));
    }

    /* Calculate sum of all leaf Nodes at each level and returns
     multiplication of sums */
    int sumAndMultiplyLevelData()
    {
        return sumAndMultiplyLevelData(root);
    }
    int sumAndMultiplyLevelData(Node node)
    {
        // Tree is empty
        if (node == null) {
            return 0;
        }

        int mul = 1; /* To store result */

        // Create an empty queue for level order traversal
        LinkedList<Node> q = new LinkedList<Node>();

        // Enqueue Root and initialize height
        q.add(node);

        // Do level order traversal of tree
        while (true) {

            // NodeCount (queue size) indicates number of Nodes
            // at current level.
            int NodeCount = q.size();

            // If there are no Nodes at current level, we are done
            if (NodeCount == 0) {
                break;
            }

            // Initialize leaf sum for current level
            int levelSum = 0;

            // A boolean variable to indicate if found a leaf
            // Node at current level or not
            boolean leafFound = false;

            // Dequeue all Nodes of current level and Enqueue all
            // Nodes of next level
            while (NodeCount > 0) {
                Node node1;
                node1 = q.poll();

                /* if Node is a leaf, update sum at the level */
                if (isLeaf(node1)) {
                    leafFound = true;
                    levelSum += node1.data;
                }

                // Add children of Node
                if (node1.left != null) {
                    q.add(node1.left);
                }
                if (node1.right != null) {
                    q.add(node1.right);
                }
                NodeCount--;
            }

            // If we found at least one leaf, we multiply
            // result with level sum.
            if (leafFound) {
                mul *= levelSum;
            }
        }

        return mul; // Return result
    }

    public static void main(String args[])
    {

        /* creating a binary tree and entering
         the nodes */
        BinaryTree tree = new BinaryTree();
        tree.root = new Node(2);
        tree.root.left = new Node(7);
        tree.root.right = new Node(5);
        tree.root.left.left = new Node(8);
        tree.root.left.right = new Node(6);
        tree.root.left.right.left = new Node(1);
        tree.root.left.right.right = new Node(11);
        tree.root.right.right = new Node(9);
        tree.root.right.right.left = new Node(4);
        tree.root.right.right.right = new Node(10);
        System.out.println("The final product value : "
                           + tree.sumAndMultiplyLevelData());
    }
}

// This code is contributed by Mayank Jaiswal
```

## 蟒蛇 3

```
"""Iterative Python3 program to find
sum of data of all leaves of a binary
tree on same level and then multiply
sums obtained of all levels."""

# A Binary Tree Node
# Utility function to create a
# new tree Node
class newNode:
    def __init__(self, data):
        self.data = data
        self.left = self.right = None

# helper function to check if a
# Node is leaf of tree
def isLeaf(root) :

    return (not root.left and
            not root.right)

""" Calculate sum of all leaf Nodes at each
level and returns multiplication of sums """
def sumAndMultiplyLevelData( root) :

    # Tree is empty
    if (not root) :
        return 0

    mul = 1

    """ To store result """
    # Create an empty queue for level
    # order traversal
    q = []

    # Enqueue Root and initialize height
    q.append(root)

    # Do level order traversal of tree
    while (1):

        # NodeCount (queue size) indicates
        # number of Nodes at current level.
        NodeCount = len(q)

        # If there are no Nodes at current
        # level, we are done
        if (NodeCount == 0) :
            break

        # Initialize leaf sum for
        # current level
        levelSum = 0

        # A boolean variable to indicate
        # if found a leaf Node at current
        # level or not
        leafFound = False

        # Dequeue all Nodes of current level
        # and Enqueue all Nodes of next level
        while (NodeCount > 0) :

            # Process next Node of current level
            Node = q[0]

            """ if Node is a leaf, update
                sum at the level """
            if (isLeaf(Node)) :
                leafFound = True
                levelSum += Node.data

            q.pop(0)

            # Add children of Node
            if (Node.left != None) :
                q.append(Node.left)
            if (Node.right != None) :
                q.append(Node.right)
            NodeCount-=1

        # If we found at least one leaf,
        # we multiply result with level sum.
        if (leafFound) :
            mul *= levelSum

    return mul # Return result

# Driver Code
if __name__ == '__main__':
    root = newNode(2)
    root.left = newNode(7)
    root.right = newNode(5)
    root.left.right = newNode(6)
    root.left.left = newNode(8)
    root.left.right.left = newNode(1)
    root.left.right.right = newNode(11)
    root.right.right = newNode(9)
    root.right.right.left = newNode(4)
    root.right.right.right = newNode(10)

    print("Final product value = ",
           sumAndMultiplyLevelData(root))

# This code is contributed
# by SHUBHAMSINGH10
```

## C#

```
/* Iterative C# program to find sum
of data of all leaves of a binary tree
on same level and then multiply sums
obtained of all levels. */

/* importing the necessary class */
using System;
using System.Collections.Generic;

/* Class containing left and right child
 of current node and key value*/
public class Node
{

    public int data;
    public Node left, right;

    public Node(int item)
    {
        data = item;
        left = right = null;
    }
}

public class BinaryTree
{

    Node root;

    // helper function to check if
    // a Node is leaf of tree
    bool isLeaf(Node node)
    {
        return ((node.left == null) &&
                (node.right == null));
    }

    /* Calculate sum of all leaf
    Nodes at each level and returns
    multiplication of sums */
    int sumAndMultiplyLevelData()
    {
        return sumAndMultiplyLevelData(root);
    }
    int sumAndMultiplyLevelData(Node node)
    {
        // Tree is empty
        if (node == null) {
            return 0;
        }

        int mul = 1; /* To store result */

        // Create an empty queue for level order traversal
        Queue<Node> q = new Queue<Node>();

        // Enqueue Root and initialize height
        q.Enqueue(node);

        // Do level order traversal of tree
        while (true) {

            // NodeCount (queue size) indicates
            // number of Nodes at current level.
            int NodeCount = q.Count;

            // If there are no Nodes at current
            // level, we are done
            if (NodeCount == 0)
            {
                break;
            }

            // Initialize leaf sum for current level
            int levelSum = 0;

            // A boolean variable to indicate if found a leaf
            // Node at current level or not
            bool leafFound = false;

            // Dequeue all Nodes of current level and
            // Enqueue all Nodes of next level
            while (NodeCount > 0)
            {
                Node node1;
                node1 = q.Dequeue();

                /* if Node is a leaf, update sum at the level */
                if (isLeaf(node1))
                {
                    leafFound = true;
                    levelSum += node1.data;
                }

                // Add children of Node
                if (node1.left != null)
                {
                    q.Enqueue(node1.left);
                }
                if (node1.right != null)
                {
                    q.Enqueue(node1.right);
                }
                NodeCount--;
            }

            // If we found at least one leaf, we multiply
            // result with level sum.
            if (leafFound)
            {
                mul *= levelSum;
            }
        }

        return mul; // Return result
    }

    // Driver code
    public static void Main(String []args)
    {

        /* creating a binary tree and entering
        the nodes */
        BinaryTree tree = new BinaryTree();
        tree.root = new Node(2);
        tree.root.left = new Node(7);
        tree.root.right = new Node(5);
        tree.root.left.left = new Node(8);
        tree.root.left.right = new Node(6);
        tree.root.left.right.left = new Node(1);
        tree.root.left.right.right = new Node(11);
        tree.root.right.right = new Node(9);
        tree.root.right.right.left = new Node(4);
        tree.root.right.right.right = new Node(10);
        Console.WriteLine("The final product value : "
                        + tree.sumAndMultiplyLevelData());
    }
}

// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>

/* Iterative Javascript program to
   find sum of data of all leaves
   of a binary tree on same level
   and then multiply sums
   obtained of all levels. */

/* importing the necessary class */

/* Class containing left and right child of current
 node and key value*/
class Node
{
    constructor(data)
    {
        this.data=data;
        this.left = this.right = null;
    }
}

let root;
// helper function to check if a Node is leaf of tree
function isLeaf(node)
{
    return ((node.left == null) && (node.right == null));
}

/* Calculate sum of all leaf Nodes at each level and returns
     multiplication of sums */   

function sumAndMultiplyLevelData(node)
{
     // Tree is empty
        if (node == null) {
            return 0;
        }

        let mul = 1; /* To store result */

        // Create an empty queue for level order traversal
        let q = [];

        // Enqueue Root and initialize height
        q.push(node);

        // Do level order traversal of tree
        while (true) {

            // NodeCount (queue size) indicates number of Nodes
            // at current level.
            let NodeCount = q.length;

            // If there are no Nodes at current level, we are done
            if (NodeCount == 0) {
                break;
            }

            // Initialize leaf sum for current level
            let levelSum = 0;

            // A boolean variable to indicate if found a leaf
            // Node at current level or not
            let leafFound = false;

            // Dequeue all Nodes of current level and Enqueue all
            // Nodes of next level
            while (NodeCount > 0) {

                let node1= q.shift();

                /* if Node is a leaf, update sum at the level */
                if (isLeaf(node1)) {
                    leafFound = true;
                    levelSum += node1.data;
                }

                // Add children of Node
                if (node1.left != null) {
                    q.push(node1.left);
                }
                if (node1.right != null) {
                    q.push(node1.right);
                }
                NodeCount--;
            }

            // If we found at least one leaf, we multiply
            // result with level sum.
            if (leafFound) {
                mul *= levelSum;
            }
        }

        return mul; // Return result
}

/* creating a binary tree and entering
         the nodes */
root = new Node(2);
root.left = new Node(7);
root.right = new Node(5);
root.left.left = new Node(8);
root.left.right = new Node(6);
root.left.right.left = new Node(1);
root.left.right.right = new Node(11);
root.right.right = new Node(9);
root.right.right.left = new Node(4);
root.right.right.right = new Node(10);
document.write("The final product value : "
                   + sumAndMultiplyLevelData(root));

// This code is contributed by rag2127

</script>
```

**输出:**

```
Final product value = 208
```

本文由[穆罕默德·拉基布](https://in.linkedin.com/in/mohammed-raqeeb-soudagar-951b345a)供稿。如果你发现任何不正确的地方，请写评论，或者你想分享更多关于上面讨论的话题的信息