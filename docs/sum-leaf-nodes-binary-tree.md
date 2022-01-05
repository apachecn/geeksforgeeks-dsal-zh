# 二叉树所有叶节点之和

> 原文:[https://www.geeksforgeeks.org/sum-leaf-nodes-binary-tree/](https://www.geeksforgeeks.org/sum-leaf-nodes-binary-tree/)

给定一棵二叉树，求所有叶节点的和。
示例:

```
Input : 
        1
      /   \
     2     3
    / \   / \
   4   5 6   7
          \
           8
Output :
Sum = 4 + 5 + 8 + 7 = 24
```

其思想是以任何方式遍历树，并检查该节点是否是叶节点。如果节点是叶节点，则将节点数据添加到 sum 变量。
以下是上述方法的实施。

## C++

```
// CPP program to find sum of
// all leaf nodes of binary tree
#include<bits/stdc++.h>
using namespace std;

// struct binary tree node
struct Node{
    int data;
    Node *left, *right;
};

// return new node
Node *newNode(int data){
    Node *temp = new Node();
    temp->data = data;
    temp->left = temp->right = NULL;
    return temp;
}

// utility function which calculates
// sum of all leaf nodes
void leafSum(Node *root, int& sum){
    if (!root)
        return;

    // add root data to sum if
    // root is a leaf node
    if (!root->left && !root->right)
        sum += root->data;

    // propagate recursively in left
    // and right subtree
    leafSum(root->left, sum);
    leafSum(root->right, sum);
}

// driver program
int main(){

    //construct binary tree
    Node *root = newNode(1);
    root->left = newNode(2);
    root->left->left = newNode(4);
    root->left->right = newNode(5);
    root->right = newNode(3);
    root->right->right = newNode(7);
    root->right->left = newNode(6);
    root->right->left->right = newNode(8);

    // variable to store sum of leaf nodes
    int sum = 0;
    leafSum(root, sum);
    cout << sum << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find sum of
// all leaf nodes of binary tree
public class GFG {

    // user define class node
    static class Node{
        int data;
        Node left, right;

        // constructor
        Node(int data){
            this.data = data;
            left = null;
            right = null;
        }
    }

    static int sum;

    // utility function which calculates
    // sum of all leaf nodes
    static void leafSum(Node root){
        if (root == null)
            return;

        // add root data to sum if
        // root is a leaf node
        if (root.left == null && root.right == null)
            sum += root.data;

        // propagate recursively in left
        // and right subtree
        leafSum(root.left);
        leafSum(root.right);
    }

    // driver program
    public static void main(String args[])
    {
        //construct binary tree
        Node root = new Node(1);
        root.left = new Node(2);
        root.left.left = new Node(4);
        root.left.right = new Node(5);
        root.right = new Node(3);
        root.right.right = new Node(7);
        root.right.left = new Node(6);
        root.right.left.right = new Node(8);

        // variable to store sum of leaf nodes
        sum = 0;
        leafSum(root);
        System.out.println(sum);
    }
}
// This code is contributed by Sumit Ghosh
```

## 蟒蛇 3

```
# Python3 Program to find the
#sum of leaf nodes of a binary tree

 # Class for node creation
class Node:

     # Constructor
    def __init__(self, data):            
        self.data = data
        self.left = None
        self.right = None

# Utility function to calculate
# the sum of all leaf nodes
def leafSum(root):
    global total
    if root is None:
        return
    if (root.left is None and root.right is None):
        total += root.data
    leafSum(root.left)
    leafSum(root.right)

# Binary tree Fromation
if __name__=='__main__':
    root = Node(1)
    root.left = Node(2)
    root.left.left = Node(4)
    root.left.right = Node(5)
    root.right = Node(3)
    root.right.right = Node(7)
    root.right.left = Node(6)
    root.right.left.right = Node(8)
# Variable to store the sum of leaf nodes
    total = 0
    leafSum(root)
# Printing the calculated sum
    print(total)

# This code is contributed by Naren Sai Krishna
```

## C#

```
using System;

// C# program to find sum of
// all leaf nodes of binary tree
public class GFG
{

    // user define class node
    public class Node
    {
        public int data;
        public Node left, right;

        // constructor
        public Node(int data)
        {
            this.data = data;
            left = null;
            right = null;
        }
    }

    public static int sum;

    // utility function which calculates
    // sum of all leaf nodes
    public static void leafSum(Node root)
    {
        if (root == null)
        {
            return;
        }

        // add root data to sum if 
        // root is a leaf node
        if (root.left == null && root.right == null)
        {
            sum += root.data;
        }

        // propagate recursively in left
        // and right subtree
        leafSum(root.left);
        leafSum(root.right);
    }

    // driver program
    public static void Main(string[] args)
    {
        //construct binary tree
        Node root = new Node(1);
        root.left = new Node(2);
        root.left.left = new Node(4);
        root.left.right = new Node(5);
        root.right = new Node(3);
        root.right.right = new Node(7);
        root.right.left = new Node(6);
        root.right.left.right = new Node(8);

        // variable to store sum of leaf nodes
        sum = 0;
        leafSum(root);
        Console.WriteLine(sum);
    }
}

  // This code is contributed by Shrikant13
```

## java 描述语言

```
<script>
    // Javascript program to find sum of
    // all leaf nodes of binary tree

    // user define class node
    class Node
    {
        constructor(data) {
           this.left = null;
           this.right = null;
           this.data = data;
        }
    }

    let sum;

    // utility function which calculates
    // sum of all leaf nodes
    function leafSum(root){
        if (root == null)
            return;

        // add root data to sum if
        // root is a leaf node
        if (root.left == null && root.right == null)
            sum += root.data;

        // propagate recursively in left
        // and right subtree
        leafSum(root.left);
        leafSum(root.right);
    }

    // construct binary tree
    let root = new Node(1);
    root.left = new Node(2);
    root.left.left = new Node(4);
    root.left.right = new Node(5);
    root.right = new Node(3);
    root.right.right = new Node(7);
    root.right.left = new Node(6);
    root.right.left.right = new Node(8);

    // variable to store sum of leaf nodes
    sum = 0;
    leafSum(root);
    document.write(sum);

  // This code is contributed by divyesh072019.
</script>
```

**Output:** 

```
24
```