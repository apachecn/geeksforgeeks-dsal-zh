# 找到宽度为 K 的二叉树的级别

> 原文:[https://www . geeksforgeeks . org/find-宽度为 k 的二进制树的级别/](https://www.geeksforgeeks.org/find-the-level-of-a-binary-tree-with-width-k/)

给定一个[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)和一个整数 **K** ，任务是找到宽度为 **K** 的二叉树的级别。如果存在宽度为 **K** 的多个级别，打印最低级别。如果没有这样的级别，打印 **-1** 。

> 二叉树的一级的**宽度**定义为该级的**最左边的**和**最右边的**节点之间的节点数，包括它们之间的空节点。

**示例:**

> **输入:** K = 4
> 
> ```
>           5  --------- 1st level width = 1 => (5)
>         /   \
>        6     2 -------- 2nd level width = 2 => (6, 2)
>       / \     \  
>      7   3     8 -------3rd level width = 4 => (7, 3, NULL, 8)
>     /     \
>    5       4  -----------4th level width = 4 => (5, NULL, NULL, 4)
> ```
> 
> **输出:** 3
> **说明:**
> 对于给定的树，宽度为 **K** ( = 4)的级别为 3 和 4。
> 既然 3 是两者中的最小值，那就打印最小值。
> 
> **输入:** K = 7
> 
> ```
>            1  --------- 1st level width = 1 => (1)
>          /   \
>         2     9 -------- 2nd level width = 2 => (2, 9)
>        /       \  
>       7         8 ---------3rd level width = 4 => (7, NULL, NULL, 8)
>      /         /
>     5         9 -----------4th level width = 7 => (5, NULL, NULL, 
>              /                                NULL, NULL, NULL, 9)
>             2  -----------5th level width = 1 => (2)
>            /
>           1  -----------6th level width = 1 => (1)
> ```
> 
> **输出:** 4
> **说明:**
> 对于给定的树，宽度为 **K** ( = 7)的级别为 4。

**做法:**
解决问题的基本思路是给每个节点添加一个标签。如果父母有一个标签 **i** ，那么分配一个标签 **2*i** 给它的左孩子，分配一个标签 **2*i+1** 给它的右孩子。这将有助于在计算中包含空节点。
按照以下步骤操作:

*   使用 [**队列**](https://www.geeksforgeeks.org/queue-data-structure/) 在给定的树上执行 [**级顺序遍历**](https://www.geeksforgeeks.org/level-order-tree-traversal/) 。
*   队列包含一对{节点，标签}。最初将{ **根节点，0** }插入队列。
*   如果父母有标签 I，那么对于左边的孩子，插入{ **leftChild，2*i** }到队列，对于右边的孩子，插入{ **rightChild，2*i+1** }到队列。
*   对于每个级别，假设 **a** 作为最左边节点的标签， **b** 作为最右边节点的标签，则 **(b-a+1)** 给出该级别的宽度。
*   检查宽度是否等于 **K** 。如果是，返回**级**。
*   如果没有一级有宽度 **K** ，则返回 **-1** 。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Structure of a Tree node
struct Node {
    int key;
    struct Node *left, *right;
};

// Utility function to create
// and initialize a new node
Node* newNode(int key)
{
    Node* temp = new Node;
    temp->key = key;
    temp->left = temp->right = NULL;
    return (temp);
}

// Function returns required level
// of width k, if found else -1
int findLevel(Node* root,
              int k, int level)
{

    // To store the node and the label
    // and perform traversal
    queue<pair<Node*, int> > qt;
    qt.push(make_pair(root, 0));

    int count = 1, b, a = 0;

    while (!qt.empty()) {

        pair<Node*, int> temp = qt.front();
        qt.pop();

        // Taking the last label
        // of each level of the tree
        if (count == 1) {
            b = temp.second;
        }

        if ((temp.first)->left) {
            qt.push(make_pair(
                temp.first->left,
                2 * temp.second));
        }
        if (temp.first->right) {
            qt.push(make_pair(
                temp.first->right,
                2 * temp.second + 1));
        }

        count--;

        // Check width of current level
        if (count == 0) {

            // If the width is equal to k
            // then return that level
            if (b - a + 1 == k)
                return level;

            pair<Node*, int> secondLabel = qt.front();

            // Taking the first label
            // of each level of the tree
            a = secondLabel.second;

            level += 1;
            count = qt.size();
        }
    }

    // If any level does not has
    // width equal to k, return -1
    return -1;
}

// Driver Code
int main()
{
    Node* root = newNode(5);
    root->left = newNode(6);
    root->right = newNode(2);
    root->right->right = newNode(8);

    root->left->left = newNode(7);
    root->left->left->left = newNode(5);
    root->left->right = newNode(3);
    root->left->right->right = newNode(4);

    int k = 4;

    cout << findLevel(root, k, 1) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Structure of
// binary tree node
static class Node
{
    int data;
    Node left, right;
};

static class pair
{
    Node first;
    int second;

    pair(Node first, int second)
    {
        this.first = first;
        this.second = second;
    }
}

// Function to create new node
static Node newNode(int data)
{
    Node temp = new Node();
    temp.data = data;
    temp.left = temp.right = null;
    return temp;
}

// Function returns required level
// of width k, if found else -1
static int findLevel(Node root,
                     int k, int level)
{

    // To store the node and the label
    // and perform traversal
    Queue<pair> qt = new LinkedList<>();
    qt.add(new pair(root, 0));

    int count = 1, b = 0, a = 0;

    while (!qt.isEmpty())
    {
        pair temp = qt.peek();
        qt.poll();

        // Taking the last label
        // of each level of the tree
        if (count == 1)
        {
            b = temp.second;
        }

        if (temp.first.left != null)
        {
            qt.add(new pair(
                temp.first.left,
                2 * temp.second));
        }
        if (temp.first.right != null)
        {
            qt.add(new pair(
                temp.first.right,
                2 * temp.second + 1));
        }

        count--;

        // Check width of current level
        if (count == 0)
        {

            // If the width is equal to k
            // then return that level
            if ((b - a + 1) == k)
                return level;

            pair secondLabel = qt.peek();

            // Taking the first label
            // of each level of the tree
            a = secondLabel.second;

            level += 1;
            count = qt.size();
        }
    }

    // If any level does not has
    // width equal to k, return -1
    return -1;
}

// Driver code
public static void main(String[] args)
{
    Node root = newNode(5);
    root.left = newNode(6);
    root.right = newNode(2);
    root.right.right = newNode(8);

    root.left.left = newNode(7);
    root.left.left.left = newNode(5);
    root.left.right = newNode(3);
    root.left.right.right = newNode(4);

    int k = 4;

    System.out.println(findLevel(root, k, 1));
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach
from collections import deque

# Structure of a Tree node
class Node:

    def __init__(self, key):

        self.key = key
        self.left = None
        self.right = None

# Function returns required level
# of width k, if found else -1
def findLevel(root: Node,
                 k: int, level: int) -> int:

    # To store the node and the label
    # and perform traversal
    qt = deque()
    qt.append([root, 0])

    count = 1
    b = 0
    a = 0

    while qt:
        temp = qt.popleft()

        # Taking the last label
        # of each level of the tree
        if (count == 1):
            b = temp[1]

        if (temp[0].left):
            qt.append([temp[0].left,
                   2 * temp[1]])

        if (temp[0].right):
            qt.append([temp[0].right,
                   2 * temp[1] + 1])

        count -= 1

        # Check width of current level
        if (count == 0):

            # If the width is equal to k
            # then return that level
            if (b - a + 1 == k):
                return level

            secondLabel = qt[0]

            # Taking the first label
            # of each level of the tree
            a = secondLabel[1]

            level += 1
            count = len(qt)

    # If any level does not has
    # width equal to k, return -1
    return -1

# Driver Code
if __name__ == "__main__":

    root = Node(5)
    root.left = Node(6)
    root.right = Node(2)
    root.right.right = Node(8)

    root.left.left = Node(7)
    root.left.left.left = Node(5)
    root.left.right = Node(3)
    root.left.right.right = Node(4)

    k = 4

    print(findLevel(root, k, 1))

# This code is contributed by sanjeev2552
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections;
using System.Collections.Generic;

class GFG{

// Structure of
// binary tree node
class Node
{
    public int data;
    public Node left, right;
};

class pair
{
    public Node first;
    public int second;

    public pair(Node first, int second)
    {
        this.first = first;
        this.second = second;
    }
}

// Function to create new node
static Node newNode(int data)
{
    Node temp = new Node();
    temp.data = data;
    temp.left = temp.right = null;
    return temp;
}

// Function returns required level
// of width k, if found else -1
static int findLevel(Node root,
                     int k, int level)
{

    // To store the node and the label
    // and perform traversal
    Queue qt = new Queue();
    qt.Enqueue(new pair(root, 0));

    int count = 1, b = 0, a = 0;

    while (qt.Count!=0)
    {
        pair temp = (pair)qt.Dequeue();

        // Taking the last label
        // of each level of the tree
        if (count == 1)
        {
            b = temp.second;
        }

        if (temp.first.left != null)
        {
            qt.Enqueue(new pair(
                temp.first.left,
                2 * temp.second));
        }
        if (temp.first.right != null)
        {
            qt.Enqueue(new pair(
                temp.first.right,
                2 * temp.second + 1));
        }

        count--;

        // Check width of current level
        if (count == 0)
        {

            // If the width is equal to k
            // then return that level
            if ((b - a + 1) == k)
                return level;

            pair secondLabel = (pair)qt.Peek();

            // Taking the first label
            // of each level of the tree
            a = secondLabel.second;

            level += 1;
            count = qt.Count;
        }
    }

    // If any level does not has
    // width equal to k, return -1
    return -1;
}

// Driver code
public static void Main(string[] args)
{
    Node root = newNode(5);
    root.left = newNode(6);
    root.right = newNode(2);
    root.right.right = newNode(8);

    root.left.left = newNode(7);
    root.left.left.left = newNode(5);
    root.left.right = newNode(3);
    root.left.right.right = newNode(4);

    int k = 4;

    Console.Write(findLevel(root, k, 1));
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Structure of
// binary tree node
class Node
{
    constructor()
    {
        this.data = 0;
        this.left = null;
        this.right = null;
    }
};

class pair
{
    constructor(first, second)
    {
        this.first = first;
        this.second = second;
    }
}

// Function to create new node
function newNode(data)
{
    var temp = new Node();
    temp.data = data;
    temp.left = temp.right = null;
    return temp;
}

// Function returns required level
// of width k, if found else -1
function findLevel(root, k, level)
{

    // To store the node and the label
    // and perform traversal
    var qt = [];
    qt.push(new pair(root, 0));

    var count = 1, b = 0, a = 0;

    while (qt.length!=0)
    {
        var temp = qt.shift();

        // Taking the last label
        // of each level of the tree
        if (count == 1)
        {
            b = temp.second;
        }

        if (temp.first.left != null)
        {
            qt.push(new pair(
                temp.first.left,
                2 * temp.second));
        }
        if (temp.first.right != null)
        {
            qt.push(new pair(
                temp.first.right,
                2 * temp.second + 1));
        }

        count--;

        // Check width of current level
        if (count == 0)
        {

            // If the width is equal to k
            // then return that level
            if ((b - a + 1) == k)
                return level;

            var secondLabel = qt[0];

            // Taking the first label
            // of each level of the tree
            a = secondLabel.second;

            level += 1;
            count = qt.length;
        }
    }

    // If any level does not has
    // width equal to k, return -1
    return -1;
}

// Driver code
var root = newNode(5);
root.left = newNode(6);
root.right = newNode(2);
root.right.right = newNode(8);

root.left.left = newNode(7);
root.left.left.left = newNode(5);
root.left.right = newNode(3);
root.left.right.right = newNode(4);

var k = 4;

document.write(findLevel(root, k, 1));

</script>
```

**Output:** 

```
3
```

***时间复杂度:** O(N)*
***辅助空间:** O(N)*