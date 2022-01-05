# 打印给定范围内的 BST 键| O(1)空格

> 原文:[https://www . geesforgeks . org/print-BST-keys-in-给定范围-o1-space/](https://www.geeksforgeeks.org/print-bst-keys-in-given-range-o1-space/)

给定两个值 n1 和 n2(其中 n1 < n2) and a root pointer to a Binary Search Tree. Print all the keys of tree in range n1 to n2\. i.e. print all nodes n such that n1<=n<=n2 and n is a key of given BST. Print all the keys in increasing order.
**先决条件:** [莫里斯遍历](https://www.geeksforgeeks.org/inorder-tree-traversal-without-recursion-and-without-stack/) | [线程二叉树](https://www.geeksforgeeks.org/threaded-binary-tree/)
有序遍历使用递归或消耗 0(n)空间的堆栈/队列。但是有一种有效的方法可以使用基于线程二叉树的莫里斯遍历来进行有序树遍历。Morris 遍历不使用递归或堆栈/队列，只是在浪费的空指针中存储一些重要信息。Morris 遍历消耗恒定的额外内存 O(1)，因为它不使用递归或堆栈/队列。因此，我们将使用 Morris 遍历来执行本教程中介绍的算法中的有序遍历，以打印给定范围内的 BST 的键，这在内存方面是高效的。
线程二叉树的概念很简单，因为它们在浪费的空指针中存储了一些有用的信息。在有 n 个节点的普通二叉树中，n+1 个空指针会浪费内存。
**方法:**莫里斯遍历是一种非常好的内存高效的技术，可以在基于线程二叉树的常量内存 O(1)中不使用堆栈或递归来进行树遍历。Morris 遍历可用于解决使用有序树遍历的问题，尤其是在**顺序统计**eg-[BST](https://www.geeksforgeeks.org/kth-largest-element-bst-using-constant-extra-space/)中第 Kth 个最大元素，[BST](https://www.geeksforgeeks.org/kth-smallest-element-in-bst-using-o1-extra-space/)中第 Kth 个最小元素等。因此，这就是 Morris 遍历作为一种更有效的方法在常量 O(1)空间中进行有序遍历而不使用任何堆栈或递归的地方。
**算法**

```
1) Initialize Current as root.

2) While current is not NULL :

  2.1) If current has no left child

   a) Check if current lies between n1 and n2.
      1)If so, then visit the current node.

   b)Otherwise, Move to the right child of current.

  3) Else, here we have 2 cases:
   a) Find the inorder predecessor of current node. 
      Inorder predecessor is the right most node 
      in the left subtree or left child itself.

   b) If the right child of the inorder predecessor is NULL:
      1) Set current as the right child of its inorder predecessor.
      2) Move current node to its left child.

   c) Else, if the threaded link between the current node 
      and it's inorder predecessor already exists :
      1) Set right pointer of the inorder predecessor as NULL.
      2) Again check if current node lies between n1 and n2.
        a)If so, then visit the current node.

      3)Now move current to it's right child.
```

**以下是上述方法的实施。**

## C++

```
// CPP code to print BST keys in given Range in
// constant space using Morris traversal.
#include <bits/stdc++.h>

using namespace std;

struct node {

    int data;
    struct node *left, *right;
};

// Function to print the keys in range
void RangeTraversal(node* root,
                    int n1, int n2)
{
    if (!root)
        return;

    node* curr = root;

    while (curr) {

        if (curr->left == NULL)
        {
            // check if current node
            // lies between n1 and n2
            if (curr->data <= n2 &&
                curr->data >= n1)
            {
                cout << curr->data << " ";
            }

            curr = curr->right;
        }

        else {
            node* pre = curr->left;
            // finding the inorder predecessor-
            // inorder predecessor is the right
            // most in left subtree or the left
            // child, i.e in BST it is the
            // maximum(right most) in left subtree.
            while (pre->right != NULL &&
                   pre->right != curr)
                        pre = pre->right;

            if (pre->right == NULL)
            {
                pre->right = curr;
                curr = curr->left;
            }

            else {
                pre->right = NULL;

                // check if current node lies
                // between n1 and n2
                if (curr->data <= n2 &&
                    curr->data >= n1)
                {
                    cout << curr->data << " ";
                }

                curr = curr->right;
            }
        }
    }
}

// Helper function to create a new node
node* newNode(int data)
{
    node* temp = new node;
    temp->data = data;
    temp->right = temp->left = NULL;

    return temp;
}

// Driver Code
int main()
{

    /* Constructed binary tree is
          4
        /   \
       2     7
     /  \   /  \
    1    3  6    10
*/

    node* root = newNode(4);
    root->left = newNode(2);
    root->right = newNode(7);
    root->left->left = newNode(1);
    root->left->right = newNode(3);
    root->right->left = newNode(6);
    root->right->right = newNode(10);

    RangeTraversal(root, 4, 12);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to print BST keys in given Range in
// constant space using Morris traversal.
class GfG {

static class node {

    int data;
    node left, right;
}

// Function to print the keys in range
static void RangeTraversal(node root, int n1, int n2)
{
    if (root == null)
        return;

    node curr = root;

    while (curr != null) {

        if (curr.left == null)
        {
            // check if current node
            // lies between n1 and n2
            if (curr.data <= n2 && curr.data >= n1)
            {
                System.out.print(curr.data + " ");
            }

            curr = curr.right;
        }

        else {
            node pre = curr.left;
            // finding the inorder predecessor-
            // inorder predecessor is the right
            // most in left subtree or the left
            // child, i.e in BST it is the
            // maximum(right most) in left subtree.
            while (pre.right != null && pre.right != curr)
                pre = pre.right;

            if (pre.right == null)
            {
                pre.right = curr;
                curr = curr.left;
            }

            else {
                pre.right = null;

                // check if current node lies
                // between n1 and n2
                if (curr.data <= n2 && curr.data >= n1)
                {
                    System.out.print(curr.data + " ");
                }

                curr = curr.right;
            }
        }
    }
}

// Helper function to create a new node
static node newNode(int data)
{
    node temp = new node();
    temp.data = data;
    temp.right = null;
    temp.left = null;

    return temp;
}

// Driver Code
public static void main(String[] args)
{

    /* Constructed binary tree is
        4
        / \
    2     7
    / \ / \
    1 3 6 10
*/

    node root = newNode(4);
    root.left = newNode(2);
    root.right = newNode(7);
    root.left.left = newNode(1);
    root.left.right = newNode(3);
    root.right.left = newNode(6);
    root.right.right = newNode(10);

    RangeTraversal(root, 4, 12);

}
}
```

## 蟒蛇 3

```
# Python3 code to print BST keys in given Range
# in constant space using Morris traversal.

# Helper function to create a new node
class newNode:

    # Constructor to create a new node
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# Function to print the keys in range
def RangeTraversal(root, n1, n2):
    if root == None:
        return

    curr = root
    while curr:
        if curr.left == None:

            # check if current node lies
            # between n1 and n2
            if curr.data <= n2 and curr.data >= n1:
                print(curr.data, end = " ")
            curr = curr.right
        else:
            pre = curr.left

            # finding the inorder predecessor-
            # inorder predecessor is the right
            # most in left subtree or the left
            # child, i.e in BST it is the
            # maximum(right most) in left subtree.
            while (pre.right != None and
                   pre.right != curr):
                pre = pre.right

            if pre.right == None:
                pre.right = curr;
                curr = curr.left
            else:
                pre.right = None

                # check if current node lies
                # between n1 and n2
                if curr.data <= n2 and curr.data >= n1:
                    print(curr.data, end = " ")
                curr = curr.right

# Driver Code
if __name__ == '__main__':

    # Constructed binary tree is
    #        4
    #      / \
    #     2      7
    #    / \ / \
    #   1  3 6 10
    root = newNode(4)
    root.left = newNode(2)
    root.right = newNode(7)
    root.left.left = newNode(1)
    root.left.right = newNode(3)
    root.right.left = newNode(6)
    root.right.right = newNode(10)

    RangeTraversal(root, 4, 12)    

# This code is contributed by PranchalK
```

## C#

```
// C# code to print BST keys in given Range in
// constant space using Morris traversal.
using System;

public class GfG
{

public class node
{

    public int data;
    public node left, right;
}

// Function to print the keys in range
static void RangeTraversal(node root, int n1, int n2)
{
    if (root == null)
        return;

    node curr = root;

    while (curr != null)
    {

        if (curr.left == null)
        {
            // check if current node
            // lies between n1 and n2
            if (curr.data <= n2 && curr.data >= n1)
            {
                Console.Write(curr.data + " ");
            }

            curr = curr.right;
        }

        else
        {
            node pre = curr.left;

            // finding the inorder predecessor-
            // inorder predecessor is the right
            // most in left subtree or the left
            // child, i.e in BST it is the
            // maximum(right most) in left subtree.
            while (pre.right != null && pre.right != curr)
                pre = pre.right;

            if (pre.right == null)
            {
                pre.right = curr;
                curr = curr.left;
            }

            else
            {
                pre.right = null;

                // check if current node lies
                // between n1 and n2
                if (curr.data <= n2 && curr.data >= n1)
                {
                    Console.Write(curr.data + " ");
                }

                curr = curr.right;
            }
        }
    }
}

// Helper function to create a new node
static node newNode(int data)
{
    node temp = new node();
    temp.data = data;
    temp.right = null;
    temp.left = null;

    return temp;
}

// Driver Code
public static void Main(String[] args)
{

    /* Constructed binary tree is
        4
        / \
    2 7
    / \ / \
    1 3 6 10
*/

    node root = newNode(4);
    root.left = newNode(2);
    root.right = newNode(7);
    root.left.left = newNode(1);
    root.left.right = newNode(3);
    root.right.left = newNode(6);
    root.right.right = newNode(10);

    RangeTraversal(root, 4, 12);
}
}

// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript code to print
// BST keys in given Range in
// constant space using Morris traversal.
class node {
    constructor() {
        this.data = 0;
        this.left = null;
        this.right = null;
    }
}

// Function to print the keys in range
function RangeTraversal( root , n1 , n2)
{
    if (root == null)
        return;

    var curr = root;

    while (curr != null) {

        if (curr.left == null)
        {
            // check if current node
            // lies between n1 and n2
            if (curr.data <= n2 && curr.data >= n1)
            {
                document.write(curr.data + " ");
            }

            curr = curr.right;
        }

        else {
            var pre = curr.left;
            // finding the inorder predecessor-
            // inorder predecessor is the right
            // most in left subtree or the left
            // child, i.e in BST it is the
            // maximum(right most) in left subtree.
            while (pre.right != null && pre.right != curr)
                pre = pre.right;

            if (pre.right == null)
            {
                pre.right = curr;
                curr = curr.left;
            }

            else {
                pre.right = null;

                // check if current node lies
                // between n1 and n2
                if (curr.data <= n2 && curr.data >= n1)
                {
                    document.write(curr.data + " ");
                }

                curr = curr.right;
            }
        }
    }
}

// Helper function to create a new node
 function newNode(data)
{
     temp = new node();
    temp.data = data;
    temp.right = null;
    temp.left = null;

    return temp;
}

// Driver Code

    /* Constructed binary tree is
        4
        / \
    2     7
    / \ / \
    1 3 6 10
*/

     root = newNode(4);
    root.left = newNode(2);
    root.right = newNode(7);
    root.left.left = newNode(1);
    root.left.right = newNode(3);
    root.right.left = newNode(6);
    root.right.right = newNode(10);

    RangeTraversal(root, 4, 12);

// This code is contributed by todaysgaurav

</script>
```

**Output:** 

```
4 6 7 10
```

**时间复杂度:**O(n)
T3】辅助空间: O(1)