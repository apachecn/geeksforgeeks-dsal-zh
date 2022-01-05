# Sudo 放置[1.4] |跳转子树

> 原文:[https://www . geesforgeks . org/sudo-placement 1-4-跳子树/](https://www.geeksforgeeks.org/sudo-placement1-4-jumping-the-subtree/)

给定具有不同值的 n 个节点的二叉查找树。还给出了 Q 查询。每个查询都由一个节点值组成，该节点值必须在 BST 中搜索，并跳过给定节点作为根的子树。如果提供的节点是根节点，则打印“空”且不带引号。之后，打印 BST 的前序遍历。

**例:**

```
Input:
N = 7, Q = 2
BST elements: 8 4 10 15 14 88 64
Query1: 15
Query2: 88

Output: 8 4 10
        8 4 10 15 14

The tree below will be formed from the elements given 

               8
            /     \
          4        10 
                     \ 
                     15
                   /    \ 
                  14    88 
                        /
                       64 

Query1 = 15\. So, skip the subtree with 15 as root.
The remaining tree is :

         8
       /    \
     4       10
The preorder traversal of the above tree is: 8 4 10

Query2 = 88\. So we skip the subtree with 88 as root. 
The remaining tree is :
          8
      /       \
    4          10
                 \
                  15
                /       
             14                  
The preorder traversal of the above tree is: 8 4 10 15 14
```

一种简单的方法是遍历整个树并存储其预排序遍历。在每个查询中，执行一个将节点视为根的预排序遍历。打印整个树的前序遍历，除了将节点视为根的树的前序遍历中的元素。

一种有效的方法是将树的整个预排序遍历存储在一个容器中。在寻找树的预序遍历时，存储来自节点的递归调用的数量，并将其存储在哈希表中( *mp* )。这有效地存储了将任何节点视为根的子树的整个大小。在执行每个查询时，打印树的前序遍历，直到找到节点，一旦找到，执行 mp[node]步骤的跳转，从而跳过子树。

下面是上述方法的实现:

## c++

```
// C++ program to insert nodes
// and print the preorder traversal
#include <bits/stdc++.h>
using namespace std;

// vector to store pre-order
vector<int> pre;

// map to store the height
// of every subtree
unordered_map<int, int> mp;

// structure to store the BST
struct Node {
    int data;
    Node* left = NULL;
    Node* right = NULL;
};

// locates the memory space
Node* newNode(int key)
{
    Node* temp = new Node;
    temp->data = key;
    temp->left = NULL;
    temp->right = NULL;
    return temp;
}

// inserts node in the BST
Node* insertNode(Node* head, int key)
{
    // if first node
    if (head == NULL)
        head = newNode(key);
    else {

        // move to left
        if (key < head->data)
            head->left = insertNode(head->left, key);
        // move to right
        else
            head->right = insertNode(head->right, key);
    }
    return head;
}

// Function to compute the pre-order
// and compute the height of every sub-tree
int preOrder(Node* head)
{
    // leaf node is null
    if (head == NULL)
        return 0;

    pre.push_back(head->data);

    mp[head->data] += preOrder(head->left);
    mp[head->data] += preOrder(head->right);
    mp[head->data] += 1;

    return mp[head->data];
}

// Function to perform every queries
void performQueries(int node)
{

    // traverse in the pre-order
    // jump the subtree which has node
    for (int i = 0; i < pre.size();) {

        // jump the subtree which has the node
        if (pre[i] == node) {
            i += mp[pre[i]];
        }

        // print the pre-order
        else {
            cout << pre[i] << " ";
            i++;
        }
    }
    cout << endl;
}

// Driver Code
int main()
{

    Node* root = NULL;

    /*           8
            /     \
          4        10
                     \
                     15
                   /    \
                  14    88
                        /
                       64  */

    root = insertNode(root, 8);
    root = insertNode(root, 4);
    root = insertNode(root, 10);
    root = insertNode(root, 15);
    root = insertNode(root, 14);
    root = insertNode(root, 88);
    root = insertNode(root, 64);

    // Pre-order traversal of tree
    preOrder(root);

    // Function call to perform queries
    performQueries(15);
    performQueries(88);

    return 0;
}
```

## Java

```
// Java program to insert nodes
// and print the preorder traversal
import java.util.*;

class Node
{
    int data;
    Node left, right;
    Node(int key)
    {
        data = key;
        left = right = null;
    }
}

class GFG
{
    // ArrayList to
    // store pre-order
    static ArrayList<Integer> pre =
                     new ArrayList<Integer>();

   // map to store the height
   // of every subtree
   static HashMap<Integer, Integer> mp =
                  new HashMap<Integer, Integer>();

public static Node insertNode(Node head, int key)
{
    // if first node
    if (head == null)
        head = new Node(key);
    else
    {

        // move to left
        if (key < head.data)
            head.left = insertNode(head.left, key);

        // move to right
        else
            head.right = insertNode(head.right, key);
    }
    return head;
}

public static int preOrder(Node head)
{
    // leaf node is null
    if (head == null)
        return 0;

    pre.add(head.data);

    mp.put(head.data, head.data +
                      preOrder(head.left));
    mp.put(head.data, head.data +
                      preOrder(head.right));
    mp.put(head.data, head.data + 1);

    return mp.get(head.data);
}

// Function to perform
// every queries
public static void performQueries(int node)
{

    // traverse in the pre-order
    // jump the subtree which has node
    for (int i = 0; i < pre.size();)
    {

        // jump the subtree
        // which has the node
        if (pre.get(i) == node)
        {
            i += mp.get(pre.get(i));
        }

        // print the pre-order
        else
        {
            System.out.print(pre.get(i) + " ");
            i++;
        }
    }
     System.out.println();
}

public static void main (String[] args)
{

Node root = null;

/*         8
        /     \
    4     10
                \
                15
            / \
            14 88
                    /
                64 */

root = insertNode(root, 8);
root = insertNode(root, 4);
root = insertNode(root, 10);
root = insertNode(root, 15);
root = insertNode(root, 14);
root = insertNode(root, 88);
root = insertNode(root, 64);

// Pre-order traversal of tree
preOrder(root);

// Function call to
// perform queries
performQueries(15);
performQueries(88);   
}
}
```

## python 3

```
# Python3 program to insert nodes
# and print the preorder traversal
from typing import Dict

# Vector to store pre-order
pre = []

# Map to store the height
# of every subtree
mp: Dict[int, int] = dict()

# Structure to store the BST
class Node:

    def __init__(self, data: int) -> None:

        self.data = data
        self.left = None
        self.right = None

# Inserts node in the BST
def insertNode(head: Node, key: int) -> Node:

    # If first node
    if (head == None):
        head = Node(key)
    else:

        # Move to left
        if (key < head.data):
            head.left = insertNode(head.left, key)

        # Move to right
        else:
            head.right = insertNode(head.right, key)

    return head

# Function to compute the pre-order
# and compute the height of every sub-tree
def preOrder(head: Node) -> int:

    global pre, mp

    # Leaf node is None
    if (head == None):
        return 0

    pre.append(head.data)

    if head.data not in mp:
        mp[head.data] = 0

    mp[head.data] += preOrder(head.left)
    mp[head.data] += preOrder(head.right)
    mp[head.data] += 1

    return mp[head.data]

# Function to perform every queries
def performQueries(node: int) -> None:

    # Traverse in the pre-order
    # jump the subtree which has node
    i = 0

    while i < len(pre):

        # Jump the subtree which has the node
        if (pre[i] == node):
            i += mp[pre[i]]

        # Print the pre-order
        else:
            print(pre[i], end = " ")
            i += 1

    print()

# Driver Code
if __name__ == "__main__":

    root = None
    '''        8
            /     \
          4        10
                     \
                     15
                   /    \
                  14    88
                        /
                       64  '''

    root = insertNode(root, 8)
    root = insertNode(root, 4)
    root = insertNode(root, 10)
    root = insertNode(root, 15)
    root = insertNode(root, 14)
    root = insertNode(root, 88)
    root = insertNode(root, 64)

    # Pre-order traversal of tree
    preOrder(root)

    # Function call to perform queries
    performQueries(15)
    performQueries(88)

# This code is contributed by sanjeev2552
```

## c#

```
// C# program to insert nodes
// and print the preorder traversal
using System;
using System.Collections.Generic;

class Node
{
    public int data;
    public Node left, right;
    public Node(int key)
    {
        data = key;
        left = right = null;
    }
}

class GFG
{
    // List to store pre-order
    static List<int> pre = new List<int>();

    // map to store the height
    // of every subtree
    static Dictionary<int,
                      int> mp = new Dictionary<int,
                                               int>();

    public static Node insertNode(Node head, int key)
    {
        // if first node
        if (head == null)
            head = new Node(key);
        else
        {

            // move to left
            if (key < head.data)
                head.left = insertNode(head.left, key);

            // move to right
            else
                head.right = insertNode(head.right, key);
        }
        return head;
    }

    public static int preOrder(Node head)
    {
        // leaf node is null
        if (head == null)
            return 0;

        pre.Add(head.data);

        mp[head.data]= head.data +
                       preOrder(head.left);
        mp[head.data]= head.data +
                       preOrder(head.right);
        mp[head.data]= head.data + 1;

        return mp[head.data];
    }

    // Function to perform every queries
    public static void performQueries(int node)
    {

        // traverse in the pre-order
        // jump the subtree which has node
        for (int i = 0; i < pre.Count;)
        {

            // jump the subtree
            // which has the node
            if (pre[i] == node)
            {
                i += mp[pre[i]];
            }

            // print the pre-order
            else
            {
                Console.Write(pre[i] + " ");
                i++;
            }
        }
        Console.WriteLine();
    }

    // Driver Code
    public static void Main(String[] args)
    {
        Node root = null;

        /*         8
                /     \
            4     10
                        \
                        15
                    / \
                    14 88
                            /
                        64 */
        root = insertNode(root, 8);
        root = insertNode(root, 4);
        root = insertNode(root, 10);
        root = insertNode(root, 15);
        root = insertNode(root, 14);
        root = insertNode(root, 88);
        root = insertNode(root, 64);

        // Pre-order traversal of tree
        preOrder(root);

        // Function call to
        // perform queries
        performQueries(15);
        performQueries(88);
    }
}

// This code is contributed by 29AjayKumar
```

T21

## Javascript

```
<script>

// Javascript program to insert nodes
// and print the preorder traversal
class Node
{
    constructor(key)
    {
        this.data = key;
        this.left = null;
        this.right = null;
    }
}

// List to store pre-order
var pre = [];

// map to store the height
// of every subtree
var mp = new Map();

function insertNode(head, key)
{

    // If first node
    if (head == null)
        head = new Node(key);
    else
    {

        // Move to left
        if (key < head.data)
            head.left = insertNode(
                head.left, key);

        // Move to right
        else
            head.right = insertNode(
                head.right, key);
    }
    return head;
}

function preOrder(head)
{

    // Leaf node is null
    if (head == null)
        return 0;

    pre.push(head.data);

    mp.set(head.data, head.data +
                      preOrder(head.left));
    mp.set(head.data, head.data +
                      preOrder(head.right));
    mp.set(head.data, mp.get(head.data) + 1);

    return mp.get(head.data);
}

// Function to perform every queries
function performQueries(node)
{

    // Traverse in the pre-order
    // jump the subtree which has node
    for(var i = 0; i < pre.length;)
    {

        // Jump the subtree
        // which has the node
        if (pre[i] == node)
        {
            i += mp.get(pre[i]);
        }

        // Print the pre-order
        else
        {
            document.write(pre[i] + " ");
            i++;
        }
    }
    document.write("<br>");
}

// Driver Code
var root = null;

/*         8
        /     \
        4     10
                \
                15
               / \
              14 88
                /
               64 */
root = insertNode(root, 8);
root = insertNode(root, 4);
root = insertNode(root, 10);
root = insertNode(root, 15);
root = insertNode(root, 14);
root = insertNode(root, 88);
root = insertNode(root, 64);

// Pre-order traversal of tree
preOrder(root);

// Function call to
// perform queries
performQueries(15);
performQueries(88);

// This code is contributed by rutvik_56

</script>
```

**输出:**

```
8 4 10 
8 4 10 15 14
```