# 求给定二叉树祖先的迭代法

> 原文:[https://www . geeksforgeeks . org/迭代方法查找给定二叉树的祖先/](https://www.geeksforgeeks.org/iterative-method-to-find-ancestors-of-a-given-binary-tree/)

给定一个二叉树，打印树中存在的特定键的所有祖先，而不使用递归。
这里我们将讨论上述问题的实现。

示例:

```
Input : 
            1
        /       \
       2         7
     /   \     /   \
    3     5    8    9 
   /       \       /
  4         6     10 
Key = 6 

Output : 5 2 1
Ancestors of 6 are 5, 2 and 1.
```

其思想是利用给定二叉树的[迭代后序遍历](https://www.geeksforgeeks.org/iterative-postorder-traversal-using-stack/)。

## C++

```
// C++ program to print all ancestors of a given key
#include <bits/stdc++.h>
using namespace std;

// Structure for a tree node
struct Node {
    int data;
    struct Node* left, *right;
};

// A utility function to create a new tree node
struct Node* newNode(int data)
{
    struct Node* node = (struct Node*)malloc(sizeof(struct Node));
    node->data = data;
    node->left = node->right = NULL;
    return node;
}

// Iterative Function to print all ancestors of a
// given key
void printAncestors(struct Node* root, int key)
{
    if (root == NULL)
        return;

    // Create a stack to hold ancestors
    stack<struct Node*> st;

    // Traverse the complete tree in postorder way till
    // we find the key
    while (1) {

        // Traverse the left side. While traversing, push
        // the nodes into  the stack so that their right
        // subtrees can be traversed later
        while (root && root->data != key) {
            st.push(root); // push current node
            root = root->left; // move to next node
        }

        // If the node whose ancestors are to be printed
        // is found, then break the while loop.
        if (root && root->data == key)
            break;

        // Check if right sub-tree exists for the node at top
        // If not then pop that node because we don't need
        // this node any more.
        if (st.top()->right == NULL) {
            root = st.top();
            st.pop();

            // If the popped node is right child of top,
            // then remove the top as well. Left child of
            // the top must have processed before.
            while (!st.empty() && st.top()->right == root) {
                root = st.top();
                st.pop();
            }
        }

        // if stack is not empty then simply set the root
        // as right child of top and start traversing right
        // sub-tree.
        root = st.empty() ? NULL : st.top()->right;
    }

    // If stack is not empty, print contents of stack
    // Here assumption is that the key is there in tree
    while (!st.empty()) {
        cout << st.top()->data << " ";
        st.pop();
    }
}

// Driver program to test above functions
int main()
{
    // Let us construct a binary tree
    struct Node* root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(7);
    root->left->left = newNode(3);
    root->left->right = newNode(5);
    root->right->left = newNode(8);
    root->right->right = newNode(9);
    root->left->left->left = newNode(4);
    root->left->right->right = newNode(6);
    root->right->right->left = newNode(10);

    int key = 6;
    printAncestors(root, key);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print all
// ancestors of a given key
import java.util.*;

class GfG
{

// Structure for a tree node
static class Node
{
    int data;
    Node left, right;
}

// A utility function to
// create a new tree node
static Node newNode(int data)
{
    Node node = new Node();
    node.data = data;
    node.left = null;
    node.right = null;
    return node;
}

// Iterative Function to print
// all ancestors of a given key
static void printAncestors(Node root, int key)
{
    if (root == null)
        return;

    // Create a stack to hold ancestors
    Stack<Node> st = new Stack<Node> ();

    // Traverse the complete tree in
    // postorder way till we find the key
    while (1 == 1)
    {

        // Traverse the left side. While
        // traversing, push the nodes into
        // the stack so that their right
        // subtrees can be traversed later
        while (root != null && root.data != key)
        {
            st.push(root); // push current node
            root = root.left; // move to next node
        }

        // If the node whose ancestors
        // are to be printed is found,
        // then break the while loop.
        if (root != null && root.data == key)
            break;

        // Check if right sub-tree exists
        // for the node at top If not then
        // pop that node because we don't 
        // need this node any more.
        if (st.peek().right == null)
        {
            root = st.peek();
            st.pop();

            // If the popped node is right child of top,
            // then remove the top as well. Left child of
            // the top must have processed before.
            while (!st.isEmpty() && st.peek().right == root)
            {
                root = st.peek();
                st.pop();
            }
        }

        // if stack is not empty then simply
        // set the root as right child of
        // top and start traversing right
        // sub-tree.
        root = st.isEmpty() ? null : st.peek().right;
    }

    // If stack is not empty, print contents of stack
    // Here assumption is that the key is there in tree
    while (!st.isEmpty())
    {
        System.out.print(st.peek().data + " ");
        st.pop();
    }
}

// Driver code
public static void main(String[] args)
{
    // Let us construct a binary tree
    Node root = newNode(1);
    root.left = newNode(2);
    root.right = newNode(7);
    root.left.left = newNode(3);
    root.left.right = newNode(5);
    root.right.left = newNode(8);
    root.right.right = newNode(9);
    root.left.left.left = newNode(4);
    root.left.right.right = newNode(6);
    root.right.right.left = newNode(10);

    int key = 6;
    printAncestors(root, key);
}
}

// This code is contributed
// by prerna saini
```

## 蟒蛇 3

```
# Python program to print all ancestors of a given key

# A class to create a new tree node
class newNode:
    def __init__(self, data):
        self.data = data
        self.left = self.right = None

# Iterative Function to print all ancestors of a
# given key
def printAncestors(root, key):
    if (root == None):
        return

    # Create a stack to hold ancestors
    st = []

    # Traverse the complete tree in postorder way till
    # we find the key
    while (1):

        # Traverse the left side. While traversing, push
        # the nodes into the stack so that their right
        # subtrees can be traversed later
        while (root and root.data != key):
            st.append(root) # push current node
            root = root.left # move to next node

        # If the node whose ancestors are to be printed
        # is found, then break the while loop.
        if (root and root.data == key):
            break

        # Check if right sub-tree exists for the node at top
        # If not then pop that node because we don't need
        # this node any more.
        if (st[-1].right == None):
            root = st[-1]
            st.pop()

            # If the popped node is right child of top,
            # then remove the top as well. Left child of
            # the top must have processed before.
            while (len(st) != 0 and st[-1].right == root):
                root = st[-1]
                st.pop()

        # if stack is not empty then simply set the root
        # as right child of top and start traversing right
        # sub-tree.
        root = None if len(st) == 0 else st[-1].right

    # If stack is not empty, print contents of stack
    # Here assumption is that the key is there in tree
    while (len(st) != 0):
        print(st[-1].data,end = " ")
        st.pop()

# Driver code
if __name__ == '__main__':

    # Let us construct a binary tree
    root = newNode(1)
    root.left = newNode(2)
    root.right = newNode(7)
    root.left.left = newNode(3)
    root.left.right = newNode(5)
    root.right.left = newNode(8)
    root.right.right = newNode(9)
    root.left.left.left = newNode(4)
    root.left.right.right = newNode(6)
    root.right.right.left = newNode(10)

    key = 6
    printAncestors(root, key)

# This code is contributed by PranchalK.
```

## C#

```
// C# program to print all
// ancestors of a given key
using System;
using System.Collections.Generic;

class GfG
{

// Structure for a tree node
public class Node
{
    public int data;
    public Node left, right;
}

// A utility function to
// create a new tree node
static Node newNode(int data)
{
    Node node = new Node();
    node.data = data;
    node.left = null;
    node.right = null;
    return node;
}

// Iterative Function to print
// all ancestors of a given key
static void printAncestors(Node root, int key)
{
    if (root == null)
        return;

    // Create a stack to hold ancestors
    Stack<Node> st = new Stack<Node> ();

    // Traverse the complete tree in
    // postorder way till we find the key
    while (1 == 1)
    {

        // Traverse the left side. While
        // traversing, push the nodes into
        // the stack so that their right
        // subtrees can be traversed later
        while (root != null && root.data != key)
        {
            st.Push(root); // push current node
            root = root.left; // move to next node
        }

        // If the node whose ancestors
        // are to be printed is found,
        // then break the while loop.
        if (root != null && root.data == key)
            break;

        // Check if right sub-tree exists
        // for the node at top If not then
        // pop that node because we don't
        // need this node any more.
        if (st.Peek().right == null)
        {
            root = st.Peek();
            st.Pop();

            // If the popped node is right child of top,
            // then remove the top as well. Left child of
            // the top must have processed before.
            while (st.Count != 0 && st.Peek().right == root)
            {
                root = st.Peek();
                st.Pop();
            }
        }

        // if stack is not empty then simply
        // set the root as right child of
        // top and start traversing right
        // sub-tree.
        root = st.Count == 0 ? null : st.Peek().right;
    }

    // If stack is not empty, print contents of stack
    // Here assumption is that the key is there in tree
    while (st.Count != 0)
    {
        Console.Write(st.Peek().data + " ");
        st.Pop();
    }
}

// Driver code
public static void Main(String[] args)
{
    // Let us construct a binary tree
    Node root = newNode(1);
    root.left = newNode(2);
    root.right = newNode(7);
    root.left.left = newNode(3);
    root.left.right = newNode(5);
    root.right.left = newNode(8);
    root.right.right = newNode(9);
    root.left.left.left = newNode(4);
    root.left.right.right = newNode(6);
    root.right.right.left = newNode(10);

    int key = 6;
    printAncestors(root, key);
}
}

// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program to print all
// ancestors of a given key
class Node
{
    constructor(data)
    {
        this.left = null;
        this.right = null;
        this.data = data;
    }
}

// A utility function to
// create a new tree node
function newNode(data)
{
    let node = new Node(data);
    return node;
}

// Iterative Function to print
// all ancestors of a given key
function printAncestors(root, key)
{
    if (root == null)
        return;

    // Create a stack to hold ancestors
    let st = [];

    // Traverse the complete tree in
    // postorder way till we find the key
    while (1 == 1)
    {

        // Traverse the left side. While
        // traversing, push the nodes into
        // the stack so that their right
        // subtrees can be traversed later
        while (root != null && root.data != key)
        {

            // Push current node
            st.push(root);

            // Move to next node
            root = root.left;
        }

        // If the node whose ancestors
        // are to be printed is found,
        // then break the while loop.
        if (root != null && root.data == key)
            break;

        // Check if right sub-tree exists
        // for the node at top If not then
        // pop that node because we don't
        // need this node any more.
        if (st[st.length - 1].right == null)
        {
            root = st[st.length - 1];
            st.pop();

            // If the popped node is right child of top,
            // then remove the top as well. Left child of
            // the top must have processed before.
            while (st.length != 0 &&
                st[st.length - 1].right == root)
            {
                root = st[st.length - 1];
                st.pop();
            }
        }

        // If stack is not empty then simply
        // set the root as right child of
        // top and start traversing right
        // sub-tree.
        root = st.length == 0 ? null :
            st[st.length - 1].right;
    }

    // If stack is not empty, print contents
    // of stack. Here assumption is that the
    // key is there in tree
    while (st.length != 0)
    {
        document.write(st[st.length - 1].data + " ");
        st.pop();
    }
}

// Driver code

// Let us construct a binary tree
let root = newNode(1);
root.left = newNode(2);
root.right = newNode(7);
root.left.left = newNode(3);
root.left.right = newNode(5);
root.right.left = newNode(8);
root.right.right = newNode(9);
root.left.left.left = newNode(4);
root.left.right.right = newNode(6);
root.right.right.left = newNode(10);

let key = 6;
printAncestors(root, key);

// This code is contributed by divyeshrabadiya07

</script>
```

**输出:**

```
5 2 1
```

本文由 [**高塔姆·辛格**](https://www.facebook.com/gautam.ngs) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。