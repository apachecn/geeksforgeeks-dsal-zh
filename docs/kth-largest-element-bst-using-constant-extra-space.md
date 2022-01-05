# 使用恒定额外空间的 BST 中第 K 大元素

> 原文:[https://www . geesforgeks . org/kth-最大元素-BST-使用-常量-额外空间/](https://www.geeksforgeeks.org/kth-largest-element-bst-using-constant-extra-space/)

给定一个二叉查找树，任务是在二叉查找树找到最大的元素。
**例:**

```
Input :  k = 3
         Root of following BST
            10
          /    \
         4      20
        /      /   \
       2     15     40
Output : 15
```

这个想法是使用[反向 Morris 遍历](https://www.geeksforgeeks.org/reverse-morris-traversal-using-threaded-binary-tree/)，它基于[线程二叉树](https://www.geeksforgeeks.org/threaded-binary-tree/)。线程二叉树使用空指针来存储后继和前置信息，这有助于我们利用这些空指针浪费的内存。
莫里斯遍历的特别之处在于，我们可以在不使用堆栈或递归的情况下进行 Inorder 遍历，这为我们节省了堆栈或递归调用堆栈所消耗的内存。
*反向莫里斯遍历只是莫里斯遍历的反向，莫里斯遍历主要用于进行反向无序遍历，因为它不使用任何堆栈或递归，所以会消耗常量 O(1)的额外内存。*
要在二叉查找树中找到第 k 个最大的元素，最简单的逻辑是进行反向有序遍历，在进行反向有序遍历时，只需记录访问的节点数。当计数等于 k 时，我们停止遍历并打印数据。它利用了这样一个事实，即反向有序遍历会给我们一个按降序排序的列表。

#### 算法

```
1) Initialize Current as root.
2) Initialize a count variable to 0.
3) While current is not NULL :
   3.1) If current has no right child
   a) Increment count and check if count is equal to K.
      1) If count is equal to K, simply return current 
         Node as it is the Kth largest Node.
   b) Otherwise, Move to the left child of current.

   3.2) Else, here we have 2 cases:
   a) Find the inorder successor of current Node. 
      Inorder successor is the left most Node 
      in the right subtree or right child itself.
   b) If the left child of the inorder successor is NULL:
      1) Set current as the left child of its inorder 
         successor.
      2) Move current Node to its right.
   c) Else, if the threaded link between the current Node 
      and it's inorder successor already exists :
      1) Set left pointer of the inorder successor as NULL.
      2) Increment count and check if count is equal to K.
           a) If count is equal to K, simply return current
              Node as it is the Kth largest Node.

      3) Otherwise, Move current to it's left child.
```

## C++

```
// CPP code for finding K-th largest Node using O(1)
// extra memory and reverse Morris traversal.
#include <bits/stdc++.h>
using namespace std;

struct Node {
    int data;
    struct Node *left, *right;
};

// helper function to create a new Node
Node* newNode(int data)
{
    Node* temp = new Node;
    temp->data = data;
    temp->right = temp->left = NULL;
    return temp;
}

Node* KthLargestUsingMorrisTraversal(Node* root, int k)
{
    Node* curr = root;
    Node* Klargest = NULL;

    // count variable to keep count of visited Nodes
    int count = 0;

    while (curr != NULL) {
        // if right child is NULL
        if (curr->right == NULL) {

            // first increment count and check if count = k
            if (++count == k)
                Klargest = curr;

            // otherwise move to the left child
            curr = curr->left;
        }

        else {

            // find inorder successor of current Node
            Node* succ = curr->right;

            while (succ->left != NULL && succ->left != curr)
                succ = succ->left;

            if (succ->left == NULL) {

                // set left child of successor to the
                // current Node
                succ->left = curr;

                // move current to its right
                curr = curr->right;
            }

            // restoring the tree back to original binary
            //  search tree removing threaded links
            else {

                succ->left = NULL;

                if (++count == k)
                    Klargest = curr;

                // move current to its left child
                curr = curr->left;
            }
        }
    }

    return Klargest;
}

int main()
{
    // Your C++ Code
    /* Constructed binary tree is
          4
        /   \
       2     7
     /  \   /  \
    1    3  6    10 */

    Node* root = newNode(4);
    root->left = newNode(2);
    root->right = newNode(7);
    root->left->left = newNode(1);
    root->left->right = newNode(3);
    root->right->left = newNode(6);
    root->right->right = newNode(10);

    cout << "Finding K-th largest Node in BST : "
         << KthLargestUsingMorrisTraversal(root, 2)->data;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program for finding K-th largest Node using O(1)
// extra memory and reverse Morris traversal.
class GfG
{

static class Node
{
    int data;
    Node left, right;
}

// helper function to create a new Node
static Node newNode(int data)
{
    Node temp = new Node();
    temp.data = data;
    temp.right = null;
    temp.left = null;
    return temp;
}

static Node KthLargestUsingMorrisTraversal(Node root, int k)
{
    Node curr = root;
    Node Klargest = null;

    // count variable to keep count of visited Nodes
    int count = 0;

    while (curr != null)
    {
        // if right child is NULL
        if (curr.right == null)
        {

            // first increment count and check if count = k
            if (++count == k)
                Klargest = curr;

            // otherwise move to the left child
            curr = curr.left;
        }

        else
        {

            // find inorder successor of current Node
            Node succ = curr.right;

            while (succ.left != null && succ.left != curr)
                succ = succ.left;

            if (succ.left == null)
            {

                // set left child of successor to the
                // current Node
                succ.left = curr;

                // move current to its right
                curr = curr.right;
            }

            // restoring the tree back to original binary
            // search tree removing threaded links
            else
            {

                succ.left = null;

                if (++count == k)
                    Klargest = curr;

                // move current to its left child
                curr = curr.left;
            }
        }
    }
    return Klargest;
}

// Driver code
public static void main(String[] args)
{
    // Your Java Code
    /* Constructed binary tree is
        4
        / \
    2 7
    / \ / \
    1 3 6 10 */

    Node root = newNode(4);
    root.left = newNode(2);
    root.right = newNode(7);
    root.left.left = newNode(1);
    root.left.right = newNode(3);
    root.right.left = newNode(6);
    root.right.right = newNode(10);

    System.out.println("Finding K-th largest Node in BST : " +
                    KthLargestUsingMorrisTraversal(root, 2).data);
}
}
```

## 蟒蛇 3

```
# Python3 code for finding K-th largest
# Node using O(1) extra memory and
# reverse Morris traversal.

# helper function to create a new Node
class newNode:
    def __init__(self, data):
        self.data = data
        self.right = self.left = None

def KthLargestUsingMorrisTraversal(root, k):
    curr = root
    Klargest = None

    # count variable to keep count
    # of visited Nodes
    count = 0

    while (curr != None):

        # if right child is None
        if (curr.right == None):

            # first increment count and
            # check if count = k
            count += 1
            if (count == k):
                Klargest = curr

            # otherwise move to the left child
            curr = curr.left

        else:

            # find inorder successor of
            # current Node
            succ = curr.right

            while (succ.left != None and
                   succ.left != curr):
                succ = succ.left

            if (succ.left == None):

                # set left child of successor
                # to the current Node
                succ.left = curr

                # move current to its right
                curr = curr.right

            # restoring the tree back to 
            # original binary search tree
            # removing threaded links
            else:

                succ.left = None
                count += 1
                if (count == k):
                    Klargest = curr

                # move current to its left child
                curr = curr.left

    return Klargest

# Driver Code
if __name__ == '__main__':

    # Constructed binary tree is
    #     4
    #     / \
    # 2     7
    # / \ / \
    # 1 3 6 10
    root = newNode(4)
    root.left = newNode(2)
    root.right = newNode(7)
    root.left.left = newNode(1)
    root.left.right = newNode(3)
    root.right.left = newNode(6)
    root.right.right = newNode(10)

    print("Finding K-th largest Node in BST : ",
           KthLargestUsingMorrisTraversal(root, 2).data)

# This code is contributed by PranchalK
```

## C#

```
// C# Program for finding K-th largest Node using O(1)
// extra memory and reverse Morris traversal.
using System;
using System.Collections.Generic;

class GfG
{

public class Node
{
    public int data;
    public Node left, right;
}

// helper function to create a new Node
static Node newNode(int data)
{
    Node temp = new Node();
    temp.data = data;
    temp.right = null;
    temp.left = null;
    return temp;
}

static Node KthLargestUsingMorrisTraversal(Node root, int k)
{
    Node curr = root;
    Node Klargest = null;

    // count variable to keep count of visited Nodes
    int count = 0;

    while (curr != null)
    {
        // if right child is NULL
        if (curr.right == null)
        {

            // first increment count and check if count = k
            if (++count == k)
                Klargest = curr;

            // otherwise move to the left child
            curr = curr.left;
        }

        else
        {

            // find inorder successor of current Node
            Node succ = curr.right;

            while (succ.left != null && succ.left != curr)
                succ = succ.left;

            if (succ.left == null)
            {

                // set left child of successor to the
                // current Node
                succ.left = curr;

                // move current to its right
                curr = curr.right;
            }

            // restoring the tree back to original binary
            // search tree removing threaded links
            else
            {

                succ.left = null;

                if (++count == k)
                    Klargest = curr;

                // move current to its left child
                curr = curr.left;
            }
        }
    }
    return Klargest;
}

// Driver code
public static void Main(String[] args)
{
    // Your C# Code
    /* Constructed binary tree is
        4
        / \
    2 7
    / \ / \
    1 3 6 10 */

    Node root = newNode(4);
    root.left = newNode(2);
    root.right = newNode(7);
    root.left.left = newNode(1);
    root.left.right = newNode(3);
    root.right.left = newNode(6);
    root.right.right = newNode(10);

    Console.Write("Finding K-th largest Node in BST : " +
                    KthLargestUsingMorrisTraversal(root, 2).data);
}
}

// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript Program for finding
// K-th largest Node using O(1)
// extra memory and reverse
// Morris traversal.

 class Node
{
     constructor(){
     this.data = 0;
     this.left = null;
     this.right = null;
     }
}

// helper function to create a new Node
function newNode(data)
{
    var temp = new Node();
    temp.data = data;
    temp.right = null;
    temp.left = null;
    return temp;
}

function KthLargestUsingMorrisTraversal(root , k)
{
    var curr = root;
    var Klargest = null;

    // count variable to keep count of visited Nodes
    var count = 0;

    while (curr != null)
    {
        // if right child is NULL
        if (curr.right == null)
        {

            // first increment count and
            // check if count = k
            if (++count == k)
                Klargest = curr;

            // otherwise move to the left child
            curr = curr.left;
        }

        else
        {

            // find inorder successor of
            // current Node
            var succ = curr.right;

            while (succ.left != null && succ.left != curr)
                succ = succ.left;

            if (succ.left == null)
            {

                // set left child of successor to the
                // current Node
                succ.left = curr;

                // move current to its right
                curr = curr.right;
            }

            // restoring the tree back to original binary
            // search tree removing threaded links
            else
            {

                succ.left = null;

                if (++count == k)
                    Klargest = curr;

                // move current to its left child
                curr = curr.left;
            }
        }
    }
    return Klargest;
}

// Driver code

    // Your JavaScript Code
    /* Constructed binary tree is
        4
        / \
       2 7
    / \ / \
    1 3 6 10 */

     root = newNode(4);
    root.left = newNode(2);
    root.right = newNode(7);
    root.left.left = newNode(1);
    root.left.right = newNode(3);
    root.right.left = newNode(6);
    root.right.right = newNode(10);

    document.write("Finding K-th largest Node in BST : " +
               KthLargestUsingMorrisTraversal(root, 2).data);

// This code contributed by aashish1995

</script>
```

**Output:** 

```
Finding K-th largest Node in BST : 7
```

**时间复杂度:**O(n)
T3】辅助空间: O(1)