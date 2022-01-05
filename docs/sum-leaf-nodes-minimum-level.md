# 最低水平叶节点的总和

> 原文:[https://www.geeksforgeeks.org/sum-leaf-nodes-minimum-level/](https://www.geeksforgeeks.org/sum-leaf-nodes-minimum-level/)

给定一个包含 **n 个**节点的二叉树。问题是得到二叉树中处于最小级别的所有叶节点的和。
**例:**

```
Input : 
              1
            /   \
           2     3
         /  \   /  \
        4   5   6   7
           /     \
          8       9

Output : 11
Leaf nodes 4 and 7 are at minimum level.
Their sum = (4 + 7) = 11\. 
```

**来源:** [微软 IDC 访谈体验|第 150 集。](https://www.geeksforgeeks.org/microsoft-idc-interview-experience-set-150-full-time/)

**方法:**使用队列执行[迭代级序遍历](https://www.geeksforgeeks.org/print-level-order-traversal-line-line/)，找到包含叶节点的第一级。汇总该级别的所有叶节点，然后停止进一步执行遍历。

## C++

```
// C++ implementation to find the sum of
// leaf nodes at minimum level
#include <bits/stdc++.h>
using namespace std;

// structure of a node of binary tree
struct Node {
    int data;
    Node *left, *right;
};

// function to get a new node
Node* getNode(int data)
{
    // allocate space
    Node* newNode = (Node*)malloc(sizeof(Node));

    // put in the data
    newNode->data = data;
    newNode->left = newNode->right = NULL;
    return newNode;
}

// function to find the sum of
// leaf nodes at minimum level
int sumOfLeafNodesAtMinLevel(Node* root)
{
    // if tree is empty
    if (!root)
        return 0;

    // if there is only one node
    if (!root->left && !root->right)
        return root->data;

    // queue used for level order traversal
    queue<Node*> q;
    int sum = 0;
    bool f = 0;

    // push root node in the queue 'q'
    q.push(root);

    while (f == 0) {

        // count number of nodes in the
        // current level
        int nc = q.size();

        // traverse the current level nodes
        while (nc--) {

            // get front element from 'q'
            Node* top = q.front();
            q.pop();

            // if it is a leaf node
            if (!top->left && !top->right) {

                // accumulate data to 'sum'
                sum += top->data;

                // set flag 'f' to 1, to signify
                // minimum level for leaf nodes
                // has been encountered
                f = 1;
            }
            else {

                // if top's left and right child
                // exists, then push them to 'q'
                if (top->left)
                    q.push(top->left);
                if (top->right)
                    q.push(top->right);
            }
        }
    }

    // required sum
    return sum;
}

// Driver program to test above
int main()
{
    // binary tree creation
    Node* root = getNode(1);
    root->left = getNode(2);
    root->right = getNode(3);
    root->left->left = getNode(4);
    root->left->right = getNode(5);
    root->right->left = getNode(6);
    root->right->right = getNode(7);
    root->left->right->left = getNode(8);
    root->right->left->right = getNode(9);

    cout << "Sum = "
         << sumOfLeafNodesAtMinLevel(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the sum of
// leaf nodes at minimum level
import java.util.*;

class GFG
{

// structure of a node of binary tree
static class Node
{
    int data;
    Node left, right;
};

// function to get a new node
static Node getNode(int data)
{
    // allocate space
    Node newNode = new Node();

    // put in the data
    newNode.data = data;
    newNode.left = newNode.right = null;
    return newNode;
}

// function to find the sum of
// leaf nodes at minimum level
static int sumOfLeafNodesAtMinLevel(Node root)
{
    // if tree is empty
    if (root == null)
        return 0;

    // if there is only one node
    if (root.left == null &&
        root.right == null)
        return root.data;

    // queue used for level order traversal
    Queue<Node> q = new LinkedList<>();
    int sum = 0;
    boolean f = false;

    // push root node in the queue 'q'
    q.add(root);

    while (f == false)
    {

        // count number of nodes in the
        // current level
        int nc = q.size();

        // traverse the current level nodes
        while (nc-- >0)
        {

            // get front element from 'q'
            Node top = q.peek();
            q.remove();

            // if it is a leaf node
            if (top.left == null &&
                top.right == null)
            {

                // accumulate data to 'sum'
                sum += top.data;

                // set flag 'f' to 1, to signify
                // minimum level for leaf nodes
                // has been encountered
                f = true;
            }
            else
            {

                // if top's left and right child
                // exists, then push them to 'q'
                if (top.left != null)
                    q.add(top.left);
                if (top.right != null)
                    q.add(top.right);
            }
        }
    }

    // required sum
    return sum;
}

// Driver Code
public static void main(String[] args)
{

    // binary tree creation
    Node root = getNode(1);
    root.left = getNode(2);
    root.right = getNode(3);
    root.left.left = getNode(4);
    root.left.right = getNode(5);
    root.right.left = getNode(6);
    root.right.right = getNode(7);
    root.left.right.left = getNode(8);
    root.right.left.right = getNode(9);

    System.out.println("Sum = " +
           sumOfLeafNodesAtMinLevel(root));
    }
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation to find the sum
# of leaf node at minimum level
from collections import deque

# Structure of a node in binary tree
class Node:

    def __init__(self, data):

        self.data = data
        self.left = None
        self.right = None

# function to find the sum of leaf nodes
# at minimum level
def sumOfLeafNodesAtLeafLevel(root):

    # if tree is empty
    if not root:
        return 0

    # if there is only root node
    if not root.left and not root.right:
        return root.data

    # Queue used for level order traversal
    Queue = deque()
    sum = f = 0

    # push rioot node in the queue
    Queue.append(root)

    while not f:

        # count no. of nodes present at current level
        nc = len(Queue)

        # traverse current level nodes
        while nc:
            top = Queue.popleft()

            # if node is leaf node
            if not top.left and not top.right:
                sum += top.data

                # set flag = 1 to signify that
                # we have encountered the minimum level
                f = 1
            else:

                # if top's left or right child exist
                # push them to Queue
                if top.left:
                    Queue.append(top.left)
                if top.right:
                    Queue.append(top.right)
            nc -= 1

    # return the sum
    return sum

# Driver code
if __name__ == "__main__":

    # binary tree creation
    root = Node(1)
    root.left = Node(2)
    root.right = Node(3)
    root.left.left = Node(4)
    root.left.right = Node(5)
    root.right.left = Node(6)
    root.right.right = Node(7)
    root.left.right.left = Node(8)
    root.right.left.right = Node(9)

    print("Sum = ", sumOfLeafNodesAtLeafLevel(root))

# This code is contributed by
# Mayank Chaudhary (chaudhary_19)
```

## C#

```
// C# implementation to find the sum of
// leaf nodes at minimum level
using System;
using System.Collections.Generic;

class GFG
{

// structure of a node of binary tree
class Node
{
    public int data;
    public Node left, right;
};

// function to get a new node
static Node getNode(int data)
{
    // allocate space
    Node newNode = new Node();

    // put in the data
    newNode.data = data;
    newNode.left = newNode.right = null;
    return newNode;
}

// function to find the sum of
// leaf nodes at minimum level
static int sumOfLeafNodesAtMinLevel(Node root)
{
    // if tree is empty
    if (root == null)
        return 0;

    // if there is only one node
    if (root.left == null &&
        root.right == null)
        return root.data;

    // queue used for level order traversal
    Queue<Node> q = new Queue<Node>();
    int sum = 0;
    bool f = false;

    // push root node in the queue 'q'
    q.Enqueue(root);

    while (f == false)
    {

        // count number of nodes in the
        // current level
        int nc = q.Count;

        // traverse the current level nodes
        while (nc-- >0)
        {

            // get front element from 'q'
            Node top = q.Peek();
            q.Dequeue();

            // if it is a leaf node
            if (top.left == null &&
                top.right == null)
            {

                // accumulate data to 'sum'
                sum += top.data;

                // set flag 'f' to 1, to signify
                // minimum level for leaf nodes
                // has been encountered
                f = true;
            }
            else
            {

                // if top's left and right child
                // exists, then push them to 'q'
                if (top.left != null)
                    q.Enqueue(top.left);
                if (top.right != null)
                    q.Enqueue(top.right);
            }
        }
    }

    // required sum
    return sum;
}

// Driver Code
public static void Main(String[] args)
{

    // binary tree creation
    Node root = getNode(1);
    root.left = getNode(2);
    root.right = getNode(3);
    root.left.left = getNode(4);
    root.left.right = getNode(5);
    root.right.left = getNode(6);
    root.right.right = getNode(7);
    root.left.right.left = getNode(8);
    root.right.left.right = getNode(9);

    Console.WriteLine("Sum = " +
            sumOfLeafNodesAtMinLevel(root));
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

    // JavaScript implementation to find the sum of
    // leaf nodes at minimum level

    class Node
    {
        constructor(data) {
           this.left = null;
           this.right = null;
           this.data = data;
        }
    }

    // function to get a new node
    function getNode(data)
    {
        // allocate space
        let newNode = new Node(data);
        return newNode;
    }

    // function to find the sum of
    // leaf nodes at minimum level
    function sumOfLeafNodesAtMinLevel(root)
    {
        // if tree is empty
        if (root == null)
            return 0;

        // if there is only one node
        if (root.left == null &&
            root.right == null)
            return root.data;

        // queue used for level order traversal
        let q = [];
        let sum = 0;
        let f = false;

        // push root node in the queue 'q'
        q.push(root);

        while (f == false)
        {

            // count number of nodes in the
            // current level
            let nc = q.length;

            // traverse the current level nodes
            while (nc-- >0)
            {

                // get front element from 'q'
                let top = q[0];
                q.shift();

                // if it is a leaf node
                if (top.left == null &&
                    top.right == null)
                {

                    // accumulate data to 'sum'
                    sum += top.data;

                    // set flag 'f' to 1, to signify
                    // minimum level for leaf nodes
                    // has been encountered
                    f = true;
                }
                else
                {

                    // if top's left and right child
                    // exists, then push them to 'q'
                    if (top.left != null)
                        q.push(top.left);
                    if (top.right != null)
                        q.push(top.right);
                }
            }
        }

        // required sum
        return sum;
    }

    // binary tree creation
    let root = getNode(1);
    root.left = getNode(2);
    root.right = getNode(3);
    root.left.left = getNode(4);
    root.left.right = getNode(5);
    root.right.left = getNode(6);
    root.right.right = getNode(7);
    root.left.right.left = getNode(8);
    root.right.left.right = getNode(9);

    document.write("Sum = " +
           sumOfLeafNodesAtMinLevel(root));

</script>
```

**输出:**

```
Sum = 11
```

时间复杂度:O(n)。
辅助空间:O(n)。