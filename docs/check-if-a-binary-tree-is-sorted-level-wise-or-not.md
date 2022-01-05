# 检查二叉树是否按级别排序

> 原文:[https://www . geesforgeks . org/check-if-a-binary-tree-is-sorted-level-wise-or-not/](https://www.geeksforgeeks.org/check-if-a-binary-tree-is-sorted-level-wise-or-not/)

给定一棵二叉树。任务是检查二叉树是否按级别排序。如果最大值(i-1 <sup>第</sup>级)小于最小值(i <sup>第</sup>级)，则对二叉树进行级别排序。
**例** :

```
Input :        1 
              / \
             /   \
            2     3
           / \   / \
          /   \ /   \
         4    5 6    7
Output : Sorted

Input:         1 
              / 
             4 
            / \
           6   5
                \
                 2
Output: Not sorted
```

**简单解法**:简单解法就是比较每一个相邻的 I 级和 i+1 的最小值和最大值。遍历 i <sup>第</sup>和 i+1 <sup>第</sup>级，将 i+1 <sup>第</sup>级的最小值与 i <sup>第</sup>级的最大值进行比较，返回结果。
时间复杂度:O(n <sup>2</sup> )。
**高效解决方案**:高效的解决方案是进行级别顺序遍历，跟踪当前级别的最小值和最大值。使用变量 *prevMax* 存储上一级的最大值。然后将当前级别的最小值与前一级别的最大值 *pevMax* 进行比较。如果最小值大于*上一个最大值*，那么给定的树被逐级排序到当前级别。对于下一个级别， *prevMax* 等于当前级别的最大值。所以用当前电平的最大值更新 *prevMax* 。重复此操作，直到给定树的所有级别都没有被遍历。
以下是上述方法的实施:

## C++

```
// CPP program to determine whether
// binary tree is level sorted or not.

#include <bits/stdc++.h>
using namespace std;

// Structure of a tree node.
struct Node {
    int key;
    Node *left, *right;
};

// Function to create new tree node.
Node* newNode(int key)
{
    Node* temp = new Node;
    temp->key = key;
    temp->left = temp->right = NULL;
    return temp;
}

// Function to determine if
// given binary tree is level sorted
// or not.
int isSorted(Node* root)
{

    // to store maximum value of previous
    // level.
    int prevMax = INT_MIN;

    // to store minimum value of current
    // level.
    int minval;

    // to store maximum value of current
    // level.
    int maxval;

    // to store number of nodes in current
    // level.
    int levelSize;

    // queue to perform level order traversal.
    queue<Node*> q;
    q.push(root);

    while (!q.empty()) {

        // find number of nodes in current
        // level.
        levelSize = q.size();

        minval = INT_MAX;
        maxval = INT_MIN;

        // traverse current level and find
        // minimum and maximum value of
        // this level.
        while (levelSize > 0) {
            root = q.front();
            q.pop();

            levelSize--;

            minval = min(minval, root->key);
            maxval = max(maxval, root->key);

            if (root->left)
                q.push(root->left);

            if (root->right)
                q.push(root->right);
        }

        // if minimum value of this level
        // is not greater than maximum
        // value of previous level then
        // given tree is not level sorted.
        if (minval <= prevMax)
            return 0;

        // maximum value of this level is
        // previous maximum value for
        // next level.
        prevMax = maxval;
    }

    return 1;
}

// Driver program
int main()
{
    /*
            1
           /
          4  
           \
            6
           / \
          8   9
         /     \
        12     10
    */

    Node* root = newNode(1);
    root->left = newNode(4);
    root->left->right = newNode(6);
    root->left->right->left = newNode(8);
    root->left->right->right = newNode(9);
    root->left->right->left->left = newNode(12);
    root->left->right->right->right = newNode(10);

    if (isSorted(root))
        cout << "Sorted";
    else
        cout << "Not sorted";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to determine whether
// binary tree is level sorted or not.
import java.util.*;

class GfG {

// Structure of a tree node.
static class Node {
    int key;
    Node left, right;
}

// Function to create new tree node.
static Node newNode(int key)
{
    Node temp = new Node();
    temp.key = key;
    temp.left = null;
    temp.right = null;
    return temp;
}

// Function to determine if
// given binary tree is level sorted
// or not.
static int isSorted(Node root)
{

    // to store maximum value of previous
    // level.
    int prevMax = Integer.MIN_VALUE;

    // to store minimum value of current
    // level.
    int minval;

    // to store maximum value of current
    // level.
    int maxval;

    // to store number of nodes in current
    // level.
    int levelSize;

    // queue to perform level order traversal.
    Queue<Node> q = new LinkedList<Node> ();
    q.add(root);

    while (!q.isEmpty()) {

        // find number of nodes in current
        // level.
        levelSize = q.size();

        minval = Integer.MAX_VALUE;
        maxval = Integer.MIN_VALUE;

        // traverse current level and find
        // minimum and maximum value of
        // this level.
        while (levelSize > 0) {
            root = q.peek();
            q.remove();

            levelSize--;

            minval = Math.min(minval, root.key);
            maxval = Math.max(maxval, root.key);

            if (root.left != null)
                q.add(root.left);

            if (root.right != null)
                q.add(root.right);
        }

        // if minimum value of this level
        // is not greater than maximum
        // value of previous level then
        // given tree is not level sorted.
        if (minval <= prevMax)
            return 0;

        // maximum value of this level is
        // previous maximum value for
        // next level.
        prevMax = maxval;
    }

    return 1;
}

// Driver program
public static void main(String[] args)
{
    /*
            1
        /
        4
        \
            6
        / \
        8 9
        /     \
        12     10
    */

    Node root = newNode(1);
    root.left = newNode(4);
    root.left.right = newNode(6);
    root.left.right.left = newNode(8);
    root.left.right.right = newNode(9);
    root.left.right.left.left = newNode(12);
    root.left.right.right.right = newNode(10);

    if (isSorted(root) == 1)
        System.out.println("Sorted");
    else
        System.out.println("Not sorted");
}
}
```

## 蟒蛇 3

```
# Python3 program to determine whether
# binary tree is level sorted or not.
from queue import Queue

# Function to create new tree node.
class newNode:
    def __init__(self, key):
        self.key = key
        self.left = self.right = None

# Function to determine if given binary
# tree is level sorted or not.
def isSorted(root):

    # to store maximum value of previous
    # level.
    prevMax = -999999999999

    # to store minimum value of current
    # level.
    minval = None

    # to store maximum value of current
    # level.
    maxval = None

    # to store number of nodes in current
    # level.
    levelSize = None

    # queue to perform level order traversal.
    q = Queue()
    q.put(root)

    while (not q.empty()):

        # find number of nodes in current
        # level.
        levelSize = q.qsize()

        minval = 999999999999
        maxval = -999999999999

        # traverse current level and find
        # minimum and maximum value of
        # this level.
        while (levelSize > 0):
            root = q.queue[0]
            q.get()

            levelSize -= 1

            minval = min(minval, root.key)
            maxval = max(maxval, root.key)

            if (root.left):
                q.put(root.left)

            if (root.right):
                q.put(root.right)

        # if minimum value of this level
        # is not greater than maximum
        # value of previous level then
        # given tree is not level sorted.
        if (minval <= prevMax):
            return 0

        # maximum value of this level is
        # previous maximum value for
        # next level.
        prevMax = maxval
    return 1

# Driver Code
if __name__ == '__main__':

    #
    #     1
    #     /
    #     4
    #     \
    #     6
    #     / \
    #     8 9
    #     /     \
    # 12     10
    root = newNode(1)
    root.left = newNode(4)
    root.left.right = newNode(6)
    root.left.right.left = newNode(8)
    root.left.right.right = newNode(9)
    root.left.right.left.left = newNode(12)
    root.left.right.right.right = newNode(10)

    if (isSorted(root)):
        print("Sorted")
    else:
        print("Not sorted")

# This code is contributed by PranchalK
```

## C#

```
// C# program to determine whether
// binary tree is level sorted or not.
using System;
using System.Collections.Generic;

class GFG
{

// Structure of a tree node.
public class Node
{
    public int key;
    public Node left, right;
}

// Function to create new tree node.
static Node newNode(int key)
{
    Node temp = new Node();
    temp.key = key;
    temp.left = null;
    temp.right = null;
    return temp;
}

// Function to determine if
// given binary tree is level sorted
// or not.
static int isSorted(Node root)
{

    // to store maximum value of previous
    // level.
    int prevMax = int.MinValue;

    // to store minimum value of current
    // level.
    int minval;

    // to store maximum value of current
    // level.
    int maxval;

    // to store number of nodes in current
    // level.
    int levelSize;

    // queue to perform level order traversal.
    Queue<Node> q = new Queue<Node> ();
    q.Enqueue(root);

    while (q.Count != 0)
    {

        // find number of nodes in current
        // level.
        levelSize = q.Count;

        minval = int.MaxValue;
        maxval = int.MinValue;

        // traverse current level and find
        // minimum and maximum value of
        // this level.
        while (levelSize > 0)
        {
            root = q.Peek();
            q.Dequeue();

            levelSize--;

            minval = Math.Min(minval, root.key);
            maxval = Math.Max(maxval, root.key);

            if (root.left != null)
                q.Enqueue(root.left);

            if (root.right != null)
                q.Enqueue(root.right);
        }

        // if minimum value of this level
        // is not greater than maximum
        // value of previous level then
        // given tree is not level sorted.
        if (minval <= prevMax)
            return 0;

        // maximum value of this level is
        // previous maximum value for
        // next level.
        prevMax = maxval;
    }

    return 1;
}

// Driver Code
public static void Main(String[] args)
{
    /*
            1
        /
        4
        \
            6
        / \
        8 9
        /     \
        12     10
    */
    Node root = newNode(1);
    root.left = newNode(4);
    root.left.right = newNode(6);
    root.left.right.left = newNode(8);
    root.left.right.right = newNode(9);
    root.left.right.left.left = newNode(12);
    root.left.right.right.right = newNode(10);

    if (isSorted(root) == 1)
        Console.WriteLine("Sorted");
    else
        Console.WriteLine("Not sorted");
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// JavaScript program to determine whether
// binary tree is level sorted or not.

// Structure of a tree node.
class Node
{
    constructor()
    {
        this.key = null;
        this.left = null;
        this.right = null;
    }
}

// Function to create new tree node.
function newNode(key)
{
    var temp = new Node();
    temp.key = key;
    temp.left = null;
    temp.right = null;
    return temp;
}

// Function to determine if
// given binary tree is level sorted
// or not.
function isSorted(root)
{

    // to store maximum value of previous
    // level.
    var prevMax = -1000000000;

    // to store minimum value of current
    // level.
    var minval;

    // to store maximum value of current
    // level.
    var maxval;

    // to store number of nodes in current
    // level.
    var levelSize;

    // queue to perform level order traversal.
    var q = [];
    q.push(root);

    while (q.length != 0)
    {

        // find number of nodes in current
        // level.
        levelSize = q.length;

        minval = 1000000000;
        maxval = -1000000000;

        // traverse current level and find
        // minimum and maximum value of
        // this level.
        while (levelSize > 0)
        {
            root = q[0];
            q.shift();

            levelSize--;

            minval = Math.min(minval, root.key);
            maxval = Math.max(maxval, root.key);

            if (root.left != null)
                q.push(root.left);

            if (root.right != null)
                q.push(root.right);
        }

        // if minimum value of this level
        // is not greater than maximum
        // value of previous level then
        // given tree is not level sorted.
        if (minval <= prevMax)
            return 0;

        // maximum value of this level is
        // previous maximum value for
        // next level.
        prevMax = maxval;
    }

    return 1;
}

// Driver Code
/*
        1
    /
    4
    \
        6
    / \
    8 9
    /     \
    12     10
*/
var root = newNode(1);
root.left = newNode(4);
root.left.right = newNode(6);
root.left.right.left = newNode(8);
root.left.right.right = newNode(9);
root.left.right.left.left = newNode(12);
root.left.right.right.right = newNode(10);
if (isSorted(root) == 1)
    document.write("Sorted");
else
    document.write("Not Sorted");

</script>
```

**Output:** 

```
Sorted
```

**时间复杂度:**O(n)
T3】辅助空间: O(n)