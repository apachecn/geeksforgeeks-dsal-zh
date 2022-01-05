# 给定两个基站的节点，其和等于 X

> 原文:[https://www . geesforgeks . org/nodes-from-给定-two-BST-with-sum-equal-to-x/](https://www.geeksforgeeks.org/nodes-from-given-two-bsts-with-sum-equal-to-x/)

给定两个二分搜索法树和一个整数 **X** ，任务是找到一对节点，一个属于第一个 BST，第二个属于另一个，这样它们的和等于 **X** 。如果有这样一对，打印**是**否则打印**否**。

**示例:**

```
Input: X = 100
BST 1:
          5 
        /   \ 
       3     7 
      / \   / \ 
     2   4 6   8
BST 2:
     11
      \
       13
Output: No
There is no such pair with given value.

Input: X = 16
BST 1:
          5 
        /   \ 
       3     7 
      / \   / \ 
     2   4 6   8
BST 2:
     11
      \
       13
Output: Yes
5 + 11 = 16
```

**方法:**我们将使用两个指针的方法来解决这个问题。
我们将在第一个 BST 上创建正向迭代器，在第二个 BST 上创建反向迭代器。因此，我们将维护一个向前和向后的迭代器，该迭代器将分别按照顺序遍历和反向顺序遍历的顺序来迭代 BST。

1.  分别为第一个和第二个 BST 创建一个向前和向后的迭代器。假设它们所指向的节点的值是 v1 和 v2。
2.  现在在每一步，
    *   如果 v1 + v2 = X，我们找到了一对。
    *   如果 v1 + v2 小于或等于 x，我们将使前向迭代器指向下一个元素。
    *   如果 v1 + v2 大于 x，我们将使向后迭代器指向前一个元素。
3.  当两个迭代器都指向一个有效节点时，我们将继续上述操作。

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

// Function that returns true if a pair
// with given sum exists in the given BSTs
bool existsPair(node* root1, node* root2, int x)
{
    // Stack to store nodes for forward and backward
    // iterator
    stack<node *> it1, it2;

    // Initializing forward iterator
    node* c = root1;
    while (c != NULL)
        it1.push(c), c = c->left;

    // Initializing backward iterator
    c = root2;
    while (c != NULL)
        it2.push(c), c = c->right;

    // Two pointer technique
    while (it1.size() and it2.size()) {

        // To store the value of the nodes
        // current iterators are pointing to
        int v1 = it1.top()->data, v2 = it2.top()->data;

        // If found a valid pair
        if (v1 + v2 == x)
            return true;

        // Moving forward iterator
        if (v1 + v2 < x) {
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

    // If no such pair found
    return false;
}

// Driver code
int main()
{

    // First BST
    node* root1 = new node(11);
    root1->right = new node(15);

    // Second BST
    node* root2 = new node(5);
    root2->left = new node(3);
    root2->right = new node(7);
    root2->left->left = new node(2);
    root2->left->right = new node(4);
    root2->right->left = new node(6);
    root2->right->right = new node(8);

    int x = 23;

    if (existsPair(root1, root2, x))
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

// Function that returns true if a pair
// with given sum exists in the given BSTs
static boolean existsPair(node root1, node root2, int x)
{
    // Stack to store nodes for forward and backward
    // iterator
    Stack<node> it1 = new Stack(), it2 = new Stack();

    // Initializing forward iterator
    node c = root1;
    while (c != null)
    {
        it1.push(c);
        c = c.left;
    }
    // Initializing backward iterator
    c = root2;
    while (c != null)
    {
        it2.push(c);
        c = c.right;
    }

    // Two pointer technique
    while (it1.size() > 0 && it2.size() > 0)
    {

        // To store the value of the nodes
        // current iterators are pointing to
        int v1 = it1.peek().data, v2 = it2.peek().data;

        // If found a valid pair
        if (v1 + v2 == x)
            return true;

        // Moving forward iterator
        if (v1 + v2 < x)
        {
            c = it1.peek().right;
            it1.pop();
            while (c != null)
            {
                it1.push(c); c = c.left;
            }
        }

        // Moving backward iterator
        else
        {
            c = it2.peek().left;
            it2.pop();
            while (c != null)
            {
                it2.push(c); c = c.right;
            }
        }
    }

    // If no such pair found
    return false;
}

// Driver code
public static void main(String[] args)
{
    // First BST
    node root1 = new node(11);
    root1.right = new node(15);

    // Second BST
    node root2 = new node(5);
    root2.left = new node(3);
    root2.right = new node(7);
    root2.left.left = new node(2);
    root2.left.right = new node(4);
    root2.right.left = new node(6);
    root2.right.right = new node(8);

    int x = 23;

    if (existsPair(root1, root2, x))
        System.out.println("Yes");
    else
        System.out.println("No");
}
}

// This code is contributed by Princi Singh
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
def existsPair(root1, root2, x):

    # Stack to store nodes for forward
    # and backward iterator
    it1, it2 = [], []

    # Initializing forward iterator
    c = root1
    while (c != None):
        it1.append(c)
        c = c.left

    # Initializing backward iterator
    c = root2
    while (c != None):
        it2.append(c)
        c = c.right

    # Two pointer technique
    while (len(it1) > 0 and len(it2) > 0):

        # To store the value of the nodes
        # current iterators are pointing to
        v1 = it1[-1].data
        v2 = it2[-1].data

        # If found a valid pair
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

    # First BST
    root1 = node(11)
    root1.right = node(15)

    # Second BST
    root2 = node(5)
    root2.left = node(3)
    root2.right = node(7)
    root2.left.left = node(2)
    root2.left.right = node(4)
    root2.right.left = node(6)
    root2.right.right = node(8)

    x = 23

    if (existsPair(root1, root2, x)):
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

// Function that returns true if a pair
// with given sum exists in the given BSTs
static bool existsPair(node root1, node root2, int x)
{
    // Stack to store nodes for forward and backward
    // iterator
    Stack<node> it1 = new Stack<node>(), it2 = new Stack<node>();

    // Initializing forward iterator
    node c = root1;
    while (c != null)
    {
        it1.Push(c);
        c = c.left;
    }

    // Initializing backward iterator
    c = root2;
    while (c != null)
    {
        it2.Push(c);
        c = c.right;
    }

    // Two pointer technique
    while (it1.Count > 0 && it2.Count > 0)
    {

        // To store the value of the nodes
        // current iterators are pointing to
        int v1 = it1.Peek().data, v2 = it2.Peek().data;

        // If found a valid pair
        if (v1 + v2 == x)
            return true;

        // Moving forward iterator
        if (v1 + v2 < x)
        {
            c = it1.Peek().right;
            it1.Pop();
            while (c != null)
            {
                it1.Push(c); c = c.left;
            }
        }

        // Moving backward iterator
        else
        {
            c = it2.Peek().left;
            it2.Pop();
            while (c != null)
            {
                it2.Push(c); c = c.right;
            }
        }
    }

    // If no such pair found
    return false;
}

// Driver code
public static void Main(String[] args)
{
    // First BST
    node root1 = new node(11);
    root1.right = new node(15);

    // Second BST
    node root2 = new node(5);
    root2.left = new node(3);
    root2.right = new node(7);
    root2.left.left = new node(2);
    root2.left.right = new node(4);
    root2.right.left = new node(6);
    root2.right.right = new node(8);

    int x = 23;

    if (existsPair(root1, root2, x))
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
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

// Function that returns true if a pair
// with given sum exists in the given BSTs
function existsPair(root1,root2,x)
{
    // Stack to store nodes for forward and backward
    // iterator
    let it1 =[], it2 = [];

    // Initializing forward iterator
    let c = root1;
    while (c != null)
    {
        it1.push(c);
        c = c.left;
    }
    // Initializing backward iterator
    c = root2;
    while (c != null)
    {
        it2.push(c);
        c = c.right;
    }

    // Two pointer technique
    while (it1.length > 0 && it2.length > 0)
    {

        // To store the value of the nodes
        // current iterators are pointing to
        let v1 = it1[it1.length-1].data, v2 = it2[it2.length-1].data;

        // If found a valid pair
        if (v1 + v2 == x)
            return true;

        // Moving forward iterator
        if (v1 + v2 < x)
        {
            c = it1[it1.length-1].right;
            it1.pop();
            while (c != null)
            {
                it1.push(c); c = c.left;
            }
        }

        // Moving backward iterator
        else
        {
            c = it2[it2.length-1].left;
            it2.pop();
            while (c != null)
            {
                it2.push(c); c = c.right;
            }
        }
    }

    // If no such pair found
    return false;
}
// Driver code

// First BST
    let root1 = new node(11);
    root1.right = new node(15);

    // Second BST
    let root2 = new node(5);
    root2.left = new node(3);
    root2.right = new node(7);
    root2.left.left = new node(2);
    root2.left.right = new node(4);
    root2.right.left = new node(6);
    root2.right.right = new node(8);

    let x = 23;

    if (existsPair(root1, root2, x))
        document.write("Yes");
    else
        document.write("No");

// This code is contributed by patel2127
</script>
```

**Output:** 

```
Yes
```

**时间复杂度:**O(N)
T3】辅助空间 : O(N)