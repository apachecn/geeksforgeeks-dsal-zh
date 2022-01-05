# 打印给定级别的叶节点

> 原文:[https://www . geesforgeks . org/print-leaf-nodes-at-a-给定级别/](https://www.geeksforgeeks.org/print-leaf-nodes-at-a-given-level/)

给定一棵二叉树，打印给定级别 l 的二叉树的所有叶节点。
**示例:**

```
Input:    
           1
          /  \
         2    3
        /    /  \
       4    5    6
 level = 3

Output: 4 5 6

Input:    
             7
            /  \
           2    3
          / \    \
         4   9   10
                 /
                6
   level = 3

Output: 4 9
```

**逼近**:以层级顺序递归遍历树。如果当前级别与给定级别相同，则检查当前节点是否是叶节点。如果它是叶节点，那么打印它。
以下是上述办法的实施情况:

## C++

```
// C++ program to print all the
// leaf nodes at a given level
// in a Binary tree
#include <bits/stdc++.h>
using namespace std;

// Binary tree node
struct node {
    struct node* left;
    struct node* right;
    int data;
};

// Function to create a new
// Binary node
struct node* newNode(int data)
{
    struct node* temp = new node;

    temp->data = data;
    temp->left = NULL;
    temp->right = NULL;

    return temp;
}

// Function to print Leaf Nodes at
// a given level
void PrintLeafNodes(struct node* root, int level)
{
    if (root == NULL)
        return;

    if (level == 1) {
        if (root->left == NULL && root->right == NULL)
            cout << root->data << " ";
    }
    else if (level > 1) {
        PrintLeafNodes(root->left, level - 1);
        PrintLeafNodes(root->right, level - 1);
    }
}

// Driver code
int main()
{
    struct node* root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(6);
    root->right->right = newNode(4);
    root->left->left->left = newNode(8);
    root->left->left->right = newNode(7);

    int level = 4;

    PrintLeafNodes(root, level);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print all the
// leaf nodes at a given level
// in a Binary tree
class GFG
{

    // Binary tree node
    static class node
    {

        node left;
        node right;
        int data;
    };

    // Function to create a new
    // Binary node
    static node newNode(int data)
    {
        node temp = new node();

        temp.data = data;
        temp.left = null;
        temp.right = null;

        return temp;
    }

    // Function to print Leaf Nodes at
    // a given level
    static void PrintLeafNodes(node root, int level)
    {
        if (root == null)
        {
            return;
        }

        if (level == 1)
        {
            if (root.left == null && root.right == null)
            {
                System.out.print(root.data + " ");
            }

        }
        else if (level > 1)
        {
            PrintLeafNodes(root.left, level - 1);
            PrintLeafNodes(root.right, level - 1);
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        node root = newNode(1);
        root.left = newNode(2);
        root.right = newNode(3);
        root.left.left = newNode(6);
        root.right.right = newNode(4);
        root.left.left.left = newNode(8);
        root.left.left.right = newNode(7);

        int level = 4;

        PrintLeafNodes(root, level);
    }
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to print all the
# leaf nodes at a given level
# in a Binary tree

# Binary tree node
class node:

    def __init__(self, data):
        self.left=None
        self.right=None
        self.data=data

# Function to create a new
# Binary node
def newNode(data):
    return node(data)

# Function to print Leaf Nodes at
# a given level
def PrintLeafNodes(root, level):
    if (root == None):
        return

    if (level == 1):
        if (root.left == None and
            root.right == None):
            print(root.data, end = " ")

    elif (level > 1):
        PrintLeafNodes(root.left, level - 1)
        PrintLeafNodes(root.right, level - 1)

if __name__=="__main__":

    root=newNode(1)
    root.left = newNode(2);
    root.right = newNode(3);
    root.left.left = newNode(6);
    root.right.right = newNode(4);
    root.left.left.left = newNode(8);
    root.left.left.right = newNode(7);
    level = 4;
    PrintLeafNodes(root, level);

# This code is contributed by rutvik_56
```

## C#

```
// C# program to print all the
// leaf nodes at a given level
// in a Binary tree
using System;

class GFG
{

    // Binary tree node
    public class node
    {

        public node left;
        public node right;
        public int data;
    };

    // Function to create a new
    // Binary node
    static node newNode(int data)
    {
        node temp = new node();

        temp.data = data;
        temp.left = null;
        temp.right = null;

        return temp;
    }

    // Function to print Leaf Nodes at
    // a given level
    static void PrintLeafNodes(node root, int level)
    {
        if (root == null)
        {
            return;
        }

        if (level == 1)
        {
            if (root.left == null && root.right == null)
            {
                Console.Write(root.data + " ");
            }

        }
        else if (level > 1)
        {
            PrintLeafNodes(root.left, level - 1);
            PrintLeafNodes(root.right, level - 1);
        }
    }

    // Driver code
    public static void Main(String[] args)
    {
        node root = newNode(1);
        root.left = newNode(2);
        root.right = newNode(3);
        root.left.left = newNode(6);
        root.right.right = newNode(4);
        root.left.left.left = newNode(8);
        root.left.left.right = newNode(7);

        int level = 4;

        PrintLeafNodes(root, level);
    }
}

// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>

    // JavaScript program to print all the
    // leaf nodes at a given level
    // in a Binary tree

    // Binary tree node
    class node
    {
        constructor(data) {
           this.left = null;
           this.right = null;
           this.data = data;
        }
    }

    // Function to create a new
    // Binary node
    function newNode(data)
    {
        let temp = new node(data);

        temp.data = data;
        temp.left = null;
        temp.right = null;

        return temp;
    }

    // Function to print Leaf Nodes at
    // a given level
    function PrintLeafNodes(root, level)
    {
        if (root == null)
        {
            return;
        }

        if (level == 1)
        {
            if (root.left == null && root.right == null)
            {
                document.write(root.data + " ");
            }

        }
        else if (level > 1)
        {
            PrintLeafNodes(root.left, level - 1);
            PrintLeafNodes(root.right, level - 1);
        }
    }

    let root = newNode(1);
    root.left = newNode(2);
    root.right = newNode(3);
    root.left.left = newNode(6);
    root.right.right = newNode(4);
    root.left.left.left = newNode(8);
    root.left.left.right = newNode(7);

    let level = 4;

    PrintLeafNodes(root, level);

</script>
```

**Output:** 

```
8 7
```

**时间复杂度** :O(N)，其中 N 为二叉树中的节点数。
**辅助空间:** O(N)