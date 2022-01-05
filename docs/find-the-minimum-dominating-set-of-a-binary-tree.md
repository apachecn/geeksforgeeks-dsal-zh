# 求二叉树的最小支配集

> 原文:[https://www . geesforgeks . org/find-二叉树的最小支配集/](https://www.geeksforgeeks.org/find-the-minimum-dominating-set-of-a-binary-tree/)

给定一棵节点编号为**【1，N】**的二叉树，任务是找到该树的最小[支配集](https://www.geeksforgeeks.org/dominant-set-of-a-graph/)的大小。

> 如果二叉树中不存在于集合中的每个节点都是该集合中任何节点的直接子节点/父节点，则称该节点集合为**支配节点**。

**示例:**

```
Input: 
                     1
                    /
                   2
                  / \
                 4   3
               /
              5
            /  \
           6    7
          / \    \
         8   9   10
Output:  3
Explanation: 
Smallest dominating set is {2, 6, 7}

Input: 
                     1
                   /   \
                  2     3
                 / \   / \
                4   5 6   7
               / \   /
              8  9  10
Output:  4
Explanation: 
One of the smallest
dominating set = {2, 3, 6, 4}
```

**方法:**
为了解决这个问题，我们使用[动态编程](https://www.geeksforgeeks.org/dynamic-programming/)方法，为每个节点定义以下两种状态:

*   第一种状态**强制**告诉我们是否强制选择集合中的节点。
*   第二种状态**覆盖了**，告诉我们节点的父/子节点是否在集合中。

如果必须选择节点，我们会选择它并将它的子节点标记为覆盖。否则，我们可以选择选择或拒绝它，然后相应地更新它的子对象是否被覆盖。检查每个节点的状态，并相应地找到所需的集合大小。
下面的代码是上述方法的实现:

## C++

```
/* C++ program to find the size of the
minimum dominating set of the tree */

#include <bits/stdc++.h>
using namespace std;

#define N 1005

// Definition of a tree node
struct Node {
    int data;
    Node *left, *right;
};

/* Helper function that allocates a
new node */
Node* newNode(int data)
{
    Node* node = new Node();
    node->data = data;
    node->left = node->right = NULL;
    return node;
}

// DP array to precompute
// and store the results
int dp[N][5][5];

// minDominatingSettion to return the size of
// the minimum dominating set of the array
int minDominatingSet(Node* root, int covered,
                     int compulsory)
{
    // Base case
    if (!root)
        return 0;

    // Setting the compulsory value if needed
    if (!root->left and !root->right and !covered)
        compulsory = true;

    // Check if the answer is already computed
    if (dp[root->data][covered][compulsory] != -1)
        return dp[root->data][covered][compulsory];

    // If it is compulsory to select
    // the node
    if (compulsory) {
        // Choose the node and set its children as covered
        return dp[root->data]
                 [covered]
                 [compulsory]
               = 1
                 + minDominatingSet(
                       root->left, 1, 0)
                 + minDominatingSet(
                       root->right, 1, 0);
    }

    // If it is covered
    if (covered) {
        return dp[root->data]
                 [covered]
                 [compulsory]
               = min(
                   1
                       + minDominatingSet(
                             root->left, 1, 0)
                       + minDominatingSet(
                             root->right, 1, 0),
                   minDominatingSet(
                       root->left, 0, 0)
                       + minDominatingSet(
                             root->right, 0, 0));
    }

    // If the current node is neither covered nor
    // needs to be selected compulsorily
    int ans = 1
              + minDominatingSet(
                    root->left, 1, 0)
              + minDominatingSet(
                    root->right, 1, 0);

    if (root->left) {
        ans = min(ans,
                  minDominatingSet(
                      root->left, 0, 1)
                      + minDominatingSet(
                            root->right, 0, 0));
    }
    if (root->right) {
        ans = min(ans,
                  minDominatingSet(
                      root->left, 0, 0)
                      + minDominatingSet(
                            root->right, 0, 1));
    }

    // Store the result
    return dp[root->data]
             [covered]
             [compulsory]
           = ans;
}

// Driver code
signed main()
{
    // initialising the DP array
    memset(dp, -1, sizeof(dp));

    // Constructing the tree
    Node* root = newNode(1);
    root->left = newNode(2);
    root->left->left = newNode(3);
    root->left->right = newNode(4);
    root->left->left->left = newNode(5);
    root->left->left->left->left = newNode(6);
    root->left->left->left->right = newNode(7);
    root->left->left->left->right->right = newNode(10);
    root->left->left->left->left->left = newNode(8);
    root->left->left->left->left->right = newNode(9);

    cout << minDominatingSet(root, 0, 0) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the size of the
//minimum dominating set of the tree
import java.util.*;

class GFG{

static final int N = 1005;

// Definition of a tree node
static class Node
{
    int data;
    Node left, right;
};

// Helper function that allocates a
// new node
static Node newNode(int data)
{
    Node node = new Node();
    node.data = data;
    node.left = node.right = null;
    return node;
}

// DP array to precompute
// and store the results
static int [][][]dp = new int[N][5][5];

// minDominatingSettion to return the size of
// the minimum dominating set of the array
static int minDominatingSet(Node root,
                            int covered,
                            int compulsory)
{
    // Base case
    if (root == null)
        return 0;

    // Setting the compulsory value if needed
    if (root.left != null &&
       root.right != null &&
       covered > 0)
        compulsory = 1;

    // Check if the answer is already computed
    if (dp[root.data][covered][compulsory] != -1)
        return dp[root.data][covered][compulsory];

    // If it is compulsory to select
    // the node
    if (compulsory > 0)
    {

        // Choose the node and set its
        // children as covered
        return dp[root.data][covered][compulsory] = 1 +
                 minDominatingSet(root.left, 1, 0) +
                 minDominatingSet(root.right, 1, 0);
    }

    // If it is covered
    if (covered > 0)
    {
        return dp[root.data][covered]
                 [compulsory] = Math.min(1 +
                  minDominatingSet(root.left, 1, 0) +
                  minDominatingSet(root.right, 1, 0),
                  minDominatingSet(root.left, 0, 0)+
                  minDominatingSet(root.right, 0, 0));
    }

    // If the current node is neither covered nor
    // needs to be selected compulsorily
    int ans = 1 + minDominatingSet(root.left, 1, 0) +
                  minDominatingSet(root.right, 1, 0);

    if (root.left != null)
    {
        ans = Math.min(ans,
              minDominatingSet(root.left, 0, 1) +
              minDominatingSet(root.right, 0, 0));
    }
    if (root.right != null)
    {
        ans = Math.min(ans,
              minDominatingSet(root.left, 0, 0) +
              minDominatingSet(root.right, 0, 1));
    }

    // Store the result
    return dp[root.data][covered][compulsory] = ans;
}

// Driver code
public static void main(String[] args)
{

    // Initialising the DP array
    for(int i = 0; i < N; i++)
    {
        for(int j = 0; j < 5; j++)
        {
            for(int l = 0; l < 5; l++)
                dp[i][j][l] = -1;
        }
    }

    // Constructing the tree
    Node root = newNode(1);
    root.left = newNode(2);
    root.left.left = newNode(3);
    root.left.right = newNode(4);
    root.left.left.left = newNode(5);
    root.left.left.left.left = newNode(6);
    root.left.left.left.right = newNode(7);
    root.left.left.left.right.right = newNode(10);
    root.left.left.left.left.left = newNode(8);
    root.left.left.left.left.right = newNode(9);

    System.out.print(minDominatingSet(
        root, 0, 0) + "\n");
}
}

// This code is contributed by amal kumar choubey
```

## 蟒蛇 3

```
# Python3 program to find the size of the
# minimum dominating set of the tree */
N = 1005

# Definition of a tree node
class Node:

    def __init__(self, data):

        self.data = data
        self.left = None
        self.right = None

# Helper function that allocates a
# new node
def newNode(data):

    node = Node(data)
    return node

# DP array to precompute
# and store the results
dp = [[[-1 for i in range(5)] for j in range(5)] for k in range(N)];

# minDominatingSettion to return the size of
# the minimum dominating set of the array
def minDominatingSet(root, covered, compulsory):

    # Base case
    if (not root):
        return 0;

    # Setting the compulsory value if needed
    if (not root.left and not root.right and not covered):
        compulsory = True;

    # Check if the answer is already computed
    if (dp[root.data][covered][compulsory] != -1):
        return dp[root.data][covered][compulsory];

    # If it is compulsory to select
    # the node
    if (compulsory):

        dp[root.data][covered][compulsory] = 1 + minDominatingSet(root.left, 1, 0) + minDominatingSet(root.right, 1, 0);

        # Choose the node and set its children as covered
        return dp[root.data][covered][compulsory]

    # If it is covered
    if (covered):
        dp[root.data][covered][compulsory] = min(1 + minDominatingSet(root.left, 1, 0) + minDominatingSet(root.right, 1, 0),minDominatingSet(root.left, 0, 0)+ minDominatingSet(root.right, 0, 0));
        return dp[root.data][covered][compulsory]

    # If the current node is neither covered nor
    # needs to be selected compulsorily
    ans = 1 + minDominatingSet(root.left, 1, 0) + minDominatingSet(root.right, 1, 0);

    if (root.left):
        ans = min(ans, minDominatingSet(root.left, 0, 1) + minDominatingSet(root.right, 0, 0));

    if (root.right):
        ans = min(ans, minDominatingSet( root.left, 0, 0) + minDominatingSet(root.right, 0, 1));

    # Store the result
    dp[root.data][covered][compulsory]= ans;
    return ans

# Driver code
if __name__=='__main__':

    # Constructing the tree
    root = newNode(1);
    root.left = newNode(2);
    root.left.left = newNode(3);
    root.left.right = newNode(4);
    root.left.left.left = newNode(5);
    root.left.left.left.left = newNode(6);
    root.left.left.left.right = newNode(7);
    root.left.left.left.right.right = newNode(10);
    root.left.left.left.left.left = newNode(8);
    root.left.left.left.left.right = newNode(9);

    print(minDominatingSet(root, 0, 0))

  # This code is contributed by rutvik_56
```

## C#

```
// C# program to find the size of the
//minimum dominating set of the tree
using System;
class GFG{

static readonly int N = 1005;

// Definition of a tree node
public class Node
{
    public
 int data;
    public
 Node left, right;
};

// Helper function that allocates a
// new node
public static Node newNode(int data)
{
    Node node = new Node();
    node.data = data;
    node.left = node.right = null;
    return node;
}

// DP array to precompute
// and store the results
static int [,,]dp = new int[N, 5, 5];

// minDominatingSettion to return the size of
// the minimum dominating set of the array
static int minDominatingSet(Node root,
                            int covered,
                            int compulsory)
{
    // Base case
    if (root == null)
        return 0;

    // Setting the compulsory value if needed
    if (root.left != null &&
       root.right != null &&
       covered > 0)
        compulsory = 1;

    // Check if the answer is already computed
    if (dp[root.data, covered, compulsory] != -1)
        return dp[root.data, covered, compulsory];

    // If it is compulsory to select
    // the node
    if (compulsory > 0)
    {

        // Choose the node and set its
        // children as covered
        return dp[root.data, covered, compulsory] = 1 +
                    minDominatingSet(root.left, 1, 0) +
                   minDominatingSet(root.right, 1, 0);
    }

    // If it is covered
    if (covered > 0)
    {
        return dp[root.data, covered, compulsory] = Math.Min(1 +
                             minDominatingSet(root.left, 1, 0) +
                             minDominatingSet(root.right, 1, 0),
                             minDominatingSet(root.left, 0, 0)+
                            minDominatingSet(root.right, 0, 0));
    }

    // If the current node is neither covered nor
    // needs to be selected compulsorily
    int ans = 1 + minDominatingSet(root.left, 1, 0) +
                  minDominatingSet(root.right, 1, 0);

    if (root.left != null)
    {
        ans = Math.Min(ans,
              minDominatingSet(root.left, 0, 1) +
              minDominatingSet(root.right, 0, 0));
    }
    if (root.right != null)
    {
        ans = Math.Min(ans,
              minDominatingSet(root.left, 0, 0) +
              minDominatingSet(root.right, 0, 1));
    }

    // Store the result
    return dp[root.data, covered, compulsory] = ans;
}

// Driver code
public static void Main(String[] args)
{

    // Initialising the DP array
    for(int i = 0; i < N; i++)
    {
        for(int j = 0; j < 5; j++)
        {
            for(int l = 0; l < 5; l++)
                dp[i, j, l] = -1;
        }
    }

    // Constructing the tree
    Node root = newNode(1);
    root.left = newNode(2);
    root.left.left = newNode(3);
    root.left.right = newNode(4);
    root.left.left.left = newNode(5);
    root.left.left.left.left = newNode(6);
    root.left.left.left.right = newNode(7);
    root.left.left.left.right.right = newNode(10);
    root.left.left.left.left.left = newNode(8);
    root.left.left.left.left.right = newNode(9);

    Console.Write(minDominatingSet
                  root, 0, 0) + "\n");
}
}

// This code is contributed by Rohit_ranjan
```

## java 描述语言

```
<script>

    // JavaScript program to find the size of the
    //minimum dominating set of the tree

    let N = 1005;

    // Definition of a tree node
    class Node
    {
       constructor(data) {
           this.left = null;
           this.right = null;
           this.data = data;
        }
    }

    // Helper function that allocates a
    // new node
    function newNode(data)
    {
        let node = new Node(data);
        return node;
    }

    // DP array to precompute
    // and store the results
    let dp = new Array(N);

    // minDominatingSettion to return the size of
    // the minimum dominating set of the array
    function minDominatingSet(root, covered, compulsory)
    {
        // Base case
        if (root == null)
            return 0;

        // Setting the compulsory value if needed
        if (root.left != null &&
           root.right != null &&
           covered > 0)
            compulsory = 1;

        // Check if the answer is already computed
        if (dp[root.data][covered][compulsory] != -1)
            return dp[root.data][covered][compulsory];

        // If it is compulsory to select
        // the node
        if (compulsory > 0)
        {

            // Choose the node and set its
            // children as covered
            return dp[root.data][covered][compulsory] = 1 +
                     minDominatingSet(root.left, 1, 0) +
                     minDominatingSet(root.right, 1, 0);
        }

        // If it is covered
        if (covered > 0)
        {
            return dp[root.data][covered]
                     [compulsory] = Math.min(1 +
                      minDominatingSet(root.left, 1, 0) +
                      minDominatingSet(root.right, 1, 0),
                      minDominatingSet(root.left, 0, 0)+
                      minDominatingSet(root.right, 0, 0));
        }

        // If the current node is neither covered nor
        // needs to be selected compulsorily
        let ans = 1 + minDominatingSet(root.left, 1, 0) +
                      minDominatingSet(root.right, 1, 0);

        if (root.left != null)
        {
            ans = Math.min(ans,
                  minDominatingSet(root.left, 0, 1) +
                  minDominatingSet(root.right, 0, 0));
        }
        if (root.right != null)
        {
            ans = Math.min(ans,
                  minDominatingSet(root.left, 0, 0) +
                  minDominatingSet(root.right, 0, 1));
        }

        // Store the result
        dp[root.data][covered][compulsory] = ans;
        return dp[root.data][covered][compulsory];
    }

    // Initialising the DP array
    for(let i = 0; i < N; i++)
    {
        dp[i] = new Array(5);
        for(let j = 0; j < 5; j++)
        {
            dp[i][j] = new Array(5);
            for(let l = 0; l < 5; l++)
                dp[i][j][l] = -1;
        }
    }

    // Constructing the tree
    let root = newNode(1);
    root.left = newNode(2);
    root.left.left = newNode(3);
    root.left.right = newNode(4);
    root.left.left.left = newNode(5);
    root.left.left.left.left = newNode(6);
    root.left.left.left.right = newNode(7);
    root.left.left.left.right.right = newNode(10);
    root.left.left.left.left.left = newNode(8);
    root.left.left.left.left.right = newNode(9);

    document.write(minDominatingSet(root, 0, 0));

</script>
```

**Output:** 

```
3
```

**时间复杂度:**O(N)
T3】辅助空间: O(N)