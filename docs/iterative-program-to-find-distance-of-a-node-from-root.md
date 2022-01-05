# 求节点到根的距离的迭代程序

> 原文:[https://www . geeksforgeeks . org/迭代程序查找根节点距离/](https://www.geeksforgeeks.org/iterative-program-to-find-distance-of-a-node-from-root/)

给定二叉树的根和其中的一个键 x，求给定键到根节点的距离。距离是指两个节点之间的边数。

**示例**:

```
Input : x = 45,
   5 is Root of below tree
        5
      /    \
    10      15
    / \    /  \
  20  25  30   35
       \
       45
Output : Distance = 3             
There are three edges on path
from root to 45.

For more understanding of question,
in above tree distance of 35 is two
and distance of 10 is 1.
```

**相关问题** : [求节点距根](https://www.geeksforgeeks.org/find-distance-root-given-node-binary-tree/)距离的递归程序。
**迭代方法:**

*   使用级别顺序遍历使用队列迭代遍历树。
*   保留一个变量*电平计数*来保持当前电平的轨迹。
*   为此，每次移动到下一个级别时，在将空节点推入队列时，也会增加变量 levelCount 的值，以便存储当前的级别号。
*   遍历树时，检查当前级别是否有任何节点与给定的键匹配。
*   如果是，则返回级别计数。

下面是上述方法的实现:

## C++

```
// C++ program to find distance of a given
// node from root.
#include <bits/stdc++.h>
using namespace std;

// A Binary Tree Node
struct Node {
    int data;
    Node *left, *right;
};

// A utility function to create a new Binary
// Tree Node
Node* newNode(int item)
{
    Node* temp = new Node;
    temp->data = item;
    temp->left = temp->right = NULL;
    return temp;
}

/* Function to find distance of a node from root
*  root : root of the Tree
*  key : data whose distance to be calculated
*/
int findDistance(Node* root, int key)
{

    // base case
    if (root == NULL) {
        return -1;
    }

    // If the key is present at root,
    // distance is zero
    if (root->data == key)
        return 0;

    // Iterating through tree using BFS
    queue<Node*> q;

    // pushing root to the queue
    q.push(root);

    // pushing marker to the queue
    q.push(NULL);

    // Variable to store count of level
    int levelCount = 0;

    while (!q.empty()) {

        Node* temp = q.front();
        q.pop();

        // if node is marker, push marker to queue
        // else, push left and right (if exists)
        if (temp == NULL && !q.empty()) {
            q.push(NULL);

            // Increment levelCount, while moving
            // to new level
            levelCount++;
        }
        else if (temp != NULL) {

            // If node at current level is Key,
            // return levelCount
            if (temp->data == key)
                return levelCount;

            if (temp->left)
                q.push(temp->left);

            if (temp->right)
                q.push(temp->right);
        }
    }

    // If key is not found
    return -1;
}

// Driver Code
int main()
{
    Node* root = newNode(5);
    root->left = newNode(10);
    root->right = newNode(15);
    root->left->left = newNode(20);
    root->left->right = newNode(25);
    root->left->right->right = newNode(45);
    root->right->left = newNode(30);
    root->right->right = newNode(35);

    cout << findDistance(root, 45);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find distance of a given
// node from root.
import java.util.*;

class GFG
{

// A Binary Tree Node
static class Node
{
    int data;
    Node left, right;
};

// A utility function to create a new Binary
// Tree Node
static Node newNode(int item)
{
    Node temp = new Node();
    temp.data = item;
    temp.left = temp.right = null;
    return temp;
}

/* Function to find distance of a node from root
* root : root of the Tree
* key : data whose distance to be calculated
*/
static int findDistance(Node root, int key)
{

    // base case
    if (root == null)
    {
        return -1;
    }

    // If the key is present at root,
    // distance is zero
    if (root.data == key)
        return 0;

    // Iterating through tree using BFS
    Queue<Node> q = new LinkedList<Node>();

    // adding root to the queue
    q.add(root);

    // adding marker to the queue
    q.add(null);

    // Variable to store count of level
    int levelCount = 0;

    while (!q.isEmpty())
    {
        Node temp = q.peek();
        q.remove();

        // if node is marker, push marker to queue
        // else, push left and right (if exists)
        if (temp == null && !q.isEmpty())
        {
            q.add(null);

            // Increment levelCount, while moving
            // to new level
            levelCount++;
        }

        else if (temp != null)
        {

            // If node at current level is Key,
            // return levelCount
            if (temp.data == key)
                return levelCount;

            if (temp.left != null)
                q.add(temp.left);

            if (temp.right != null)
                q.add(temp.right);
        }
    }

    // If key is not found
    return -1;
}

// Driver Code
public static void main(String[] args)
{
    Node root = newNode(5);
    root.left = newNode(10);
    root.right = newNode(15);
    root.left.left = newNode(20);
    root.left.right = newNode(25);
    root.left.right.right = newNode(45);
    root.right.left = newNode(30);
    root.right.right = newNode(35);

    System.out.println(findDistance(root, 45));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python program to find distance of a given
# node from root.
from collections import deque

# A tree binary node
class Node:
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# Function to find distance of a node from root
# root : root of the Tree
# key : data whose distance to be calculated
def findDistance(root: Node, key: int) -> int:

    # base case
    if root is None:
        return -1

    # If the key is present at root,
    # distance is zero
    if root.data == key:
        return 0

    # Iterating through tree using BFS
    q = deque()

    # pushing root to the queue
    q.append(root)

    # pushing marker to the queue
    q.append(None)

    # Variable to store count of level
    levelCount = 0

    while q:
        temp = q[0]
        q.popleft()

        # if node is marker, push marker to queue
        # else, push left and right (if exists)
        if temp is None and q:
            q.append(None)

            # Increment levelCount, while moving
            # to new level
            levelCount += 1
        elif temp:

            # If node at current level is Key,
            # return levelCount
            if temp.data == key:
                return levelCount

            if temp.left:
                q.append(temp.left)

            if temp.right:
                q.append(temp.right)

    # If key is not found
    return -1

# Driver Code
if __name__ == "__main__":

    root = Node(5)
    root.left = Node(10)
    root.right = Node(15)
    root.left.left = Node(20)
    root.left.right = Node(25)
    root.left.right.right = Node(45)
    root.right.left = Node(30)
    root.right.right = Node(35)

    print(findDistance(root, 45))

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# program to find distance of a given
// node from root.
using System;
using System.Collections.Generic;

class GFG
{

// A Binary Tree Node
class Node
{
    public int data;
    public Node left, right;
};

// A utility function to create a new Binary
// Tree Node
static Node newNode(int item)
{
    Node temp = new Node();
    temp.data = item;
    temp.left = temp.right = null;
    return temp;
}

/* Function to find distance of a node from root
* root : root of the Tree
* key : data whose distance to be calculated*/
static int findDistance(Node root, int key)
{

    // base case
    if (root == null)
    {
        return -1;
    }

    // If the key is present at root,
    // distance is zero
    if (root.data == key)
        return 0;

    // Iterating through tree using BFS
    Queue<Node> q = new Queue<Node>();

    // adding root to the queue
    q.Enqueue(root);

    // adding marker to the queue
    q.Enqueue(null);

    // Variable to store count of level
    int levelCount = 0;

    while (q.Count!=0)
    {
        Node temp = q.Peek();
        q.Dequeue();

        // if node is marker, push marker to queue
        // else, push left and right (if exists)
        if (temp == null && q.Count!=0)
        {
            q.Enqueue(null);

            // Increment levelCount, while moving
            // to new level
            levelCount++;
        }

        else if (temp != null)
        {

            // If node at current level is Key,
            // return levelCount
            if (temp.data == key)
                return levelCount;

            if (temp.left != null)
                q.Enqueue(temp.left);

            if (temp.right != null)
                q.Enqueue(temp.right);
        }
    }

    // If key is not found
    return -1;
}

// Driver Code
public static void Main(String[] args)
{
    Node root = newNode(5);
    root.left = newNode(10);
    root.right = newNode(15);
    root.left.left = newNode(20);
    root.left.right = newNode(25);
    root.left.right.right = newNode(45);
    root.right.left = newNode(30);
    root.right.right = newNode(35);

    Console.WriteLine(findDistance(root, 45));
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript program to find distance
// of a given node from root.

// A Binary Tree Node
class Node
{
    constructor(item)
    {
        this.left = null;
        this.right = null;
        this.data = item;
    }
}

// A utility function to create a new Binary
// Tree Node
function newNode(item)
{
    let temp = new Node(item);
    return temp;
}

/* Function to find distance of a node from root
* root : root of the Tree
* key : data whose distance to be calculated
*/
function findDistance(root, key)
{

    // Base case
    if (root == null)
    {
        return -1;
    }

    // If the key is present at root,
    // distance is zero
    if (root.data == key)
        return 0;

    // Iterating through tree using BFS
    let q = [];

    // Adding root to the queue
    q.push(root);

    // Adding marker to the queue
    q.push(null);

    // Variable to store count of level
    let levelCount = 0;

    while (q.length > 0)
    {
        let temp = q[0];
        q.shift();

        // If node is marker, push marker to queue
        // else, push left and right (if exists)
        if (temp == null && q.length > 0)
        {
            q.push(null);

            // Increment levelCount, while moving
            // to new level
            levelCount++;
        }

        else if (temp != null)
        {

            // If node at current level is Key,
            // return levelCount
            if (temp.data == key)
                return levelCount;

            if (temp.left != null)
                q.push(temp.left);

            if (temp.right != null)
                q.push(temp.right);
        }
    }

    // If key is not found
    return -1;
}

// Driver code
let root = newNode(5);
root.left = newNode(10);
root.right = newNode(15);
root.left.left = newNode(20);
root.left.right = newNode(25);
root.left.right.right = newNode(45);
root.right.left = newNode(30);
root.right.right = newNode(35);

document.write(findDistance(root, 45));

// This code is contributed by suresh07

</script>
```

**Output:** 

```
3
```