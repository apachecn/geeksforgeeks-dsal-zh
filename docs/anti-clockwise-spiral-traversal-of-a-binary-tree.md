# 二叉树的逆时针螺旋遍历

> 原文:[https://www . geesforgeks . org/逆时针-螺旋-遍历二叉树/](https://www.geeksforgeeks.org/anti-clockwise-spiral-traversal-of-a-binary-tree/)

给定一棵二叉树，任务是以逆时针螺旋方式打印树的节点。

**示例:**

```
Input:
     1
   /  \
  2    3
 / \  / \
4   5 6  7 
Output: 1 4 5 6 7 3 2

Input:
      1
     /  \
    2    3
   /    / \
  4    5   6
 / \  /   / \
7   8 9  10  11
Output: 1 7 8 9 10 11 3 2 4 5 6
```

**方法:**想法是用两个变量 I 初始化为 1，j 初始化为树高，运行一个 while 循环，直到我变得大于 j 才会中断。我们将使用另一个变量**标记**并将其初始化为 0。现在，在 while 循环中，我们将检查一个条件，如果**标志**等于 0，我们将从右向左遍历树并将**标志**标记为 1，以便下次我们从左向右遍历树，然后增加 I 的值，以便下次我们访问刚好低于当前级别的级别。同样，当我们从底部遍历级别时，我们将把**标志**标记为 0，以便下次我们从左向右遍历树，然后减少 j 的值，以便下次我们访问当前级别之上的级别。重复整个过程，直到二叉树被完全遍历。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Binary tree node
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
    // Base condition
    if (root == NULL)
        return 0;

    // Compute the height of each subtree
    int lheight = height(root->left);
    int rheight = height(root->right);

    // Return the maximum of two
    return max(1 + lheight, 1 + rheight);
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

// Function to print anti clockwise spiral
// traversal of a binary tree
void antiClockWiseSpiral(struct Node* root)
{
    int i = 1;
    int j = height(root);

    // Flag to mark a change in the direction
    // of printing nodes
    int flag = 0;
    while (i <= j) {

        // If flag is zero print nodes
        // from right to left
        if (flag == 0) {
            rightToLeft(root, i);

            // Set the value of flag as zero
            // so that nodes are next time
            // printed from left to right
            flag = 1;

            // Increment i
            i++;
        }

        // If flag is one print nodes
        // from left to right
        else {
            leftToRight(root, j);

            // Set the value of flag as zero
            // so that nodes are next time
            // printed from right to left
            flag = 0;

            // Decrement j
            j--;
        }
    }
}

// Driver code
int main()
{
    struct Node* root = new Node(1);
    root->left = new Node(2);
    root->right = new Node(3);
    root->left->left = new Node(4);
    root->right->left = new Node(5);
    root->right->right = new Node(7);
    root->left->left->left = new Node(10);
    root->left->left->right = new Node(11);
    root->right->right->left = new Node(8);

    antiClockWiseSpiral(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GfG
{

// Binary tree node
static class Node
{
    Node left;
    Node right;
    int data;

    Node(int data)
    {
        this.data = data;
        this.left = null;
        this.right = null;
    }
}

// Recursive Function to find height
// of binary tree
static int height(Node root)
{
    // Base condition
    if (root == null)
        return 0;

    // Compute the height of each subtree
    int lheight = height(root.left);
    int rheight = height(root.right);

    // Return the maximum of two
    return Math.max(1 + lheight, 1 + rheight);
}

// Function to Print Nodes from left to right
static void leftToRight(Node root, int level)
{
    if (root == null)
        return;

    if (level == 1)
        System.out.print(root.data + " ");

    else if (level > 1)
    {
        leftToRight(root.left, level - 1);
        leftToRight(root.right, level - 1);
    }
}

// Function to Print Nodes from right to left
static void rightToLeft(Node root, int level)
{
    if (root == null)
        return;

    if (level == 1)
        System.out.print(root.data + " ");

    else if (level > 1)
    {
        rightToLeft(root.right, level - 1);
        rightToLeft(root.left, level - 1);
    }
}

// Function to print anti clockwise spiral
// traversal of a binary tree
static void antiClockWiseSpiral(Node root)
{
    int i = 1;
    int j = height(root);

    // Flag to mark a change in the direction
    // of printing nodes
    int flag = 0;
    while (i <= j)
    {

        // If flag is zero print nodes
        // from right to left
        if (flag == 0)
        {
            rightToLeft(root, i);

            // Set the value of flag as zero
            // so that nodes are next time
            // printed from left to right
            flag = 1;

            // Increment i
            i++;
        }

        // If flag is one print nodes
        // from left to right
        else {
            leftToRight(root, j);

            // Set the value of flag as zero
            // so that nodes are next time
            // printed from right to left
            flag = 0;

            // Decrement j
            j--;
        }
    }
}

// Driver code
public static void main(String[] args)
{
    Node root = new Node(1);
    root.left = new Node(2);
    root.right = new Node(3);
    root.left.left = new Node(4);
    root.right.left = new Node(5);
    root.right.right = new Node(7);
    root.left.left.left = new Node(10);
    root.left.left.right = new Node(11);
    root.right.right.left = new Node(8);

    antiClockWiseSpiral(root);
}
}

// This code is contributed by Prerna Saini.
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Binary tree node
class newNode:

    # Constructor to create a newNode
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None
        self.visited = False

# Recursive Function to find height
# of binary tree
def height(root):

    # Base condition
    if (root == None):
        return 0

    # Compute the height of each subtree
    lheight = height(root.left)
    rheight = height(root.right)

    # Return the maximum of two
    return max(1 + lheight, 1 + rheight)

# Function to PrNodes from left to right
def leftToRight(root, level):

    if (root == None):
        return

    if (level == 1):
        print(root.data, end = " ")

    elif (level > 1):
        leftToRight(root.left, level - 1)
        leftToRight(root.right, level - 1)

# Function to PrNodes from right to left
def rightToLeft(root, level):

    if (root == None) :
        return

    if (level == 1):
        print(root.data, end = " ")

    elif (level > 1):
        rightToLeft(root.right, level - 1)
        rightToLeft(root.left, level - 1)

# Function to print anti clockwise spiral
# traversal of a binary tree
def antiClockWiseSpiral(root):

    i = 1
    j = height(root)

    # Flag to mark a change in the
    # direction of printing nodes
    flag = 0
    while (i <= j):

        # If flag is zero prnodes
        # from right to left
        if (flag == 0):
            rightToLeft(root, i)

            # Set the value of flag as zero
            # so that nodes are next time
            # printed from left to right
            flag = 1

            # Increment i
            i += 1

        # If flag is one prnodes
        # from left to right
        else:
            leftToRight(root, j)

            # Set the value of flag as zero
            # so that nodes are next time
            # printed from right to left
            flag = 0

            # Decrement j
            j-=1

# Driver Code
if __name__ == '__main__':
    root = newNode(1)
    root.left = newNode(2)
    root.right = newNode(3)
    root.left.left = newNode(4)
    root.right.left = newNode(5)
    root.right.right = newNode(7)
    root.left.left.left = newNode(10)
    root.left.left.right = newNode(11)
    root.right.right.left = newNode(8)

    antiClockWiseSpiral(root)

# This code is contributed by
# SHUBHAMSINGH10
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Binary tree node
public class Node
{
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
static int height( Node root)
{
    // Base condition
    if (root == null)
        return 0;

    // Compute the height of each subtree
    int lheight = height(root.left);
    int rheight = height(root.right);

    // Return the maximum of two
    return Math.Max(1 + lheight, 1 + rheight);
}

// Function to Print Nodes from left to right
static void leftToRight( Node root, int level)
{
    if (root == null)
        return;

    if (level == 1)
        Console.Write( root.data + " ");

    else if (level > 1)
    {
        leftToRight(root.left, level - 1);
        leftToRight(root.right, level - 1);
    }
}

// Function to Print Nodes from right to left
static void rightToLeft( Node root, int level)
{
    if (root == null)
        return;

    if (level == 1)
        Console.Write( root.data + " ");

    else if (level > 1)
    {
        rightToLeft(root.right, level - 1);
        rightToLeft(root.left, level - 1);
    }
}

// Function to print anti clockwise spiral
// traversal of a binary tree
static void antiClockWiseSpiral( Node root)
{
    int i = 1;
    int j = height(root);

    // Flag to mark a change in the direction
    // of printing nodes
    int flag = 0;
    while (i <= j)
    {

        // If flag is zero print nodes
        // from right to left
        if (flag == 0)
        {
            rightToLeft(root, i);

            // Set the value of flag as zero
            // so that nodes are next time
            // printed from left to right
            flag = 1;

            // Increment i
            i++;
        }

        // If flag is one print nodes
        // from left to right
        else
        {
            leftToRight(root, j);

            // Set the value of flag as zero
            // so that nodes are next time
            // printed from right to left
            flag = 0;

            // Decrement j
            j--;
        }
    }
}

// Driver code
public static void Main(String []args)
{
    Node root = new Node(1);
    root.left = new Node(2);
    root.right = new Node(3);
    root.left.left = new Node(4);
    root.right.left = new Node(5);
    root.right.right = new Node(7);
    root.left.left.left = new Node(10);
    root.left.left.right = new Node(11);
    root.right.right.left = new Node(8);

    antiClockWiseSpiral(root);

}
}

//This code is contributed by Arnab Kundu
```

## java 描述语言

```
<script>

    // JavaScript implementation of the approach

    // Binary tree node
    class Node
    {
        constructor(data) {
           this.left = null;
           this.right = null;
           this.data = data;
        }
    }

    // Recursive Function to find height
    // of binary tree
    function height(root)
    {
        // Base condition
        if (root == null)
            return 0;

        // Compute the height of each subtree
        let lheight = height(root.left);
        let rheight = height(root.right);

        // Return the maximum of two
        return Math.max(1 + lheight, 1 + rheight);
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

    // Function to print anti clockwise spiral
    // traversal of a binary tree
    function antiClockWiseSpiral(root)
    {
        let i = 1;
        let j = height(root);

        // Flag to mark a change in the direction
        // of printing nodes
        let flag = 0;
        while (i <= j)
        {

            // If flag is zero print nodes
            // from right to left
            if (flag == 0)
            {
                rightToLeft(root, i);

                // Set the value of flag as zero
                // so that nodes are next time
                // printed from left to right
                flag = 1;

                // Increment i
                i++;
            }

            // If flag is one print nodes
            // from left to right
            else {
                leftToRight(root, j);

                // Set the value of flag as zero
                // so that nodes are next time
                // printed from right to left
                flag = 0;

                // Decrement j
                j--;
            }
        }
    }

    let root = new Node(1);
    root.left = new Node(2);
    root.right = new Node(3);
    root.left.left = new Node(4);
    root.right.left = new Node(5);
    root.right.right = new Node(7);
    root.left.left.left = new Node(10);
    root.left.left.right = new Node(11);
    root.right.right.left = new Node(8);

    antiClockWiseSpiral(root);

</script>
```

**输出:**

```
1 10 11 8 3 2 4 5 7 
```

**另一种方法:**
由于每次调用打印级别，上述方法具有 O(n^2)最坏情况的复杂性。对它的改进可以是存储水平方向的节点并使用它来打印。

## C++

```
// C++ implementation of the above approach

#include <bits/stdc++.h>
using namespace std;

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

void antiClockWiseSpiral(struct Node* root)
{
    // Initialize the queue
    queue<Node*> q;

    // Add the root node
    q.push(root);

    //  Initialize the vector
    vector<Node*> topone;

    // Until queue is not empty
    while (!q.empty()) {
        int len = q.size();

        // len is greater than zero
        while (len > 0) {
            Node* nd = q.front();
            q.pop();
            if (nd != NULL) {
                topone.push_back(nd);
                if (nd->right != NULL)
                    q.push(nd->right);
                if (nd->left != NULL)
                    q.push(nd->left);
            }
            len--;
        }
        topone.push_back(NULL);
    }
    bool top = true;
    int l = 0, r = (int)topone.size() - 2;

    while (l < r) {
        if (top) {
            while (l < (int)topone.size()) {
                Node* nd = topone[l++];
                if (nd == NULL) {
                    break;
                }
                cout << nd->data << " ";
            }
        }
        else {
            while (r >= l) {
                Node* nd = topone[r--];
                if (nd == NULL)
                    break;
                cout << nd->data << " ";
            }
        }
        top = !top;
    }
}

// Build Tree
int main()
{
    /*
               1
            2     3
          4     5   7
         10 11     8
   */

    struct Node* root = new Node(1);
    root->left = new Node(2);
    root->right = new Node(3);
    root->left->left = new Node(4);
    root->right->left = new Node(5);
    root->right->right = new Node(7);
    root->left->left->left = new Node(10);
    root->left->left->right = new Node(11);
    root->right->right->left = new Node(8);

    antiClockWiseSpiral(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach

import java.io.*;
import java.util.*;

class GFG {

    // Structure of each node
    class Node {
        int val;
        Node left, right;
        Node(int val)
        {
            this.val = val;
            this.left = this.right = null;
        }
    }

    private void work(Node root)
    {
        // Initialize queue
        Queue<Node> q = new LinkedList<>();

        // Add the root node
        q.add(root);

        // Initialize the vector
        Vector<Node> topone = new Vector<>();

        // Until queue is not empty
        while (!q.isEmpty()) {
            int len = q.size();

            // len is greater than zero
            while (len > 0) {
                Node nd = q.poll();
                if (nd != null) {
                    topone.add(nd);
                    if (nd.right != null)
                        q.add(nd.right);
                    if (nd.left != null)
                        q.add(nd.left);
                }
                len--;
            }
            topone.add(null);
        }
        boolean top = true;
        int l = 0, r = topone.size() - 2;

        while (l < r) {
            if (top) {
                while (l < topone.size()) {
                    Node nd = topone.get(l++);
                    if (nd == null) {
                        break;
                    }
                    System.out.print(nd.val + " ");
                }
            }
            else {
                while (r >= l) {
                    Node nd = topone.get(r--);
                    if (nd == null)
                        break;
                    System.out.print(nd.val + " ");
                }
            }
            top = !top;
        }
    }

    // Build Tree
    public void solve()
    {
        /*
                            1
                         2     3
                       4     5   7
                      10 11     8
                    */

        Node root = new Node(1);
        root.left = new Node(2);
        root.right = new Node(3);
        root.left.left = new Node(4);
        root.right.left = new Node(5);
        root.right.right = new Node(7);
        root.left.left.left = new Node(10);
        root.left.left.right = new Node(11);
        root.right.right.left = new Node(8);

        // Function call
        work(root);
    }

    // Driver Code
    public static void main(String[] args)
    {
        GFG t = new GFG();
        t.solve();
    }
}
```

## 蟒蛇 3

```
# Python 3 implementation of the above approach

from collections import  deque as dq

class Node:
    def __init__(self, data):

        self.data = data
        self.left = None
        self.right = None

def antiClockWiseSpiral(root):

    # Initialize the queue
    q=dq([root])

    # Initialize the list
    topone=[]

    # Until queue is not empty
    while (q):
        l = len(q)

        # l is greater than zero
        while (l > 0):
            nd = q.popleft()
            if (nd != None):
                topone.append(nd)
                if (nd.right != None):
                    q.append(nd.right)
                if (nd.left != None):
                    q.append(nd.left)
            l-=1

        topone.append(None)

    top = True
    l = 0; r = len(topone) - 2

    while (l < r):
        if (top):
            while (l < len(topone)):
                nd = topone[l]
                l+=1
                if (nd == None):
                    break
                print(nd.data,end=" ")
        else:
            while (r >= l):
                nd = topone[r]
                r-=1
                if (nd == None):
                    break
                print(nd.data,end=" ")

        top = not top
    print()

# Build Tree
if __name__ == '__main__':

    #        1
    #     2     3
    #   4     5  7
    # 10 11     8

    root = Node(1)
    root.left = Node(2)
    root.right =  Node(3)
    root.left.left = Node(4)
    root.right.left = Node(5)
    root.right.right = Node(7)
    root.left.left.left = Node(10)
    root.left.left.right = Node(11)
    root.right.right.left = Node(8)

    antiClockWiseSpiral(root)
```

**输出:**

```
1 10 11 8 3 2 4 5 7 
```

**时间复杂度:**O(N)
T3】辅助空间: O(N)