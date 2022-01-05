# 从叶节点开始燃烧一棵树的最短时间

> 原文:[https://www . geeksforgeeks . org/从叶节点开始烧树的最短时间/](https://www.geeksforgeeks.org/minimum-time-to-burn-a-tree-starting-from-a-leaf-node/)

给定一棵二叉树和该树上的一个叶节点。众所周知，在 1 秒钟内，所有连接到给定节点(左子节点、右子节点和父节点)的节点都会在 1 秒钟内被烧毁。然后通过一个中间节点连接的所有节点在 2 秒钟内被烧毁，以此类推。任务是找到刻录完整二叉树所需的最短时间。
**例:**

```
Input : 
            1
       /       \
      2          3
    /  \          \
   4    5          6
      /   \         \
     7     8         9
                      \
                       10
Leaf = 8
Output : 7
Initially 8 is set to fire at 0th sec.
            1
       /       \
      2          3
    /  \          \
   4    5          6
      /   \         \
     7     F         9
                      \
                       10
After 1s: 5 is set to fire.
            1
       /       \
      2          3
    /  \          \
   4    F          6
      /   \         \
     7     F         9
                      \
                       10
After 2s: 2, 7 are set to fire.
            1
       /       \
      F          3
    /  \          \
   4    F          6
      /   \         \
     F     F         9
                      \
                       10
After 3s: 4, 1 are set to fire.
            F
       /       \
      F          3
    /  \          \
   F    F          6
      /   \         \
     F     F         9
                      \
                       10
After 4s: 3 is set to fire.
            F
       /       \
      F          F
    /  \          \
   F    F          6
      /   \         \
     F     F         9
                      \
                       10
After 5s: 6 is set to fire.
            F
       /       \
      F          F
    /  \          \
   F    F          F
      /   \         \
     F     F         9
                      \
                       10
After 6s: 9 is set to fire.
            F
       /       \
      F          F
    /  \          \
   F    F          F
      /   \         \
     F     F         F
                      \
                       10
After 7s: 10 is set to fire.
            F
       /       \
      F          F
    /  \          \
   F    F          F
      /   \         \
     F     F         F
                      \
                       F
It takes 7s to burn the complete tree.
```

想法是为每个节点存储附加信息:

*   左子树的深度。
*   右子树的深度。
*   从第一个叶节点燃烧开始，火到达当前节点所需的时间。
*   一个布尔变量，用于检查初始燃烧节点是否在当前节点下的树中。

在继续前进之前，让我们看看下面的树:

```
              1
          /      \          
       2            3
     /   \         /
    4     5       6 
   /     / \
  8     9   10
       /
      11
```

在上面的树中，如果我们设置叶节点 11 为火。

1.  1s 内，火势将到达节点 9。
2.  2 秒后，火势将到达节点 5。
3.  在第 3 秒，火势将到达节点 2 和 10。这里有一个观察:
    *   在 2 秒钟内火力到达 5 号节点。对于节点 5 来说，最初被烧毁的叶子在它的左子树中，因此烧毁右子树所花费的时间将是右子树的高度，即 1。因此，火在(2+1) = 3s 中到达节点 10。
    *   同样，对于节点 2。火从右子树到达 3s 中的节点 2。因此，燃烧左子树所需的时间将是它的高度。

因此，解决方案是应用递归，并为每个节点计算以下要求的值:

*   左深度。
*   右深度。
*   火到达当前节点所需的时间。
*   当前子树包含初始的已烧叶节点。

因此，燃烧任何子树所需的最短时间为:

> 火从最初的焦叶+对侧深度到达根节所需的时间

因此，为了找到刻录完整树所需的时间，我们需要计算每个节点的上述值，并取该值的最大值。

> ans = max(ans，(火到达当前节点所需的时间+其他子树的深度))

以下是上述方法的实现:

## C++

```
// C++ program to find minimum time required
// to burn the binary tree completely

#include <bits/stdc++.h>
using namespace std;

// Tree Node
struct Node {
    int data;
    Node* left;
    Node* right;

    Node()
    {
        left = NULL;
        right = NULL;
    }
};

// Utility function to create a new Node
Node* newNode(int val)
{
    Node* temp = new Node;

    temp->data = val;

    return temp;
}

/*
        ***********ADDITIONAL INFO*************
        lDepth - maximum height of left subtree
        rDepth - maximum height of right subtree
        contains - stores true if tree rooted at current
           node contains the first burnt node time - time to reach
           fire from the initially burnt leaf node to this node
*/
struct Info {
    int lDepth;
    int rDepth;
    bool contains;

    int time;

    Info()
    {
        lDepth = rDepth = 0;
        contains = false;

        time = -1;
    }
};

/*
        Function to calculate time required to burn
        tree completely

        node - address of current node
        info - extra information about current node
        target - node that is fired
        res - stores the result
*/
Info calcTime(Node* node, Info& info, int target, int& res)
{

    // Base case: if root is null
    if (node == NULL) {
        return info;
    }

    // If current node is leaf
    if (node->left == NULL && node->right == NULL) {

        // If current node is the first burnt node
        if (node->data == target) {
            info.contains = true;
            info.time = 0;
        }
        return info;
    }

    // Information about left child of root
    Info leftInfo;
    calcTime(node->left, leftInfo, target, res);

    // Information about right child of root
    Info rightInfo;
    calcTime(node->right, rightInfo, target, res);

    // If left subtree contains the fired node then
    // time required to reach fire to current node
    // will be (1 + time required for left child)
    info.time = (node->left && leftInfo.contains)
                    ? (leftInfo.time + 1)
                    : -1;

    // If right subtree contains the fired node then
    // time required to reach fire to current node
    // will be (1 + time required for right child)
    if (info.time == -1)
        info.time = (node->right && rightInfo.contains)
                        ? (rightInfo.time + 1)
                        : -1;

    // Storing(true or false) if the tree rooted at
    // current node contains the fired node
    info.contains
        = ((node->left && leftInfo.contains)
           || (node->right && rightInfo.contains));

    // Calculate the maximum depth of left subtree
    info.lDepth
        = !(node->left)
              ? 0
              : (1 + max(leftInfo.lDepth, leftInfo.rDepth));

    // Calculate the maximum depth of right subtree
    info.rDepth
        = !(node->right)
              ? 0
              : (1
                 + max(rightInfo.lDepth, rightInfo.rDepth));

    // Calculating answer
    if (info.contains) {
        // If left subtree exists and
        // it contains the fired node
        if (node->left && leftInfo.contains) {
            // calculate result
            res = max(res, info.time + info.rDepth);
        }

        // If right subtree exists and it
        // contains the fired node
        if (node->right && rightInfo.contains) {
            // calculate result
            res = max(res, info.time + info.lDepth);
        }
    }
}

// Driver function to calculate minimum
// time required
int minTime(Node* root, int target)
{
    int res = 0;
    Info info;

    calcTime(root, info, target, res);

    return res;
}

// Driver Code
int main()
{
    Node* root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->left->right = newNode(5);
    root->right->left = newNode(6);
    root->left->left->left = newNode(8);
    root->left->right->left = newNode(9);
    root->left->right->right = newNode(10);
    root->left->right->left->left = newNode(11);

    // target node is 8
    int target = 11;

    cout << minTime(root, target);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum time required
// to burn the binary tree completely

public class GFG {

    // Tree Node
    static class Node {
        int data;
        Node left, right;

        Node(int data)
        {
            this.data = data;
            this.left = null;
            this.right = null;
        }
    }

    /*
        ***********ADDITIONAL INFO*************
        lDepth - maximum height of left subtree
        rDepth - maximum height of right subtree
        contains - stores true if tree rooted at current node
                contains the first burnt node
        time - time to reach fire from the initially burnt leaf
            node to this node
    */
    static class Data {
        int leftDepth, rightDepth, time;
        boolean contains;

        Data()
        {
            contains = false;
            leftDepth = rightDepth = 0;
            time = -1;
        }
    }

    /*
        Function to calculate time required to burn
        tree completely

        node - address of current node
        info - extra information about current node
        target - node that is fired
        res - stores the result
    */
    public static void getResult(Node node, Data data, int target)
    {

        // Base case: if root is null
        if (node == null) {
            return;
        }

        // If current node is leaf
        if (node.left == null && node.right == null) {

            // If current node is the first burnt node
            if (node.data == target) {
                data.contains = true;
                data.time = 0;
            }
            return;
        }

        // Information about left child
        Data leftData = new Data();
        getResult(node.left, leftData, target);

        // Information about right child
        Data rightData = new Data();
        getResult(node.right, rightData, target);

        // If left subtree contains the fired node then
        // time required to reach fire to current node
        // will be (1 + time required for left child)
        data.time = (leftData.contains) ? (leftData.time + 1) : -1;

        // If right subtree contains the fired node then
        // time required to reach fire to current node
        // will be (1 + time required for right child)
        if (data.time == -1)
            data.time = (rightData.contains) ? (rightData.time + 1) : -1;

        // Storing(true or false) if the tree rooted at
        // current node contains the fired node
        data.contains = (leftData.contains || rightData.contains);

        // Calculate the maximum depth of left subtree
        data.leftDepth = (node.left == null) ? 0 : (1 + Math.max(leftData.leftDepth, leftData.rightDepth));

        // Calculate the maximum depth of right subtree
        data.rightDepth = (node.right == null) ? 0 : (1 + Math.max(rightData.leftDepth, rightData.rightDepth));

        // Calculating answer
        if (data.contains) {

            // If left subtree exists and
            // it contains the fired node
            if (leftData.contains) {

                // calculate result
                res = Math.max(res, data.time + data.rightDepth);
            }

            // If right subtree exists and it
            // contains the fired node
            if (rightData.contains) {

                // calculate result
                res = Math.max(res, data.time + data.leftDepth);
            }
        }
    }

    // To store the result
    public static int res;

    // Driver Code
    public static void main(String args[])
    {

        Node root = new Node(1);
        root.left = new Node(2);
        root.right = new Node(3);
        root.left.left = new Node(4);
        root.left.right = new Node(5);
        root.right.left = new Node(6);
        root.left.left.left = new Node(8);
        root.left.right.left = new Node(9);
        root.left.right.right = new Node(10);
        root.left.right.left.left = new Node(11);

        int target = 11;

        res = 0;
        getResult(root, new Data(), target);
        System.out.println(res);
    }
}
```

## 蟒蛇 3

```
# Python program to find minimum time required
# to burn the binary tree completely

# Definition for a  binary tree node

class TreeNode:
    def __init__(self, x):
        self.val = x
        self.left = None
        self.right = None

'''
    ***********ADDITIONAL INFO*************
    lDepth - maximum height of left subtree
    rDepth - maximum height of right subtree
    contains - stores true if tree rooted at current node
               contains the first burnt node
    time - time to reach fire from the initially burnt leaf
           node to this node
'''

class Info:
    def __init__(self):
        self.lDepth = 0
        self.rDepth = 0
        self.contains = False
        self.time = -1

class Solution:
    # Class Variable
    res = 0

    '''
        Function to calculate time required to burn
        tree completely

        node - address of current node
        info - extra information about current node
        target - node that is fired
        res - stores the result
    '''

    def calcTime(self, node, info, target):
        # Base case: if root is null
        if node == None:
            return info

        if node.left == None and node.right == None:
            # If current node is the first burnt node
            if node.val == target:
                info.contains = True
                info.time = 0
            return info

        # Information about left child of root
        leftInfo = Info()
        leftInfo = self.calcTime(node.left, leftInfo, target)

        # Information about right child of root
        rightInfo = Info()
        rightInfo = self.calcTime(node.right, rightInfo, target)

        # If left subtree contains the fired node then
        # time required to reach fire to current node
        # will be (1 + time required for left child)
        info.time = leftInfo.time + \
            1 if (node.left and leftInfo.contains) else -1

        # If right subtree contains the fired node then
        # time required to reach fire to current node
        # will be (1 + time required for right child)
        if info.time == -1:
            info.time = rightInfo.time + \
                1 if (node.right and rightInfo.contains) else -1

        # Storing(true or false) if the tree rooted at
        # current node contains the fired node
        info.contains = (node.left and leftInfo.contains) or (
            node.right and rightInfo.contains)

        # Calculate the maximum depth of left subtree
        info.lDepth = 0 if (not node.left) else (
            1+max(leftInfo.lDepth, leftInfo.rDepth))

        # Calculate the maximum depth of right subtree
        info.rDepth = 0 if (not node.right) else (
            1+max(rightInfo.lDepth, rightInfo.rDepth))

        # Calculating answer
        if info.contains:
            # If left subtree exists and
            # it contains the fired node
            if node.left and leftInfo.contains:
                # calculate result
                self.res = max(self.res, info.time+info.rDepth)

            # If right subtree exists and it
            # contains the fired node
            if node.right and rightInfo.contains:
                # calculate result
                self.res = max(self.res, info.time+info.lDepth)

        return info

    # Driver function to calculate minimum
    # time required
    def solve(self, root, target):
        info = Info()
        self.calcTime(root, info, target)
        return self.res

# Driver Code
if __name__ == '__main__':
    # Construct tree shown in the above example
    root = TreeNode(1)
    root.left = TreeNode(2)
    root.right = TreeNode(3)
    root.left.left = TreeNode(4)
    root.left.right = TreeNode(5)
    root.right.left = TreeNode(6)
    root.left.left.left = TreeNode(8)
    root.left.right.left = TreeNode(9)
    root.left.right.right = TreeNode(10)
    root.left.right.left.left = TreeNode(11)

    # Target Leaf Node
    target = 11

    # Print min time to burn the complete tree
    s = Solution()
    print(s.solve(root, target))

# This code is contributed by Naman Taneja
```

## C#

```
// C# program to find minimum time required
// to burn the binary tree completely
using System;

class GFG
{

    // Tree Node
    class Node
    {
        public int data;
        public Node left, right;

        public Node(int data)
        {
            this.data = data;
            this.left = null;
            this.right = null;
        }
    }

    /*
        ***********ADDITIONAL INFO*************
        lDepth - maximum height of left subtree
        rDepth - maximum height of right subtree
        contains - stores true if tree rooted at current node
                contains the first burnt node
        time - time to reach fire from the initially burnt leaf
            node to this node
    */
    class Data
    {
        public int leftDepth, rightDepth, time;
        public bool contains;

        public Data()
        {
            contains = false;
            leftDepth = rightDepth = 0;
            time = -1;
        }
    }

    /*
        Function to calculate time required to burn
        tree completely

        node - address of current node
        info - extra information about current node
        target - node that is fired
        res - stores the result
    */
    static void getResult(Node node, Data data,
                            int target)
    {

        // Base case: if root is null
        if (node == null)
        {
            return;
        }

        // If current node is leaf
        if (node.left == null &&
            node.right == null)
        {

            // If current node is the first burnt node
            if (node.data == target)
            {
                data.contains = true;
                data.time = 0;
            }
            return;
        }

        // Information about left child
        Data leftData = new Data();
        getResult(node.left, leftData, target);

        // Information about right child
        Data rightData = new Data();
        getResult(node.right, rightData, target);

        // If left subtree contains the fired node then
        // time required to reach fire to current node
        // will be (1 + time required for left child)
        data.time = (leftData.contains) ?
                    (leftData.time + 1) : -1;

        // If right subtree contains the fired node then
        // time required to reach fire to current node
        // will be (1 + time required for right child)
        if (data.time == -1)
            data.time = (rightData.contains) ?
                        (rightData.time + 1) : -1;

        // Storing(true or false) if the tree rooted at
        // current node contains the fired node
        data.contains = (leftData.contains ||
                        rightData.contains);

        // Calculate the maximum depth of left subtree
        data.leftDepth = (node.left == null) ?
                        0 : (1 + Math.Max(
                        leftData.leftDepth,
                        leftData.rightDepth));

        // Calculate the maximum depth of right subtree
        data.rightDepth = (node.right == null) ?
                        0 : (1 + Math.Max(
                        rightData.leftDepth,
                        rightData.rightDepth));

        // Calculating answer
        if (data.contains)
        {

            // If left subtree exists and
            // it contains the fired node
            if (leftData.contains)
            {

                // calculate result
                res = Math.Max(res, data.time +
                                data.rightDepth);
            }

            // If right subtree exists and it
            // contains the fired node
            if (rightData.contains)
            {

                // calculate result
                res = Math.Max(res, data.time +
                                data.leftDepth);
            }
        }
    }

    // To store the result
    public static int res;

    // Driver Code
    public static void Main(String []args)
    {

        Node root = new Node(1);
        root.left = new Node(2);
        root.right = new Node(3);
        root.left.left = new Node(4);
        root.left.right = new Node(5);
        root.right.left = new Node(6);
        root.left.left.left = new Node(8);
        root.left.right.left = new Node(9);
        root.left.right.right = new Node(10);
        root.left.right.left.left = new Node(11);

        int target = 11;

        res = 0;
        getResult(root, new Data(), target);
        Console.WriteLine(res);
    }
}

// This code is contributed by PrinciRaj1992
```

**Output:** 

```
6
```