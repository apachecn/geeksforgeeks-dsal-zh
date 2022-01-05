# 螺旋形式的反向水平顺序遍历

> 原文:[https://www . geeksforgeeks . org/逆向层次-顺序-螺旋形式遍历/](https://www.geeksforgeeks.org/reverse-level-order-traversal-in-spiral-form/)

给定一棵二叉树，任务是以螺旋的形式打印逆序。

**示例:**

```
Input: 
     1
   /  \
  2    3
 / \  / \
4   5 6  7
Output: 4 5 6 7 3 2 1

Input:
     5
   /   \
  6     4
 / \   / 
7   1 8
 \     \
  3     10
Output: 3 10 8 1 7 6 4 5
```

**方法:**想法是以[反向水平顺序](https://www.geeksforgeeks.org/reverse-level-order-traversal/)的方式遍历树，但稍加修改。我们将使用一个变量**标记**，并将其值设置为 1。当我们完成树的反向级别顺序遍历时，从左到右，我们将把**标志**的值设置为零，这样下次我们从右到左遍历树时，当我们完成遍历时，我们把它的值设置回 1。我们将重复这整个步骤，直到我们完全遍历了二叉树。

下面是上述方法的实现:

## C++

```
// C++ program to print reverse level order
// traversal of a binary tree in spiral form
#include <bits/stdc++.h>
using namespace std;

// Binary tree Node
struct Node {
    struct Node* left;
    struct Node* right;
    int data;

    Node(int data)
    {
        this->data = data;
        this->left = NULL;
        this->right = NULL;
    }
};

// Recursive Function to find height
// of binary tree
int height(struct Node* root)
{
    if (root == NULL)
        return 0;

    // Compute the height of each subtree
    int lheight = height(root->left);
    int rheight = height(root->right);

    // Return the maximum of two
    return max(lheight + 1, rheight + 1);
}

// Function to Print Nodes from right to left
void rightToLeft(struct Node* root, int level)
{
    if (root == NULL)
        return;

    if (level == 1)
        cout << root->data << " ";

    else if (level > 1) {
        rightToLeft(root->right, level - 1);
        rightToLeft(root->left, level - 1);
    }
}

// Function to Print Nodes from left to right
void leftToRight(struct Node* root, int level)
{
    if (root == NULL)
        return;

    if (level == 1)
        cout << root->data << " ";

    else if (level > 1) {
        leftToRight(root->left, level - 1);
        leftToRight(root->right, level - 1);
    }
}

// Function to print Reverse level order traversal
// of a Binary tree in spiral form
void reverseSpiral(struct Node* root)
{
    // Flag is used to mark the change
    // in level
    int flag = 1;

    // Height of tree
    int h = height(root);

    for (int i = h; i >= 1; i--) {

        // If flag value is one print Nodes
        // from left to right
        if (flag == 1) {
            leftToRight(root, i);

            // Mark flag as zero so that next time
            // tree is traversed from right to left
            flag = 0;
        }

        // If flag is zero print Nodes
        // from right to left
        else if (flag == 0) {
            rightToLeft(root, i);

            // Mark flag as one so that next time
            // Nodes are printed from left to right
            flag = 1;
        }
    }
}

// Driver code
int main()
{
    struct Node* root = new Node(5);
    root->left = new Node(9);
    root->right = new Node(3);
    root->left->left = new Node(6);
    root->right->right = new Node(4);
    root->left->left->left = new Node(8);
    root->left->left->right = new Node(7);

    reverseSpiral(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print reverse level order
// traversal of a binary tree in spiral form
class Solution {

    // Binary tree Node
    static class Node {
        Node left;
        Node right;
        int data;

        Node(int data)
        {
            this.data = data;
            this.left = null;
            this.right = null;
        }
    };

    // Recursive Function to find height
    // of binary tree
    static int height(Node root)
    {
        if (root == null)
            return 0;

        // Compute the height of each subtree
        int lheight = height(root.left);
        int rheight = height(root.right);

        // Return the maximum of two
        return Math.max(lheight + 1, rheight + 1);
    }

    // Function to Print Nodes from right to left
    static void rightToLeft(Node root, int level)
    {
        if (root == null)
            return;

        if (level == 1)
            System.out.print(root.data + " ");

        else if (level > 1) {
            rightToLeft(root.right, level - 1);
            rightToLeft(root.left, level - 1);
        }
    }

    // Function to Print Nodes from left to right
    static void leftToRight(Node root, int level)
    {
        if (root == null)
            return;

        if (level == 1)
            System.out.print(root.data + " ");

        else if (level > 1) {
            leftToRight(root.left, level - 1);
            leftToRight(root.right, level - 1);
        }
    }

    // Function to print Reverse level order traversal
    // of a Binary tree in spiral form
    static void reverseSpiral(Node root)
    {
        // Flag is used to mark the change
        // in level
        int flag = 1;

        // Height of tree
        int h = height(root);

        for (int i = h; i >= 1; i--) {

            // If flag value is one print Nodes
            // from left to right
            if (flag == 1) {
                leftToRight(root, i);

                // Mark flag as zero so that next time
                // tree is traversed from right to left
                flag = 0;
            }

            // If flag is zero print Nodes
            // from right to left
            else if (flag == 0) {
                rightToLeft(root, i);

                // Mark flag as one so that next time
                // Nodes are printed from left to right
                flag = 1;
            }
        }
    }

    // Driver code
    public static void main(String args[])
    {
        Node root = new Node(5);
        root.left = new Node(9);
        root.right = new Node(3);
        root.left.left = new Node(6);
        root.right.right = new Node(4);
        root.left.left.left = new Node(8);
        root.left.left.right = new Node(7);

        reverseSpiral(root);
    }
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 program to prreverse level order
# traversal of a binary tree in spiral form

class newNode:

    # Construct to create a newNode
    def __init__(self, key):
        self.data = key
        self.left = None
        self.right = None

# Recursive Function to find height
# of binary tree
def height(root):

    if (root == None):
        return 0

    # Compute the height of each subtree
    lheight = height(root.left)
    rheight = height(root.right)

    # Return the maximum of two
    return max(lheight + 1, rheight + 1)

# Function to PrNodes from right to left
def rightToLeft(root, level):
    if (root == None):
        return

    if (level == 1):
        print(root.data, end =" ")

    elif (level > 1):
        rightToLeft(root.right, level - 1)
        rightToLeft(root.left, level - 1)

# Function to PrNodes from left to right
def leftToRight(root, level):
    if (root == None):
        return

    if (level == 1) :
        print(root.data, end = " ")

    elif (level > 1):
        leftToRight(root.left, level - 1)
        leftToRight(root.right, level - 1)

# Function to prReverse level order traversal
# of a Binary tree in spiral form
def reverseSpiral(root):

    # Flag is used to mark the
    # change in level
    flag = 1

    # Height of tree
    h = height(root)

    for i in range(h, 0, -1):

        # If flag value is one prNodes
        # from left to right
        if (flag == 1):
            leftToRight(root, i)

            # Mark flag as zero so that next time
            # tree is traversed from right to left
            flag = 0

        # If flag is zero prNodes
        # from right to left
        elif (flag == 0):
            rightToLeft(root, i)

            # Mark flag as one so that next time
            # Nodes are printed from left to right
            flag = 1

# Driver Code
if __name__ == '__main__':
    root = newNode(5)
    root.left = newNode(9)
    root.right = newNode(3)
    root.left.left = newNode(6)
    root.right.right = newNode(4)
    root.left.left.left = newNode(8)
    root.left.left.right = newNode(7)

    reverseSpiral(root)

# This code is contributed
# by SHUBHAMSINGH10
```

## C#

```
// C# program to print reverse level order
// traversal of a binary tree in spiral form
using System;

class GFG {

    // Binary tree Node
    public class Node {
        public Node left;
        public Node right;
        public int data;

        public Node(int data)
        {
            this.data = data;
            this.left = null;
            this.right = null;
        }
    };

    // Recursive Function to find height
    // of binary tree
    static int height(Node root)
    {
        if (root == null)
            return 0;

        // Compute the height of each subtree
        int lheight = height(root.left);
        int rheight = height(root.right);

        // Return the maximum of two
        return Math.Max(lheight + 1, rheight + 1);
    }

    // Function to Print Nodes from right to left
    static void rightToLeft(Node root, int level)
    {
        if (root == null)
            return;

        if (level == 1)
            Console.Write(root.data + " ");

        else if (level > 1) {
            rightToLeft(root.right, level - 1);
            rightToLeft(root.left, level - 1);
        }
    }

    // Function to Print Nodes from left to right
    static void leftToRight(Node root, int level)
    {
        if (root == null)
            return;

        if (level == 1)
            Console.Write(root.data + " ");

        else if (level > 1) {
            leftToRight(root.left, level - 1);
            leftToRight(root.right, level - 1);
        }
    }

    // Function to print Reverse level order traversal
    // of a Binary tree in spiral form
    static void reverseSpiral(Node root)
    {
        // Flag is used to mark the change
        // in level
        int flag = 1;

        // Height of tree
        int h = height(root);

        for (int i = h; i >= 1; i--) {

            // If flag value is one print Nodes
            // from left to right
            if (flag == 1) {
                leftToRight(root, i);

                // Mark flag as zero so that next time
                // tree is traversed from right to left
                flag = 0;
            }

            // If flag is zero print Nodes
            // from right to left
            else if (flag == 0) {
                rightToLeft(root, i);

                // Mark flag as one so that next time
                // Nodes are printed from left to right
                flag = 1;
            }
        }
    }

    // Driver code
    public static void Main(String[] args)
    {
        Node root = new Node(5);
        root.left = new Node(9);
        root.right = new Node(3);
        root.left.left = new Node(6);
        root.right.right = new Node(4);
        root.left.left.left = new Node(8);
        root.left.left.right = new Node(7);

        reverseSpiral(root);
    }
}

/* This code is contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>

// Javascript program to print reverse level order
// traversal of a binary tree in spiral form

// Binary tree Node
class Node
{
    constructor(data)
    {
        this.data = data;
        this.left = null;
        this.right = null;
    }
}

// Recursive Function to find height
// of binary tree
function height(root)
{
    if (root == null)
        return 0;

    // Compute the height of each subtree
    let lheight = height(root.left);
    let rheight = height(root.right);

    // Return the maximum of two
    return Math.max(lheight + 1, rheight + 1);
}

// Function to Print Nodes from right to left
function rightToLeft(root, level)
{
    if (root == null)
        return;

    if (level == 1)
        document.write(root.data + " ");

    else if (level > 1)
    {
        rightToLeft(root.right, level - 1);
        rightToLeft(root.left, level - 1);
    }
}

// Function to Print Nodes from left to right
function leftToRight(root, level)
{
    if (root == null)
        return;

    if (level == 1)
        document.write(root.data + " ");

    else if (level > 1)
    {
        leftToRight(root.left, level - 1);
        leftToRight(root.right, level - 1);
    }
}

// Function to print Reverse level order traversal
// of a Binary tree in spiral form
function reverseSpiral(root)
{

    // Flag is used to mark the change
    // in level
    let flag = 1;

    // Height of tree
    let h = height(root);

    for(let i = h; i >= 1; i--)
    {

        // If flag value is one print Nodes
        // from left to right
        if (flag == 1)
        {
            leftToRight(root, i);

            // Mark flag as zero so that next time
            // tree is traversed from right to left
            flag = 0;
        }

        // If flag is zero print Nodes
        // from right to left
        else if (flag == 0)
        {
            rightToLeft(root, i);

            // Mark flag as one so that next time
            // Nodes are printed from left to right
            flag = 1;
        }
    }
}

// Driver code
let root = new Node(5);
root.left = new Node(9);
root.right = new Node(3);
root.left.left = new Node(6);
root.right.right = new Node(4);
root.left.left.left = new Node(8);
root.left.left.right = new Node(7);

reverseSpiral(root);

// This code is contributed by unknown2108

</script>
```

**Output:** 

```
8 7 4 6 9 3 5
```

*时间复杂度分析:*reverseSpiral()的最佳情况时间复杂度在完美二叉树的情况下为 O(n+n/2+n/4…) = O(n)。而最坏的情况时间复杂度是 O(n**2) [O((n)+(n-1)+(n-2)+…]在偏斜树作为输入的情况下。

**迭代实现–**
上述问题可以借助队列和栈来解决。只是执行一个正常的螺旋遍历，使用堆栈来使用反向元素交替。以下是相同的实现–

## C++14

```
#include <bits/stdc++.h>
using namespace std;

// Node structure
struct Node {
    int data;
    Node* left;
    Node* right;
    Node(int val)
    {
        data = val;
        left = right = NULL;
    }
};

// function to perform
// reversal spiral traversal
void reverseSpiral(Node* root)
{
    if (root == NULL) {
        return;
    }
    queue<Node*> q;
    stack<int> s;
    bool reverse = true;
    q.push(root);
    // iterate until queue is empty
    while (!q.empty()) {
        // calculate size of level
        int count = q.size();

        // iterate over level nodes
        for (int i = 0; i < count; i++) {
            Node* curr = q.front();
            q.pop();
            s.push(curr->data);
            if (reverse) {
                if (curr->right) {
                    q.push(curr->right);
                }
                if (curr->left) {
                    q.push(curr->left);
                }
            }
            else {
                if (curr->left) {
                    q.push(curr->left);
                }
                if (curr->right) {
                    q.push(curr->right);
                }
            }
        }
        reverse = !reverse;
    }
    // pop and print reversed nodes
    while (!s.empty()) {
        int curr = s.top();
        cout << curr << " ";
        s.pop();
    }
}

// Driver code
int main()
{
    Node* root = new Node(5);
    root->left = new Node(9);
    root->right = new Node(3);
    root->left->left = new Node(6);
    root->left->right = new Node(4);
    root->left->left->left = new Node(8);
    root->left->left->right = new Node(7);
    reverseSpiral(root);
    return 0;
}
```

## 蟒蛇 3

```
from collections import deque

# Node structure
class Node:
    def __init__(self, x):
        self.data = x
        self.right = None
        self.left = None

# function to perform
# reversal spiral traversal
def reverseSpiral(root):
    if (root == None):
        return

    q =  deque()
    s = []
    reverse = True
    q.append(root)

    # iterate until queue is empty
    while (len(q) > 0):

        # calculate size of level
        count = len(q)

        # iterate over level nodes
        for i in range(count):
            curr = q.popleft()
            s.append(curr.data)
            if (reverse):
                if (curr.right):
                    q.append(curr.right)
                if (curr.left):
                    q.append(curr.left)
            else:
                if (curr.left):
                    q.append(curr.left)
                if (curr.right):
                    q.append(curr.right)

        reverse = not reverse

    # pop and prreversed nodes
    while (len(s) > 0):
        curr = s[-1]
        print(curr, end = " ")
        del s[-1]

# Driver code
if __name__ == '__main__':
    root = Node(5)
    root.left = Node(9)
    root.right = Node(3)
    root.left.left = Node(6)
    root.left.right = Node(4)
    root.left.left.left = Node(8)
    root.left.left.right = Node(7)
    reverseSpiral(root)

# This code is contributed by mohit kumar 29.
```

## java 描述语言

```
<script>

class Node
{
    constructor(data)
    {
        this.data = data;
        this.left = this.right = null;
    }
}

// function to perform
// reversal spiral traversal
function reverseSpiral(root)
{
    if (root == null)
        return
    let q =  [];
    let s = [];
    let reverse = true;

    q.push(root)
    while ((q).length > 0)
    {
        // calculate size of level
        let count = (q).length;

        // iterate over level nodes
        for (let i = 0; i < (count); i++)
        {
            curr = q.shift();
            s.push(curr.data);
            if (reverse)
            {
                if (curr.right)
                    q.push(curr.right);
                if (curr.left)
                    q.push(curr.left);
            }
            else
            {
                if (curr.left)
                    q.push(curr.left);
                if (curr.right)
                    q.push(curr.right);
            }
         }
        reverse = !reverse
    }

    // pop and prreversed nodes
    while ((s).length > 0)
    {
        curr = s.pop();
        document.write(curr+" ");
    }
}

// Driver code
let root = new Node(5)
root.left = new Node(9)
root.right = new Node(3)
root.left.left = new Node(6)
root.left.right = new Node(4)
root.left.left.left = new Node(8)
root.left.left.right = new Node(7)
reverseSpiral(root)

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
8 7 4 6 9 3 5
```

**时间复杂度**:O(N)
T3】辅助空间: O(N)

*改良者:*T2【哈兰德拉辛 22T4】