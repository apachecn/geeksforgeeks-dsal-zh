# 最短根到叶路径和等于给定数

> 原文:[https://www . geesforgeks . org/最短根到叶路径总和等于给定数字/](https://www.geeksforgeeks.org/shortest-root-to-leaf-path-sum-equal-to-a-given-number/)

给定一棵二叉树和一个数，任务是返回最短路径的长度，从根节点开始，到叶节点结束，这样沿着该路径的数之和等于“和”。如果不存在这样的路径，则打印“-1”。
**例:**

```
Input: 
                 1
             /       \ 
          10         15 
       /      \     
     5        2 
Number = 16 
Output: 2 

There are two paths: 
1->15, length of path is 3
1->10->5, length of path is 2 

Input:
                 1
             /       \ 
          10         15 
       /      \     
     5        2 
Number = 20
Output: -1 
There exists no such path with 20 as sum from root to any node 
```

**来源:** [微软采访](https://www.geeksforgeeks.org/microsoft-interview-experience-set-130-internship/)

**方法**:在这个[帖子](https://www.geeksforgeeks.org/root-to-leaf-path-sum-equal-to-a-given-number/)中已经讨论了一种检查这种路径是否存在的方法。可以按照以下步骤找到最短路径。

*   递归调用路径和级别为的左右子节点(number–当前节点的值，级别+1)。
*   如果到达叶节点，则存储该叶节点所有级别的最小值。

以下是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

/* A binary tree node has data, pointer to left child
and a pointer to right child */
struct Node {
    int data;
    struct Node* left;
    struct Node* right;
};

// Function to find the shortes path from root
// to leaf with given sum
void hasPathSum(struct Node* node, int sum,
                int& mini, int level)
{
    // went beyond tree
    if (node == NULL)
        return;
    int subSum = sum - (node->data);
    if (node->left == NULL && node->right == NULL) {
        // Store the minimum path
        if (subSum == 0)
            mini = min(level - 1, mini);
        return;
    }

    else {
        // Recur in the left tree
        hasPathSum(node->left, subSum, mini, level + 1);

        // Recur in the right tree
        hasPathSum(node->right, subSum, mini, level + 1);
    }
}

/* UTILITY FUNCTIONS */
/* Helper function that allocates a new node with the
given data and NULL left and right pointers. */
struct Node* newnode(int data)
{
    struct Node* node = new Node;
    node->data = data;
    node->left = NULL;
    node->right = NULL;

    return (node);
}

/* Driver program to test above functions*/
int main()
{

    int sum = 16;

    /* Constructed binary tree is

                 1
             /       \
          10         15
       /      \    
     5        2
*/
    struct Node* root = newnode(1);
    root->left = newnode(10);
    root->right = newnode(15);
    root->left->left = newnode(5);
    root->left->right = newnode(2);

    int mini = INT_MAX;

    // Function call
    hasPathSum(root, sum, mini, 0);

    if (mini != INT_MAX)
        printf("There is a root-to-leaf path with sum %d\n"
               "and the shortest path length is: %d",
               sum, mini + 1);
    else
        printf("There is no root-to-leaf path with sum %d", sum);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG
{

static int mini;

/* A binary tree node has data, pointer to left child
and a pointer to right child */
static class Node
{
    int data;
    Node left;
    Node right;
};

// Function to find the shortes path from root
// to leaf with given sum
static void hasPathSum(Node node, int sum,
                int level)
{
    // went beyond tree
    if (node == null)
        return;
    int subSum = sum - (node.data);
    if (node.left == null && node.right == null)
    {
        // Store the minimum path
        if (subSum == 0)
            mini = Math.min(level - 1, mini);
        return;
    }

    else
    {
        // Recur in the left tree
        hasPathSum(node.left, subSum, level + 1);

        // Recur in the right tree
        hasPathSum(node.right, subSum, level + 1);
    }
}

/* UTILITY FUNCTIONS */
/* Helper function that allocates a new node with the
given data and null left and right pointers. */
static Node newnode(int data)
{
    Node node = new Node();
    node.data = data;
    node.left = null;
    node.right = null;

    return (node);
}

/* Driver code*/
public static void main(String[] args)
{
    int sum = 16;

    /* Constructed binary tree is

                1
            / \
        10     15
    / \
    5 2
*/
    Node root = newnode(1);
    root.left = newnode(10);
    root.right = newnode(15);
    root.left.left = newnode(5);
    root.left.right = newnode(2);

    mini = Integer.MAX_VALUE;

    // Function call
    hasPathSum(root, sum, 0);

    if (mini != Integer.MAX_VALUE)
        System.out.printf("There is a root-to-leaf path with sum %d\n"
            +"and the shortest path length is: %d"
                        ,sum, mini + 1);
    else
        System.out.printf("There is no root-to-leaf path with sum %d", sum);

    }
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

INT_MAX = 2147483647

""" A binary tree node has data, pointer
to left child and a pointer to right child """

"""UTILITY FUNCTIONS
Helper function that allocates a new node
with the given data and NULL left and right
pointers."""
class newnode:

    # Construct to create a newNode
    def __init__(self, key):
        self.data = key
        self.left = None
        self.right = None

# Function to find the shortes path
# from root to leaf with given summ
def hasPathSum(node, summ, mini, level) :

    # check if leaf node and check summ
    if (node == None) :
        return
    subsumm = summ - node.data

    if(node.left == None and node.right == None):
        # Store the minimum path
        if (subsumm == 0) :
            mini[0] = min(level - 1, mini[0])
        return

    else:

        # Recur in the left tree
        hasPathSum(node.left, subsumm,
                    mini, level + 1)

        # Recur in the right tree
        hasPathSum(node.right, subsumm,
                    mini, level + 1)

# Driver Code
if __name__ == '__main__':

    summ = 16

    """ Constructed binary tree is

                1
            /     \
        10         15

    /     \           \
    5     2         15
    """
    root = newnode(1)
    root.left = newnode(10)
    root.right = newnode(15)
    root.left.left = newnode(5)
    root.left.right = newnode(2)

    mini = [INT_MAX]

    # Function call
    hasPathSum(root, summ, mini, 0)

    if (mini[0] != INT_MAX) :
        print("There is a root-to-leaf path",
                        "with sum", summ)
        print("and the shortest path length is:",
                                        mini[0] + 1)
    else:
        print("There is no root-to-leaf path",
                            "with sum ", summ)

# This code is contributed by
# Shubham Singh(SHUBHAMSINGH10)
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

static int mini;

/* A binary tree node has data, pointer to left child
and a pointer to right child */
public class Node
{
    public int data;
    public Node left;
    public Node right;
};

// Function to find the shortes path from root
// to leaf with given sum
static void hasPathSum(Node node, int sum,
                int level)
{
    // went beyond tree
    if (node == null)
        return;
    int subSum = sum - (node.data);
    if (node.left == null && node.right == null)
    {
        // Store the minimum path
        if (subSum == 0)
            mini = Math.Min(level - 1, mini);
        return;
    }

    else
    {
        // Recur in the left tree
        hasPathSum(node.left, subSum, level + 1);

        // Recur in the right tree
        hasPathSum(node.right, subSum, level + 1);
    }
}

/* UTILITY FUNCTIONS */
/* Helper function that allocates a new node with the
given data and null left and right pointers. */
static Node newnode(int data)
{
    Node node = new Node();
    node.data = data;
    node.left = null;
    node.right = null;

    return (node);
}

/* Driver code*/
public static void Main(String[] args)
{
    int sum = 16;

    /* Constructed binary tree is

                1
            / \
        10     15
    / \
    5 2
*/
    Node root = newnode(1);
    root.left = newnode(10);
    root.right = newnode(15);
    root.left.left = newnode(5);
    root.left.right = newnode(2);

    mini = int.MaxValue;

    // Function call
    hasPathSum(root, sum, 0);

    if (mini != int.MaxValue)
        Console.Write("There is a root-to-leaf path with sum {0}\n"
            +"and the shortest path length is: {1}"
                        ,sum, mini + 1);
    else
        Console.Write("There is no root-to-leaf path with sum {0}", sum);

    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript implementation of the
// above approach

    /*
     * A binary tree node has data,
     pointer to left child and a pointer to right
     * child
     */

class Node {
        constructor() {
            this.data = 0;
            this.left = null;
            this.right = null;
        }
    }

    // Function to find the shortes path from root
    // to leaf with given sum
    function hasPathSum(node , sum , level) {
        // went beyond tree
        if (node == null)
            return;
        var subSum = sum - (node.data);
        if (node.left == null && node.right == null) {
            // Store the minimum path
            if (subSum == 0)
                mini = Math.min(level - 1, mini);
            return;
        }

        else {
            // Recur in the left tree
            hasPathSum(node.left, subSum, level + 1);

            // Recur in the right tree
            hasPathSum(node.right, subSum, level + 1);
        }
    }

    /* UTILITY FUNCTIONS */
    /*
     * Helper function that allocates a new node with
     the given data and null left
     * and right pointers.
     */
    function newnode(data) {
        var node = new Node();
        node.data = data;
        node.left = null;
        node.right = null;

        return (node);
    }

    /* Driver code */

        var sum = 16;

        /*
         * Constructed binary tree is
         *
         * 1
         / \
        10 15
        / \
        5 2
         */
        var root = newnode(1);
        root.left = newnode(10);
        root.right = newnode(15);
        root.left.left = newnode(5);
        root.left.right = newnode(2);

        mini = Number.MAX_VALUE;

        // Function call
        hasPathSum(root, sum, 0);

        if (mini != Number.MAX_VALUE)
            document.write(
        "There is a root-to-leaf path with sum "+sum+"<br/>" +
        "and the shortest path length is: "+(mini + 1));
        else
            document.write(
            "There is no root-to-leaf path with sum "+ sum
            );

// This code is contributed by todaysgaurav

</script>
```

**Output:** 

```
There is a root-to-leaf path with sum 16
and the shortest path length is: 1
```