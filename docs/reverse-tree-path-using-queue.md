# 使用队列

反转树路径

> 原文:[https://www . geesforgeks . org/reverse-tree-path-use-queue/](https://www.geeksforgeeks.org/reverse-tree-path-using-queue/)

给定一棵树和一个节点，任务是反转路径直到给定的节点，并打印修改后的树的有序遍历。

**示例:**

```
Input:  
             7
           /   \
          6     5
         / \   / \
        4   3 2   1    
Node = 4 
Output: 7 6 3 4 2 5 1
The path from root to node 4 is 7 -> 6 -> 4
Reversing this path, the modified tree will be:
             4
           /   \
          6     5
         / \   / \
        7   3 2   1 
whose in-order traversal is 7 6 3 4 2 5 1

Input:
            7
         /    \
        6       5
       / \     / \
      4  3     2  1   
Node = 2 
Output: 4 6 3 2 7 5 1
```

**进场:**

*   首先将给定路径上的所有节点存储在[队列](https://www.geeksforgeeks.org/queue-data-structure/)中。
*   如果找到关键字，则用队列数据的前面替换该节点数据，并弹出前面。
*   继续以递归方式执行此操作，直到根，并且路径将在原始树中反转。
*   现在，打印修改后的树的有序遍历。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// A Binary Tree Node
struct Node {
    int data;
    struct Node *left, *right;
};

// Function to reverse the tree path
queue<int> reverseTreePathUtil(Node* root, int data,
                               queue<int> q1)
{
    queue<int> emptyQueue;

    // If root is null then return
    // an empty queue
    if (root == NULL)
        return emptyQueue;

    // If the node is found
    if (root->data == data) {

        // Replace it with the queue's front
        q1.push(root->data);
        root->data = q1.front();
        q1.pop();
        return q1;
    }

    // Push data into the queue for
    // storing data from start to end
    q1.push(root->data);

    // If the returned queue is empty then
    // it means that the left sub-tree doesn't
    // contain the required node
    queue<int> left = reverseTreePathUtil(root->left,
                                          data, q1);

    // If the returned queue is empty then
    // it means that the right sub-tree doesn't
    // contain the required node
    queue<int> right = reverseTreePathUtil(root->right,
                                           data, q1);

    // If the required node is found
    // in the right sub-tree
    if (!right.empty()) {

        // Replace with the queue's front
        root->data = right.front();
        right.pop();
        return right;
    }

    // If the required node is found
    // in the right sub-tree
    if (!left.empty()) {

        // Replace with the queue's front
        root->data = left.front();
        left.pop();
        return left;
    }

    // Return emptyQueue if path
    // is not found
    return emptyQueue;
}

// Function to call reverseTreePathUtil
// to reverse the tree path
void reverseTreePath(Node* root, int data)
{
    queue<int> q1;
    // reverse tree path
    reverseTreePathUtil(root, data, q1);
}

// Function to print the in-order
// traversal of the tree
void inorder(Node* root)
{
    if (root != NULL) {
        inorder(root->left);
        cout << root->data << " ";
        inorder(root->right);
    }
}

// Utility function to create a new tree node
Node* newNode(int data)
{
    Node* temp = new Node;
    temp->data = data;
    temp->left = temp->right = NULL;
    return temp;
}

// Driver code
int main()
{
    Node* root = newNode(7);
    root->left = newNode(6);
    root->right = newNode(5);
    root->left->left = newNode(4);
    root->left->right = newNode(3);
    root->right->left = newNode(2);
    root->right->right = newNode(1);

    int data = 4;

    // Function call to reverse the path
    reverseTreePath(root, data);

    // Print the in-order traversal
    // of the modified tree
    inorder(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;
public class Main
{
  // A Binary Tree Node
  static class Node {

    public int data;
    public Node left, right;

    public Node(int data)
    {
      this.data = data;
      left = right = null;
    }
  }

  // Function to reverse the tree path
  static Vector<Integer> reverseTreePathUtil(Node root, int data, Vector<Integer> q1)
  {
    Vector<Integer> emptyQueue = new Vector<Integer>();

    // If root is null then return
    // an empty queue
    if (root == null)
      return emptyQueue;

    // If the node is found
    if (root.data == data) {

      // Replace it with the queue's front
      q1.add(root.data);
      root.data = q1.get(0);
      q1.remove(0);
      return q1;
    }

    // Push data into the queue for
    // storing data from start to end
    q1.add(root.data);

    // If the returned queue is empty then
    // it means that the left sub-tree doesn't
    // contain the required node
    Vector<Integer> left = reverseTreePathUtil(root.left, data, q1);

    // If the returned queue is empty then
    // it means that the right sub-tree doesn't
    // contain the required node
    Vector<Integer> right = reverseTreePathUtil(root.right, data, q1);

    // If the required node is found
    // in the right sub-tree
    if (right.size() > 0) {

      // Replace with the queue's front
      root.data = right.get(0);
      right.remove(0);
      return right;
    }

    // If the required node is found
    // in the right sub-tree
    if (left.size() > 0) {

      // Replace with the queue's front
      root.data = left.get(0);
      left.remove(0);
      return left;
    }

    // Return emptyQueue if path
    // is not found
    return emptyQueue;
  }

  // Function to call reverseTreePathUtil
  // to reverse the tree path
  static void reverseTreePath(Node root, int data)
  {
    Vector<Integer> q1 = new Vector<Integer>();
    // reverse tree path
    reverseTreePathUtil(root, data, q1);
  }

  // Function to print the in-order
  // traversal of the tree
  static void inorder(Node root)
  {
    if (root != null) {
      inorder(root.left);
      System.out.print(root.data + " ");
      inorder(root.right);
    }
  }

  // Utility function to create a new tree node
  static Node newNode(int data)
  {
    Node temp = new Node(data);
    return temp;
  }

  public static void main(String[] args)
  {
    // Driver code
    Node root = newNode(7);
    root.left = newNode(6);
    root.right = newNode(5);
    root.left.left = newNode(4);
    root.left.right = newNode(3);
    root.right.left = newNode(2);
    root.right.right = newNode(1);

    int data = 4;

    // Function call to reverse the path
    reverseTreePath(root, data);

    // Print the in-order traversal
    // of the modified tree
    inorder(root);
  }
}

// This code is contributed by divyesh072019.
```

## 蟒蛇 3

```
# Python3 implementation of the
# above approach

# A Binary Tree Node
class Node:

    def __init__(self, data):

        self.data = data
        self.left = None
        self.right = None

# Function to reverse the
# tree path
def reverseTreePathUtil(root,
                        data, q1):

    emptyQueue = []

    # If root is null then
    # return an empty queue
    if (root == None):
        return emptyQueue;

    # If the node is found
    if (root.data == data):

        # Replace it with the
        # queue's front
        q1.append(root.data);
        root.data = q1[0]
        q1.pop(0);
        return q1;   

    # Push data into the
    # queue for storing
    # data from start to end
    q1.append(root.data);

    # If the returned queue
    # is empty then it means
    # that the left sub-tree
    # doesn't contain the
    # required node
    left = reverseTreePathUtil(root.left,
                               data, q1);

    # If the returned queue is empty
    # then it means that the right
    # sub-tree doesn't contain the
    # required node
    right = reverseTreePathUtil(root.right,
                                data, q1);

    # If the required node is found
    # in the right sub-tree
    if len(right) != 0:

        # Replace with the queue's
        # front
        root.data = right[0]
        right.pop(0);
        return right;

    # If the required node
    # is found in the right
    # sub-tree
    if len(left) != 0:

        # Replace with the
        # queue's front
        root.data = left[0]
        left.pop(0);
        return left;

    # Return emptyQueue
    # if path is not found
    return emptyQueue;

# Function to call reverseTreePathUtil
# to reverse the tree path
def reverseTreePath(root, data):

    q1 = []

    # reverse tree path
    reverseTreePathUtil(root,
                        data, q1);

# Function to print the in-order
# traversal of the tree
def inorder(root):

    if (root != None):
        inorder(root.left);
        print(root.data,
              end = ' ')
        inorder(root.right);

# Utility function to create
# a new tree node
def newNode(data):

    temp = Node(data)
    return temp;

# Driver code
if __name__ == "__main__":

    root = newNode(7);
    root.left = newNode(6);
    root.right = newNode(5);
    root.left.left = newNode(4);
    root.left.right = newNode(3);
    root.right.left = newNode(2);
    root.right.right = newNode(1);

    data = 4;

    # Function call to reverse
    # the path
    reverseTreePath(root, data);

    # Print the in-order traversal
    # of the modified tree
    inorder(root);

# This code is contributed by Rutvik_56
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;
class GFG {

    // A Binary Tree Node
    class Node {

        public int data;
        public Node left, right;

        public Node(int data)
        {
            this.data = data;
            left = right = null;
        }
    }

    // Function to reverse the tree path
    static List<int> reverseTreePathUtil(Node root, int data, List<int> q1)
    {
        List<int> emptyQueue = new List<int>();

        // If root is null then return
        // an empty queue
        if (root == null)
            return emptyQueue;

        // If the node is found
        if (root.data == data) {

            // Replace it with the queue's front
            q1.Add(root.data);
            root.data = q1[0];
            q1.RemoveAt(0);
            return q1;
        }

        // Push data into the queue for
        // storing data from start to end
        q1.Add(root.data);

        // If the returned queue is empty then
        // it means that the left sub-tree doesn't
        // contain the required node
        List<int> left = reverseTreePathUtil(root.left, data, q1);

        // If the returned queue is empty then
        // it means that the right sub-tree doesn't
        // contain the required node
        List<int> right = reverseTreePathUtil(root.right, data, q1);

        // If the required node is found
        // in the right sub-tree
        if (right.Count > 0) {

            // Replace with the queue's front
            root.data = right[0];
            right.RemoveAt(0);
            return right;
        }

        // If the required node is found
        // in the right sub-tree
        if (left.Count > 0) {

            // Replace with the queue's front
            root.data = left[0];
            left.RemoveAt(0);
            return left;
        }

        // Return emptyQueue if path
        // is not found
        return emptyQueue;
    }

    // Function to call reverseTreePathUtil
    // to reverse the tree path
    static void reverseTreePath(Node root, int data)
    {
        List<int> q1 = new List<int>();
        // reverse tree path
        reverseTreePathUtil(root, data, q1);
    }

    // Function to print the in-order
    // traversal of the tree
    static void inorder(Node root)
    {
        if (root != null) {
            inorder(root.left);
            Console.Write(root.data + " ");
            inorder(root.right);
        }
    }

    // Utility function to create a new tree node
    static Node newNode(int data)
    {
        Node temp = new Node(data);
        return temp;
    }

  static void Main() {
    // Driver code
    Node root = newNode(7);
    root.left = newNode(6);
    root.right = newNode(5);
    root.left.left = newNode(4);
    root.left.right = newNode(3);
    root.right.left = newNode(2);
    root.right.right = newNode(1);

    int data = 4;

    // Function call to reverse the path
    reverseTreePath(root, data);

    // Print the in-order traversal
    // of the modified tree
    inorder(root); 
  }
}

// This code is contributed by mukesh07.
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// A Binary Tree Node
class Node
{
    constructor(data)
    {
        this.left = null;
        this.right = null;
        this.data = data;
    }
}

// Function to reverse the tree path
function reverseTreePathUtil(root, data, q1)
{
    let emptyQueue = [];

    // If root is null then return
    // an empty queue
    if (root == null)
        return emptyQueue;

    // If the node is found
    if (root.data == data)
    {

        // Replace it with the queue's front
        q1.push(root.data);
        root.data = q1[0];
        q1.shift();
        return q1;
    }

    // Push data into the queue for
    // storing data from start to end
    q1.push(root.data);

    // If the returned queue is empty then
    // it means that the left sub-tree doesn't
    // contain the required node
    let left = reverseTreePathUtil(root.left, data, q1);

    // If the returned queue is empty then
    // it means that the right sub-tree doesn't
    // contain the required node
    let right = reverseTreePathUtil(root.right, data, q1);

    // If the required node is found
    // in the right sub-tree
    if (right.length > 0)
    {

        // Replace with the queue's front
        root.data = right[0];
        right.shift();
        return right;
    }

    // If the required node is found
    // in the right sub-tree
    if (left.length > 0)
    {

        // Replace with the queue's front
        root.data = left[0];
        left.shift();
        return left;
    }

    // Return emptyQueue if path
    // is not found
    return emptyQueue;
}

// Function to call reverseTreePathUtil
// to reverse the tree path
function reverseTreePath(root, data)
{
    let q1 = [];

    // Reverse tree path
    reverseTreePathUtil(root, data, q1);
}

// Function to print the in-order
// traversal of the tree
function inorder(root)
{
    if (root != null)
    {
        inorder(root.left);
        document.write(root.data + " ");
        inorder(root.right);
    }
}

// Utility function to create a new tree node
function newNode(data)
{
    let temp = new Node(data);
    return temp;
}

// Driver code
let root = newNode(7);
root.left = newNode(6);
root.right = newNode(5);
root.left.left = newNode(4);
root.left.right = newNode(3);
root.right.left = newNode(2);
root.right.right = newNode(1);

let data = 4;

// Function call to reverse the path
reverseTreePath(root, data);

// Print the in-order traversal
// of the modified tree
inorder(root);  

// This code is contributed by divyeshrabadiya07

</script>
```

**Output:** 

```
7 6 3 4 2 5 1
```