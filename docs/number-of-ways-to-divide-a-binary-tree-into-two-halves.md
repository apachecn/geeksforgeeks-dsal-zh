# 将二叉树分成两半的方法数量

> 原文:[https://www . geesforgeks . org/将二叉树分成两半的方法数/](https://www.geeksforgeeks.org/number-of-ways-to-divide-a-binary-tree-into-two-halves/)

给定一棵[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)，任务是计算从树上移除单个边的方法的数量，使得树以相等的和分成两半。
**例:**

```
Input: 
          1 
        /   \ 
      -1     -1 
               \ 
                1 
Output: 1
Only way to do this will be to remove the edge from the right of the root.
After that we will get 2 sub-trees with sum = 0.
   1 
  /
-1

and 

-1
  \
   1
will be the two sub-trees.

Input:
          1 
        /   \ 
      -1     -1 
               \ 
                -1 
Output: 2
```

一个简单的**解决方案是一个接一个地移除树的所有边，并检查这是否将树分成具有相同总和的两半。如果是，我们将把最终答案增加 1。在“N”是树中节点数的最坏情况下，这将花费 O(N <sup>2</sup> )时间。
**高效进场:**** 

1.  **创建一个变量“sum”，并在其中存储二叉树所有元素的总和。我们可以在 O(N)时间内找到二叉树所有元素的和，如这篇[文章](https://www.geeksforgeeks.org/sum-nodes-binary-tree/)所讨论的。**
2.  **现在，我们从根节点开始递归执行以下步骤:

    *   求其右子树所有元素的和(“R”)。如果它等于总和的一半，我们将计数增加 1。这是因为移除连接当前节点及其右子节点的边会将树分成两个总和相等的树。
    *   求其左子树(“L”)所有元素的和。如果它等于总和的一半，我们将计数增加 1。** 

**以下是上述方法的实现:** 

## **C++**

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Node of a binary tree
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

// Function to find the sum of
// all the nodes of BST
int findSum(node* curr)
{
    // If current node is
    // null
    if (curr == NULL)
        return 0;

    // Else
    return curr->data + findSum(curr->left)
           + findSum(curr->right);
}

// Function to recursively check
// if removing any edge divides tree into
// two halves
int checkSum(node* curr, int sum, int& ans)
{
    // Variable to store the
    // sum from left and right
    // child
    int l = 0, r = 0;

    // Checking sum from left sub-tree
    // if its not null
    if (curr->left != NULL) {
        l = checkSum(curr->left, sum, ans);
        if (2 * l == sum)
            ans++;
    }

    // Checking sum from right sub-tree
    // if its not null
    if (curr->right != NULL) {
        r = checkSum(curr->right, sum, ans);
        if (2 * r == sum)
            ans++;
    }

    // Finding the sum of all the elements
    // of current node
    return l + r + curr->data;
}

// Function to return the number
// of ways to remove an edge
int cntWays(node* root)
{
    // If root is null
    if (root == NULL)
        return 0;

    // To store the final answer
    int ans = 0;

    // Sum of all the elements of BST
    int sum = findSum(root);

    // If sum is odd then it won't be possible
    // to break it into two halves
    if (sum % 2 == 1)
        return 0;

    // Calling the checkSum function
    checkSum(root, sum, ans);

    // Returning the final answer
    return ans;
}

// Driver code
int main()
{
    node* root = new node(1);
    root->left = new node(-1);
    root->right = new node(-1);
    root->right->right = new node(1);

    // Print the count of possible ways
    cout << cntWays(root);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java implementation of the approach
class GFG
{

// Node of a binary tree
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
static int ans;

// Function to find the sum of
// all the nodes of BST
static int findSum(node curr)
{
    // If current node is
    // null
    if (curr == null)
        return 0;

    // Else
    return curr.data + findSum(curr.left) +
                       findSum(curr.right);
}

// Function to recursively check
// if removing any edge divides tree
// into two halves
static int checkSum(node curr, int sum)
{
    // Variable to store the
    // sum from left and right
    // child
    int l = 0, r = 0;

    // Checking sum from left sub-tree
    // if its not null
    if (curr.left != null)
    {
        l = checkSum(curr.left, sum);
        if (2 * l == sum)
            ans++;
    }

    // Checking sum from right sub-tree
    // if its not null
    if (curr.right != null)
    {
        r = checkSum(curr.right, sum);
        if (2 * r == sum)
            ans++;
    }

    // Finding the sum of all the elements
    // of current node
    return l + r + curr.data;
}

// Function to return the number
// of ways to remove an edge
static int cntWays(node root)
{
    // If root is null
    if (root == null)
        return 0;

    // To store the final answer
    ans = 0;

    // Sum of all the elements of BST
    int sum = findSum(root);

    // If sum is odd then it won't be possible
    // to break it into two halves
    if (sum % 2 == 1)
        return 0;

    // Calling the checkSum function
    checkSum(root, sum);

    // Returning the final answer
    return ans;
}

// Driver code
public static void main(String[] args)
{
    node root = new node(1);
    root.left = new node(-1);
    root.right = new node(-1);
    root.right.right = new node(1);

    // Print the count of possible ways
    System.out.print(cntWays(root));
}
}

// This code is contributed by PrinciRaj1992
```

## **C#**

```
// C# implementation of the approach
using System;

class GFG
{

// Node of a binary tree
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
static int ans;

// Function to find the sum of
// all the nodes of BST
static int findSum(node curr)
{
    // If current node is
    // null
    if (curr == null)
        return 0;

    // Else
    return curr.data + findSum(curr.left) +
                       findSum(curr.right);
}

// Function to recursively check
// if removing any edge divides tree
// into two halves
static int checkSum(node curr, int sum)
{
    // Variable to store the
    // sum from left and right
    // child
    int l = 0, r = 0;

    // Checking sum from left sub-tree
    // if its not null
    if (curr.left != null)
    {
        l = checkSum(curr.left, sum);
        if (2 * l == sum)
            ans++;
    }

    // Checking sum from right sub-tree
    // if its not null
    if (curr.right != null)
    {
        r = checkSum(curr.right, sum);
        if (2 * r == sum)
            ans++;
    }

    // Finding the sum of all the elements
    // of current node
    return l + r + curr.data;
}

// Function to return the number
// of ways to remove an edge
static int cntWays(node root)
{
    // If root is null
    if (root == null)
        return 0;

    // To store the final answer
    ans = 0;

    // Sum of all the elements of BST
    int sum = findSum(root);

    // If sum is odd then it won't be possible
    // to break it into two halves
    if (sum % 2 == 1)
        return 0;

    // Calling the checkSum function
    checkSum(root, sum);

    // Returning the final answer
    return ans;
}

// Driver code
public static void Main(String[] args)
{
    node root = new node(1);
    root.left = new node(-1);
    root.right = new node(-1);
    root.right.right = new node(1);

    // Print the count of possible ways
    Console.Write(cntWays(root));
}
}

// This code is contributed by Princi Singh
```

## **java 描述语言**

```
<script>
// javascript implementation of the approach   
// Node of a binary tree
class node {
    constructor(val) {
        this.data = val;
        this.prev = null;
        this.next = null;
    }
}

    var ans;

    // Function to find the sum of
    // all the nodes of BST
    function findSum( curr) {
        // If current node is
        // null
        if (curr == null)
            return 0;

        // Else
        return curr.data + findSum(curr.left) + findSum(curr.right);
    }

    // Function to recursively check
    // if removing any edge divides tree
    // into two halves
    function checkSum( curr , sum) {
        // Variable to store the
        // sum from left and right
        // child
        var l = 0, r = 0;

        // Checking sum from left sub-tree
        // if its not null
        if (curr.left != null) {
            l = checkSum(curr.left, sum);
            if (2 * l == sum)
                ans++;
        }

        // Checking sum from right sub-tree
        // if its not null
        if (curr.right != null) {
            r = checkSum(curr.right, sum);
            if (2 * r == sum)
                ans++;
        }

        // Finding the sum of all the elements
        // of current node
        return l + r + curr.data;
    }

    // Function to return the number
    // of ways to remove an edge
    function cntWays( root) {
        // If root is null
        if (root == null)
            return 0;

        // To store the final answer
        ans = 0;

        // Sum of all the elements of BST
        var sum = findSum(root);

        // If sum is odd then it won't be possible
        // to break it into two halves
        if (sum % 2 == 1)
            return 0;

        // Calling the checkSum function
        checkSum(root, sum);

        // Returning the final answer
        return ans;
    }

    // Driver code

         root = new node(1);
        root.left = new node(-1);
        root.right = new node(-1);
        root.right.right = new node(1);

        // Print the count of possible ways
        document.write(cntWays(root));

// This code contributed by Rajput-Ji
</script>
```

## **蟒蛇 3**

```
# Python3 implementation of the approach

# Node of a binary tree
class node:
    def __init__(self,data):
        self.data = data
        self.left = None
        self.right = None

# Function to find the s of
# all the nodes of BST
def findSum(curr):

    # If current node is
    # null
    if (curr == None):
        return 0

    # Else
    return curr.data + findSum(curr.left)+ findSum(curr.right)

# Function to recursively check
# if removing any edge divides tree into
# two halves
def checkSum(curr, s):
    global ans
    # Variable to store the
    # s from left and right
    # child
    l = 0; r = 0

    # Checking s from left sub-tree
    # if its not null
    if (curr.left != None):
        l = checkSum(curr.left, s)
        if (2 * l == s):
            ans+=1

    # Checking s from right sub-tree
    # if its not null
    if (curr.right != None):
        r = checkSum(curr.right, s)
        if (2 * r == s):
            ans+=1

    # Finding the s of all the elements
    # of current node
    return l + r + curr.data

# Function to return the number
# of ways to remove an edge
def cntWays(root):
    # If root is null
    if (root == None):
        return 0

    # To store the final answer
    global ans
    ans = 0

    # s of all the elements of BST
    s = findSum(root)

    # If s is odd then it won't be possible
    # to break it into two halves
    if (s % 2):
        return 0

    # Calling the checkSum function
    checkSum(root, s)

    # Returning the final answer
    return ans

# Driver code
if __name__ == '__main__':

    root = node(1)
    root.left = node(-1)
    root.right = node(-1)
    root.right.right = node(1)

    # Print the count of possible ways
    print(cntWays(root))
```

****Output:** 

```
1
```** 

**该方法的时间复杂度为 0(N)，空间复杂度为 0(H)，其中“N”等于二叉树中的节点数，“H”等于二叉树的高度。**