# 二叉查找树中具有给定范围内的值的节点的总和

> 原文:[https://www . geeksforgeeks . org/二进制搜索树中节点的总和-给定范围内的值/](https://www.geeksforgeeks.org/sum-of-nodes-in-a-binary-search-tree-with-values-from-a-given-range/)

给定一个由 **N** 节点和两个正整数 **L** 和 **R** 组成的[二叉查找树](https://www.geeksforgeeks.org/binary-search-tree-set-1-search-and-insertion/)，任务是找出位于**【L，R】**范围内的所有节点的值之和。

**示例:**

> **输入:** L = 7，R = 15
> 10
> /\
> 5 15
> /\ \
> 3 7 18
> **输出:** 32
> **解释:**
> 给定树中位于范围【7，15】内的节点为{7，10，15}。因此，节点的总和是 7 + 10 + 15 = 32。
> 
> **输入:** L = 11，R = 15
> 8
> /\
> 5 11
> /\ \
> 3 6 20
> **输出:** 11

**方法:**给定的问题可以通过执行任意[树遍历](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)并计算位于范围**【L，R】**内的节点的和来解决。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Class for node of the Tree
class Node {
public:
    int val;
    Node *left, *right;
};

// Function to create a new BST node
Node* newNode(int item)
{
    Node* temp = new Node();
    temp->val = item;
    temp->left = temp->right = NULL;

    // Return the newly created node
    return temp;
}

// Stores the sum of all nodes
// lying in the range [L, R]
int sum = 0;

// Function to perform level order
// traversal on the Tree and
// calculate the required sum
int rangeSumBST(Node* root, int low,
                int high)
{
    // Base Case
    if (root == NULL)
        return 0;

    // Stores the nodes while
    // performing level order traversal
    queue<Node*> q;

    // Push the root node
    // into the queue
    q.push(root);

    // Iterate until queue is empty
    while (q.empty() == false) {

        // Stores the front
        // node of the queue
        Node* curr = q.front();
        q.pop();

        // If the value of the node
        // lies in the given range
        if (curr->val >= low
            && curr->val <= high) {

            // Add it to sum
            sum += curr->val;
        }

        // If the left child is
        // not NULL and exceeds low
        if (curr->left != NULL
            && curr->val > low)

            // Insert into queue
            q.push(curr->left);

        // If the right child is not
        // NULL and exceeds low
        if (curr->right != NULL
            && curr->val < high)

            // Insert into queue
            q.push(curr->right);
    }

    // Return the resultant sum
    return sum;
}

// Function to insert a new node
// into the Binary Search Tree
Node* insert(Node* node, int data)
{
    // Base Case
    if (node == NULL)
        return newNode(data);

    // If the data is less than the
    // value of the current node
    if (data <= node->val)

        // Recur for left subtree
        node->left = insert(node->left,
                            data);

    // Otherwise
    else

        // Recur for the right subtree
        node->right = insert(node->right,
                             data);

    // Return the node
    return node;
}

// Driver Code
int main()
{
    /* Let us create following BST
         10   
        / \
       5   15
      / \     \
     3   7    18  */
    Node* root = NULL;
    root = insert(root, 10);
    insert(root, 5);
    insert(root, 15);
    insert(root, 3);
    insert(root, 7);
    insert(root, 18);

    int L = 7, R = 15;
    cout << rangeSumBST(root, L, R);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Class for node of the Tree
static class Node
{
    int val;
    Node left, right;
};

// Function to create a new BST node
static Node newNode(int item)
{
    Node temp = new Node();
    temp.val = item;
    temp.left = temp.right = null;

    // Return the newly created node
    return temp;
}

// Stores the sum of all nodes
// lying in the range [L, R]
static int sum = 0;

// Function to perform level order
// traversal on the Tree and
// calculate the required sum
static int rangeSumBST(Node root, int low,
                                  int high)
{

    // Base Case
    if (root == null)
    return 0;

    // Stores the nodes while
    // performing level order traversal
    Queue<Node> q = new LinkedList<Node>();

    // Push the root node
    // into the queue
    q.add(root);

    // Iterate until queue is empty
    while (q.isEmpty() == false)
    {

        // Stores the front
        // node of the queue
        Node curr = q.peek();
        q.remove();

        // If the value of the node
        // lies in the given range
        if (curr.val >= low &&
            curr.val <= high)
        {

            // Add it to sum
            sum += curr.val;
        }

        // If the left child is
        // not null and exceeds low
        if (curr.left != null &&
            curr.val > low)

            // Insert into queue
            q.add(curr.left);

        // If the right child is not
        // null and exceeds low
        if (curr.right != null &&
            curr.val < high)

            // Insert into queue
            q.add(curr.right);
    }

    // Return the resultant sum
    return sum;
}

// Function to insert a new node
// into the Binary Search Tree
static Node insert(Node node, int data)
{

    // Base Case
    if (node == null)
        return newNode(data);

    // If the data is less than the
    // value of the current node
    if (data <= node.val)

        // Recur for left subtree
        node.left = insert(node.left,
                           data);

    // Otherwise
    else

        // Recur for the right subtree
        node.right = insert(node.right,
                            data);

    // Return the node
    return node;
}

// Driver Code
public static void main(String[] args)
{

    /* Let us create following BST
         10   
        / \
       5   15
      / \     \
     3   7    18  */
    Node root = null;
    root = insert(root, 10);
    insert(root, 5);
    insert(root, 15);
    insert(root, 3);
    insert(root, 7);
    insert(root, 18);

    int L = 7, R = 15;
    System.out.print(rangeSumBST(root, L, R));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for the above approach
from collections import deque

# Class for node of the Tree
class Node:
    def __init__(self,v):
        self.val = v
        self.left = None
        self.right = None

# Function to perform level order
# traversal on the Tree and
# calculate the required sum
def rangeSumBST(root, low, high):
    sum = 0

    # Base Case
    if (root == None):
        return 0

    # Stores the nodes while
    # performing level order traversal
    q = deque()

    # Push the root node
    # into the queue
    q.append(root)

    # Iterate until queue is empty
    while (len(q) > 0):

        # Stores the front
        # node of the queue
        curr = q.popleft()
        # q.pop()

        # If the value of the node
        # lies in the given range
        if (curr.val >= low
            and curr.val <= high):

            # Add it to sum
            sum += curr.val

        # If the left child is
        # not NULL and exceeds low
        if (curr.left != None
            and curr.val > low):

            # Insert into queue
            q.append(curr.left)

        # If the right child is not
        # NULL and exceeds low
        if (curr.right != None
            and curr.val < high):

            # Insert into queue
            q.append(curr.right)

    # Return the resultant sum
    return sum

# Function to insert a new node
# into the Binary Search Tree
def insert(node, data):

    # Base Case
    if (node == None):
        return Node(data)

    # If the data is less than the
    # value of the current node
    if (data <= node.val):

        # Recur for left subtree
        node.left = insert(node.left, data)
    # Otherwise
    else:
        # Recur for the right subtree
        node.right = insert(node.right, data)

    # Return the node
    return node

# Driver Code
if __name__ == '__main__':
    # /* Let us create following BST
    #      10
    #     / \
    #    5   15
    #   / \     \
    #  3   7    18  */
    root = None
    root = insert(root, 10)
    root = insert(root, 5)
    root = insert(root, 15)
    root = insert(root, 3)
    root = insert(root, 7)
    root = insert(root, 18)

    L, R = 7, 15
    print(rangeSumBST(root, L, R))

# This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Class for node of the Tree
class Node
{
    public int val;
    public Node left, right;
};

// Function to create a new BST node
static Node newNode(int item)
{
    Node temp = new Node();
    temp.val = item;
    temp.left = temp.right = null;

    // Return the newly created node
    return temp;
}

// Stores the sum of all nodes
// lying in the range [L, R]
static int sum = 0;

// Function to perform level order
// traversal on the Tree and
// calculate the required sum
static int rangeSumBST(Node root, int low,
                                  int high)
{

    // Base Case
    if (root == null)
    return 0;

    // Stores the nodes while
    // performing level order traversal
    Queue<Node> q = new Queue<Node>();

    // Push the root node
    // into the queue
    q.Enqueue(root);

    // Iterate until queue is empty
    while (q.Count!=0)
    {

        // Stores the front
        // node of the queue
        Node curr = q.Peek();
        q.Dequeue();

        // If the value of the node
        // lies in the given range
        if (curr.val >= low &&
            curr.val <= high)
        {

            // Add it to sum
            sum += curr.val;
        }

        // If the left child is
        // not null and exceeds low
        if (curr.left != null &&
            curr.val > low)

            // Insert into queue
            q.Enqueue(curr.left);

        // If the right child is not
        // null and exceeds low
        if (curr.right != null &&
            curr.val < high)

            // Insert into queue
            q.Enqueue(curr.right);
    }

    // Return the resultant sum
    return sum;
}

// Function to insert a new node
// into the Binary Search Tree
static Node insert(Node node, int data)
{

    // Base Case
    if (node == null)
        return newNode(data);

    // If the data is less than the
    // value of the current node
    if (data <= node.val)

        // Recur for left subtree
        node.left = insert(node.left,
                           data);

    // Otherwise
    else

        // Recur for the right subtree
        node.right = insert(node.right,
                            data);

    // Return the node
    return node;
}

// Driver Code
public static void Main(String[] args)
{

    /* Let us create following BST
         10   
        / \
       5   15
      / \     \
     3   7    18  */
    Node root = null;
    root = insert(root, 10);
    insert(root, 5);
    insert(root, 15);
    insert(root, 3);
    insert(root, 7);
    insert(root, 18);

    int L = 7, R = 15;
    Console.Write(rangeSumBST(root, L, R));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Class for node of the Tree
class Node
{
    // Function to create a new BST node
    constructor(item)
    {
        this.val=item;
        this.left=this.right=null;
    }
}

// Stores the sum of all nodes
// lying in the range [L, R]
let sum = 0;

// Function to perform level order
// traversal on the Tree and
// calculate the required sum
function rangeSumBST(root,low,high)
{
    // Base Case
    if (root == null)
        return 0;

    // Stores the nodes while
    // performing level order traversal
    let q = [];

    // Push the root node
    // into the queue
    q.push(root);

    // Iterate until queue is empty
    while (q.length!=0)
    {

        // Stores the front
        // node of the queue
        let curr = q.shift();

        // If the value of the node
        // lies in the given range
        if (curr.val >= low &&
            curr.val <= high)
        {

            // Add it to sum
            sum += curr.val;
        }

        // If the left child is
        // not null and exceeds low
        if (curr.left != null &&
            curr.val > low)

            // Insert into queue
            q.push(curr.left);

        // If the right child is not
        // null and exceeds low
        if (curr.right != null &&
            curr.val < high)

            // Insert into queue
            q.push(curr.right);
    }

    // Return the resultant sum
    return sum;
}

// Function to insert a new node
// into the Binary Search Tree
function  insert(node,data)
{
    // Base Case
    if (node == null)
        return new Node(data);

    // If the data is less than the
    // value of the current node
    if (data <= node.val)

        // Recur for left subtree
        node.left = insert(node.left,
                           data);

    // Otherwise
    else

        // Recur for the right subtree
        node.right = insert(node.right,
                            data);

    // Return the node
    return node;
}

// Driver Code
/* Let us create following BST
         10  
        / \
       5   15
      / \     \
     3   7    18  */
let root = null;
root = insert(root, 10);
insert(root, 5);
insert(root, 15);
insert(root, 3);
insert(root, 7);
insert(root, 18);

let L = 7, R = 15;
document.write(rangeSumBST(root, L, R));

// This code is contributed by patel2127

</script>
```

**Output**

```
32
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)

**另一种方法:**
在这种方法中，我们可以直接在二叉查找树上应用 In-Order [遍历](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)，如果该节点值位于范围【L，R】之间，那么我们可以简单地将其添加到总和中。

## C++

```
// C++ program for the above approach
// This Code is contributed by Omkar Subhash Ghongade
#include <bits/stdc++.h>
using namespace std;

// Class for node of the Tree
class Node {
public:
    int val;
    Node *left, *right;
};

// Function to create a new BST node
Node* newNode(int item)
{
    Node* temp = new Node();
    temp->val = item;
    temp->left = temp->right = NULL;

    // Return the newly created node
    return temp;
}

// Stores the sum of all nodes
// lying in the range [L, R]
int sum = 0;

// Function to perform level order
// traversal on the Tree and
// calculate the required sum
void rangeSumBST(Node* root, int low, int high, int* sum)
{
    if (root != NULL) {
        // Giving a call to the left subtree
        rangeSumBST(root->left, low, high, sum);
        // checking if the value at that node is in the
        // range or not.
        if (root->val >= low && root->val <= high)
            *sum += root->val;
        // Giving a call to the right subtree
        rangeSumBST(root->right, low, high, sum);
    }
}

// Function to insert a new node
// into the Binary Search Tree
Node* insert(Node* node, int data)
{
    // Base Case
    if (node == NULL)
        return newNode(data);

    // If the data is less than the
    // value of the current node
    if (data <= node->val)

        // Recur for left subtree
        node->left = insert(node->left, data);

    // Otherwise
    else

        // Recur for the right subtree
        node->right = insert(node->right, data);

    // Return the node
    return node;
}

// Driver Code
int main()
{
    /* Let us create following BST
            10
            / \
    5 15
    / \     \
    3 7 18 */
    Node* root = NULL;
    root = insert(root, 10);
    insert(root, 5);
    insert(root, 15);
    insert(root, 3);
    insert(root, 7);
    insert(root, 18);

    int L = 7, R = 15, sum = 0;
    rangeSumBST(root, L, R, &sum);
    cout << sum;
    return 0;
}
```

**Output**

```
32
```

**时间复杂度:** O(n)，n 为树中节点数。
**辅助空间:** O(1)