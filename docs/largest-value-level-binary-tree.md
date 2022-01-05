# 二叉树每级最大值

> 原文:[https://www . geesforgeks . org/最大值级二叉树/](https://www.geeksforgeeks.org/largest-value-level-binary-tree/)

给定一棵二叉树，找出每一级中最大的值。
**例:**

```
Input :
        1
       / \
      2   3 
Output : 1 3

Input : 
        4
       / \
      9   2
     / \   \
    3   5   7 
Output : 4 9 7
```

**方法:**想法是以预先排序的方式递归遍历树。根被认为是零级的。遍历时，跟踪元素的级别，如果其当前级别不等于列表中的元素数量，则更新列表中该级别的最大元素。
下面是在二叉树的每一级寻找最大值的实现。

## C++

```
// C++ program to find largest
// value on each level of binary tree.
#include <bits/stdc++.h>
using namespace std;

/* A binary tree node has data,
pointer to left child and a
pointer to right child */
struct Node {
    int val;
    struct Node *left, *right;
};

/* Recursive function to find
the largest value on each level */
void helper(vector<int>& res, Node* root, int d)
{
    if (!root)
        return;

    // Expand list size
    if (d == res.size())
        res.push_back(root->val);

    else

        // to ensure largest value
        // on level is being stored
        res[d] = max(res[d], root->val);

    // Recursively traverse left and
    // right subtrees in order to find
    // out the largest value on each level
    helper(res, root->left, d + 1);
    helper(res, root->right, d + 1);
}

// function to find largest values
vector<int> largestValues(Node* root)
{
    vector<int> res;
    helper(res, root, 0);
    return res;
}

/* Helper function that allocates a
new node with the given data and
NULL left and right pointers. */
Node* newNode(int data)
{
    Node* temp = new Node;
    temp->val = data;
    temp->left = temp->right = NULL;
    return temp;
}

// Driver code
int main()
{
    /* Let us construct a Binary Tree
        4
       / \
      9   2
     / \   \
    3   5   7 */

    Node* root = NULL;
    root = newNode(4);
    root->left = newNode(9);
    root->right = newNode(2);
    root->left->left = newNode(3);
    root->left->right = newNode(5);
    root->right->right = newNode(7);

    vector<int> res = largestValues(root);
    for (int i = 0; i < res.size(); i++)
        cout << res[i] << " ";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find largest
// value on each level of binary tree.
import java.util.*;

class GFG
{

/* A binary tree node has data,
pointer to left child and a
pointer to right child */
static class Node
{
    int val;
    Node left, right;
};

/* Recursive function to find
the largest value on each level */
static void helper(Vector<Integer> res, Node root, int d)
{
    if (root == null)
        return;

    // Expand list size
    if (d == res.size())
        res.add(root.val);

    else

        // to ensure largest value
        // on level is being stored
        res.set(d, Math.max(res.get(d), root.val));

    // Recursively traverse left and
    // right subtrees in order to find
    // out the largest value on each level
    helper(res, root.left, d + 1);
    helper(res, root.right, d + 1);
}

// function to find largest values
static Vector<Integer> largestValues(Node root)
{
    Vector<Integer> res = new Vector<>();
    helper(res, root, 0);
    return res;
}

/* Helper function that allocates a
new node with the given data and
NULL left and right pointers. */
static Node newNode(int data)
{
    Node temp = new Node();
    temp.val = data;
    temp.left = temp.right = null;
    return temp;
}

// Driver code
public static void main(String[] args)
{
    /* Let us construct a Binary Tree
        4
    / \
    9 2
    / \ \
    3 5 7 */

    Node root = null;
    root = newNode(4);
    root.left = newNode(9);
    root.right = newNode(2);
    root.left.left = newNode(3);
    root.left.right = newNode(5);
    root.right.right = newNode(7);

    Vector<Integer> res = largestValues(root);
    for (int i = 0; i < res.size(); i++)
            System.out.print(res.get(i)+" ");
}
}

/* This code is contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Python program to find largest value
# on each level of binary tree.

""" Recursive function to find
the largest value on each level """
def helper(res, root, d):

    if ( not root):
        return

    # Expand list size
    if (d == len(res)):
        res.append(root.val)

    else:

        # to ensure largest value
        # on level is being stored
        res[d] = max(res[d], root.val)

    # Recursively traverse left and
    # right subtrees in order to find
    # out the largest value on each level
    helper(res, root.left, d + 1)
    helper(res, root.right, d + 1)

# function to find largest values
def largestValues(root):

    res = []
    helper(res, root, 0)
    return res

# Helper function that allocates a new
# node with the given data and None left
# and right pointers.                                    
class newNode:

    # Constructor to create a new node
    def __init__(self, data):
        self.val = data
        self.left = None
        self.right = None

# Driver Code
if __name__ == '__main__':
    """ Let us construct the following Tree
        4
        / \
        9 2
    / \ \
    3 5 7 """
    root = newNode(4)
    root.left = newNode(9)
    root.right = newNode(2)
    root.left.left = newNode(3)
    root.left.right = newNode(5)
    root.right.right = newNode(7)
    print(*largestValues(root))                        

# This code is contributed
# Shubham Singh(SHUBHAMSINGH10)
```

## C#

```
// C# program to find largest
// value on each level of binary tree.
using System;
using System.Collections.Generic;

class GFG
{

/* A binary tree node has data,
pointer to left child and a
pointer to right child */
public class Node
{
    public int val;
    public Node left, right;
};

/* Recursive function to find
the largest value on each level */
static void helper(List<int> res,
                   Node root, int d)
{
    if (root == null)
        return;

    // Expand list size
    if (d == res.Count)
        res.Add(root.val);

    else

        // to ensure largest value
        // on level is being stored
        res[d] = Math.Max(res[d], root.val);

    // Recursively traverse left and
    // right subtrees in order to find
    // out the largest value on each level
    helper(res, root.left, d + 1);
    helper(res, root.right, d + 1);
}

// function to find largest values
static List<int> largestValues(Node root)
{
    List<int> res = new List<int>();
    helper(res, root, 0);
    return res;
}

/* Helper function that allocates a
new node with the given data and
NULL left and right pointers. */
static Node newNode(int data)
{
    Node temp = new Node();
    temp.val = data;
    temp.left = temp.right = null;
    return temp;
}

// Driver code
public static void Main(String[] args)
{

    /* Let us construct a Binary Tree
        4
    / \
    9 2
    / \ \
    3 5 7 */
    Node root = null;
    root = newNode(4);
    root.left = newNode(9);
    root.right = newNode(2);
    root.left.left = newNode(3);
    root.left.right = newNode(5);
    root.right.right = newNode(7);

    List<int> res = largestValues(root);
    for (int i = 0; i < res.Count; i++)
        Console.Write(res[i] + " ");
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

    // JavaScript program to find largest
    // value on each level of binary tree.

    /* A binary tree node has data,
    pointer to left child and a
    pointer to right child */
    class Node
    {
        constructor(data) {
           this.left = null;
           this.right = null;
           this.val = data;
        }
    }

    /* Recursive function to find
    the largest value on each level */
    function helper(res, root, d)
    {
        if (root == null)
            return;

        // Expand list size
        if (d == res.length)
            res.push(root.val);

        else

            // to ensure largest value
            // on level is being stored
            res[d] =  Math.max(res[d], root.val);

        // Recursively traverse left and
        // right subtrees in order to find
        // out the largest value on each level
        helper(res, root.left, d + 1);
        helper(res, root.right, d + 1);
    }

    // function to find largest values
    function largestValues(root)
    {
        let res = [];
        helper(res, root, 0);
        return res;
    }

    /* Helper function that allocates a
    new node with the given data and
    NULL left and right pointers. */
    function newNode(data)
    {
        let temp = new Node(data);
        return temp;
    }

    /* Let us construct a Binary Tree
        4
    / \
    9 2
    / \ \
    3 5 7 */

    let root = null;
    root = newNode(4);
    root.left = newNode(9);
    root.right = newNode(2);
    root.left.left = newNode(3);
    root.left.right = newNode(5);
    root.right.right = newNode(7);

    let res = largestValues(root);
    for (let i = 0; i < res.length; i++)
            document.write(res[i]+" ");

</script>
```

**输出:**

```
4 9 7
```

[二叉树每级最大值| Set-2(迭代方法)](https://www.geeksforgeeks.org/largest-value-level-binary-tree-set-2-iterative-approach/)
**复杂度分析:**

*   **时间复杂度:** O(n)，其中 n 为二叉树中的节点数。
*   **辅助空间:** O(n)最差情况下，二叉树深度将为 n。