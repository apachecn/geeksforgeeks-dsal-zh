# 二叉查找树中给定和的对数

> 原文:[https://www . geesforgeks . org/二进制搜索树中给定和的配对数/](https://www.geeksforgeeks.org/number-of-pairs-with-a-given-sum-in-a-binary-search-tree/)

给定一个二叉查找树和一个数字 **X** 。任务是找到 BST 中不同节点的不同对的数量，其和等于 **X** 。没有两个节点具有相同的值。

**示例:**

```
Input : X = 5
          5 
        /   \ 
       3     7 
      / \   / \ 
     2   4 6   8    
Output : 1
{2, 3} is the only possible pair. 
Thus, the answer is equal to 1.

Input : X = 6
      1
       \
        2
         \
          3
           \
            4
             \
              5

Output : 2
Possible pairs are {{1, 5}, {2, 4}}.
```

**天真的方法**:想法是把 BST 的所有元素散列或者把 BST 转换成一个排序的数组。之后，使用这里给出的算法找到配对的数量。
**时间复杂度:** O(N)。
**空间复杂度:** O(N)。

**空间优化方法:**思路是在 BST 上使用双指针技术。维护前向和后向迭代器，它们将分别以有序遍历和反向有序遍历的顺序迭代 BST。

1.  为 BST 创建向前和向后迭代器。假设他们所指向的节点的值分别等于 v <sub>1</sub> 和 v <sub>2</sub> 。
2.  现在在每一步，
    *   如果 v <sub>1</sub> + v <sub>2</sub> = X，则找到该对，从而将计数增加 1。
    *   如果 v <sub>1</sub> + v <sub>2</sub> 小于或等于 x，我们将使向前迭代器指向下一个元素。
    *   如果 v <sub>1</sub> + v <sub>2</sub> 大于 x，我们将使向后迭代器指向前一个元素。
3.  重复以上步骤，直到两个迭代器没有指向同一个节点。

下面是上述方法的实现:

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

// Function to find a pair
int cntPairs(node* root, int x)
{
    // Stack to store nodes for
    // forward and backward iterator
    stack<node *> it1, it2;

    // Initializing forward iterator
    node* c = root;
    while (c != NULL)
        it1.push(c), c = c->left;

    // Initializing backward iterator
    c = root;
    while (c != NULL)
        it2.push(c), c = c->right;

    // Variable to store final answer
    int ans = 0;

    // two pointer technique
    while (it1.top() != it2.top()) {

        // Variables to store the
        // value of the nodes current
        // iterators are pointing to.
        int v1 = it1.top()->data;
        int v2 = it2.top()->data;

        // If we find a pair
        // then count is increased by 1
        if (v1 + v2 == x)
            ans++;

        // Moving forward iterator
        if (v1 + v2 <= x) {
            c = it1.top()->right;
            it1.pop();
            while (c != NULL)
                it1.push(c), c = c->left;
        }

        // Moving backward iterator
        else {
            c = it2.top()->left;
            it2.pop();
            while (c != NULL)
                it2.push(c), c = c->right;
        }
    }

    // Returning final answer
    return ans;
}

// Driver code
int main()
{
    /*    5
        /   \
       3     7
      / \   / \
     2   4 6   8 */
    node* root = new node(5);
    root->left = new node(3);
    root->right = new node(7);
    root->left->left = new node(2);
    root->left->right = new node(4);
    root->right->left = new node(6);
    root->right->right = new node(8);

    int x = 10;

    cout << cntPairs(root, x);

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

// Function to find a pair
static int cntPairs(node root, int x)
{
    // Stack to store nodes for
    // forward and backward iterator
    Stack<node > it1 = new Stack<>();
    Stack<node > it2 = new Stack<>();

    // Initializing forward iterator
    node c = root;
    while (c != null)
    {
        it1.push(c);
        c = c.left;
    }

    // Initializing backward iterator
    c = root;
    while (c != null)
    {
        it2.push(c);
        c = c.right;
    }

    // Variable to store final answer
    int ans = 0;

    // two pointer technique
    while (it1.peek() != it2.peek())
    {

        // Variables to store the
        // value of the nodes current
        // iterators are pointing to.
        int v1 = it1.peek().data;
        int v2 = it2.peek().data;

        // If we find a pair
        // then count is increased by 1
        if (v1 + v2 == x)
            ans++;

        // Moving forward iterator
        if (v1 + v2 <= x)
        {
            c = it1.peek().right;
            it1.pop();
            while (c != null)
            {
                it1.push(c);
                c = c.left;
            }
        }

        // Moving backward iterator
        else
        {
            c = it2.peek().left;
            it2.pop();
            while (c != null)
            {
                it2.push(c);
                c = c.right;
            }
        }
    }

    // Returning final answer
    return ans;
}

// Driver code
public static void main(String[] args)
{
    /* 5
        / \
    3     7
    / \ / \
    2 4 6 8 */
    node root = new node(5);
    root.left = new node(3);
    root.right = new node(7);
    root.left.left = new node(2);
    root.left.right = new node(4);
    root.right.left = new node(6);
    root.right.right = new node(8);

    int x = 10;

    System.out.print(cntPairs(root, x));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python implementation of above algorithm

# Utility class to create a node
class node:
    def __init__(self, key):
        self.data = key
        self.left = self.right = None

# Function to find a pair
def cntPairs( root, x):

    # Stack to store nodes for
    # forward and backward iterator
    it1 = []
    it2 = []

    # Initializing forward iterator
    c = root
    while (c != None):
        it1.append(c)
        c = c.left

    # Initializing backward iterator
    c = root
    while (c != None):
        it2.append(c)
        c = c.right

    # Variable to store final answer
    ans = 0

    # two pointer technique
    while (it1[-1] != it2[-1]) :

        # Variables to store the
        # value of the nodes current
        # iterators are pointing to.
        v1 = it1[-1].data
        v2 = it2[-1].data

        # If we find a pair
        # then count is increased by 1
        if (v1 + v2 == x):
            ans=ans+1

        # Moving forward iterator
        if (v1 + v2 <= x) :
            c = it1[-1].right
            it1.pop()
            while (c != None):
                it1.append(c)
                c = c.left

        # Moving backward iterator
        else :
            c = it2[-1].left
            it2.pop()
            while (c != None):
                it2.append(c)
                c = c.right

    # Returning final answer
    return ans

# Driver code

#         5
#     / \
#     3     7
#     / \ / \
#     2 4 6 8
root = node(5)
root.left = node(3)
root.right = node(7)
root.left.left = node(2)
root.left.right = node(4)
root.right.left = node(6)
root.right.right = node(8)

x = 10

print(cntPairs(root, x))

# This code is contributed by Arnab Kundu
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

// Node of Binary tree
public class node
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

// Function to find a pair
static int cntPairs(node root, int x)
{
    // Stack to store nodes for
    // forward and backward iterator
    Stack<node > it1 = new Stack<node>();
    Stack<node > it2 = new Stack<node>();

    // Initializing forward iterator
    node c = root;
    while (c != null)
    {
        it1.Push(c);
        c = c.left;
    }

    // Initializing backward iterator
    c = root;
    while (c != null)
    {
        it2.Push(c);
        c = c.right;
    }

    // Variable to store readonly answer
    int ans = 0;

    // two pointer technique
    while (it1.Peek() != it2.Peek())
    {

        // Variables to store the
        // value of the nodes current
        // iterators are pointing to.
        int v1 = it1.Peek().data;
        int v2 = it2.Peek().data;

        // If we find a pair
        // then count is increased by 1
        if (v1 + v2 == x)
            ans++;

        // Moving forward iterator
        if (v1 + v2 <= x)
        {
            c = it1.Peek().right;
            it1.Pop();
            while (c != null)
            {
                it1.Push(c);
                c = c.left;
            }
        }

        // Moving backward iterator
        else
        {
            c = it2.Peek().left;
            it2.Pop();
            while (c != null)
            {
                it2.Push(c);
                c = c.right;
            }
        }
    }

    // Returning readonly answer
    return ans;
}

// Driver code
public static void Main(String[] args)
{
    /* 5
        / \
    3     7
    / \ / \
    2 4 6 8 */
    node root = new node(5);
    root.left = new node(3);
    root.right = new node(7);
    root.left.left = new node(2);
    root.left.right = new node(4);
    root.right.left = new node(6);
    root.right.right = new node(8);

    int x = 10;

    Console.Write(cntPairs(root, x));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Node of Binary tree
class node
{
    constructor(data)
    {
        this.data = data;
        this.left = null;
        this.right = null;
    }
};

// Function to find a pair
function cntPairs(root, x)
{

    // Stack to store nodes for
    // forward and backward iterator
    var it1 = [];
    var it2 = [];

    // Initializing forward iterator
    var c = root;

    while (c != null)
    {
        it1.push(c);
        c = c.left;
    }

    // Initializing backward iterator
    c = root;
    while (c != null)
    {
        it2.push(c);
        c = c.right;
    }

    // Variable to store readonly answer
    var ans = 0;

    // two pointer technique
    while (it1[it1.length - 1] != it2[it2.length - 1])
    {

        // Variables to store the
        // value of the nodes current
        // iterators are pointing to.
        var v1 = it1[it1.length - 1].data;
        var v2 = it2[it2.length - 1].data;

        // If we find a pair
        // then count is increased by 1
        if (v1 + v2 == x)
            ans++;

        // Moving forward iterator
        if (v1 + v2 <= x)
        {
            c = it1[it1.length - 1].right;
            it1.pop();

            while (c != null)
            {
                it1.push(c);
                c = c.left;
            }
        }

        // Moving backward iterator
        else
        {
            c = it2[it2.length - 1].left;
            it2.pop();

            while (c != null)
            {
                it2.push(c);
                c = c.right;
            }
        }
    }

    // Returning readonly answer
    return ans;
}

// Driver code
/* 5
    / \
3     7
/ \ / \
2 4 6 8 */
var root = new node(5);
root.left = new node(3);
root.right = new node(7);
root.left.left = new node(2);
root.left.right = new node(4);
root.right.left = new node(6);
root.right.right = new node(8);
var x = 10;

document.write(cntPairs(root, x));

// This code is contributed by noob2000

</script>
```

**Output:** 

```
3
```

**时间复杂度:**O(N)
T3】空间复杂度: O(H)其中 H 是 BST
的高度