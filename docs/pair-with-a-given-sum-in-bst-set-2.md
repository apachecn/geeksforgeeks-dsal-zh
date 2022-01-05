# 与 BST | Set 2 中给定的和配对

> 原文:[https://www . geesforgeks . org/pair-with-a-given-sum-in-BST-set-2/](https://www.geeksforgeeks.org/pair-with-a-given-sum-in-bst-set-2/)

给定一个二叉查找树和一个整数 **X** ，任务是检查 BST 中是否存在一对和等于 **X** 的不同节点。如果是，则打印**是**否则打印**否**。

**示例:**

```
Input: X = 5
          5 
        /   \ 
       3     7 
      / \   / \ 
     2   4 6   8
Output: Yes
2 + 3 = 5\. Thus, the answer is "Yes"

Input: X = 10
      1
       \
        2
         \
          3
           \
            4
             \
              5
Output: No
```

**方法:**我们已经在这篇[文章](https://www.geeksforgeeks.org/find-a-pair-with-given-sum-in-bst/)中讨论了基于哈希的方法。这个的空间复杂度是 O(N)，其中 N 是 BST 中的节点数。

在本文中，我们将使用一种空间高效的方法来解决同样的问题，方法是将空间复杂度降低到 O(H)，其中 H 是 BST 的高度。为此，我们将在 BST 上使用两个指针技术。因此，我们将维护一个前向和一个后向迭代器，它们将分别以有序遍历和反向有序遍历的顺序迭代 BST。以下是解决问题的步骤:

1.  为 BST 创建一个向前和向后的迭代器。假设它们所指向的节点的值是 v1 和 v2。
2.  现在在每一步，
    *   如果 v1 + v2 = X，我们找到了一对。
    *   如果 v1 + v2 < x，我们将使前向迭代器指向下一个元素。
    *   如果 v1 + v2 > x，我们将使向后迭代器指向前一个元素。
3.  如果我们没有找到这样的一对，答案将是“没有”。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Node of the binary tree
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

// Function to find a pair with given sum
bool existsPair(node* root, int x)
{
    // Iterators for BST
    stack<node *> it1, it2;

    // Initializing forward iterator
    node* c = root;
    while (c != NULL)
        it1.push(c), c = c->left;

    // Initializing backward iterator
    c = root;
    while (c != NULL)
        it2.push(c), c = c->right;

    // Two pointer technique
    while (it1.top() != it2.top()) {

        // Variables to store values at
        // it1 and it2
        int v1 = it1.top()->data, v2 = it2.top()->data;

        // Base case
        if (v1 + v2 == x)
            return true;

        // Moving forward pointer
        if (v1 + v2 < x) {
            c = it1.top()->right;
            it1.pop();
            while (c != NULL)
                it1.push(c), c = c->left;
        }

        // Moving backward pointer
        else {
            c = it2.top()->left;
            it2.pop();
            while (c != NULL)
                it2.push(c), c = c->right;
        }
    }

    // Case when no pair is found
    return false;
}

// Driver code
int main()
{
    node* root = new node(5);
    root->left = new node(3);
    root->right = new node(7);
    root->left->left = new node(2);
    root->left->right = new node(4);
    root->right->left = new node(6);
    root->right->right = new node(8);

    int x = 5;

    // Calling required function
    if (existsPair(root, x))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Node of the binary tree
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

// Function to find a pair with given sum
static boolean existsPair(node root, int x)
{
    // Iterators for BST
    Stack<node > it1 = new Stack<node>(), it2 = new Stack<node>();

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

    // Two pointer technique
    while (it1.peek() != it2.peek())
    {

        // Variables to store values at
        // it1 and it2
        int v1 = it1.peek().data, v2 = it2.peek().data;

        // Base case
        if (v1 + v2 == x)
            return true;

        // Moving forward pointer
        if (v1 + v2 < x)
        {
            c = it1.peek().right;
            it1.pop();
            while (c != null)
            {
                it1.push(c);
                c = c.left;
            }
        }

        // Moving backward pointer
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

    // Case when no pair is found
    return false;
}

// Driver code
public static void main(String[] args)
{
    node root = new node(5);
    root.left = new node(3);
    root.right = new node(7);
    root.left.left = new node(2);
    root.left.right = new node(4);
    root.right.left = new node(6);
    root.right.right = new node(8);

    int x = 5;

    // Calling required function
    if (existsPair(root, x))
        System.out.print("Yes");
    else
        System.out.print("No");

}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Node of the binary tree
class node:

    def __init__ (self, key):

        self.data = key
        self.left = None
        self.right = None

# Function that returns true if a pair
# with given sum exists in the given BSTs
def existsPair(root1, x):

    # Stack to store nodes for forward
    # and backward iterator
    it1, it2 = [], []

    # Initializing forward iterator
    c = root1
    while (c != None):
        it1.append(c)
        c = c.left

    # Initializing backward iterator
    c = root1
    while (c != None):
        it2.append(c)
        c = c.right

    # Two pointer technique
    while (it1[-1] != it2[-1]):

        # To store the value of the nodes
        # current iterators are pointing to
        v1 = it1[-1].data
        v2 = it2[-1].data

        # Base case
        if (v1 + v2 == x):
            return True

        # Moving forward iterator
        if (v1 + v2 < x):
            c = it1[-1].right
            del it1[-1]

            while (c != None):
                it1.append(c)
                c = c.left

        # Moving backward iterator
        else:
            c = it2[-1].left
            del it2[-1]

            while (c != None):
                it2.append(c)
                c = c.right

    # If no such pair found
    return False

# Driver code
if __name__ == '__main__':

    root2 = node(5)
    root2.left = node(3)
    root2.right = node(7)
    root2.left.left = node(2)
    root2.left.right = node(4)
    root2.right.left = node(6)
    root2.right.right = node(8)

    x = 5

    # Calling required function
    if (existsPair(root2, x)):
        print("Yes")
    else:
        print("No")

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

// Node of the binary tree
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

// Function to find a pair with given sum
static bool existsPair(node root, int x)
{
    // Iterators for BST
    Stack<node > it1 = new Stack<node>(),
                 it2 = new Stack<node>();

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

    // Two pointer technique
    while (it1.Peek() != it2.Peek())
    {

        // Variables to store values at
        // it1 and it2
        int v1 = it1.Peek().data,
            v2 = it2.Peek().data;

        // Base case
        if (v1 + v2 == x)
            return true;

        // Moving forward pointer
        if (v1 + v2 < x)
        {
            c = it1.Peek().right;
            it1.Pop();
            while (c != null)
            {
                it1.Push(c);
                c = c.left;
            }
        }

        // Moving backward pointer
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

    // Case when no pair is found
    return false;
}

// Driver code
public static void Main(String[] args)
{
    node root = new node(5);
    root.left = new node(3);
    root.right = new node(7);
    root.left.left = new node(2);
    root.left.right = new node(4);
    root.right.left = new node(6);
    root.right.right = new node(8);

    int x = 5;

    // Calling required function
    if (existsPair(root, x))
        Console.Write("Yes");
    else
        Console.Write("No");
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
        this.left = this.right = null;
    }
}

// Function to find a pair with given sum
function existsPair(root, x)
{

    // Iterators for BST
    let it1 = [], it2 = [];

    // Initializing forward iterator
    let c = root;
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

    // Two pointer technique
    while (it1[it1.length-1] != it2[it2.length-1])
    {

        // Variables to store values at
        // it1 and it2
        let v1 = it1[it1.length - 1].data,
            v2 = it2[it2.length - 1].data;

        // Base case
        if (v1 + v2 == x)
            return true;

        // Moving forward pointer
        if (v1 + v2 < x)
        {
            c = it1[it1.length - 1].right;
            it1.pop();

            while (c != null)
            {
                it1.push(c);
                c = c.left;
            }
        }

        // Moving backward pointer
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

    // Case when no pair is found
    return false;
}

// Driver code
let root = new node(5);
root.left = new node(3);
root.right = new node(7);
root.left.left = new node(2);
root.left.right = new node(4);
root.right.left = new node(6);
root.right.right = new node(8);

let x = 5;

// Calling required function
if (existsPair(root, x))
    document.write("Yes");
else
    document.write("No");

// This code is contributed by unknown2108

</script>
```

**Output:** 

```
Yes
```

**时间复杂度** : O(N)。
**辅助空间** : O(N)。