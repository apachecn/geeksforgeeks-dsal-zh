# 普通树的左右视图

> 原文:[https://www . geeksforgeeks . org/左右通用树视图/](https://www.geeksforgeeks.org/left-and-right-view-of-a-generic-tree/)

给定一个由 **N** 节点组成的[类属树](https://www.geeksforgeeks.org/generic-treesn-array-trees/)，任务是找到给定类属树的[左右视图](https://www.geeksforgeeks.org/print-left-view-binary-tree/)。

**示例:**

> **输入:**
> 1
> /\
> 2 3
> /\/\ \
> 4 5 6 7 8
> 
> **输出:**
> 左视图:1 2 4
> 右视图:1 3 8
> **说明:**
> 从左侧看树，那么可见的节点是 1 2 4。
> 从右侧看树，可见的节点是 1 3 8。
> 
> **输入:**
> 1
> /\
> 2 3
> /\
> 4 5 6
> \
> 7
> **输出:**
> 左视图:1 2 4 7
> 右视图:1 3 6 7

**方法:**给定的问题可以通过使用[树的层次顺序遍历](https://www.geeksforgeeks.org/level-order-tree-traversal/)的概念来解决。在这种情况下，树的遍历以层次有序的方式完成。在存储了级别顺序遍历中的所有节点之后，很明显，在树的左视图中是所有级别的第一个节点，类似地，树的右视图是从根开始的所有级别的最后一个节点。

因此，在存储级别顺序遍历后，首先打印**左视图**的每个级别中存储的所有第一个节点，并打印**右视图**的每个级别中存储的所有最后一个节点。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Structure of Node
struct Node {
    int val;
    vector<Node*> child;
};

// Utility function to create a
// new tree node
Node* newNode(int key)
{
    Node* temp = new Node;
    temp->val = key;
    return temp;
}

// Function to get the left view and
// right view of the given tree
void getLeftRightview(Node* root)
{
    // Stores the nodes of each level
    queue<Node*> curNodes;

    // Push the root to initiate the
    // level ordered traversal
    curNodes.push(root);

    // Stores the left and right views
    vector<int> leftView, rightView;

    // Iterate until queue is non-empty
    while (!curNodes.empty()) {

        // Find the number of ndoes in
        // current level
        int n = curNodes.size();

        for (int i = 0; i < n; i++) {
            Node* cur = curNodes.front();
            curNodes.pop();

            // If the node is first node
            // in the level
            if (i == 0)
                leftView.push_back(
                    cur->val);

            // If the node is last node
            // in the level
            if (i == n - 1)
                rightView.push_back(
                    cur->val);

            // Push all the childs of the
            // current node into the queue
            for (int it = 0;
                 it < cur->child.size(); it++) {
                curNodes.push(
                    cur->child[it]);
            }
        }
    }

    // Print the left view
    cout << "Left View: ";
    for (int i = 0; i < leftView.size(); i++)
        cout << leftView[i] << ' ';
    cout << endl;

    // Print the right view
    cout << "RIght View: ";
    for (int i = 0; i < rightView.size(); i++)
        cout << rightView[i] << ' ';
}

// Driver Code
int main()
{
    Node* root = newNode(1);
    (root->child).push_back(newNode(2));
    (root->child).push_back(newNode(3));
    (root->child[0]->child).push_back(newNode(4));
    (root->child[1]->child).push_back(newNode(6));
    (root->child[0]->child).push_back(newNode(5));
    (root->child[1])->child.push_back(newNode(7));
    (root->child[1]->child).push_back(newNode(8));

    getLeftRightview(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
public class Main
{

    // Structure of Node
    static class Node {

        public int val;
        public Vector<Node> child;

        public Node(int key)
        {
            val = key;
            child = new Vector<Node>();
        }
    }

    // Utility function to create a
    // new tree node
    static Node newNode(int key)
    {
        Node temp = new Node(key);
        return temp;
    }

    // Function to get the left view and
    // right view of the given tree
    static void getLeftRightview(Node root)
    {
        // Stores the nodes of each level
        Vector<Node> curNodes = new Vector<Node>();

        // Push the root to initiate the
        // level ordered traversal
        curNodes.add(root);

        // Stores the left and right views
        Vector<Integer> leftView = new Vector<Integer>();
        Vector<Integer> rightView = new Vector<Integer>();

        // Iterate until queue is non-empty
        while (curNodes.size() > 0) {

            // Find the number of ndoes in
            // current level
            int n = curNodes.size();

            for (int i = 0; i < n; i++) {
                Node cur = (Node)curNodes.get(0);
                curNodes.remove(0);

                // If the node is first node
                // in the level
                if (i == 0)
                    leftView.add(cur.val);

                // If the node is last node
                // in the level
                if (i == n - 1)
                    rightView.add(cur.val);

                // Push all the childs of the
                // current node into the queue
                for (int it = 0; it < cur.child.size(); it++) {
                    curNodes.add(cur.child.get(it));
                }
            }
        }

        // Print the left view
        System.out.print("Left View: ");
        for (int i = 0; i < leftView.size(); i++)
            System.out.print(leftView.get(i) + " ");
        System.out.println();

        // Print the right view
        System.out.print("RIght View: ");
        for (int i = 0; i < rightView.size(); i++)
            System.out.print(rightView.get(i) + " ");
    }

    public static void main(String[] args) {
        Node root = newNode(1);
        (root.child).add(newNode(2));
        (root.child).add(newNode(3));
        (root.child.get(0).child).add(newNode(4));
        (root.child.get(1).child).add(newNode(6));
        (root.child.get(0).child).add(newNode(5));
        (root.child.get(1)).child.add(newNode(7));
        (root.child.get(1).child).add(newNode(8));

        getLeftRightview(root);
    }
}

// This code is contributed by divyeshrabadiya07.
```

## 蟒蛇 3

```
# Python3 implementation for the above approach
import sys

# Structure of Node
class Node:
    def __init__(self, key):
        self.val = key
        self.child = []

# Utility function to create a
# new tree node
def newNode(key):
    temp = Node(key)
    return temp

# Function to get the left view and
# right view of the given tree
def getLeftRightview(root):
    # Stores the nodes of each level
    curNodes = []

    # Push the root to initiate the
    # level ordered traversal
    curNodes.append(root)

    # Stores the left and right views
    leftView, rightView = [], []

    # Iterate until queue is non-empty
    while (len(curNodes) != 0):
        # Find the number of ndoes in
        # current level
        n = len(curNodes)

        for i in range(n):
            cur = curNodes[0]
            curNodes.pop(0)

            # If the node is first node
            # in the level
            if (i == 0):
                leftView.append(cur.val)

            # If the node is last node
            # in the level
            if (i == n - 1):
                rightView.append(cur.val)

            # Push all the childs of the
            # current node into the queue
            for it in range(len(cur.child)):
                curNodes.append(cur.child[it])

    # Print the left view
    print("Left View: ", end = "")
    for i in range(len(leftView)):
        print(leftView[i], "", end = "")
    print()

    # Print the right view
    print("RIght View: ", end = "")
    for i in range(len(rightView)):
        print(rightView[i], "", end = "")

root = newNode(1)
(root.child).append(newNode(2))
(root.child).append(newNode(3))
(root.child[0].child).append(newNode(4))
(root.child[1].child).append(newNode(6))
(root.child[0].child).append(newNode(5))
(root.child[1]).child.append(newNode(7))
(root.child[1].child).append(newNode(8))

getLeftRightview(root)

# This code is contributed by rameshtravel07.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections;
using System.Collections.Generic;
class GFG {

    // Structure of Node
    class Node {

        public int val;
        public List<Node> child;

        public Node(int key)
        {
            val = key;
            child = new List<Node>();
        }
    }

    // Utility function to create a
    // new tree node
    static Node newNode(int key)
    {
        Node temp = new Node(key);
        return temp;
    }

    // Function to get the left view and
    // right view of the given tree
    static void getLeftRightview(Node root)
    {
        // Stores the nodes of each level
        Queue curNodes = new Queue();

        // Push the root to initiate the
        // level ordered traversal
        curNodes.Enqueue(root);

        // Stores the left and right views
        List<int> leftView = new List<int>();
        List<int> rightView = new List<int>();

        // Iterate until queue is non-empty
        while (curNodes.Count > 0) {

            // Find the number of ndoes in
            // current level
            int n = curNodes.Count;

            for (int i = 0; i < n; i++) {
                Node cur = (Node)curNodes.Peek();
                curNodes.Dequeue();

                // If the node is first node
                // in the level
                if (i == 0)
                    leftView.Add(cur.val);

                // If the node is last node
                // in the level
                if (i == n - 1)
                    rightView.Add(cur.val);

                // Push all the childs of the
                // current node into the queue
                for (int it = 0; it < cur.child.Count; it++) {
                    curNodes.Enqueue(cur.child[it]);
                }
            }
        }

        // Print the left view
        Console.Write("Left View: ");
        for (int i = 0; i < leftView.Count; i++)
            Console.Write(leftView[i] + " ");
        Console.WriteLine();

        // Print the right view
        Console.Write("RIght View: ");
        for (int i = 0; i < rightView.Count; i++)
            Console.Write(rightView[i] + " ");
    }

  static void Main() {
    Node root = newNode(1);
    (root.child).Add(newNode(2));
    (root.child).Add(newNode(3));
    (root.child[0].child).Add(newNode(4));
    (root.child[1].child).Add(newNode(6));
    (root.child[0].child).Add(newNode(5));
    (root.child[1]).child.Add(newNode(7));
    (root.child[1].child).Add(newNode(8));

    getLeftRightview(root);
  }
}

// This code is contributed by mukesh07.
```

## java 描述语言

```
<script>
    // Javascript program for the above approach

    // Structure of Node
    class Node
    {
        constructor(key) {
           this.val = key;
           this.child = [];
        }
    }

    // Utility function to create a
    // new tree node
    function newNode(key)
    {
        let temp = new Node(key);
        return temp;
    }

    // Function to get the left view and
    // right view of the given tree
    function getLeftRightview(root)
    {
        // Stores the nodes of each level
        let curNodes = [];

        // Push the root to initiate the
        // level ordered traversal
        curNodes.push(root);

        // Stores the left and right views
        let leftView = [], rightView = [];

        // Iterate until queue is non-empty
        while (curNodes.length != 0) {

            // Find the number of ndoes in
            // current level
            let n = curNodes.length;

            for (let i = 0; i < n; i++) {
                let cur = curNodes[0];
                curNodes.shift();

                // If the node is first node
                // in the level
                if (i == 0)
                    leftView.push(cur.val);

                // If the node is last node
                // in the level
                if (i == n - 1)
                    rightView.push(cur.val);

                // Push all the childs of the
                // current node into the queue
                for (let it = 0; it < cur.child.length; it++) {
                    curNodes.push(cur.child[it]);
                }
            }
        }

        // Print the left view
        document.write("Left View: ");
        for (let i = 0; i < leftView.length; i++)
            document.write(leftView[i] + " ");
        document.write("</br>");

        // Print the right view
        document.write("RIght View: ");
        for (let i = 0; i < rightView.length; i++)
            document.write(rightView[i] + " ");
    }

    let root = newNode(1);
    (root.child).push(newNode(2));
    (root.child).push(newNode(3));
    (root.child[0].child).push(newNode(4));
    (root.child[1].child).push(newNode(6));
    (root.child[0].child).push(newNode(5));
    (root.child[1]).child.push(newNode(7));
    (root.child[1].child).push(newNode(8));

    getLeftRightview(root);

// This code is contributed by decode2207.
</script>
```

**Output:** 

```
Left View: 1 2 4 
RIght View: 1 3 8
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)