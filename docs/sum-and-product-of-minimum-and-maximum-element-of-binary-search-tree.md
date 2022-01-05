# 二叉查找树最小和最大元素的和与积

> 原文:[https://www . geeksforgeeks . org/二进制搜索树最小和最大元素之和与乘积/](https://www.geeksforgeeks.org/sum-and-product-of-minimum-and-maximum-element-of-binary-search-tree/)

给一个二叉查找树。任务是找到树的最大值和最小值的和与积。

![](img/8ae9fabdbc84861420368ee7e052a538.png)

对于上面的树，树的最大值和最小值的和与积分别是 26 和 88。

**进场:**

1.  **对于最小值的节点:**找到最左边的叶节点
2.  **对于最大值的节点:**找到最右边的叶节点

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

/* A binary tree node has data, pointer to left child 
   and a pointer to right child */
struct node {
    int data;
    struct node* left;
    struct node* right;
};

/* Helper function that allocates a new node 
with the given data and NULL left and right 
pointers. */
struct node* newNode(int data)
{
    struct node* newnode = new node();
    newnode->data = data;
    newnode->left = NULL;
    newnode->right = NULL;

    return (newnode);
}

// Function to insert a node in BST
struct node* insert(struct node* node, int data)
{
    /* 1\. If the tree is empty, return a new,     
      single node */
    if (node == NULL)
        return (newNode(data));
    else {
        /* 2\. Otherwise, recur down the tree */
        if (data <= node->data)
            node->left = insert(node->left, data);
        else
            node->right = insert(node->right, data);

        /* return the (unchanged) node pointer */
        return node;
    }
}

// Function to find the node with maximum value
int maxValue(struct node* node)
{
    struct node* current = node;

    // Find the rightmost leaf
    while (current->right != NULL) {
        current = current->right;
    }
    return (current->data);
}

// Function to find the node with minimum value
int minValue(struct node* node)
{
    struct node* current = node;

    // Find the leftmost leaf
    while (current->left != NULL) {
        current = current->left;
    }
    return (current->data);
}

// Driver code
int main()
{
    struct node* root = NULL;
    root = insert(root, 4);
    insert(root, 2);
    insert(root, 1);
    insert(root, 3);
    insert(root, 6);
    insert(root, 5);

   int maxNodeValue = maxValue(root);
   int minNodeValue = minValue(root);

    cout << "Sum of Maximum value and Minimum value in BST is "
         << maxNodeValue + minNodeValue << endl;

    cout << "Product of Maximum value and Minimum value in BST is "
         << maxNodeValue * minNodeValue;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG
{

/* A binary tree node has data,
pointer to left child and
a pointer to right child */
static class node
{
    int data;
    node left;
    node right;
};

/* Helper function that allocates a new node
with the given data and null left and right
pointers. */
static node newNode(int data)
{
    node node = new node();
    node.data = data;
    node.left = null;
    node.right = null;

    return (node);
}

// Function to insert a node in BST
static node insert( node node, int data)
{
    /* 1\. If the tree is empty,     
    return a new, single node */
    if (node == null)
        return (newNode(data));
    else
    {
        /* 2\. Otherwise, recur down the tree */
        if (data <= node.data)
            node.left = insert(node.left, data);
        else
            node.right = insert(node.right, data);

        /* return the (unchanged) node pointer */
        return node;
    }
}

// Function to find the node with maximum value
static int maxValue(node node)
{
    node current = node;

    // Find the rightmost leaf
    while (current.right != null)
    {
        current = current.right;
    }
    return (current.data);
}

// Function to find the node with minimum value
static int minValue(node node)
{
    node current = node;

    // Find the leftmost leaf
    while (current.left != null)
    {
        current = current.left;
    }
    return (current.data);
}

// Driver code
public static void main(String args[])
{
    node root = null;
    root = insert(root, 4);
    root = insert(root, 2);
    root = insert(root, 1);
    root = insert(root, 3);
    root = insert(root, 6);
    root = insert(root, 5);

    int maxNodeValue = maxValue(root);
    int minNodeValue = minValue(root);

    System.out.println( "Sum of Maximum value and" +
                        " Minimum value in BST is " +
                        (maxNodeValue + minNodeValue));

    System.out.println( "Product of Maximum value and " +
                        "Minimum value in BST is " +
                         maxNodeValue * minNodeValue);
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python program to find sum and product of
# maximum and minimum in a Binary search Tree

_MIN=-2147483648
_MAX=2147483648

# Helper function that allocates a new
# node with the given data and None left
# and right pointers.                                
class newNode:

    # Constructor to create a new node
    def __init__(self,data):
        self.data = data
        self.left = None
        self.right = None

# Function to insert a node in BST
def insert(node, data):

    # 1\. If the tree is empty, return a new,    
    # single node
    if (node == None):
        return (newNode(data))
    else:

        # 2\. Otherwise, recur down the tree
        if (data <= node.data):
            node.left = insert(node.left, data)
        else:
            node.right = insert(node.right, data)

        # return the (unchanged) node pointer
        return node

# Function to find the node with maximum value
def maxValue(node):
    current = node

    # Find the rightmost leaf
    while (current.right != None) :
        current = current.right

    return (current.data)

# Function to find the node with minimum value
def minValue(node):

    current = node

    # Find the leftmost leaf
    while (current.left != None):
        current = current.left

    return (current.data)

# Driver Code
if __name__ == '__main__':

    # Create binary Tree
    root = newNode(2)
    insert(root, 1)
    insert(root, 3)
    insert(root, 6)
    insert(root, 5)
    max = maxValue(root)
    min = minValue(root)

    print("Sum of Maximum and Minimum" +
            "element is ", max + min)
    print("Product of Maximum and Minimum" +
            "element is", max * min)

# This code is contributed
# Shubham Singh(SHUBHAMSINGH10)
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

/* A binary tree node has data,
pointer to left child and
a pointer to right child */
public class node
{
    public int data;
    public node left;
    public node right;
};

/* Helper function that allocates a new node
with the given data and null left and right
pointers. */
static node newNode(int data)
{
    node node = new node();
    node.data = data;
    node.left = null;
    node.right = null;

    return (node);
}

// Function to insert a node in BST
static node insert( node node, int data)
{
    /* 1\. If the tree is empty,    
    return a new, single node */
    if (node == null)
        return (newNode(data));
    else
    {
        /* 2\. Otherwise, recur down the tree */
        if (data <= node.data)
            node.left = insert(node.left, data);
        else
            node.right = insert(node.right, data);

        /* return the (unchanged) node pointer */
        return node;
    }
}

// Function to find the node with maximum value
static int maxValue(node node)
{
    node current = node;

    // Find the rightmost leaf
    while (current.right != null)
    {
        current = current.right;
    }
    return (current.data);
}

// Function to find the node with minimum value
static int minValue(node node)
{
    node current = node;

    // Find the leftmost leaf
    while (current.left != null)
    {
        current = current.left;
    }
    return (current.data);
}

// Driver code
public static void Main(String []args)
{
    node root = null;
    root = insert(root, 4);
    root = insert(root, 2);
    root = insert(root, 1);
    root = insert(root, 3);
    root = insert(root, 6);
    root = insert(root, 5);

    int maxNodeValue = maxValue(root);
    int minNodeValue = minValue(root);

    Console.WriteLine( "Sum of Maximum value and" +
                        " Minimum value in BST is " +
                        (maxNodeValue + minNodeValue));

    Console.WriteLine( "Product of Maximum value and " +
                        "Minimum value in BST is " +
                        maxNodeValue * minNodeValue);
}
}

/* This code is contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>
    // javascript implementation of the above approach   
    /*
     * A binary tree node has data, pointer to left child and a pointer to right
     * child
     */

     class Node {
        constructor(val) {
            this.data = val;
            this.left = null;
            this.right = null;
        }
     }
    /*
     * Helper function that allocates a new node with the given data and null left
     * and right pointers.
     */
     function newNode(data) {
        var node = new Node();
        node.data = data;
        node.left = null;
        node.right = null;

        return (node);
    }

    // Function to insert a node in BST
     function insert( node , data) {
        /*
         * 1\. If the tree is empty, return a new, single node
         */
        if (node == null)
            return (newNode(data));
        else {
            /* 2\. Otherwise, recur down the tree */
            if (data <= node.data)
                node.left = insert(node.left, data);
            else
                node.right = insert(node.right, data);

            /* return the (unchanged) node pointer */
            return node;
        }
    }

    // Function to find the node with maximum value
    function maxValue( node) {
        var current = node;

        // Find the rightmost leaf
        while (current.right != null) {
            current = current.right;
        }
        return (current.data);
    }

    // Function to find the node with minimum value
    function minValue( node) {
        var current = node;

        // Find the leftmost leaf
        while (current.left != null) {
            current = current.left;
        }
        return (current.data);
    }

    // Driver code

        var root = null;
        root = insert(root, 4);
        root = insert(root, 2);
        root = insert(root, 1);
        root = insert(root, 3);
        root = insert(root, 6);
        root = insert(root, 5);

        var maxNodeValue = maxValue(root);
        var minNodeValue = minValue(root);

        document.write("Sum of Maximum value and"
        + " Minimum value in BST is " + (maxNodeValue + minNodeValue)+"<br/>");

        document.write("Product of Maximum value and "
        + "Minimum value in BST is " + maxNodeValue * minNodeValue);

// This code contributed by Rajput-Ji
</script>
```

**Output:** 

```
Sum of Maximum value and Minimum value in BST is 7
Product of Maximum value and Minimum value in BST is 6
```

***时间复杂度** : O(N)*
***辅助空间** : O(1)*