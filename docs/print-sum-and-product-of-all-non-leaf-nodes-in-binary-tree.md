# 打印二叉树中所有非叶节点的和与积

> 原文:[https://www . geesforgeks . org/print-sum-and-product-of-all-non-leaf-nodes-in-binary-tree/](https://www.geeksforgeeks.org/print-sum-and-product-of-all-non-leaf-nodes-in-binary-tree/)

给定一个二叉树。任务是查找并打印树中所有内部节点(非叶节点)的乘积和总和。

![](img/f873e44d4eb588f2f91322a871fd3627.png)

在上面的树中，只有两个节点 1 和 2 是非叶节点。
因此，非叶节点的积= 1 * 2 = 2。
非叶节点之和= 1 + 2 =3。
**例:**

```
Input :
        1
      /   \
     2     3
    / \   / \
   4   5 6   7
          \
           8
Output : Product  = 36, Sum = 12
Non-leaf nodes are: 1, 2, 3, 6 
```

**方法:**想法是以任何方式遍历树，并检查当前节点是否是非叶节点。取两个变量*积*和*和*分别存储非叶节点的积和。如果当前节点是非叶节点，则将该节点的数据乘以用于存储非叶节点乘积的变量乘积，并将该节点的数据加到用于存储非叶节点总和的变量和上。
以下是上述思路的实现:

## C++

```
// CPP program to find product and sum of
// non-leaf nodes in a binary tree
#include <bits/stdc++.h>
using namespace std;

/* A binary tree node has data, pointer to
left child and a pointer to right child */
struct Node {
    int data;
    struct Node* left;
    struct Node* right;
};

/* Helper function that allocates a new node with the
given data and NULL left and right pointers. */
struct Node* newNode(int data)
{
    struct Node* node = new Node;
    node->data = data;
    node->left = node->right = NULL;
    return (node);
}

// Computes the product of non-leaf
// nodes in a tree
void findProductSum(struct Node* root, int& prod, int& sum)
{
    // Base cases
    if (root == NULL || (root->left == NULL
                            && root->right == NULL))
        return;

    // if current node is non-leaf,
    // calculate product and sum
    if (root->left != NULL || root->right != NULL)
    {
        prod *= root->data;
        sum += root->data;
    }

    // If root is Not NULL and its one of its
    // child is also not NULL
    findProductSum(root->left, prod, sum);
    findProductSum(root->right, prod, sum);
}

// Driver Code
int main()
{  
    // Binary Tree
    struct Node* root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->left->right = newNode(5);

    int prod = 1;
    int sum = 0;

    findProductSum(root, prod, sum);

    cout <<"Product = "<<prod<<" , Sum = "<<sum;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find product and sum of
// non-leaf nodes in a binary tree
class GFG
{

/* A binary tree node has data, pointer to
left child and a pointer to right child */
static class Node
{
    int data;
    Node left;
    Node right;
};

/* Helper function that allocates a new node with the
given data and null left and right pointers. */
static Node newNode(int data)
{
    Node node = new Node();
    node.data = data;
    node.left = node.right = null;
    return (node);
}

//int class
static class Int
{
    int a;
}

// Computes the product of non-leaf
// nodes in a tree
static void findProductSum(Node root, Int prod, Int sum)
{
    // Base cases
    if (root == null || (root.left == null
                            && root.right == null))
        return;

    // if current node is non-leaf,
    // calculate product and sum
    if (root.left != null || root.right != null)
    {
        prod.a *= root.data;
        sum.a += root.data;
    }

    // If root is Not null and its one of its
    // child is also not null
    findProductSum(root.left, prod, sum);
    findProductSum(root.right, prod, sum);
}

// Driver Code
public static void main(String args[])
{
    // Binary Tree
    Node root = newNode(1);
    root.left = newNode(2);
    root.right = newNode(3);
    root.left.left = newNode(4);
    root.left.right = newNode(5);

    Int prod = new Int();prod.a = 1;
    Int sum = new Int(); sum.a = 0;

    findProductSum(root, prod, sum);

    System.out.print("Product = " + prod.a + " , Sum = " + sum.a);
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 program to find product and sum
# of non-leaf nodes in a binary tree

# Helper function that allocates a new
# node with the given data and None
# left and right poers.                                
class newNode:

    # Construct to create a new node
    def __init__(self, key):
        self.data = key
        self.left = None
        self.right = None

# Computes the product of non-leaf
# nodes in a tree
class new:
    def findProductSum(sf,root) :

        # Base cases
        if (root == None or (root.left == None and
                             root.right == None)) :
            return

        # if current node is non-leaf,
        # calculate product and sum
        if (root.left != None or
            root.right != None) :

            sf.prod *= root.data
            sf.sum += root.data

        # If root is Not None and its one
        # of its child is also not None
        sf.findProductSum(root.left)
        sf.findProductSum(root.right)

    def main(sf):
        root = newNode(1)

        root.left = newNode(2)
        root.right = newNode(3)
        root.left.left = newNode(4)
        root.left.right = newNode(5)

        sf.prod = 1
        sf.sum = 0

        sf.findProductSum(root)

        print("Product =", sf.prod,
              ", Sum =", sf.sum)

# Driver Code
if __name__ == '__main__':
    x = new()
    x.main()

# This code is contributed by
# Shubham Singh(SHUBHAMSINGH10)
```

## C#

```
// C# program to find product and sum of
// non-leaf nodes in a binary tree
using System;

class GFG
{

/* A binary tree node has data, pointer to
left child and a pointer to right child */
public class Node
{
    public int data;
    public Node left;
    public Node right;
};

/* Helper function that allocates a new node with the
given data and null left and right pointers. */
static Node newNode(int data)
{
    Node node = new Node();
    node.data = data;
    node.left = node.right = null;
    return (node);
}

// int class
public class Int
{
    public int a;
}

// Computes the product of non-leaf
// nodes in a tree
static void findProductSum(Node root, Int prod, Int sum)
{
    // Base cases
    if (root == null || (root.left == null
                            && root.right == null))
        return;

    // if current node is non-leaf,
    // calculate product and sum
    if (root.left != null || root.right != null)
    {
        prod.a *= root.data;
        sum.a += root.data;
    }

    // If root is Not null and its one of its
    // child is also not null
    findProductSum(root.left, prod, sum);
    findProductSum(root.right, prod, sum);
}

// Driver Code
public static void Main(String []args)
{
    // Binary Tree
    Node root = newNode(1);
    root.left = newNode(2);
    root.right = newNode(3);
    root.left.left = newNode(4);
    root.left.right = newNode(5);

    Int prod = new Int();prod.a = 1;
    Int sum = new Int(); sum.a = 0;

    findProductSum(root, prod, sum);

    Console.Write("Product = " + prod.a + " , Sum = " + sum.a);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program to find product and sum of
// non-leaf nodes in a binary tree
/* A binary tree node has data, pointer to
left child and a pointer to right child */
class Node {
    constructor() {
        this.data = 0;
        this.left = null;
        this.right = null;
    }
}

/* Helper function that allocates a new node with the
given data and null left and right pointers. */
function newNode(data)
{
    var node = new Node();
    node.data = data;
    node.left = node.right = null;
    return (node);
}

//var class
 class Int
{
constructor(){
    this.a = 0;
    }
}

// Computes the product of non-leaf
// nodes in a tree
function findProductSum(root,  prod,  sum)
{
    // Base cases
    if (root == null || (root.left == null
                            && root.right == null))
        return;

    // if current node is non-leaf,
    // calculate product and sum
    if (root.left != null || root.right != null)
    {
        prod.a *= root.data;
        sum.a += root.data;
    }

    // If root is Not null and its one of its
    // child is also not null
    findProductSum(root.left, prod, sum);
    findProductSum(root.right, prod, sum);
}

// Driver Code

    // Binary Tree
     root = newNode(1);
    root.left = newNode(2);
    root.right = newNode(3);
    root.left.left = newNode(4);
    root.left.right = newNode(5);

    var prod = new Int();
    prod.a = 1;
    var sum = new Int();
    sum.a = 0;

    findProductSum(root, prod, sum);

    document.write("Product = " + prod.a + " , Sum = " + sum.a);

// This code contributed by aashish1995

</script>
```

**Output:** 

```
Product = 2 , Sum = 3
```