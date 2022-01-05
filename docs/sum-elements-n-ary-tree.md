# N 元树所有元素之和

> 原文:[https://www.geeksforgeeks.org/sum-elements-n-ary-tree/](https://www.geeksforgeeks.org/sum-elements-n-ary-tree/)

给定一棵 N 元树，求其中所有元素的和。

![](img/b94c33f60ebf857b4a5d653568898998.png)

**例:**

```
Input : Above tree
Output : Sum is 536
```

**方法:**使用的方法类似于二叉树中的[级顺序遍历。首先推送队列中的根节点。对于每个节点，当它从队列中弹出时，在 **sum** 变量中添加该节点的值，并将弹出元素的子元素推入队列。在一般树的情况下，将子节点存储在向量中。因此，将向量的所有元素放入队列。
以下是上述思路的实现:](https://www.geeksforgeeks.org/level-order-tree-traversal/) 

## C++

```
// C++ program to find sum of all
// elements in generic tree
#include <bits/stdc++.h>
using namespace std;

// Represents a node of an n-ary tree
struct Node {
    int key;
    vector<Node*> child;
};

// Utility function to create a new tree node
Node* newNode(int key)
{
    Node* temp = new Node;
    temp->key = key;
    return temp;
}

// Function to compute the sum
// of all elements in generic tree
int sumNodes(Node* root)
{
    // initialize the sum variable
    int sum = 0;

    if (root == NULL)
        return 0;

    // Creating a queue and pushing the root
    queue<Node*> q;
    q.push(root);

    while (!q.empty()) {
        int n = q.size();

        // If this node has children
        while (n > 0) {

            // Dequeue an item from queue and
            // add it to variable "sum"
            Node* p = q.front();
            q.pop();
            sum += p->key;

            // Enqueue all children of the dequeued item
            for (int i = 0; i < p->child.size(); i++)
                q.push(p->child[i]);
            n--;
        }
    }
    return sum;
}

// Driver program
int main()
{
    // Creating a generic tree
    Node* root = newNode(20);
    (root->child).push_back(newNode(2));
    (root->child).push_back(newNode(34));
    (root->child).push_back(newNode(50));
    (root->child).push_back(newNode(60));
    (root->child).push_back(newNode(70));
    (root->child[0]->child).push_back(newNode(15));
    (root->child[0]->child).push_back(newNode(20));
    (root->child[1]->child).push_back(newNode(30));
    (root->child[2]->child).push_back(newNode(40));
    (root->child[2]->child).push_back(newNode(100));
    (root->child[2]->child).push_back(newNode(20));
    (root->child[0]->child[1]->child).push_back(newNode(25));
    (root->child[0]->child[1]->child).push_back(newNode(50));

    cout << sumNodes(root) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find sum of all
// elements in generic tree
import java.util.*;

class GFG
{

// Represents a node of an n-ary tree
static class Node
{
    int key;
    Vector<Node> child;
};

// Utility function to create a new tree node
static Node newNode(int key)
{
    Node temp = new Node();
    temp.key = key;
    temp.child = new Vector<>();
    return temp;
}

// Function to compute the sum
// of all elements in generic tree
static int sumNodes(Node root)
{
    // initialize the sum variable
    int sum = 0;

    if (root == null)
        return 0;

    // Creating a queue and pushing the root
    Queue<Node> q = new LinkedList<>();
    q.add(root);

    while (!q.isEmpty())
    {
        int n = q.size();

        // If this node has children
        while (n > 0)
        {

            // Dequeue an item from queue and
            // add it to variable "sum"
            Node p = q.peek();
            q.remove();
            sum += p.key;

            // Enqueue all children of the dequeued item
            for (int i = 0; i < p.child.size(); i++)
                q.add(p.child.get(i));
            n--;
        }
    }
    return sum;
}

// Driver program
public static void main(String[] args)
{
    // Creating a generic tree
    Node root = newNode(20);
    (root.child).add(newNode(2));
    (root.child).add(newNode(34));
    (root.child).add(newNode(50));
    (root.child).add(newNode(60));
    (root.child).add(newNode(70));
    (root.child.get(0).child).add(newNode(15));
    (root.child.get(0).child).add(newNode(20));
    (root.child.get(1).child).add(newNode(30));
    (root.child.get(2).child).add(newNode(40));
    (root.child.get(2).child).add(newNode(100));
    (root.child.get(2).child).add(newNode(20));
    (root.child.get(0).child.get(1).child).add(newNode(25));
    (root.child.get(0).child.get(1).child).add(newNode(50));

    System.out.print(sumNodes(root) +"\n");
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to find sum of all
# elements in generic tree

# Represents a node of an n-ary tree
class Node:
    def __init__(self):
        self.key = 0
        self.child = []

# Utility function to create a new tree node
def newNode(key):
    temp = Node()
    temp.key = key
    temp.child = []
    return temp

# Function to compute the sum
# of all elements in generic tree
def sumNodes(root):
    # initialize the sum variable
    Sum = 0

    if root == None:
        return 0

    # Creating a queue and pushing the root
    q = []
    q.append(root)

    while len(q) != 0:
        n = len(q)

        # If this node has children
        while n > 0:
            # Dequeue an item from queue and
            # add it to variable "sum"
            p = q[0]
            q.pop(0)
            Sum += p.key

            # push all children of the dequeued item
            for i in range(len(p.child)):
                q.append(p.child[i])
            n-=1
    return Sum

# Creating a generic tree
root = newNode(20)
(root.child).append(newNode(2))
(root.child).append(newNode(34))
(root.child).append(newNode(50))
(root.child).append(newNode(60))
(root.child).append(newNode(70))
(root.child[0].child).append(newNode(15))
(root.child[0].child).append(newNode(20))
(root.child[1].child).append(newNode(30))
(root.child[2].child).append(newNode(40))
(root.child[2].child).append(newNode(100))
(root.child[2].child).append(newNode(20))
(root.child[0].child[1].child).append(newNode(25))
(root.child[0].child[1].child).append(newNode(50))
print(sumNodes(root))

# This code is contributed by divyeshrabadiya07.
```

## C#

```

// C# program to find sum of all
// elements in generic tree
using System;
using System.Collections.Generic;

class GFG
{

// Represents a node of an n-ary tree
class Node
{
    public int key;
    public List<Node> child;
};

// Utility function to create a new tree node
static Node newNode(int key)
{
    Node temp = new Node();
    temp.key = key;
    temp.child = new List<Node>();
    return temp;
}

// Function to compute the sum
// of all elements in generic tree
static int sumNodes(Node root)
{
    // initialize the sum variable
    int sum = 0;

    if (root == null)
        return 0;

    // Creating a queue and pushing the root
    Queue<Node> q = new Queue<Node>();
    q.Enqueue(root);

    while (q.Count != 0)
    {
        int n = q.Count;

        // If this node has children
        while (n > 0)
        {

            // Dequeue an item from queue and
            // add it to variable "sum"
            Node p = q.Peek();
            q.Dequeue();
            sum += p.key;

            // Enqueue all children of the dequeued item
            for (int i = 0; i < p.child.Count; i++)
                q.Enqueue(p.child[i]);
            n--;
        }
    }
    return sum;
}

// Driver program
public static void Main(String[] args)
{
    // Creating a generic tree
    Node root = newNode(20);
    (root.child).Add(newNode(2));
    (root.child).Add(newNode(34));
    (root.child).Add(newNode(50));
    (root.child).Add(newNode(60));
    (root.child).Add(newNode(70));
    (root.child[0].child).Add(newNode(15));
    (root.child[0].child).Add(newNode(20));
    (root.child[1].child).Add(newNode(30));
    (root.child[2].child).Add(newNode(40));
    (root.child[2].child).Add(newNode(100));
    (root.child[2].child).Add(newNode(20));
    (root.child[0].child[1].child).Add(newNode(25));
    (root.child[0].child[1].child).Add(newNode(50));

    Console.Write(sumNodes(root) +"\n");
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// JavaScript program to find sum of all
// elements in generic tree

// Represents a node of an n-ary tree
class Node
{
  constructor()
  {
    this.key = 0;
    this.child = [];
  }
};

// Utility function to create a new tree node
function newNode(key)
{
    var temp = new Node();
    temp.key = key;
    temp.child = [];
    return temp;
}

// Function to compute the sum
// of all elements in generic tree
function sumNodes(root)
{
    // initialize the sum variable
    var sum = 0;

    if (root == null)
        return 0;

    // Creating a queue and pushing the root
    var q = [];
    q.push(root);

    while (q.length != 0)
    {
        var n = q.length;

        // If this node has children
        while (n > 0)
        {

            // Dequeue an item from queue and
            // add it to variable "sum"
            var p = q[0];
            q.shift();
            sum += p.key;

            // push all children of the dequeued item
            for (var i = 0; i < p.child.length; i++)
                q.push(p.child[i]);
            n--;
        }
    }
    return sum;
}

// Driver program
// Creating a generic tree
var root = newNode(20);
(root.child).push(newNode(2));
(root.child).push(newNode(34));
(root.child).push(newNode(50));
(root.child).push(newNode(60));
(root.child).push(newNode(70));
(root.child[0].child).push(newNode(15));
(root.child[0].child).push(newNode(20));
(root.child[1].child).push(newNode(30));
(root.child[2].child).push(newNode(40));
(root.child[2].child).push(newNode(100));
(root.child[2].child).push(newNode(20));
(root.child[0].child[1].child).push(newNode(25));
(root.child[0].child[1].child).push(newNode(50));
document.write(sumNodes(root) +"<br>");

</script>
```

**输出:**

```
536
```

**时间复杂度:** O(N)，其中 N 为树中节点数。
**辅助空间:** O(N)，其中 N 为树中节点数。