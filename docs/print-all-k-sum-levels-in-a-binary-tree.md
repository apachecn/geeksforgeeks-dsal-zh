# 在二叉树中打印所有 K-sum 级别

> 原文:[https://www . geesforgeks . org/print-all-k-sum-levels-in-a-a-binary-tree/](https://www.geeksforgeeks.org/print-all-k-sum-levels-in-a-binary-tree/)

给定一个**二叉树**和一个整数 **K** ，其中该树有正负节点，任务是打印其和等于 **K** 的级别的元素。如果不存在这样的结果，则打印“**不可能**”。

**示例:**

```
Input: 
            -10
           /    \
          2      -3
        /   \       \
       4     15      -6
      /       \      /
     7         -8   9 
K = 13
Output: 4 15 -6
Explanation: 
Level 1 (-10): Sum = -10
Level 2 (2, 3): Sum = 5
Level 3 (4, 15, -6): Sum = 13
Level 4 (7, -8, 9): Sum = 8
Only level 3 (4, 15, -6) has sum = K

Input:
                  1
                /  \ 
              12    13 
             /     /   \ 
            11    6    -11 
                   \    / 
                   2   2  
K = 30
Output:  Not Possible
Explanation: 
There is no such level whose sum = K
```

**进场:**

*   执行[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)的[级顺序遍历](https://www.geeksforgeeks.org/level-order-tree-traversal/)，存储查找各级之和。
*   如果总和等于 K，打印级别。否则就更上一层楼。
*   重复该过程，直到遍历并检查了所有级别。
*   如果总和 K 没有这样的水平，打印“不可能”。

下面是上述方法的实现:

## C++

```
// C++ program to print all
// K-sum levels in a Binary Tree
#include <bits/stdc++.h>
using namespace std;

// Vector to store the
// elements of a level
vector<int> level;

// Binary Tree Node
struct node {
    struct node* left;
    int data;
    struct node* right;
};

// Function to display elements
void display(bool flag)
{

    // Check if boolean variable is true
    // then print the level
    if (flag) {

        for (auto x : level)
            cout << x << " ";
    }

    else

        cout << "Not Possible\n";
}

// Function to find sum of
// elements by level order traversal
void SumlevelOrder(node* root, int k)
{

    if (root == NULL)
        return;

    // Queue data structure for
    // level order traversal
    queue<node*> q;

    // Enqueue Root in Queue
    q.push(root);

    bool flag = false;

    while (q.empty() == false) {

        // number of nodes at current level
        int nodeCount = q.size();

        int Present_level_sum = 0;

        // Dequeue all nodes of current level and
        // Enqueue all nodes of next level
        while (nodeCount > 0) {

            node* node = q.front();

            // To add node data
            Present_level_sum += node->data;

            level.push_back(node->data);

            q.pop();

            if (node->left != NULL)
                q.push(node->left);

            if (node->right != NULL)
                q.push(node->right);

            nodeCount--;
        }

        if (Present_level_sum == k) {

            flag = true;
            break;
        }

        level.clear();
    }

    display(flag);
}

// Function to create a new tree node
node* newNode(int data)
{
    node* temp = new node;
    temp->data = data;
    temp->left = NULL;
    temp->right = NULL;
    return temp;
}

// Driver code
int main()
{
    // Create binary tree
    node* root = newNode(1);

    root->left = newNode(2);
    root->right = newNode(3);

    root->left->left = newNode(4);
    root->left->right = newNode(5);
    root->right->right = newNode(6);

    int K = 15;

    SumlevelOrder(root, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print all
// K-sum levels in a Binary Tree
import java.util.*;

class GFG{

// Vector to store the
// elements of a level
static Vector<Integer> level = new Vector<Integer>();

// Binary Tree Node
static class node {
    node left;
    int data;
    node right;
};

// Function to display elements
static void display(boolean flag)
{

    // Check if boolean variable is true
    // then print the level
    if (flag) {

        for (Integer x : level)
            System.out.print(x+ " ");
    }

    else

        System.out.print("Not Possible\n");
}

// Function to find sum of
// elements by level order traversal
static void SumlevelOrder(node root, int k)
{

    if (root == null)
        return;

    // Queue data structure for
    // level order traversal
    Queue<node> q = new LinkedList<>();

    // Enqueue Root in Queue
    q.add(root);

    boolean flag = false;

    while (q.isEmpty() == false) {

        // number of nodes at current level
        int nodeCount = q.size();

        int Present_level_sum = 0;

        // Dequeue all nodes of current level and
        // Enqueue all nodes of next level
        while (nodeCount > 0) {

            node node = q.peek();

            // To add node data
            Present_level_sum += node.data;

            level.add(node.data);

            q.remove();

            if (node.left != null)
                q.add(node.left);

            if (node.right != null)
                q.add(node.right);

            nodeCount--;
        }

        if (Present_level_sum == k) {

            flag = true;
            break;
        }

        level.clear();
    }

    display(flag);
}

// Function to create a new tree node
static node newNode(int data)
{
    node temp = new node();
    temp.data = data;
    temp.left = null;
    temp.right = null;
    return temp;
}

// Driver code
public static void main(String[] args)
{
    // Create binary tree
    node root = newNode(1);

    root.left = newNode(2);
    root.right = newNode(3);

    root.left.left = newNode(4);
    root.left.right = newNode(5);
    root.right.right = newNode(6);

    int K = 15;

    SumlevelOrder(root, K);

}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to prall
# K-sum levels in a Binary Tree
from collections import deque as queue

# A BST node
class Node:

    def __init__(self, x):

        self.data = x
        self.left = None
        self.right = None

# Vector to store the
# elements of a level
level = []

# Function to display elements
def display(flag):

    # Check if boolean variable is
    # true then print level
    if (flag):
        for x in level:
            print(x, end = " ")
    else:
        print("Not Possible\n")

# Function to find sum of elements
# by level order traversal
def SumlevelOrder(root, k):

    if (root == None):
        return

    # Queue data structure for
    # level order traversal
    q = queue()

    # Enqueue Root in Queue
    q.append(root)

    flag = False

    while (len(q) > 0):

        # Number of nodes at current level
        nodeCount = len(q)

        Present_level_sum = 0

        # Dequeue all nodes of current level
        # and Enqueue all nodes of next level
        while (nodeCount > 0):
            node = q.popleft()

            # To add node data
            Present_level_sum += node.data

            level.append(node.data)

            # q.pop()

            if (node.left != None):
                q.append(node.left)

            if (node.right != None):
                q.append(node.right)

            nodeCount -= 1

        if (Present_level_sum == k):
            flag = True
            break

        level.clear()

    display(flag)

# Driver code
if __name__ == '__main__':

    # Create binary tree
    root = Node(1)

    root.left = Node(2)
    root.right = Node(3)

    root.left.left = Node(4)
    root.left.right = Node(5)
    root.right.right = Node(6)

    K = 15

    SumlevelOrder(root, K)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to print all
// K-sum levels in a Binary Tree
using System;
using System.Collections.Generic;

class GFG{

// List to store the
// elements of a level
static List<int> level = new List<int>();

// Binary Tree Node
class node {
    public node left;
    public int data;
    public node right;
};

// Function to display elements
static void display(bool flag)
{

    // Check if bool variable is true
    // then print the level
    if (flag) {

        foreach (int x in level)
            Console.Write(x+ " ");
    }

    else

        Console.Write("Not Possible\n");
}

// Function to find sum of
// elements by level order traversal
static void SumlevelOrder(node root, int k)
{

    if (root == null)
        return;

    // Queue data structure for
    // level order traversal
    Queue<node> q = new Queue<node>();

    // Enqueue Root in Queue
    q.Enqueue(root);

    bool flag = false;

    while (q.Count!=0) {

        // number of nodes at current level
        int nodeCount = q.Count;

        int Present_level_sum = 0;

        // Dequeue all nodes of current level and
        // Enqueue all nodes of next level
        while (nodeCount > 0) {

            node node = q.Peek();

            // To add node data
            Present_level_sum += node.data;

            level.Add(node.data);

            q.Dequeue();

            if (node.left != null)
                q.Enqueue(node.left);

            if (node.right != null)
                q.Enqueue(node.right);

            nodeCount--;
        }

        if (Present_level_sum == k) {

            flag = true;
            break;
        }

        level.Clear();
    }

    display(flag);
}

// Function to create a new tree node
static node newNode(int data)
{
    node temp = new node();
    temp.data = data;
    temp.left = null;
    temp.right = null;
    return temp;
}

// Driver code
public static void Main(String[] args)
{
    // Create binary tree
    node root = newNode(1);

    root.left = newNode(2);
    root.right = newNode(3);

    root.left.left = newNode(4);
    root.left.right = newNode(5);
    root.right.right = newNode(6);

    int K = 15;

    SumlevelOrder(root, K);

}
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>

// Javascript program to print all
// K-sum levels in a Binary Tree

// Vector to store the
// elements of a level
let level = [];

// Binary Tree Node
class Node
{

    // Utility function to create a new node
    constructor(key)
    {
        this.data = key;
        this.left = this.right = null;
    }
}

// Function to display elements
function display(flag)
{

    // Check if boolean variable is true
    // then print the level
    if (flag)
    {
        for(let x = 0; x < level.length; x++)
            document.write(level[x] + " ");
    }
    else
        document.write("Not Possible<br>");
}

// Function to find sum of
// elements by level order traversal
function SumlevelOrder(root, k)
{
    if (root == null)
        return;

    // Queue data structure for
    // level order traversal
    let q = [];

    // Enqueue Root in Queue
    q.push(root);

    let flag = false;

    while (q.length != 0)
    {

        // Number of nodes at current level
        let nodeCount = q.length;

        let Present_level_sum = 0;

        // Dequeue all nodes of current level and
        // Enqueue all nodes of next level
        while (nodeCount > 0)
        {
            let node = q[0];

            // To add node data
            Present_level_sum += node.data;

            level.push(node.data);
            q.shift();

            if (node.left != null)
                q.push(node.left);

            if (node.right != null)
                q.push(node.right);

            nodeCount--;
        }

        if (Present_level_sum == k)
        {
            flag = true;
            break;
        }
        level = [];
    }
    display(flag);
}

// Driver code
let root = new Node(1);

root.left = new Node(2);
root.right = new Node(3);

root.left.left = new Node(4);
root.left.right = new Node(5);
root.right.right = new Node(6);

let K = 15;

SumlevelOrder(root, K);

// This code is contributed by unknown2108

</script>
```

**Output:** 

```
4 5 6
```