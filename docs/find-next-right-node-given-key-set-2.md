# 找到给定键的下一个右节点|设置 2

> 原文:[https://www . geesforgeks . org/find-next-right-node-given-key-set-2/](https://www.geeksforgeeks.org/find-next-right-node-given-key-set-2/)

给定一棵二叉树和二叉树中的一个键，找到给定键右边的节点。如果右侧没有节点，则返回空值。预期时间复杂度为 O(n)，其中 n 是给定二叉树中的节点数。
例如，考虑下面的二叉树。2 的输出是 6，4 的输出是 5。10、6 和 5 的输出为空。

```
                  10
               /      \
             2         6
           /   \         \ 
         8      4          5
Input : 2
Output : 6

Input : 4
Output : 5
```

在我们之前的帖子中，我们讨论了一个使用[级序遍历](https://www.geeksforgeeks.org/level-order-tree-traversal/)的解决方案。在这篇文章中，我们将讨论一个基于 Preorder 遍历的解决方案，它需要恒定的辅助空间。
想法是使用[前序遍历](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)遍历给定的树，并搜索给定的键。找到给定的密钥后，我们将标记该密钥的级别号。现在，我们将在同一级别找到的下一个节点是位于给定键右侧的所需节点。
以下是上述思路的实现:

## C++

```
/* C++ program to find next right of a given key
   using preorder traversal */
#include <bits/stdc++.h>
using namespace std;

// A Binary Tree Node
struct Node {
    struct Node *left, *right;
    int key;
};

// Utility function to create a new tree node
Node* newNode(int key)
{
    Node* temp = new Node;
    temp->key = key;
    temp->left = temp->right = NULL;
    return temp;
}

// Function to find next node for given node
// in same level in a binary tree by using
// pre-order traversal
Node* nextRightNode(Node* root, int k, int level,
                               int& value_level)
{
    // return null if tree is empty
    if (root == NULL)
        return NULL;

    // if desired node is found, set value_level
    // to current level
    if (root->key == k) {
        value_level = level;
        return NULL;
    }

    // if value_level is already set, then current
    // node is the next right node
    else if (value_level) {
        if (level == value_level)
            return root;
    }

    // recurse for left subtree by increasing level by 1
    Node* leftNode = nextRightNode(root->left, k,
                        level + 1,  value_level);

    // if node is found in left subtree, return it
    if (leftNode)
        return leftNode;

    // recurse for right subtree by increasing level by 1
    return nextRightNode(root->right, k, level + 1,
                                       value_level);
}

// Function to find next node of given node in the
//  same level in given binary tree
Node* nextRightNodeUtil(Node* root, int k)
{
    int value_level = 0;

    return nextRightNode(root, k, 1, value_level);
}

// A utility function to test above functions
void test(Node* root, int k)
{
    Node* nr = nextRightNodeUtil(root, k);
    if (nr != NULL)
        cout << "Next Right of " << k << " is "
             << nr->key << endl;
    else
        cout << "No next right node found for "
             << k << endl;
}

// Driver program to test above functions
int main()
{
    // Let us create binary tree given in the
    // above example
    Node* root = newNode(10);
    root->left = newNode(2);
    root->right = newNode(6);
    root->right->right = newNode(5);
    root->left->left = newNode(8);
    root->left->right = newNode(4);

    test(root, 10);
    test(root, 2);
    test(root, 6);
    test(root, 5);
    test(root, 8);
    test(root, 4);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/* Java program to find next right of a given key
using preorder traversal */
import java.util.*;
class GfG {

// A Binary Tree Node
static class Node {
    Node left, right;
    int key;
}

// Utility function to create a new tree node
static Node newNode(int key)
{
    Node temp = new Node();
    temp.key = key;
    temp.left = null;
    temp.right = null;
    return temp;
}

// Function to find next node for given node
// in same level in a binary tree by using
// pre-order traversal
static Node nextRightNode(Node root, int k, int level, int[] value)
{
    // return null if tree is empty
    if (root == null)
        return null;

    // if desired node is found, set value[0]
    // to current level
    if (root.key == k) {
        value[0] = level;
        return null;
    }

    // if value[0] is already set, then current
    // node is the next right node
    else if (value[0] != 0) {
        if (level == value[0])
            return root;
    }

    // recurse for left subtree by increasing level by 1
    Node leftNode = nextRightNode(root.left, k, level + 1, value);

    // if node is found in left subtree, return it
    if (leftNode != null)
        return leftNode;

    // recurse for right subtree by increasing level by 1
    return nextRightNode(root.right, k, level + 1, value);
}

// Function to find next node of given node in the
// same level in given binary tree
static Node nextRightNodeUtil(Node root, int k)
{

    int[] v = new int[1];
    v[0] = 0;
    return nextRightNode(root, k, 1, v);
}

// A utility function to test above functions
static void test(Node root, int k)
{
    Node nr = nextRightNodeUtil(root, k);
    if (nr != null)
        System.out.println("Next Right of " + k + " is "+ nr.key);
    else
        System.out.println("No next right node found for " + k);
}

// Driver program to test above functions
public static void main(String[] args)
{
    // Let us create binary tree given in the
    // above example
    Node root = newNode(10);
    root.left = newNode(2);
    root.right = newNode(6);
    root.right.right = newNode(5);
    root.left.left = newNode(8);
    root.left.right = newNode(4);

    test(root, 10);
    test(root, 2);
    test(root, 6);
    test(root, 5);
    test(root, 8);
    test(root, 4);
}
}
// This code has been contributed by Mukul Sharma
```

## 蟒蛇 3

```
# Python3 program to find next right of a
# given key using preorder traversal

# class to create a new tree node
class newNode:
    def __init__(self, key):
        self.key = key
        self.left = self.right = None

# Function to find next node for given node
# in same level in a binary tree by using
# pre-order traversal
def nextRightNode(root, k, level, value_level):

    # return None if tree is empty
    if (root == None):
        return None

    # if desired node is found, set
    # value_level to current level
    if (root.key == k):
        value_level[0] = level
        return None

    # if value_level is already set, then
    # current node is the next right node
    elif (value_level[0]):
        if (level == value_level[0]):
            return root

    # recurse for left subtree by increasing
    # level by 1
    leftNode = nextRightNode(root.left, k,
                             level + 1, value_level)

    # if node is found in left subtree,
    # return it
    if (leftNode):
        return leftNode

    # recurse for right subtree by
    # increasing level by 1
    return nextRightNode(root.right, k,
                         level + 1, value_level)

# Function to find next node of given node
# in the same level in given binary tree
def nextRightNodeUtil(root, k):
    value_level = [0]

    return nextRightNode(root, k, 1, value_level)

# A utility function to test above functions
def test(root, k):
    nr = nextRightNodeUtil(root, k)
    if (nr != None):
        print("Next Right of", k, "is", nr.key)
    else:
        print("No next right node found for", k)

# Driver Code
if __name__ == '__main__':

    # Let us create binary tree given in the
    # above example
    root = newNode(10)
    root.left = newNode(2)
    root.right = newNode(6)
    root.right.right = newNode(5)
    root.left.left = newNode(8)
    root.left.right = newNode(4)

    test(root, 10)
    test(root, 2)
    test(root, 6)
    test(root, 5)
    test(root, 8)
    test(root, 4)

# This code is contributed by PranchalK
```

## C#

```
/* C# program to find next right of a given key
using preorder traversal */
using System;

class GfG
{

public class V
{
    public int value_level = 0;
}

// A Binary Tree Node
public class Node
{
    public Node left, right;
    public int key;
}

// Utility function to create a new tree node
static Node newNode(int key)
{
    Node temp = new Node();
    temp.key = key;
    temp.left = null;
    temp.right = null;
    return temp;
}

// Function to find next node for given node
// in same level in a binary tree by using
// pre-order traversal
static Node nextRightNode(Node root, int k,
                            int level, V value)
{
    // return null if tree is empty
    if (root == null)
        return null;

    // if desired node is found, set
    // value_level to current level
    if (root.key == k)
    {
        value.value_level = level;
        return null;
    }

    // if value_level is already set, then current
    // node is the next right node
    else if (value.value_level != 0)
    {
        if (level == value.value_level)
            return root;
    }

    // recurse for left subtree by increasing level by 1
    Node leftNode = nextRightNode(root.left,
                            k, level + 1, value);

    // if node is found in left subtree, return it
    if (leftNode != null)
        return leftNode;

    // recurse for right subtree by
    // increasing level by 1
    return nextRightNode(root.right, k,
                       level + 1, value);
}

// Function to find next node of given node in the
// same level in given binary tree
static Node nextRightNodeUtil(Node root, int k)
{
    V v = new V();

    return nextRightNode(root, k, 1, v);
}

// A utility function to test above functions
static void test(Node root, int k)
{
    Node nr = nextRightNodeUtil(root, k);
    if (nr != null)
        Console.WriteLine("Next Right of " +
                            k + " is "+ nr.key);
    else
        Console.WriteLine("No next right node" +
                            " found for " + k);
}

// Driver main
public static void Main(String[] args)
{
    // Let us create binary tree given in the
    // above example
    Node root = newNode(10);
    root.left = newNode(2);
    root.right = newNode(6);
    root.right.right = newNode(5);
    root.left.left = newNode(8);
    root.left.right = newNode(4);

    test(root, 10);
    test(root, 2);
    test(root, 6);
    test(root, 5);
    test(root, 8);
    test(root, 4);
}
}

// This code contributed by Rajput-Ji
```

## java 描述语言

```
<script>

    /* Javascript program to find next right of a given key
    using preorder traversal */

    // A Binary Tree Node
    class Node
    {
        constructor(key) {
           this.left = null;
           this.right = null;
           this.key = key;
        }
    }

    // Utility function to create a new tree node
    function newNode(key)
    {
        let temp = new Node(key);
        return temp;
    }

    // Function to find next node for given node
    // in same level in a binary tree by using
    // pre-order traversal
    function nextRightNode(root, k, level, value)
    {
        // return null if tree is empty
        if (root == null)
            return null;

        // if desired node is found, set value[0]
        // to current level
        if (root.key == k) {
            value[0] = level;
            return null;
        }

        // if value[0] is already set, then current
        // node is the next right node
        else if (value[0] != 0) {
            if (level == value[0])
                return root;
        }

        // recurse for left subtree by increasing level by 1
        let leftNode = nextRightNode(root.left, k, level + 1, value);

        // if node is found in left subtree, return it
        if (leftNode != null)
            return leftNode;

        // recurse for right subtree by increasing level by 1
        return nextRightNode(root.right, k, level + 1, value);
    }

    // Function to find next node of given node in the
    // same level in given binary tree
    function nextRightNodeUtil(root, k)
    {

        let v = new Array(1);
        v[0] = 0;
        return nextRightNode(root, k, 1, v);
    }

    // A utility function to test above functions
    function test(root, k)
    {
        let nr = nextRightNodeUtil(root, k);
        if (nr != null)
            document.write("Next Right of " + k + " is "+ nr.key +
            "</br>");
        else
            document.write("No next right node found for " + k +
            "</br>");
    }

    // Let us create binary tree given in the
    // above example
    let root = newNode(10);
    root.left = newNode(2);
    root.right = newNode(6);
    root.right.right = newNode(5);
    root.left.left = newNode(8);
    root.left.right = newNode(4);

    test(root, 10);
    test(root, 2);
    test(root, 6);
    test(root, 5);
    test(root, 8);
    test(root, 4);

</script>
```

**输出**:

```
No next right node found for 10
Next Right of 2 is 6
No next right node found for 6
No next right node found for 5
Next Right of 8 is 4
Next Right of 4 is 5
```

**时间复杂度:**O(n)
T3】辅助空间: O(1)