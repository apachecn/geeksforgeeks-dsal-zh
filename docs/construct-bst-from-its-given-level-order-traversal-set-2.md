# 从其给定的层级顺序遍历| Set-2

构造 BST

> 原文:[https://www . geesforgeks . org/construct-BST-from-its-level-order-遍历-set-2/](https://www.geeksforgeeks.org/construct-bst-from-its-given-level-order-traversal-set-2/)

根据给定的级别顺序遍历来构造 BST(二叉查找树)。

**示例:**

```
Input : {7, 4, 12, 3, 6, 8, 1, 5, 10}
Output : 
BST: 
        7        
       / \       
      4   12      
     / \  /     
    3  6 8    
   /  /   \
  1   5   10
```

**方法:**
想法是制作一个结构元素 NodeDetails，它包含一个指向祖先的节点、最小数据和最大数据的指针。现在执行以下步骤:

*   将根节点推入节点详细信息类型的队列。
*   从队列中提取节点的详细信息，并将其与最小值和最大值进行比较。
*   检查 arr[]中是否有更多的元素，arr[i]是否可以保留为“temp.ptr”的子元素。
*   检查 arr[]中是否有更多的元素，arr[i]是否可以是“temp.ptr”的右子元素。
*   当队列变空时结束循环。

下面是上述方法的实现:

## C++

```
// C++ program to construct BST
// using level order traversal
#include <bits/stdc++.h>
using namespace std;

// Node structure of a binary tree
struct Node {
    int data;
    Node* right;
    Node* left;

    Node(int x)
    {
        data = x;
        right = NULL;
        left = NULL;
    }
};

// Structure formed to store the
// details of the ancestor
struct NodeDetails {
    Node* ptr;
    int min, max;
};

// Function for the preorder traversal
void preorderTraversal(Node* root)
{
    if (!root)
        return;
    cout << root->data << " ";

    // Traversing left child
    preorderTraversal(root->left);

    // Traversing right child
    preorderTraversal(root->right);
}

// Function to make a new node
// and return its pointer
Node* getNode(int data)
{
    Node* temp = new Node(0);
    temp->data = data;
    temp->left = NULL;
    temp->right = NULL;
    return temp;
}

// Function to construct the BST
Node* constructBst(int arr[], int n)
{
    if (n == 0)
        return NULL;

    Node* root;

    queue<NodeDetails> q;

    // index variable to
    // access array elements
    int i = 0;

    // Node details for the
    // root of the BST
    NodeDetails newNode;
    newNode.ptr = getNode(arr[i++]);
    newNode.min = INT_MIN;
    newNode.max = INT_MAX;
    q.push(newNode);

    // Getting the root of the BST
    root = newNode.ptr;

    // Until there are no more
    // elements in arr[]
    while (i != n) {

        // Extracting NodeDetails of a
        // node from the queue
        NodeDetails temp = q.front();
        q.pop();

        // Check whether there are more elements
        // in the arr[] and arr[i] can be
        // left child of 'temp.ptr' or not
        if (i < n
            && (arr[i] < temp.ptr->data
                && arr[i] > temp.min)) {

            // Create NodeDetails for newNode
            // and add it to the queue
            newNode.ptr = getNode(arr[i++]);
            newNode.min = temp.min;
            newNode.max = temp.ptr->data;
            q.push(newNode);

            // Make this 'newNode' as left child
            // of 'temp.ptr'
            temp.ptr->left = newNode.ptr;
        }

        // Check whether there are more elements
        // in the arr[] and arr[i] can be
        // right child of 'temp.ptr' or not
        if (i < n
            && (arr[i] > temp.ptr->data
                && arr[i] < temp.max)) {

            // Create NodeDetails for newNode
            // and add it to the queue
            newNode.ptr = getNode(arr[i++]);
            newNode.min = temp.ptr->data;
            newNode.max = temp.max;
            q.push(newNode);

            // Make this 'newNode' as right
            // child of 'temp.ptr'
            temp.ptr->right = newNode.ptr;
        }
    }

    // Root of the required BST
    return root;
}

// Driver code
int main()
{
    int n = 9;

    int arr[n] = { 7, 4, 12, 3, 6, 8, 1, 5, 10 };

    // Function Call
    Node* root = constructBst(arr, n);

    preorderTraversal(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA program to construct BST
// using level order traversal
import java.io.*;
import java.util.*;

// Node class of a binary tree
class Node {
    int data;
    Node left, right;

    public Node(int data)
    {
        this.data = data;
        left = right = null;
    }
}

// Class formed to store the
// details of the ancestors
class NodeDetails {
    Node node;
    int min, max;
    public NodeDetails(Node node, int min, int max)
    {
        this.node = node;
        this.min = min;
        this.max = max;
    }
}

class GFG {

    // Function for the preorder traversal
    public static void preorder(Node root)
    {
        if (root == null)
            return;
        System.out.print(root.data + " ");

        // traversing left child
        preorder(root.left);

        // traversing right child
        preorder(root.right);
    }

    // Function to construct BST
    public static Node constructBST(int[] arr, int n)
    {
        // creating root of the BST
        Node root = new Node(arr[0]);
        Queue<NodeDetails> q = new LinkedList<>();

        // node details for the root of the BST
        q.add(new NodeDetails(root, Integer.MIN_VALUE,
                              Integer.MAX_VALUE));

        // index variable to access array elements
        int i = 1;

        // until queue is not empty
        while (!q.isEmpty()) {

            // extracting NodeDetails of a node from the
            // queue
            NodeDetails temp = q.poll();
            Node c = temp.node;
            int min = temp.min, max = temp.max;

            // checking whether there are more elements in
            // the array and arr[i] can be left child of
            // 'temp.node' or not
            if (i < n && min < arr[i] && arr[i] < c.data) {

                // make this node as left child of
                // 'temp.node'
                c.left = new Node(arr[i]);
                i++;

                // create new node details and add it to
                // queue
                q.add(new NodeDetails(c.left, min, c.data));
            }

            // checking whether there are more elements in
            // the array and arr[i] can be right child of
            // 'temp.node' or not
            if (i < n && c.data < arr[i] && arr[i] < max) {

                // make this node as right child of
                // 'temp.node'
                c.right = new Node(arr[i]);
                i++;

                // create new node details and add it to
                // queue
                q.add(
                    new NodeDetails(c.right, c.data, max));
            }
        }

        // root of the required BST
        return root;
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 9;
        int[] arr = { 7, 4, 12, 3, 6, 8, 1, 5, 10 };

        // Function Call
        Node root = constructBST(arr, n);
        preorder(root);
    }
}
```

## C#

```
// C# program to construct BST
// using level order traversal
using System;
using System.Collections.Generic;

// Node class of a binary tree
public class Node
{
    public int data;
    public Node left, right;

    public Node(int data)
    {
        this.data = data;
        left = right = null;
    }
}

// Class formed to store the
// details of the ancestors
public class NodeDetails
{
    public Node node;
    public int min, max;

    public NodeDetails(Node node, int min,
                                  int max)
    {
        this.node = node;
        this.min = min;
        this.max = max;
    }
}

class GFG{

// Function for the preorder traversal
public static void preorder(Node root)
{
    if (root == null)
        return;

    Console.Write(root.data + " ");

    // Traversing left child
    preorder(root.left);

    // Traversing right child
    preorder(root.right);
}

// Function to construct BST
public static Node constructBST(int[] arr, int n)
{

    // Creating root of the BST
    Node root = new Node(arr[0]);
    Queue<NodeDetails> q = new Queue<NodeDetails>();

    // Node details for the root of the BST
    q.Enqueue(new NodeDetails(root, int.MinValue,
                                    int.MaxValue));

    // Index variable to access array elements
    int i = 1;

    // Until queue is not empty
    while (q.Count != 0)
    {

        // Extracting NodeDetails of a node
        // from the queue
        NodeDetails temp = q.Dequeue();
        Node c = temp.node;
        int min = temp.min, max = temp.max;

        // Checking whether there are more
        // elements in the array and arr[i]
        // can be left child of
        // 'temp.node' or not
        if (i < n && min < arr[i] &&
                  arr[i] < c.data)
        {

            // Make this node as left child of
            // 'temp.node'
            c.left = new Node(arr[i]);
            i++;

            // Create new node details and add
            // it to queue
            q.Enqueue(new NodeDetails(c.left, min,
                                      c.data));
        }

        // Checking whether there are more elements in
        // the array and arr[i] can be right child of
        // 'temp.node' or not
        if (i < n && c.data < arr[i] && arr[i] < max)
        {

            // Make this node as right child of
            // 'temp.node'
            c.right = new Node(arr[i]);
            i++;

            // Create new node details and add it to
            // queue
            q.Enqueue( new NodeDetails(c.right,
                                       c.data, max));
        }
    }

    // Root of the required BST
    return root;
}

// Driver code
public static void Main(String[] args)
{
    int n = 9;
    int[] arr = { 7, 4, 12, 3, 6, 8, 1, 5, 10 };

    // Function Call
    Node root = constructBST(arr, n);

    preorder(root);
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript program to construct BST
// using level order traversal

// Node class of a binary tree
class Node
{
    constructor(data)
    {
        this.data = data;
        this.left = null;
        this.right = null;
    }
}

// Class formed to store the
// details of the ancestors
class NodeDetails
{
    constructor(node, min, max)
    {
        this.node = node;
        this.min = min;
        this.max = max;
    }
}

// Function for the preorder traversal
function preorder(root)
{
    if (root == null)
        return;

    document.write(root.data + " ");

    // Traversing left child
    preorder(root.left);

    // Traversing right child
    preorder(root.right);
}

// Function to construct BST
function constructBST(arr, n)
{

    // Creating root of the BST
    var root = new Node(arr[0])
    var q = [];

    // Node details for the root of the BST
    q.push(new NodeDetails(root, -1000000000,
                                  1000000000));

    // Index variable to access array elements
    var i = 1;

    // Until queue is not empty
    while (q.length != 0)
    {

        // Extracting NodeDetails of a node
        // from the queue
        var temp = q.shift();
        var c = temp.node;
        var min = temp.min, max = temp.max;

        // Checking whether there are more
        // elements in the array and arr[i]
        // can be left child of
        // 'temp.node' or not
        if (i < n && min < arr[i] &&
                  arr[i] < c.data)
        {

            // Make this node as left child of
            // 'temp.node'
            c.left = new Node(arr[i]);
            i++;

            // Create new node details and add
            // it to queue
            q.push(new NodeDetails(c.left, min,
                                      c.data));
        }

        // Checking whether there are more elements in
        // the array and arr[i] can be right child of
        // 'temp.node' or not
        if (i < n && c.data < arr[i] && arr[i] < max)
        {

            // Make this node as right child of
            // 'temp.node'
            c.right = new Node(arr[i]);
            i++;

            // Create new node details and add it to
            // queue
            q.push( new NodeDetails(c.right,
                                    c.data, max));
        }
    }

    // Root of the required BST
    return root;
}

// Driver code
var n = 9;
var arr = [ 7, 4, 12, 3, 6, 8, 1, 5, 10 ];

// Function Call
var root = constructBST(arr, n);

preorder(root);

// This code is contributed by noob2000

</script>
```

**Output:** 

```
7 4 3 1 6 5 12 8 10
```

**时间复杂度:** O(N)

**递归方法:**

下面是构造 BST 的递归方法。

## C++

```
// C++ implementation to construct a BST
// from its level order traversal
#include<bits/stdc++.h>
using namespace std;

// Node* of a BST
struct Node
{
    int data;
    Node* left;
    Node* right;

    Node(int data)
    {
        this->data = data;
        this->left  = NULL;
        this->right = NULL;
    }
};

Node* root;

// Function to print the inorder traversal
void  preorderTraversal(Node* root)
{
    if (root == NULL)
        return;

    cout<<(root->data) << " ";

    preorderTraversal(root->left);
    preorderTraversal(root->right);
}

// Function to get a new Node*
Node* getNode(int data)
{

    // Allocate memory
    Node* node = new Node(data);

    return node;
}

// Function to cona BST from
// its level order traversal
Node* LevelOrder(Node* root, int data)
{
    if (root == NULL)
    {
        root = getNode(data);
        return root;
    }

    if (data <= root->data)
        root->left = LevelOrder(root->left, data);
    else
        root->right = LevelOrder(root->right, data);
    return root;
}

Node* constructBst(int arr[], int n)
{
    if (n == 0)
        return NULL;

     root = NULL;

    for(int i = 0; i < n; i++)
        root = LevelOrder(root, arr[i]);

    return root;
}

// Driver code
int main()
{

    int arr[] = { 7, 4, 12, 3, 6,
                  8, 1, 5, 10 };

    int n = sizeof(arr)/sizeof(arr[0]);

    // Function Call
    root = constructBst(arr, n);
    preorderTraversal(root);
    return 0;
}

// This code is contributed by pratham76
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to construct a BST
// from its level order traversal
class GFG{

// Node of a BST
static class Node
{
    int data;
    Node left;
    Node right;

    Node(int data)
    {
        this.data = data;
        this.left  = null;
        this.right = null;
    }
};

static Node root;

// Function to print the inorder traversal
static void  preorderTraversal(Node root)
{
    if (root == null)
        return;

    System.out.print(root.data + " ");

    preorderTraversal(root.left);
    preorderTraversal(root.right);
}

// Function to get a new node
static Node getNode(int data)
{

    // Allocate memory
    Node node = new Node(data);

    return node;
}

// Function to cona BST from
// its level order traversal
static Node LevelOrder(Node root, int data)
{
    if (root == null)
    {
        root = getNode(data);
        return root;
    }

    if (data <= root.data)
        root.left = LevelOrder(root.left, data);
    else
        root.right = LevelOrder(root.right, data);
    return root;
}

static Node constructBst(int []arr, int n)
{
    if (n == 0)
        return null;

     root = null;

    for(int i = 0; i < n; i++)
        root = LevelOrder(root, arr[i]);

    return root;
}

// Driver code
public static void main(String[] args)
{
    int[] arr = { 7, 4, 12, 3, 6,
                  8, 1, 5, 10 };

    int n = arr.length;

    // Function Call
    root = constructBst(arr, n);
    preorderTraversal(root);
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 implementation to construct a BST
# from its level order traversal
import math

# node of a BST
class Node:
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# function to print the inorder traversal
def preorderTraversal(root):
    if (root == None):
        return None
    print(root.data, end=" ")
    preorderTraversal(root.left)
    preorderTraversal(root.right)

# function to get a new node
def getNode(data):

    # Allocate memory
    newNode = Node(data)

    # put in the data
    newNode.data = data
    newNode.left = None
    newNode.right = None
    return newNode

# function to construct a BST from
# its level order traversal
def LevelOrder(root, data):
    if(root == None):
        root = getNode(data)
        return root

    if(data <= root.data):
        root.left = LevelOrder(root.left, data)
    else:
        root.right = LevelOrder(root.right, data)
    return root

def constructBst(arr, n):
    if(n == 0):
        return None
    root = None

    for i in range(0, n):
        root = LevelOrder(root, arr[i])

    return root

# Driver code
if __name__ == '__main__':

    arr = [7, 4, 12, 3, 6, 8, 1, 5, 10]
    n = len(arr)

    # Function Call
    root = constructBst(arr, n)
    root = preorderTraversal(root)

# This code is contributed by Srathore
```

## C#

```
// C# implementation to construct a BST
// from its level order traversal
using System;

class GFG{

// Node of a BST
public class Node
{
    public int data;
    public Node left;
    public Node right;

    public Node(int data)
    {
        this.data = data;
        this.left  = null;
        this.right = null;
    }
};

static Node root;

// Function to print the inorder traversal
static void  preorderTraversal(Node root)
{
    if (root == null)
        return;

    Console.Write(root.data + " ");

    preorderTraversal(root.left);
    preorderTraversal(root.right);
}

// Function to get a new node
static Node getNode(int data)
{

    // Allocate memory
    Node node = new Node(data);

    return node;
}

// Function to cona BST from
// its level order traversal
static Node LevelOrder(Node root, int data)
{
    if (root == null)
    {
        root = getNode(data);
        return root;
    }

    if (data <= root.data)
        root.left = LevelOrder(root.left, data);
    else
        root.right = LevelOrder(root.right, data);
    return root;
}

static Node constructBst(int []arr, int n)
{
    if (n == 0)
        return null;

     root = null;

    for(int i = 0; i < n; i++)
        root = LevelOrder(root, arr[i]);

    return root;
}

// Driver code
public static void Main(string[] args)
{
    int[] arr = { 7, 4, 12, 3, 6,
                  8, 1, 5, 10 };

    int n = arr.Length;

    // Function Call
    root = constructBst(arr, n);
    preorderTraversal(root);
}
}

// This code is contributed by rutvik_56
```

**Output:** 

```
7 4 3 1 6 5 12 8 10
```

**Python 代码的时间复杂度** O(N log(N))