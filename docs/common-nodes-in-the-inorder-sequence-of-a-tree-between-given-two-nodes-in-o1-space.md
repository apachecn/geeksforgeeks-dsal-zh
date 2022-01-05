# O(1)空间中给定两个节点之间的树的有序序列中的公共节点

> 原文:[https://www . geeksforgeeks . org/在给定的两个 o1 空间节点之间的有序公共节点树序列/](https://www.geeksforgeeks.org/common-nodes-in-the-inorder-sequence-of-a-tree-between-given-two-nodes-in-o1-space/)

给定一个由不同值和两个数字组成的**二叉树****K1**和 **K2** ，任务是按照树的顺序找到它们之间的所有节点。
**举例:**

> **输入:**
> 1
> /\
> 12 11
> /\
> 3 4 13
> \/
> 15 9
> k1 = 12
> k2 = 15
> **输出:**
> 1 4
> **解释:**
> 顺序为 3 12 1 4 15 11 9 13
> 12 和 12 之间的公共节点
> **输入:**
> 5
> /\
> 21 77
> /\ \
> 61 16 36
> \/
> 10 3
> /
> 23
> k1 = 23
> k2 = 3
> **输出:**
> 10 5 77
> **解释:**
> 顺序为

**方法:**
为了解决这个问题，我们使用二叉树的 [Morris Inorder 遍历](https://www.geeksforgeeks.org/inorder-tree-traversal-without-recursion-and-without-stack/)来避免使用任何额外的空间。当找到 K1 或 K2 时，我们保留一个标志来设置。找到后，按顺序打印出现的每个节点，直到找到另一个节点。
以下是上述方法的实施:

## C++

```
// C++ Program to find
// the common nodes
// between given two nodes
// in the inorder sequence
// of the binary tree

#include <bits/stdc++.h>
using namespace std;

// Definition of Binary
// Tree Structure
struct tNode {
    int data;
    struct tNode* left;
    struct tNode* right;
};

// Helper function to allocate
// memory to create new nodes
struct tNode* newtNode(int data)
{
    struct tNode* node = new tNode;
    node->data = data;
    node->left = NULL;
    node->right = NULL;

    return (node);
}

// Flag to set if
// either of K1 or
// K2 is found
int flag = 0;

// Function to traverse the
// binary tree without recursion
// and without stack using
// Morris Traversal
void findCommonNodes(struct tNode* root,
                     int K1, int K2)
{
    struct tNode *current, *pre;

    if (root == NULL)
        return;

    current = root;
    while (current != NULL) {

        if (current->left == NULL) {

            if (current->data == K1 || current->data == K2) {
                if (flag) {
                    return;
                }
                else {
                    flag = 1;
                }
            }
            else if (flag) {
                cout << current->data << " ";
            }
            current = current->right;
        }
        else {

            // Find the inorder predecessor
            // of current
            pre = current->left;
            while (pre->right != NULL
                   && pre->right != current)
                pre = pre->right;

            // Make current as the right
            // child of its inorder
            // predecessor
            if (pre->right == NULL) {
                pre->right = current;
                current = current->left;
            }

            // Revert the changes made
            // to restore the original tree
            // i.e., fix the right child
            // of predecessor
            else {
                pre->right = NULL;
                if (current->data == K1 || current->data == K2) {
                    if (flag) {
                        return;
                    }
                    else {
                        flag = 1;
                    }
                }
                else if (flag) {
                    cout << current->data << " ";
                }
                current = current->right;
            } // End of if condition pre->right == NULL
        } // End of if condition current->left == NULL
    } // End of while
}

// Driver code
int main()
{
    struct tNode* root = newtNode(1);
    root->left = newtNode(12);
    root->right = newtNode(11);
    root->left->left = newtNode(3);
    root->right->left = newtNode(4);
    root->right->right = newtNode(13);
    root->right->left->right = newtNode(15);
    root->right->right->left = newtNode(9);

    int K1 = 12, K2 = 15;

    findCommonNodes(root, K1, K2);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the common nodes
// between given two nodes in the inorder
// sequence of the binary tree
import java.util.*;

class GFG{

// Definition of Binary Tree
static class tNode
{
    int data;
    tNode left;
    tNode right;
};

// Helper function to allocate
// memory to create new nodes
static tNode newtNode(int data)
{
    tNode node = new tNode();
    node.data = data;
    node.left = null;
    node.right = null;

    return (node);
}

// Flag to set if either
// of K1 or K2 is found
static int flag = 0;

// Function to traverse the binary
// tree without recursion and
// without stack using
// Morris Traversal
static void findCommonNodes(tNode root,
                            int K1, int K2)
{
    tNode current, pre;

    if (root == null)
        return;
    current = root;

    while (current != null)
    {
        if (current.left == null)
        {
            if (current.data == K1 ||
                current.data == K2)
            {
                if (flag == 1)
                {
                    return;
                }
                else
                {
                    flag = 1;
                }
            }
            else if (flag == 1)
            {
                System.out.print(current.data + " ");
            }
            current = current.right;
        }
        else
        {

            // Find the inorder predecessor
            // of current
            pre = current.left;
            while (pre.right != null &&
                   pre.right != current)
            {
                pre = pre.right;
            }

            // Make current as the right
            // child of its inorder
            // predecessor
            if (pre.right == null)
            {
                pre.right = current;
                current = current.left;
            }

            // Revert the changes made
            // to restore the original tree
            // i.e., fix the right child
            // of predecessor
            else
            {
                pre.right = null;
                if (current.data == K1 ||
                    current.data == K2)
                {
                    if (flag == 1)
                    {
                        return;
                    }
                    else
                    {
                        flag = 1;
                    }
                }
                else if (flag == 1)
                {
                    System.out.print(current.data + " ");
                }
                current = current.right;
            } // End of if condition pre.right == null
        } // End of if condition current.left == null
    } // End of while
}

// Driver code
public static void main(String[] args)
{
    tNode root = newtNode(1);
    root.left = newtNode(12);
    root.right = newtNode(11);
    root.left.left = newtNode(3);
    root.right.left = newtNode(4);
    root.right.right = newtNode(13);
    root.right.left.right = newtNode(15);
    root.right.right.left = newtNode(9);

    int K1 = 12, K2 = 15;

    findCommonNodes(root, K1, K2);
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program for the
# above approach
from collections import deque

# A Tree node
class Node:

    def __init__(self, x):

        self.data = x
        self.left = None
        self.right = None

# Flag to set if
# either of K1 or
# K2 is found
flag = 0

# Function to traverse the
# binary tree without recursion
# and without stack using
# Morris Traversal
def findCommonNodes(root,
                    K1, K2):

    global flag
    current, pre = None, None

    if (root == None):
        return

    current = root
    while (current != None):
        if (current.left == None):
            if (current.data == K1 or
                current.data == K2):
                if (flag):
                    return

                else:
                    flag = 1

            elif (flag):
                print(current.data,
                      end = " ")
            else:
                None

            current = current.right

        else:

            # Find the inorder
            # predecessor of current
            pre = current.left
            while (pre.right != None and
                   pre.right != current):
                pre = pre.right

            # Make current as the right
            # child of its inorder
            # predecessor
            if (pre.right == None):
                pre.right = current
                current = current.left

            # Revert the changes made
            # to restore the original tree
            # i.e., fix the right child
            # of predecessor
            else:
                pre.right = None
                if (current.data == K1 or
                    current.data == K2):
                    if (flag):
                        return
                    else:
                        flag = 1

                elif (flag):
                    print(current.data,
                          end = " ")

                current = current.right
             # End of if condition
            # pre.right == None
         # End of if condition
         #current.left == None
     # End of while

# Driver code
if __name__ == '__main__':

    root = Node(1)
    root.left = Node(12)
    root.right = Node(11)
    root.left.left = Node(3)
    root.right.left = Node(4)
    root.right.right = Node(13)
    root.right.left.right = Node(15)
    root.right.right.left = Node(9)

    K1 = 12
    K2 = 15

    findCommonNodes(root, K1, K2)

# This code is contributed by Mohit Kumar 29
```

## C#

```
// C# program to find the common nodes
// between given two nodes in the inorder
// sequence of the binary tree
using System;

class GFG{

// Definition of Binary Tree
class tNode
{
    public int data;
    public tNode left;
    public tNode right;
};

// Helper function to allocate
// memory to create new nodes
static tNode newtNode(int data)
{
    tNode node = new tNode();
    node.data = data;
    node.left = null;
    node.right = null;

    return (node);
}

// Flag to set if either
// of K1 or K2 is found
static int flag = 0;

// Function to traverse the binary
// tree without recursion and
// without stack using
// Morris Traversal
static void findCommonNodes(tNode root,
                            int K1, int K2)
{
    tNode current, pre;

    if (root == null)
        return;
    current = root;

    while (current != null)
    {
        if (current.left == null)
        {
            if (current.data == K1 ||
                current.data == K2)
            {
                if (flag == 1)
                {
                    return;
                }
                else
                {
                    flag = 1;
                }
            }
            else if (flag == 1)
            {
                Console.Write(current.data + " ");
            }
            current = current.right;
        }
        else
        {

            // Find the inorder predecessor
            // of current
            pre = current.left;
            while (pre.right != null &&
                   pre.right != current)
            {
                pre = pre.right;
            }

            // Make current as the right
            // child of its inorder
            // predecessor
            if (pre.right == null)
            {
                pre.right = current;
                current = current.left;
            }

            // Revert the changes made
            // to restore the original tree
            // i.e., fix the right child
            // of predecessor
            else
            {
                pre.right = null;
                if (current.data == K1 ||
                    current.data == K2)
                {
                    if (flag == 1)
                    {
                        return;
                    }
                    else
                    {
                        flag = 1;
                    }
                }
                else if (flag == 1)
                {
                    Console.Write(current.data + " ");
                }
                current = current.right;
            } // End of if condition pre.right == null
        } // End of if condition current.left == null
    } // End of while
}

// Driver code
public static void Main(String[] args)
{
    tNode root = newtNode(1);
    root.left = newtNode(12);
    root.right = newtNode(11);
    root.left.left = newtNode(3);
    root.right.left = newtNode(4);
    root.right.right = newtNode(13);
    root.right.left.right = newtNode(15);
    root.right.right.left = newtNode(9);

    int K1 = 12, K2 = 15;

    findCommonNodes(root, K1, K2);
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>
// Javascript program to find the common nodes
// between given two nodes in the inorder
// sequence of the binary tree

// Definition of Binary Tree
class Node
{

    // Helper function to allocate
// memory to create new nodes
    constructor(data)
    {
        this.data = data;
        this.left = this.right=null;
    }

}

// Flag to set if either
// of K1 or K2 is found
let flag = 0;

// Function to traverse the binary
// tree without recursion and
// without stack using
// Morris Traversal
function findCommonNodes(root, K1, K2)
{
    let current, pre;

    if (root == null)
        return;
    current = root;

    while (current != null)
    {
        if (current.left == null)
        {
            if (current.data == K1 ||
                current.data == K2)
            {
                if (flag == 1)
                {
                    return;
                }
                else
                {
                    flag = 1;
                }
            }
            else if (flag == 1)
            {
                document.write(current.data + " ");
            }
            current = current.right;
        }
        else
        {

            // Find the inorder predecessor
            // of current
            pre = current.left;
            while (pre.right != null &&
                   pre.right != current)
            {
                pre = pre.right;
            }

            // Make current as the right
            // child of its inorder
            // predecessor
            if (pre.right == null)
            {
                pre.right = current;
                current = current.left;
            }

            // Revert the changes made
            // to restore the original tree
            // i.e., fix the right child
            // of predecessor
            else
            {
                pre.right = null;
                if (current.data == K1 ||
                    current.data == K2)
                {
                    if (flag == 1)
                    {
                        return;
                    }
                    else
                    {
                        flag = 1;
                    }
                }
                else if (flag == 1)
                {
                    document.write(current.data + " ");
                }
                current = current.right;
            } // End of if condition pre.right == null
        } // End of if condition current.left == null
    } // End of while
}

// Driver code
let root = new Node(1);
root.left = new Node(12);
root.right = new Node(11);
root.left.left = new Node(3);
root.right.left = new Node(4);
root.right.right = new Node(13);
root.right.left.right = new Node(15);
root.right.right.left = new Node(9);

let K1 = 12, K2 = 15;
findCommonNodes(root, K1, K2);

// This code is contributed by patel2127
</script>
```

**Output:** 

```
1 4
```

**时间复杂度:***O(N)*
T5】辅助空间: *O(1)*