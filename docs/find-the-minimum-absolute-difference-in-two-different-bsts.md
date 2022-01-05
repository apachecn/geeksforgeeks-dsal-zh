# 求两个不同 BST 的最小绝对差

> 原文:[https://www . geeksforgeeks . org/find-两个不同 BST 中的最小绝对差值/](https://www.geeksforgeeks.org/find-the-minimum-absolute-difference-in-two-different-bsts/)

给定 2 棵二分搜索法树，从每棵树中选择一个节点，使它们的绝对差异尽可能最小。假设每个基站至少有一个节点。

**示例:**

```
Input : N1 = 7, N2 = 2 

BST1 :
          5 
        /   \ 
       3     7 
      / \   / \ 
     2   4 6   8

BST2 :
         11
           \
            13

Output : 3
8 is largest number in the first BST
and 11 is smallest in the second.
Thus, the final answer will be 11-8 = 3

Input : N1 = 4, N2 = 2
BST1 :
          3 
        /   \ 
       2     4
              \
              14

BST2 :
          7
           \
            13

Output : 1
```

**方法:**
想法是使用双指针技术，并使用以下步骤迭代指针。

1.  为两个 BST 创建前向迭代器。假设它们所指向的节点的值分别为 v <sub>1</sub> 和 v <sub>2</sub> 。
2.  现在在每一步:
    *   最后更新年数为 **min(年数，ABS(v<sub>【1】</sub>-v<sub>【2】</sub>)**。
    *   如果 v <sub>1</sub> < v <sub>2</sub> ，移动第一个 BST 的迭代器，否则移动第二个 BST 的迭代器。
3.  重复以上步骤，直到两个 BST 都指向一个有效节点。

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Node of Binary tree
struct node {
    int data;
    node* left;
    node* right;
    node(int data)
    {
        this->data = data;
        left = NULL;
        right = NULL;
    }
};

// Function to iterate to the
// next element of the BST
void next(stack<node*>& it)
{

    node* curr = it.top()->right;
    it.pop();
    while (curr != NULL)
        it.push(curr), curr = curr->left;
}

// Function to find minimum difference
int minDiff(node* root1, node* root2)
{

    // Iterator for two Binary Search Trees
    stack<node *> it1, it2;

    // Initializing first iterator
    node* curr = root1;
    while (curr != NULL)
        it1.push(curr), curr = curr->left;

    // Initializing second iterator
    curr = root2;
    while (curr != NULL)
        it2.push(curr), curr = curr->left;

    // Variable to store final answer
    int ans = INT_MAX;

    // Two pointer technique
    while (it1.size() and it2.size()) {

        // value it1 and it2 are pointing to
        int v1 = it1.top()->data;
        int v2 = it2.top()->data;

        // Updating final answer
        ans = min(abs(v1 - v2), ans);

        // Case when v1 < v2
        if (v1 < v2)
            next(it1);
        else
            next(it2);
    }

    // Return ans
    return ans;
}

// Driver code
int main()
{
    // BST-1

    /*    5
        /   \
       3     7
      / \   / \
     2   4 6   8 */
    node* root2 = new node(5);
    root2->left = new node(3);
    root2->right = new node(7);
    root2->left->left = new node(2);
    root2->left->right = new node(4);
    root2->right->left = new node(6);
    root2->right->right = new node(8);

    // BST-2

    /*  11
         \
          15
    */
    node* root1 = new node(11);
    root1->right = new node(15);

    cout << minDiff(root1, root2);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Node of Binary tree
static class node
{
    int data;
    node left;
    node right;
    node(int data)
    {
        this.data = data;
        left = null;
        right = null;
    }
};

// Function to iterate to the
// next element of the BST
static void next(Stack<node> it)
{
    node curr = it.peek().right;
    it.pop();
    while (curr != null)
    {
        it.push(curr);
        curr = curr.left;
    }
}

// Function to find minimum difference
static int minDiff(node root1, node root2)
{

    // Iterator for two Binary Search Trees
    Stack<node> it1 = new Stack<node>();
    Stack<node> it2 = new Stack<node>();

    // Initializing first iterator
    node curr = root1;
    while (curr != null)
    {
        it1.push(curr);
        curr = curr.left;
    }

    // Initializing second iterator
    curr = root2;
    while (curr != null)
    {
        it2.push(curr);
        curr = curr.left;
    }

    // Variable to store final answer
    int ans = Integer.MAX_VALUE;

    // Two pointer technique
    while (it1.size() > 0 && it2.size() > 0)
    {

        // value it1 and it2 are pointing to
        int v1 = it1.peek().data;
        int v2 = it2.peek().data;

        // Updating final answer
        ans = Math.min(Math.abs(v1 - v2), ans);

        // Case when v1 < v2
        if (v1 < v2)
            next(it1);
        else
            next(it2);
    }

    // Return ans
    return ans;
}

// Driver code
public static void main(String[] args)
{
    // BST-1

    /* 5
        / \
    3     7
    / \ / \
    2 4 6 8 */
    node root2 = new node(5);
    root2.left = new node(3);
    root2.right = new node(7);
    root2.left.left = new node(2);
    root2.left.right = new node(4);
    root2.right.left = new node(6);
    root2.right.right = new node(8);

    // BST-2

    /* 11
        \
        15
    */
    node root1 = new node(11);
    root1.right = new node(15);

    System.out.println(minDiff(root1, root2));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach
import sys

# Node of the binary tree
class node:

    def __init__ (self, key):

        self.data = key
        self.left = None
        self.right = None

# Function to iterate to the
# next element of the BST
def next(it):

    curr = it[-1].right

    del it[-1]
    while (curr != None):
        it.append(curr)
        curr = curr.left

    return it

# Function to find minimum difference
def minDiff(root1, root2):

    # Iterator for two Binary Search Trees
    it1, it2 = [], []

    # Initializing first iterator
    curr = root1
    while (curr != None):
        it1.append(curr)
        curr = curr.left

    # Initializing second iterator
    curr = root2
    while (curr != None):
        it2.append(curr)
        curr = curr.left

    # Variable to store final answer
    ans = sys.maxsize

    # Two pointer technique
    while (len(it1) > 0 and len(it2) > 0):

        # Value it1 and it2 are pointing to
        v1 = it1[-1].data
        v2 = it2[-1].data

        # Updating final answer
        ans = min(abs(v1 - v2), ans)

        # Case when v1 < v2
        if (v1 < v2):
            it1 = next(it1)
        else:
            it2 = next(it2)

    # Return ans
    return ans

# Driver code
if __name__ == '__main__':

    # BST-1
    #       5
    #     /   \
    #    3     7
    #   / \   / \
    #  2   4 6   8
    root2 = node(5)
    root2.left = node(3)
    root2.right = node(7)
    root2.left.left = node(2)
    root2.left.right = node(4)
    root2.right.left = node(6)
    root2.right.right = node(8)

    # BST-2
    #    11
    #      \
    #       15
    #
    root1 = node(11)
    root1.right = node(15)

    print(minDiff(root1, root2))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

// Node of Binary tree
class node
{
    public int data;
    public node left;
    public node right;
    public node(int data)
    {
        this.data = data;
        left = null;
        right = null;
    }
};

// Function to iterate to the
// next element of the BST
static void next(Stack<node> it)
{
    node curr = it.Peek().right;
    it.Pop();
    while (curr != null)
    {
        it.Push(curr);
        curr = curr.left;
    }
}

// Function to find minimum difference
static int minDiff(node root1, node root2)
{

    // Iterator for two Binary Search Trees
    Stack<node> it1 = new Stack<node>();
    Stack<node> it2 = new Stack<node>();

    // Initializing first iterator
    node curr = root1;
    while (curr != null)
    {
        it1.Push(curr);
        curr = curr.left;
    }

    // Initializing second iterator
    curr = root2;
    while (curr != null)
    {
        it2.Push(curr);
        curr = curr.left;
    }

    // Variable to store readonly answer
    int ans = int.MaxValue;

    // Two pointer technique
    while (it1.Count > 0 && it2.Count > 0)
    {

        // value it1 and it2 are pointing to
        int v1 = it1.Peek().data;
        int v2 = it2.Peek().data;

        // Updating readonly answer
        ans = Math.Min(Math.Abs(v1 - v2), ans);

        // Case when v1 < v2
        if (v1 < v2)
            next(it1);
        else
            next(it2);
    }

    // Return ans
    return ans;
}

// Driver code
public static void Main(String[] args)
{
    // BST-1

    /* 5
        / \
    3     7
    / \ / \
    2 4 6 8 */
    node root2 = new node(5);
    root2.left = new node(3);
    root2.right = new node(7);
    root2.left.left = new node(2);
    root2.left.right = new node(4);
    root2.right.left = new node(6);
    root2.right.right = new node(8);

    // BST-2

    /* 11
        \
        15
    */
    node root1 = new node(11);
    root1.right = new node(15);

    Console.WriteLine(minDiff(root1, root2));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Node of the binary tree
class node
{
    constructor(data)
    {
        this.data = data;
        this.left = null;
        this.right = null;
    }
}

// Function to iterate to the
// next element of the BST
function next(it)
{
    let curr = it[it.length-1].right;
    it.pop();
    while (curr != null)
    {
        it.push(curr);
        curr = curr.left;
    }
}

// Function to find minimum difference
function minDiff(root1,root2)
{
    // Iterator for two Binary Search Trees
    let it1 = [];
    let it2 = [];

    // Initializing first iterator
    let curr = root1;
    while (curr != null)
    {
        it1.push(curr);
        curr = curr.left;
    }

    // Initializing second iterator
    curr = root2;
    while (curr != null)
    {
        it2.push(curr);
        curr = curr.left;
    }

    // Variable to store final answer
    let ans = Number.MAX_VALUE;

    // Two pointer technique
    while (it1.length > 0 && it2.length > 0)
    {

        // value it1 and it2 are pointing to
        let v1 = it1[it1.length-1].data;
        let v2 = it2[it2.length-1].data;

        // Updating final answer
        ans = Math.min(Math.abs(v1 - v2), ans);

        // Case when v1 < v2
        if (v1 < v2)
            next(it1);
        else
            next(it2);
    }

    // Return ans
    return ans;
}

// Driver code
// BST-1

    /* 5
        / \
    3     7
    / \ / \
    2 4 6 8 */
    let root2 = new node(5);
    root2.left = new node(3);
    root2.right = new node(7);
    root2.left.left = new node(2);
    root2.left.right = new node(4);
    root2.right.left = new node(6);
    root2.right.right = new node(8);

    // BST-2

    /* 11
        \
        15
    */
    let root1 = new node(11);
    root1.right = new node(15);

    document.write(minDiff(root1, root2));

// This code is contributed by patel2127
</script>
```

**Output:** 

```
3
```

**时间复杂度:** O(N <sub>1</sub> + N <sub>2</sub> )其中 N <sub>1</sub> 和 N <sub>2</sub> 分别是第一个和第二个 BST 的节点数。
**空间复杂度:** O(H <sub>1</sub> + H <sub>2</sub> )其中 H <sub>1</sub> 和 H <sub>2</sub> 分别为第一个和第二个 BST 的高度。