# 二叉树中级别的平均值

> 原文:[https://www.geeksforgeeks.org/averages-levels-binary-tree/](https://www.geeksforgeeks.org/averages-levels-binary-tree/)

给定一个非空二叉树，打印每一级节点的平均值。

**示例:**

```
Input : 
    4
   / \
  2   9
 / \   \
3   5   7

Output : [4 5.5 5]
The average value of nodes on level 0 is 4, 
on level 1 is 5.5, and on level 2 is 5\. 
Hence, print [4 5.5 5].
```

这个想法是基于[逐行水平顺序遍历|集合 2(使用两个队列)](https://www.geeksforgeeks.org/level-order-traversal-line-line-set-2-using-two-queues/)

1.  首先将根节点推入队列。然后，从队列的前面移除一个节点。
2.  对于从队列中移除的每个节点，将其所有子节点推入一个新的临时队列。
3.  继续从队列中弹出节点，并将这些节点的子节点添加到临时队列中，直到队列变空。
4.  每当队列变空时，它表明已经考虑了树的一个级别。
5.  将节点推入临时队列时，跟踪节点的总和以及推入的节点数量，并利用这些总和和计数值找出每一层上节点的平均值。
6.  在考虑了每个级别之后，再次用临时队列初始化队列，并继续该过程，直到两个队列都变空。

## C++

```
// C++ program to find averages of all levels
// in a binary tree.
#include <bits/stdc++.h>
using namespace std;

/* A binary tree node has data, pointer to
   left child and a pointer to right child */
struct Node {
    int val;
    struct Node* left, *right;
};

/* Function to print the average value of the
   nodes on each level */
void averageOfLevels(Node* root)
{
    vector<float> res;

    // Traversing level by level
    queue<Node*> q;
    q.push(root);

    while (!q.empty()) {

        // Compute sum of nodes and
        // count of nodes in current
        // level.
        int sum = 0, count = 0;
        queue<Node*> temp;
        while (!q.empty()) {
            Node* n = q.front();
            q.pop();
            sum += n->val;
            count++;
            if (n->left != NULL)
                temp.push(n->left);
            if (n->right != NULL)
                temp.push(n->right);
        }
        q = temp;
        cout << (sum * 1.0 / count) << " ";
    }
}

/* Helper function that allocates a
   new node with the given data and
   NULL left and right pointers. */
Node* newNode(int data)
{
    Node* temp = new Node;
    temp->val = data;
    temp->left = temp->right = NULL;
    return temp;
}

// Driver code
int main()
{
    /* Let us construct a Binary Tree
        4
       / \
      2   9
     / \   \
    3   5   7 */

    Node* root = NULL;
    root = newNode(4);
    root->left = newNode(2);
    root->right = newNode(9);
    root->left->left = newNode(3);
    root->left->right = newNode(8);
    root->right->right = newNode(7);
    averageOfLevels(root);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find averages of all levels
// in a binary tree.
import java.util.*;
class GfG {

/* A binary tree node has data, pointer to
left child and a pointer to right child */
static class Node {
    int val;
    Node left, right;
}

/* Function to print the average value of the
nodes on each level */
static void averageOfLevels(Node root)
{
    //vector<float> res;

    // Traversing level by level
    Queue<Node> q = new LinkedList<Node> ();
    q.add(root);
    int sum = 0, count  = 0;

    while (!q.isEmpty()) {

        // Compute sum of nodes and
        // count of nodes in current
        // level.
        sum = 0;
        count = 0;
        Queue<Node> temp = new LinkedList<Node> ();
        while (!q.isEmpty()) {
            Node n = q.peek();
            q.remove();
            sum += n.val;
            count++;
            if (n.left != null)
                temp.add(n.left);
            if (n.right != null)
                temp.add(n.right);
        }
        q = temp;
        System.out.print((sum * 1.0 / count) + " ");
    }
}

/* Helper function that allocates a
new node with the given data and
NULL left and right pointers. */
static Node newNode(int data)
{
    Node temp = new Node();
    temp.val = data;
    temp.left = null;
    temp.right = null;
    return temp;
}

// Driver code
public static void main(String[] args)
{
    /* Let us construct a Binary Tree
        4
    / \
    2 9
    / \ \
    3 5 7 */

    Node root = null;
    root = newNode(4);
    root.left = newNode(2);
    root.right = newNode(9);
    root.left.left = newNode(3);
    root.left.right = newNode(5);
    root.right.right = newNode(7);
    System.out.println("Averages of levels : ");
    System.out.print("[");
    averageOfLevels(root);
    System.out.println("]");
}
}
```

## 蟒蛇 3

```
# Python3 program to find averages of
# all levels in a binary tree.

# Importing Queue
from queue import Queue

# Helper class that allocates a
# new node with the given data and
# None left and right pointers.
class newNode:
    def __init__(self, data):
        self.val = data
        self.left = self.right = None

# Function to print the average value
# of the nodes on each level
def averageOfLevels(root):

    # Traversing level by level
    q = Queue()
    q.put(root)
    while (not q.empty()):

        # Compute Sum of nodes and
        # count of nodes in current
        # level.
        Sum = 0
        count = 0
        temp = Queue()
        while (not q.empty()):
            n = q.queue[0]
            q.get()
            Sum += n.val
            count += 1
            if (n.left != None):
                temp.put(n.left)
            if (n.right != None):
                temp.put(n.right)
        q = temp
        print((Sum * 1.0 / count), end = " ")

# Driver code
if __name__ == '__main__':

    # Let us construct a Binary Tree
    #     4
    # / \
    # 2 9
    # / \ \
    # 3 5 7
    root = None
    root = newNode(4)
    root.left = newNode(2)
    root.right = newNode(9)
    root.left.left = newNode(3)
    root.left.right = newNode(8)
    root.right.right = newNode(7)
    averageOfLevels(root)

# This code is contributed by PranchalK
```

## C#

```
// C# program to find averages of all levels
// in a binary tree.
using System;
using System.Collections.Generic;

class GfG
{

    /* A binary tree node has data, pointer to
    left child and a pointer to right child */
    class Node
    {
        public int val;
        public Node left, right;
    }

    /* Function to print the average value of the
    nodes on each level */
    static void averageOfLevels(Node root)
    {
        //vector<float> res;

        // Traversing level by level
        Queue<Node> q = new Queue<Node> ();
        q.Enqueue(root);
        int sum = 0, count = 0;

        while ((q.Count!=0))
        {

            // Compute sum of nodes and
            // count of nodes in current
            // level.
            sum = 0;
            count = 0;
            Queue<Node> temp = new Queue<Node> ();
            while (q.Count != 0)
            {
                Node n = q.Peek();
                q.Dequeue();
                sum += n.val;
                count++;
                if (n.left != null)
                    temp.Enqueue(n.left);
                if (n.right != null)
                    temp.Enqueue(n.right);
            }
            q = temp;
            Console.Write((sum * 1.0 / count) + " ");
        }
    }

    /* Helper function that allocates a
    new node with the given data and
    NULL left and right pointers. */
    static Node newNode(int data)
    {
        Node temp = new Node();
        temp.val = data;
        temp.left = null;
        temp.right = null;
        return temp;
    }

    // Driver code
    public static void Main(String[] args)
    {
        /* Let us construct a Binary Tree
            4
        / \
        2 9
        / \ \
        3 5 7 */

        Node root = null;
        root = newNode(4);
        root.left = newNode(2);
        root.right = newNode(9);
        root.left.left = newNode(3);
        root.left.right = newNode(5);
        root.right.right = newNode(7);
        Console.WriteLine("Averages of levels : ");
        Console.Write("[");
        averageOfLevels(root);
        Console.WriteLine("]");
    }
}

// This code has been contributed by
// 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program to find averages of
// all levels in a binary tree.
class Node
{
    constructor(data)
    {
        this.left = null;
        this.right = null;
        this.val = data;
    }
}

// Function to print the average value
// of the nodes on each level
function averageOfLevels(root)
{

    // Traversing level by level
    let q = [];
    q.push(root);
    let sum = 0, count  = 0;

    while (q.length > 0)
    {

        // Compute sum of nodes and
        // count of nodes in current
        // level.
        sum = 0;
        count = 0;
        let temp = [];

        while (q.length > 0)
        {
            let n = q[0];
            q.shift();
            sum += n.val;
            count++;

            if (n.left != null)
                temp.push(n.left);
            if (n.right != null)
                temp.push(n.right);
        }
        q = temp;
        document.write((sum * 1.0 / count) + " ");
    }
}

// Helper function that allocates a
// new node with the given data and
// NULL left and right pointers.
function newNode(data)
{
    let temp = new Node(data);
    return temp;
}

// Driver code

/* Let us construct a Binary Tree
     4
    / \
   2   9
  / \   \
 3   5   7 */
let root = null;
root = newNode(4);
root.left = newNode(2);
root.right = newNode(9);
root.left.left = newNode(3);
root.left.right = newNode(5);
root.right.right = newNode(7);

document.write("Averages of levels : " + "</br>");
document.write("[");
averageOfLevels(root);
document.write("]" + "</br>");

// This code is contributed by divyeshrabadiya07

</script>
```

**输出:**

```
Average of levels: 
[4 5.5 5]
```

**复杂度分析:**

*   **时间复杂度:** O(n)。
    整棵树一次穿越大气层。这里，n 指给定二叉树中的节点数。
*   辅助空间:0(n)。
    队列的大小可以增长到给定二叉树中任何级别的最大节点数。这里，n 指的是输入树中任何级别的最大节点数。

本文由 **Aakash Pal** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。