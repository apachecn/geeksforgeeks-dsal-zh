# 从其前序遍历

构建全 k 元树

> 原文:[https://www . geesforgeks . org/construct-full-k-ary-tree-preorder-traversation/](https://www.geeksforgeeks.org/construct-full-k-ary-tree-preorder-traversal/)

给定一个包含全 k 元树的前序遍历的数组，构造全 k 元树并打印其后序遍历。全 k 元树是指每个节点都有 0 或 k 个子节点的树。

**示例:**

```
Input : preorder[] = {1, 2, 5, 6, 7, 
                     3, 8, 9, 10, 4}
        k = 3
Output : Postorder traversal of constructed 
         full k-ary tree is: 5 6 7 2 8 9 10 
         3 4 1 
         Tree formed is:         1
                             /   |   \
                           2     3    4
                          /|\   /|\
                         5 6 7 8 9 10

Input : preorder[] = {1, 2, 5, 6, 7, 3, 4}
        k = 3 
Output : Postorder traversal of constructed 
         full k-ary tree is: 5 6 7 2 4 3 1
         Tree formed is:        1
                             /  |  \
                           2    3   4
                          /|\   
                         5 6 7  
```

我们已经在下面的帖子中讨论了二叉树的这个问题。
[根据给定的前序遍历构建一个特殊的树](https://www.geeksforgeeks.org/construct-a-special-tree-from-given-preorder-traversal/)

在这篇文章中，讨论了 k 元树的解决方案。
在[前序遍历](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)中，首先处理根节点，然后处理左子树和右子树。正因为如此，为了构建一个完整的 k 元树，我们只需要继续创建节点，而不需要考虑之前构建的节点。我们可以用它递归地构建树。

以下是解决问题的步骤:
1。找到树的高度。
2。遍历预排序数组并递归添加每个节点

## C++

```
// C++ program to build full k-ary tree from
// its preorder traversal and to print the
// postorder traversal of the tree.
#include <bits/stdc++.h>
using namespace std;

// Structure of a node of an n-ary tree
struct Node {
    int key;
    vector<Node*> child;
};

// Utility function to create a new tree
// node with k children
Node* newNode(int value)
{
    Node* nNode = new Node;
    nNode->key = value;
    return nNode;
}

// Function to build full k-ary tree
Node* BuildKaryTree(int A[], int n, int k, int h, int& ind)
{
    // For null tree
    if (n <= 0)
        return NULL;

    Node* nNode = newNode(A[ind]);
    if (nNode == NULL) {
        cout << "Memory error" << endl;
        return NULL;
    }

    // For adding k children to a node
    for (int i = 0; i < k; i++) {

        // Check if ind is in range of array
        // Check if height of the tree is greater than 1
        if (ind < n - 1 && h > 1) {
            ind++;

            // Recursively add each child
            nNode->child.push_back(BuildKaryTree(A, n, k, h - 1, ind));
        } else {
            nNode->child.push_back(NULL);
        }
    }
    return nNode;
}

// Function to find the height of the tree
Node* BuildKaryTree(int* A, int n, int k, int ind)
{
    int height = (int)ceil(log((double)n * (k - 1) + 1)
                 / log((double)k));
    return BuildKaryTree(A, n, k, height, ind);
}

// Function to print postorder traversal of the tree
void postord(Node* root, int k)
{
    if (root == NULL)
        return;
    for (int i = 0; i < k; i++)
        postord(root->child[i], k);
    cout << root->key << " ";
}

// Driver program to implement full k-ary tree
int main()
{
    int ind = 0;
    int k = 3, n = 10;
    int preorder[] = { 1, 2, 5, 6, 7, 3, 8, 9, 10, 4 };
    Node* root = BuildKaryTree(preorder, n, k, ind);
    cout << "Postorder traversal of constructed"
             " full k-ary tree is: ";
    postord(root, k);
    cout << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to build full k-ary tree from
// its preorder traversal and to print the
// postorder traversal of the tree.
import java.util.*;

class GFG
{

// Structure of a node of an n-ary tree
static class Node
{
    int key;
    Vector<Node> child;
};

// Utility function to create a new tree
// node with k children
static Node newNode(int value)
{
    Node nNode = new Node();
    nNode.key = value;
    nNode.child= new Vector<Node>();
    return nNode;
}

static int ind;

// Function to build full k-ary tree
static Node BuildKaryTree(int A[], int n,
                          int k, int h)
{
    // For null tree
    if (n <= 0)
        return null;

    Node nNode = newNode(A[ind]);
    if (nNode == null)
    {
        System.out.println("Memory error" );
        return null;
    }

    // For adding k children to a node
    for (int i = 0; i < k; i++)
    {

        // Check if ind is in range of array
        // Check if height of the tree is greater than 1
        if (ind < n - 1 && h > 1)
        {
            ind++;

            // Recursively add each child
            nNode.child.add(BuildKaryTree(A, n, k, h - 1));
        }
        else
        {
            nNode.child.add(null);
        }
    }
    return nNode;
}

// Function to find the height of the tree
static Node BuildKaryTree_1(int[] A, int n, int k, int in)
{
    int height = (int)Math.ceil(Math.log((double)n * (k - 1) + 1) /
                                Math.log((double)k));
    ind = in;
    return BuildKaryTree(A, n, k, height);
}

// Function to print postorder traversal of the tree
static void postord(Node root, int k)
{
    if (root == null)
        return;
    for (int i = 0; i < k; i++)
        postord(root.child.get(i), k);
    System.out.print(root.key + " ");
}

// Driver Code
public static void main(String args[])
{
    int ind = 0;
    int k = 3, n = 10;
    int preorder[] = { 1, 2, 5, 6, 7, 3, 8, 9, 10, 4 };
    Node root = BuildKaryTree_1(preorder, n, k, ind);
    System.out.println("Postorder traversal of " +
                       "constructed full k-ary tree is: ");
    postord(root, k);
    System.out.println();
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 program to build full k-ary tree
# from its preorder traversal and to print the
# postorder traversal of the tree.
from math import ceil, log

# Utility function to create a new
# tree node with k children
class newNode:
    def __init__(self, value):
        self.key = value
        self.child = []

# Function to build full k-ary tree
def BuildkaryTree(A, n, k, h, ind):

    # For None tree
    if (n <= 0):
        return None

    nNode = newNode(A[ind[0]])
    if (nNode == None):
        print("Memory error")
        return None

    # For adding k children to a node
    for i in range(k):

        # Check if ind is in range of array
        # Check if height of the tree is
        # greater than 1
        if (ind[0] < n - 1 and h > 1):
            ind[0] += 1

            # Recursively add each child
            nNode.child.append(BuildkaryTree(A, n, k,
                                             h - 1, ind))
        else:
            nNode.child.append(None)
    return nNode

# Function to find the height of the tree
def BuildKaryTree(A, n, k, ind):
    height = int(ceil(log(float(n) * (k - 1) + 1) /
                                      log(float(k))))
    return BuildkaryTree(A, n, k, height, ind)

# Function to prpostorder traversal
# of the tree
def postord(root, k):
    if (root == None):
        return
    for i in range(k):
        postord(root.child[i], k)
    print(root.key, end = " ")

# Driver Code
if __name__ == '__main__':
    ind = [0]
    k = 3
    n = 10
    preorder = [ 1, 2, 5, 6, 7, 3, 8, 9, 10, 4]
    root = BuildKaryTree(preorder, n, k, ind)
    print("Postorder traversal of constructed",
                        "full k-ary tree is: ")
    postord(root, k)

# This code is contributed by pranchalK
```

## C#

```
// C# program to build full k-ary tree from
// its preorder traversal and to print the
// postorder traversal of the tree.
using System;
using System.Collections.Generic;

class GFG
{

// Structure of a node of an n-ary tree
class Node
{
    public int key;
    public List<Node> child;
};

// Utility function to create a new tree
// node with k children
static Node newNode(int value)
{
    Node nNode = new Node();
    nNode.key = value;
    nNode.child= new List<Node>();
    return nNode;
}

static int ind;

// Function to build full k-ary tree
static Node BuildKaryTree(int []A, int n,
                          int k, int h)
{
    // For null tree
    if (n <= 0)
        return null;

    Node nNode = newNode(A[ind]);
    if (nNode == null)
    {
        Console.WriteLine("Memory error" );
        return null;
    }

    // For adding k children to a node
    for (int i = 0; i < k; i++)
    {

        // Check if ind is in range of array
        // Check if height of the tree is greater than 1
        if (ind < n - 1 && h > 1)
        {
            ind++;

            // Recursively add each child
            nNode.child.Add(BuildKaryTree(A, n, k, h - 1));
        }
        else
        {
            nNode.child.Add(null);
        }
    }
    return nNode;
}

// Function to find the height of the tree
static Node BuildKaryTree_1(int[] A, int n, int k, int iN)
{
    int height = (int)Math.Ceiling(Math.Log((double)n * (k - 1) + 1) /
                                   Math.Log((double)k));
    ind = iN;
    return BuildKaryTree(A, n, k, height);
}

// Function to print postorder traversal of the tree
static void postord(Node root, int k)
{
    if (root == null)
        return;
    for (int i = 0; i < k; i++)
        postord(root.child[i], k);
    Console.Write(root.key + " ");
}

// Driver Code
public static void Main(String []args)
{
    int ind = 0;
    int k = 3, n = 10;
    int []preorder = { 1, 2, 5, 6, 7, 3, 8, 9, 10, 4 };
    Node root = BuildKaryTree_1(preorder, n, k, ind);
    Console.WriteLine("Postorder traversal of " +
                      "constructed full k-ary tree is: ");
    postord(root, k);
    Console.WriteLine();
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
    // Javascript program to build full k-ary tree from
    // its preorder traversal and to print the
    // postorder traversal of the tree.

    class Node
    {
        constructor(key) {
           this.child = [];
           this.key = key;
        }
    }

    // Utility function to create a new tree
    // node with k children
    function newNode(value)
    {
        let nNode = new Node(value);
        return nNode;
    }

    let ind;

    // Function to build full k-ary tree
    function BuildKaryTree(A, n, k, h)
    {
        // For null tree
        if (n <= 0)
            return null;

        let nNode = newNode(A[ind]);
        if (nNode == null)
        {
            document.write("Memory error" );
            return null;
        }

        // For adding k children to a node
        for (let i = 0; i < k; i++)
        {

            // Check if ind is in range of array
            // Check if height of the tree is greater than 1
            if (ind < n - 1 && h > 1)
            {
                ind++;

                // Recursively add each child
                nNode.child.push(BuildKaryTree(A, n, k, h - 1));
            }
            else
            {
                nNode.child.push(null);
            }
        }
        return nNode;
    }

    // Function to find the height of the tree
    function BuildKaryTree_1(A, n, k, In)
    {
        let height = Math.ceil(Math.log(n * (k - 1) + 1) / Math.log(k));
        ind = In;
        return BuildKaryTree(A, n, k, height);
    }

    // Function to print postorder traversal of the tree
    function postord(root, k)
    {
        if (root == null)
            return;
        for (let i = 0; i < k; i++)
            postord(root.child[i], k);
        document.write(root.key + " ");
    }

    ind = 0;
    let k = 3, n = 10;
    let preorder = [ 1, 2, 5, 6, 7, 3, 8, 9, 10, 4 ];
    let root = BuildKaryTree_1(preorder, n, k, ind);
    document.write("Postorder traversal of " +
                       "constructed full k-ary" + "</br>" + "tree is: ");
    postord(root, k);
    document.write("</br>");

</script>
```

**输出:**

```
Postorder traversal of constructed full k-ary
tree is: 5 6 7 2 8 9 10 3 4 1 
```

本文由**普拉克里提·古普塔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。