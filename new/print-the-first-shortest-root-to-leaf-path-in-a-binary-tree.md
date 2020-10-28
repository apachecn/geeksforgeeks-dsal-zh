# 在二叉树中打印第一个最短的根到叶路径

> 原文：[https://www.geeksforgeeks.org/print-the-first-shortest-root-to-leaf-path-in-a-binary-tree/](https://www.geeksforgeeks.org/print-the-first-shortest-root-to-leaf-path-in-a-binary-tree/)

给定具有不同值的二叉树，任务是打印第一个最小的根到叶路径。 我们基本上需要打印出节点数最少的最左边的根到叶的路径。

```
Input:
          1
         /  \
        2    3
       /    / \
      4    5   7
     / \        \
    10  11       8
Output: 1 3 5

Input:
          1
         /  \
        2    3
       /    / \
      40   5   7
                \
                 8
Output: 1 2 40

```

**方法**：这个想法是使用队列执行[级别顺序遍历](https://www.geeksforgeeks.org/level-order-tree-traversal/)，即映射**父级**来存储将出现在最短路径中的节点。 使用级别顺序遍历，我们找到最左边的叶子。 找到最左边的叶子后，便使用地图打印路径。

下面是上述方法的实现：

## C++

```cpp

// C++ program to print first shortest
// root to leaf path
#include <bits/stdc++.h>
using namespace std;

// Binary tree node
struct Node {
    struct Node* left;
    struct Node* right;
    int data;
};

// Function to create a new
// Binary node
struct Node* newNode(int data)
{
    struct Node* temp = new Node;

    temp->data = data;
    temp->left = NULL;
    temp->right = NULL;

    return temp;
}

// Recursive function used by leftMostShortest
// to print the first shortest root to leaf path
void printPath(int Data, unordered_map<int,
                             int> parent)
{
    // If the root's data is same as
    // its parent data then return
    if (parent[Data] == Data)
        return;

    // Recur for the function printPath
    printPath(parent[Data], parent);

    // Print the parent node's data
    cout << parent[Data] << " ";
}

// Function to perform level order traversal
// until we find the first leaf node
void leftMostShortest(struct Node* root)
{
    // Queue to store the nodes
    queue<struct Node*> q;

    // Push the root node
    q.push(root);

    // Initialize the value of first
    // leaf node to occur as -1
    int LeafData = -1;

    // To store the current node
    struct Node* temp = NULL;

    // Map to store the parent node's data
    unordered_map<int, int> parent;

    // Parent of root data is set as it's
    // own value
    parent[root->data] = root->data;

    // We store first node of the smallest level
    while (!q.empty()) {
        temp = q.front();
        q.pop();

        // If the first leaf node has been found
        // set the flag variable as 1
        if (!temp->left && !temp->right) {
            LeafData = temp->data;
            break;
        }
        else {

            // If current node has left
            // child, push in the queue
            if (temp->left) {
                q.push(temp->left);

                // Set temp's left node's parent as temp
                parent[temp->left->data] = temp->data;
            }

            // If current node has right
            // child, push in the queue
            if (temp->right) {
                q.push(temp->right);

                // Set temp's right node's parent
                // as temp
                parent[temp->right->data] = temp->data;
            }
        }
    }

    // Recursive function to print the first 
    // shortest root to leaf path
    printPath(LeafData, parent);

    // Print the leaf node of the first
    // shortest path
    cout << LeafData << " ";
}

// Driver code
int main()
{
    struct Node* root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->right->left = newNode(5);
    root->right->right = newNode(7);
    root->left->left->left = newNode(10);
    root->left->left->right = newNode(11);
    root->right->right->left = newNode(8);

    leftMostShortest(root);

    return 0;
}

```

## Java

```java

// Java program to print first shortest
// root to leaf path
import java.util.*;

class GFG{

// Binary tree node
static class Node
{
    Node left;
    Node right;
    int data;
};

// Function to create a new
// Binary node
static Node newNode(int data)
{
    Node temp = new Node();

    temp.data = data;
    temp.left = null;
    temp.right = null;

    return temp;
}

// Recursive function used by leftMostShortest
// to print the first shortest root to leaf path
static void printPath(int Data,
                      HashMap<Integer, 
                              Integer> parent) 
{

    // If the root's data is same as
    // its parent data then return
    if (parent.get(Data) == Data)
        return;

    // Recur for the function printPath
    printPath(parent.get(Data), parent);

    // Print the parent node's data
    System.out.print(parent.get(Data) + " ");
}

// Function to perform level order traversal
// until we find the first leaf node
static void leftMostShortest(Node root)
{

    // Queue to store the nodes
    Queue<Node> q = new LinkedList<>();

    // Add the root node
    q.add(root);

    // Initialize the value of first
    // leaf node to occur as -1
    int LeafData = -1;

    // To store the current node
    Node temp = null;

    // Map to store the parent node's data
    HashMap<Integer, 
            Integer> parent = new HashMap<>();

    // Parent of root data is set as it's
    // own value
    parent.put(root.data, root.data);

    // We store first node of the smallest level
    while (!q.isEmpty())
    {
        temp = q.poll();

        // If the first leaf node has been found
        // set the flag variable as 1
        if (temp.left == null &&
            temp.right == null)
        {
            LeafData = temp.data;
            break;
        } 
        else
        {

            // If current node has left
            // child, add in the queue
            if (temp.left != null) 
            {
                q.add(temp.left);

                // Set temp's left node's parent 
                // as temp
                parent.put(temp.left.data, 
                           temp.data);
            }

            // If current node has right
            // child, add in the queue
            if (temp.right != null)
            {
                q.add(temp.right);

                // Set temp's right node's parent
                // as temp
                parent.put(temp.right.data, 
                                 temp.data);
            }
        }
    }

    // Recursive function to print the 
    // first shortest root to leaf path
    printPath(LeafData, parent);

    // Print the leaf node of the first
    // shortest path
    System.out.println(LeafData + " ");
}

// Driver Code
public static void main(String[] args)
{
    Node root = newNode(1);
    root.left = newNode(2);
    root.right = newNode(3);
    root.left.left = newNode(4);
    root.right.left = newNode(5);
    root.right.right = newNode(7);
    root.left.left.left = newNode(10);
    root.left.left.right = newNode(11);
    root.right.right.left = newNode(8);

    leftMostShortest(root);
}
}

// This code is contributed by sanjeev2552

```

## Python3

```py

# Python3 program to print first 

> 原文：[https://www.geeksforgeeks.org/print-the-first-shortest-root-to-leaf-path-in-a-binary-tree/](https://www.geeksforgeeks.org/print-the-first-shortest-root-to-leaf-path-in-a-binary-tree/)
# shortest root to leaf path 

> 原文：[https://www.geeksforgeeks.org/print-the-first-shortest-root-to-leaf-path-in-a-binary-tree/](https://www.geeksforgeeks.org/print-the-first-shortest-root-to-leaf-path-in-a-binary-tree/)

# Binary tree node 

> 原文：[https://www.geeksforgeeks.org/print-the-first-shortest-root-to-leaf-path-in-a-binary-tree/](https://www.geeksforgeeks.org/print-the-first-shortest-root-to-leaf-path-in-a-binary-tree/)
class Node:

    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# Recursive function used by leftMostShortest 

> 原文：[https://www.geeksforgeeks.org/print-the-first-shortest-root-to-leaf-path-in-a-binary-tree/](https://www.geeksforgeeks.org/print-the-first-shortest-root-to-leaf-path-in-a-binary-tree/)
# to print the first shortest root to leaf path 

> 原文：[https://www.geeksforgeeks.org/print-the-first-shortest-root-to-leaf-path-in-a-binary-tree/](https://www.geeksforgeeks.org/print-the-first-shortest-root-to-leaf-path-in-a-binary-tree/)
def printPath(Data, parent): 

    # If the root's data is same as 
    # its parent data then return 
    if parent[Data] == Data: 
        return

    # Recur for the function printPath 
    printPath(parent[Data], parent) 

    # Print the parent node's data 
    print(parent[Data], end = " ") 

# Function to perform level order traversal 

> 原文：[https://www.geeksforgeeks.org/print-the-first-shortest-root-to-leaf-path-in-a-binary-tree/](https://www.geeksforgeeks.org/print-the-first-shortest-root-to-leaf-path-in-a-binary-tree/)
# until we find the first leaf node 

> 原文：[https://www.geeksforgeeks.org/print-the-first-shortest-root-to-leaf-path-in-a-binary-tree/](https://www.geeksforgeeks.org/print-the-first-shortest-root-to-leaf-path-in-a-binary-tree/)
def leftMostShortest(root): 

    # Queue to store the nodes 
    q = [] 

    # Push the root node 
    q.append(root) 

    # Initialize the value of first 
    # leaf node to occur as -1 
    LeafData = -1

    # To store the current node 
    temp = None

    # Map to store the parent node's data 
    parent = {} 

    # Parent of root data is set 
    # as it's own value 
    parent[root.data] = root.data 

    # We store first node of the 
    # smallest level 
    while len(q) != 0: 
        temp = q.pop(0)

        # If the first leaf node has been 
        # found set the flag variable as 1 
        if not temp.left and not temp.right: 
            LeafData = temp.data 
            break

        else: 

            # If current node has left 
            # child, push in the queue 
            if temp.left: 
                q.append(temp.left) 

                # Set temp's left node's parent as temp 
                parent[temp.left.data] = temp.data 

            # If current node has right 
            # child, push in the queue 
            if temp.right:
                q.append(temp.right) 

                # Set temp's right node's parent 
                # as temp 
                parent[temp.right.data] = temp.data 

    # Recursive function to print the first 
    # shortest root to leaf path 
    printPath(LeafData, parent) 

    # Print the leaf node of the 
    # first shortest path 
    print(LeafData, end = " ")

# Driver code 

> 原文：[https://www.geeksforgeeks.org/print-the-first-shortest-root-to-leaf-path-in-a-binary-tree/](https://www.geeksforgeeks.org/print-the-first-shortest-root-to-leaf-path-in-a-binary-tree/)
if __name__ == "__main__": 

    root = Node(1) 
    root.left = Node(2) 
    root.right = Node(3) 
    root.left.left = Node(4) 
    root.right.left = Node(5) 
    root.right.right = Node(7) 
    root.left.left.left = Node(10) 
    root.left.left.right = Node(11) 
    root.right.right.left = Node(8) 

    leftMostShortest(root) 

# This code is contributed by Rituraj Jain

> 原文：[https://www.geeksforgeeks.org/print-the-first-shortest-root-to-leaf-path-in-a-binary-tree/](https://www.geeksforgeeks.org/print-the-first-shortest-root-to-leaf-path-in-a-binary-tree/)

```

## C#

```cs

// C# program to print first shortest
// root to leaf path
using System;
using System.Collections; 
using System.Collections.Generic;

class GFG{

// Binary tree node
public class Node
{
    public Node left;
    public Node right;
    public int data;
};

// Function to create a new
// Binary node
public static Node newNode(int data)
{
    Node temp = new Node();

    temp.data = data;
    temp.left = null;
    temp.right = null;

    return temp;
}

// Recursive function used by leftMostShortest
// to print the first shortest root to leaf path
static void printPath(int Data, 
           Dictionary<int, int> parent) 
{

    // If the root's data is same as
    // its parent data then return
    if (parent[Data] == Data)
        return;

    // Recur for the function printPath
    printPath(parent[Data], parent);

    // Print the parent node's data
    Console.Write(parent[Data] + " ");
}

// Function to perform level order traversal
// until we find the first leaf node
static void leftMostShortest(Node root)
{

    // Queue to store the nodes
    Queue q = new Queue();

    // Add the root node
    q.Enqueue(root);

    // Initialize the value of first
    // leaf node to occur as -1
    int LeafData = -1;

    // To store the current node
    Node temp = null;

    // Map to store the parent node's data
    Dictionary<int,
               int> parent = new Dictionary<int, 
                                            int>();

    // Parent of root data is set as it's
    // own value
    parent[root.data] = root.data;

    // We store first node of the 
    // smallest level
    while (q.Count != 0)
    {
        temp = (Node)q.Dequeue();

        // If the first leaf node has been 
        // found set the flag variable as 1
        if (temp.left == null &&
           temp.right == null)
        {
            LeafData = temp.data;
            break;
        } 
        else
        {

            // If current node has left
            // child, add in the queue
            if (temp.left != null) 
            {
                q.Enqueue(temp.left);

                // Set temp's left node's parent 
                // as temp
                parent[temp.left.data] = temp.data;
            }

            // If current node has right
            // child, add in the queue
            if (temp.right != null)
            {
                q.Enqueue(temp.right);

                // Set temp's right node's parent
                // as temp
                parent[temp.right.data] = temp.data;
            }
        }
    }

    // Recursive function to print the 
    // first shortest root to leaf path
    printPath(LeafData, parent);

    // Print the leaf node of the first
    // shortest path
    Console.Write(LeafData + " ");
}

// Driver Code
public static void Main(string[] args)
{
    Node root = newNode(1);
    root.left = newNode(2);
    root.right = newNode(3);
    root.left.left = newNode(4);
    root.right.left = newNode(5);
    root.right.right = newNode(7);
    root.left.left.left = newNode(10);
    root.left.left.right = newNode(11);
    root.right.right.left = newNode(8);

    leftMostShortest(root);
}
}

// This code is contributed by rutvik_56

```

**Output:** 

```
1 3 5

```



* * *

* * *



