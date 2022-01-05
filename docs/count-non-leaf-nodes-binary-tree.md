# 计数二叉树中的非叶节点

> 原文:[https://www . geesforgeks . org/count-非叶节点-二叉树/](https://www.geeksforgeeks.org/count-non-leaf-nodes-binary-tree/)

给定一棵二叉树，计算树中非叶节点的总数
**示例:**

```
Input :
```

![](img/b5491310da49860ab40de0269f426ec4.png)

```
Output :2
Explanation
In the above tree only two nodes 1 and 2 are non-leaf nodes
```

我们递归遍历给定的树。遍历时，我们计算左右子树中的非叶节点，并将结果加 1。

## C++

```
// CPP program to count total number of
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

/* Computes the number of non-leaf nodes in a tree. */
int countNonleaf(struct Node* root)
{
    // Base cases.
    if (root == NULL || (root->left == NULL &&
                         root->right == NULL))
        return 0;

    // If root is Not NULL and its one of its
    // child is also not NULL
    return 1 + countNonleaf(root->left) +
               countNonleaf(root->right);
}

/* Driver program to test size function*/
int main()
{
    struct Node* root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->left->right = newNode(5);
    cout << countNonleaf(root);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count total number of
// non-leaf nodes in a binary tree
class GfG {

/* A binary tree node has data, pointer to
left child and a pointer to right child */
static class Node {
    int data;
    Node left;
    Node right;
}

/* Helper function that allocates a new node with the
given data and NULL left and right pointers. */
static Node newNode(int data)
{
    Node node = new Node();
    node.data = data;
    node.left = null;
    node.right = null;
    return (node);
}

/* Computes the number of non-leaf nodes in a tree. */
static int countNonleaf(Node root)
{
    // Base cases.
    if (root == null || (root.left == null &&
                        root.right == null))
        return 0;

    // If root is Not NULL and its one of its
    // child is also not NULL
    return 1 + countNonleaf(root.left) +
                countNonleaf(root.right);
}

/* Driver program to test size function*/
public static void main(String[] args)
{
    Node root = newNode(1);
    root.left = newNode(2);
    root.right = newNode(3);
    root.left.left = newNode(4);
    root.left.right = newNode(5);
    System.out.println(countNonleaf(root));
}
}
```

## 蟒蛇 3

```
# Python3 program to count total number
# of non-leaf nodes in a binary tree

# class that allocates a new node with the
#given data and None left and right pointers.
class newNode:
    def __init__(self,data):
        self.data = data
        self.left = self.right = None

# Computes the number of non-leaf
# nodes in a tree.
def countNonleaf(root):

    # Base cases.
    if (root == None or (root.left == None and
                         root.right == None)):
        return 0

    # If root is Not None and its one of 
    # its child is also not None
    return (1 + countNonleaf(root.left) +
                countNonleaf(root.right))

# Driver Code
if __name__ == '__main__':

    root = newNode(1)
    root.left = newNode(2)
    root.right = newNode(3)
    root.left.left = newNode(4)
    root.left.right = newNode(5)
    print(countNonleaf(root))

# This code is contributed by PranchalK
```

## C#

```
// C# program to count total number of
// non-leaf nodes in a binary tree
using System;

class GfG
{

    /* A binary tree node has data, pointer to
    left child and a pointer to right child */
    class Node {
        public int data;
        public Node left;
        public Node right;
    }

    /* Helper function that allocates a new node with the
    given data and NULL left and right pointers. */
    static Node newNode(int data)
    {
        Node node = new Node();
        node.data = data;
        node.left = null;
        node.right = null;
        return (node);
    }

    /* Computes the number of non-leaf nodes in a tree. */
    static int countNonleaf(Node root)
    {
        // Base cases.
        if (root == null || (root.left == null &&
                            root.right == null))
            return 0;

        // If root is Not NULL and its one of its
        // child is also not NULL
        return 1 + countNonleaf(root.left) +
                    countNonleaf(root.right);
    }

    /* Driver code*/
    public static void Main(String[] args)
    {
        Node root = newNode(1);
        root.left = newNode(2);
        root.right = newNode(3);
        root.left.left = newNode(4);
        root.left.right = newNode(5);
        Console.WriteLine(countNonleaf(root));
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
    // Javascript program to count total number of
    // non-leaf nodes in a binary tree

    /* A binary tree node has data, pointer to
    left child and a pointer to right child */
    class Node
    {
        constructor(data) {
           this.left = null;
           this.right = null;
           this.data = data;
        }
    }

    /* Helper function that allocates a new node with the
    given data and NULL left and right pointers. */
    function newNode(data)
    {
        let node = new Node(data);
        return (node);
    }

    /* Computes the number of non-leaf nodes in a tree. */
    function countNonleaf(root)
    {
        // Base cases.
        if (root == null || (root.left == null &&
                            root.right == null))
            return 0;

        // If root is Not NULL and its one of its
        // child is also not NULL
        return 1 + countNonleaf(root.left) +
                    countNonleaf(root.right);
    }

    let root = newNode(1);
    root.left = newNode(2);
    root.right = newNode(3);
    root.left.left = newNode(4);
    root.left.right = newNode(5);
    document.write(countNonleaf(root));

 // This code is contributed by mukesh07.
</script>
```

**输出:**

```
2
```