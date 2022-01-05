# 求二叉树中叶到根路径的最大和

> 原文:[https://www . geesforgeks . org/find-二叉树中最大和路径/](https://www.geeksforgeeks.org/find-the-maximum-sum-path-in-a-binary-tree/)

```
                  10
               /      \
             -2        7
           /   \     
          8     -4    

```

**解**
1)首先找到最大和路径上的叶节点。在下面的代码中，getTargetLeaf()通过将结果赋给*target_leaf_ref 来实现这一点。
2)一旦我们有了目标叶节点，我们就可以通过遍历树来打印最大和路径。在下面的代码中，printPath()实现了这一点。

主要函数是 maxSumPath()，利用上面两个函数得到完整的解。

## C++

```
// CPP program to find maximum sum leaf to root
// path in Binary Tree
#include <bits/stdc++.h>
using namespace std;

/* A tree node structure */
class node {
public:
    int data;
    node* left;
    node* right;
};

// A utility function that prints all nodes
// on the path from root to target_leaf
bool printPath(node* root,
               node* target_leaf)
{
    // base case
    if (root == NULL)
        return false;

    // return true if this node is the target_leaf
    // or target leaf is present in one of its
    // descendants
    if (root == target_leaf || printPath(root->left, target_leaf) || 
                               printPath(root->right, target_leaf)) {
        cout << root->data << " ";
        return true;
    }

    return false;
}

// This function Sets the target_leaf_ref to refer
// the leaf node of the maximum path sum. Also,
// returns the max_sum using max_sum_ref
void getTargetLeaf(node* Node, int* max_sum_ref,
                   int curr_sum, node** target_leaf_ref)
{
    if (Node == NULL)
        return;

    // Update current sum to hold sum of nodes on path
    // from root to this node
    curr_sum = curr_sum + Node->data;

    // If this is a leaf node and path to this node has
    // maximum sum so far, then make this node target_leaf
    if (Node->left == NULL && Node->right == NULL) {
        if (curr_sum > *max_sum_ref) {
            *max_sum_ref = curr_sum;
            *target_leaf_ref = Node;
        }
    }

    // If this is not a leaf node, then recur down
    // to find the target_leaf
    getTargetLeaf(Node->left, max_sum_ref, curr_sum,
                  target_leaf_ref);
    getTargetLeaf(Node->right, max_sum_ref, curr_sum,
                  target_leaf_ref);
}

// Returns the maximum sum and prints the nodes on max
// sum path
int maxSumPath(node* Node)
{
    // base case
    if (Node == NULL)
        return 0;

    node* target_leaf;
    int max_sum = INT_MIN;

    // find the target leaf and maximum sum
    getTargetLeaf(Node, &max_sum, 0, &target_leaf);

    // print the path from root to the target leaf
    printPath(Node, target_leaf);

    return max_sum; // return maximum sum
}

/* Utility function to create a new Binary Tree node */
node* newNode(int data)
{
    node* temp = new node;
    temp->data = data;
    temp->left = NULL;
    temp->right = NULL;
    return temp;
}

/* Driver function to test above functions */
int main()
{
    node* root = NULL;

    /* Constructing tree given in the above figure */
    root = newNode(10);
    root->left = newNode(-2);
    root->right = newNode(7);
    root->left->left = newNode(8);
    root->left->right = newNode(-4);

    cout << "Following are the nodes on the maximum "
            "sum path \n";
    int sum = maxSumPath(root);
    cout << "\nSum of the nodes is " << sum;
    return 0;
}

// This code is contributed by rathbhupendra
```

## C

```
// C program to find maximum sum leaf to root
// path in Binary Tree
#include <limits.h>
#include <stdbool.h>
#include <stdio.h>
#include <stdlib.h>

/* A tree node structure */
struct node {
    int data;
    struct node* left;
    struct node* right;
};

// A utility function that prints all nodes
// on the path from root to target_leaf
bool printPath(struct node* root,
               struct node* target_leaf)
{
    // base case
    if (root == NULL)
        return false;

    // return true if this node is the target_leaf
    // or target leaf is present in one of its
    // descendants
    if (root == target_leaf || printPath(root->left, target_leaf) || 
                               printPath(root->right, target_leaf)) {
        printf("%d ", root->data);
        return true;
    }

    return false;
}

// This function Sets the target_leaf_ref to refer
// the leaf node of the maximum path sum. Also,
// returns the max_sum using max_sum_ref
void getTargetLeaf(struct node* node, int* max_sum_ref,
                   int curr_sum, struct node** target_leaf_ref)
{
    if (node == NULL)
        return;

    // Update current sum to hold sum of nodes on path
    // from root to this node
    curr_sum = curr_sum + node->data;

    // If this is a leaf node and path to this node has
    // maximum sum so far, then make this node target_leaf
    if (node->left == NULL && node->right == NULL) {
        if (curr_sum > *max_sum_ref) {
            *max_sum_ref = curr_sum;
            *target_leaf_ref = node;
        }
    }

    // If this is not a leaf node, then recur down
    // to find the target_leaf
    getTargetLeaf(node->left, max_sum_ref, curr_sum,
                  target_leaf_ref);
    getTargetLeaf(node->right, max_sum_ref, curr_sum,
                  target_leaf_ref);
}

// Returns the maximum sum and prints the nodes on max
// sum path
int maxSumPath(struct node* node)
{
    // base case
    if (node == NULL)
        return 0;

    struct node* target_leaf;
    int max_sum = INT_MIN;

    // find the target leaf and maximum sum
    getTargetLeaf(node, &max_sum, 0, &target_leaf);

    // print the path from root to the target leaf
    printPath(node, target_leaf);

    return max_sum; // return maximum sum
}

/* Utility function to create a new Binary Tree node */
struct node* newNode(int data)
{
    struct node* temp = (struct node*)malloc(sizeof(struct node));
    temp->data = data;
    temp->left = NULL;
    temp->right = NULL;
    return temp;
}

/* Driver function to test above functions */
int main()
{
    struct node* root = NULL;

    /* Constructing tree given in the above figure */
    root = newNode(10);
    root->left = newNode(-2);
    root->right = newNode(7);
    root->left->left = newNode(8);
    root->left->right = newNode(-4);

    printf("Following are the nodes on the maximum "
           "sum path \n");
    int sum = maxSumPath(root);
    printf("\nSum of the nodes is %d ", sum);

    getchar();
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find maximum sum leaf to root
// path in Binary Tree

// A Binary Tree node
class Node {
    int data;
    Node left, right;

    Node(int item)
    {
        data = item;
        left = right = null;
    }
}

// A wrapper class is used so that max_no
// can be updated among function calls.
class Maximum {
    int max_no = Integer.MIN_VALUE;
}

class BinaryTree {
    Node root;
    Maximum max = new Maximum();
    Node target_leaf = null;

    // A utility function that prints all nodes on the
    // path from root to target_leaf
    boolean printPath(Node node, Node target_leaf)
    {
        // base case
        if (node == null)
            return false;

        // return true if this node is the target_leaf or
        // target leaf is present in one of its descendants
        if (node == target_leaf || printPath(node.left, target_leaf)
            || printPath(node.right, target_leaf)) {
            System.out.print(node.data + " ");
            return true;
        }

        return false;
    }

    // This function Sets the target_leaf_ref to refer
    // the leaf node of the maximum path sum. Also,
    // returns the max_sum using max_sum_ref
    void getTargetLeaf(Node node, Maximum max_sum_ref,
                       int curr_sum)
    {
        if (node == null)
            return;

        // Update current sum to hold sum of nodes on
        // path from root to this node
        curr_sum = curr_sum + node.data;

        // If this is a leaf node and path to this node
        // has maximum sum so far, the n make this node
        // target_leaf
        if (node.left == null && node.right == null) {
            if (curr_sum > max_sum_ref.max_no) {
                max_sum_ref.max_no = curr_sum;
                target_leaf = node;
            }
        }

        // If this is not a leaf node, then recur down
        // to find the target_leaf
        getTargetLeaf(node.left, max_sum_ref, curr_sum);
        getTargetLeaf(node.right, max_sum_ref, curr_sum);
    }

    // Returns the maximum sum and prints the nodes on
    // max sum path
    int maxSumPath()
    {
        // base case
        if (root == null)
            return 0;

        // find the target leaf and maximum sum
        getTargetLeaf(root, max, 0);

        // print the path from root to the target leaf
        printPath(root, target_leaf);
        return max.max_no; // return maximum sum
    }

    // driver function to test the above functions
    public static void main(String args[])
    {
        BinaryTree tree = new BinaryTree();
        tree.root = new Node(10);
        tree.root.left = new Node(-2);
        tree.root.right = new Node(7);
        tree.root.left.left = new Node(8);
        tree.root.left.right = new Node(-4);
        System.out.println("Following are the nodes "
                           + "on maximum sum path");
        int sum = tree.maxSumPath();
        System.out.println("");
        System.out.println("Sum of nodes is : " + sum);
    }
}
// This code has been contributed by Mayank Jaiswal
```

## 蟒蛇 3

```
# Python3 program to find maximum sum leaf to root
# path in Binary Tree

# A tree node structure 
class node :
    def __init__(self):
        self.data = 0
        self.left = None
        self.right = None

# A utility function that prints all nodes
# on the path from root to target_leaf
def printPath( root,target_leaf):

    # base case
    if (root == None):
        return False

    # return True if this node is the target_leaf
    # or target leaf is present in one of its
    # descendants
    if (root == target_leaf or 
        printPath(root.left, target_leaf) or 
        printPath(root.right, target_leaf)) :
        print( root.data, end = " ")
        return True

    return False

max_sum_ref = 0
target_leaf_ref = None

# This function Sets the target_leaf_ref to refer
# the leaf node of the maximum path sum. Also,
# returns the max_sum using max_sum_ref
def getTargetLeaf(Node, curr_sum):

    global max_sum_ref
    global target_leaf_ref

    if (Node == None):
        return

    # Update current sum to hold sum of nodes on path
    # from root to this node
    curr_sum = curr_sum + Node.data

    # If this is a leaf node and path to this node has
    # maximum sum so far, then make this node target_leaf
    if (Node.left == None and Node.right == None): 
        if (curr_sum > max_sum_ref) :
            max_sum_ref = curr_sum
            target_leaf_ref = Node

    # If this is not a leaf node, then recur down
    # to find the target_leaf
    getTargetLeaf(Node.left, curr_sum)
    getTargetLeaf(Node.right, curr_sum)

# Returns the maximum sum and prints the nodes on max
# sum path
def maxSumPath( Node):

    global max_sum_ref
    global target_leaf_ref

    # base case
    if (Node == None):
        return 0

    target_leaf_ref = None
    max_sum_ref = -32676

    # find the target leaf and maximum sum
    getTargetLeaf(Node, 0)

    # print the path from root to the target leaf
    printPath(Node, target_leaf_ref);

    return max_sum_ref; # return maximum sum

# Utility function to create a new Binary Tree node 
def newNode(data):

    temp = node();
    temp.data = data;
    temp.left = None;
    temp.right = None;
    return temp;

# Driver function to test above functions 

root = None;

# Constructing tree given in the above figure 
root = newNode(10);
root.left = newNode(-2);
root.right = newNode(7);
root.left.left = newNode(8);
root.left.right = newNode(-4);

print( "Following are the nodes on the maximum sum path ");
sum = maxSumPath(root);
print( "\nSum of the nodes is " , sum);

# This code is contributed by Arnab Kundu

```

## C#

```
using System;

// C# program to find maximum sum leaf to root
// path in Binary Tree

// A Binary Tree node
public class Node {
    public int data;
    public Node left, right;

    public Node(int item)
    {
        data = item;
        left = right = null;
    }
}

// A wrapper class is used so that max_no
// can be updated among function calls.
public class Maximum {
    public int max_no = int.MinValue;
}

public class BinaryTree {
    public Node root;
    public Maximum max = new Maximum();
    public Node target_leaf = null;

    // A utility function that prints all nodes on the
    // path from root to target_leaf
    public virtual bool printPath(Node node, Node target_leaf)
    {
        // base case
        if (node == null) {
            return false;
        }

        // return true if this node is the target_leaf or
        // target leaf is present in one of its descendants
        if (node == target_leaf || printPath(node.left, target_leaf)
            || printPath(node.right, target_leaf)) {
            Console.Write(node.data + " ");
            return true;
        }

        return false;
    }

    // This function Sets the target_leaf_ref to refer
    // the leaf node of the maximum path sum. Also,
    // returns the max_sum using max_sum_ref
    public virtual void getTargetLeaf(Node node, Maximum max_sum_ref,
                                      int curr_sum)
    {
        if (node == null) {
            return;
        }

        // Update current sum to hold sum of nodes on
        // path from root to this node
        curr_sum = curr_sum + node.data;

        // If this is a leaf node and path to this node
        // has maximum sum so far, the n make this node
        // target_leaf
        if (node.left == null && node.right == null) {
            if (curr_sum > max_sum_ref.max_no) {
                max_sum_ref.max_no = curr_sum;
                target_leaf = node;
            }
        }

        // If this is not a leaf node, then recur down
        // to find the target_leaf
        getTargetLeaf(node.left, max_sum_ref, curr_sum);
        getTargetLeaf(node.right, max_sum_ref, curr_sum);
    }

    // Returns the maximum sum and prints the nodes on
    // max sum path
    public virtual int maxSumPath()
    {
        // base case
        if (root == null) {
            return 0;
        }

        // find the target leaf and maximum sum
        getTargetLeaf(root, max, 0);

        // print the path from root to the target leaf
        printPath(root, target_leaf);
        return max.max_no; // return maximum sum
    }

    // driver function to test the above functions
    public static void Main(string[] args)
    {
        BinaryTree tree = new BinaryTree();
        tree.root = new Node(10);
        tree.root.left = new Node(-2);
        tree.root.right = new Node(7);
        tree.root.left.left = new Node(8);
        tree.root.left.right = new Node(-4);
        Console.WriteLine("Following are the nodes "
                          + "on maximum sum path");
        int sum = tree.maxSumPath();
        Console.WriteLine("");
        Console.WriteLine("Sum of nodes is : " + sum);
    }
}

// This code is contributed by Shrikant13
```

**Output:**

```
Following are the nodes on the maximum sum path
7 10
Sum of the nodes is 17

```

**时间复杂度:**上述解决方案的时间复杂度为 O(n)，因为它涉及两次树遍历。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。