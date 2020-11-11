# 二叉树

> 原文：[https://www.geeksforgeeks.org/sum-of-nodes-in-top-view-of-binary-tree/](https://www.geeksforgeeks.org/sum-of-nodes-in-top-view-of-binary-tree/)

顶视图中的节点总数

二叉树的顶视图是从顶部查看树时可见的节点集。 给定一个二叉树，任务是在顶视图中打印节点总数。

**示例**：

```
Input: 
       1
      /  \
     2    3
    / \    \
   4   5    6

Output: 16

Input:
       1
      /  \
    2      3
      \   
        4  
          \
            5
             \
               6

Output: 12

```

**方法**：想法是将水平距离相同的节点放在一起。 我们执行[层次顺序遍历](https://www.geeksforgeeks.org/level-order-tree-traversal/)，以便先访问水平节点上的最高节点，然后再访问其下相同水平距离的任何其他节点，然后继续求和它们的值并将结果存储在变量 **sum 中** 。 散列用于检查是否看到给定水平距离的节点。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation of the approach 
#include <bits/stdc++.h> 
using namespace std; 

// Structure of binary tree 
struct Node { 
    Node* left; 
    Node* right; 
    int hd; 
    int data; 
}; 

// Function to create a new node 
Node* newNode(int key) 
{ 
    Node* node = new Node(); 
    node->left = node->right = NULL; 
    node->data = key; 
    return node; 
} 

// Function that returns the sum of 
// nodes in top view of binary tree 
int SumOfTopView(Node* root) 
{ 
    if (root == NULL) 
        return 0; 

    queue<Node*> q; 

    map<int, int> m; 
    int hd = 0; 

    root->hd = hd; 

    int sum = 0; 

    // Push node and horizontal distance to queue 
    q.push(root); 

    while (q.size()) { 
        hd = root->hd; 

        // Count function returns 1 if the container 
        // contains an element whose key is equivalent 
        // to hd, or returns zero otherwise. 
        if (m.count(hd) == 0) { 
            m[hd] = root->data; 
            sum += m[hd]; 
        } 
        if (root->left) { 
            root->left->hd = hd - 1; 
            q.push(root->left); 
        } 
        if (root->right) { 
            root->right->hd = hd + 1; 
            q.push(root->right); 
        } 
        q.pop(); 
        root = q.front(); 
    } 

    return sum; 
} 

// Driver code 
int main() 
{ 
    Node* root = newNode(1); 
    root->left = newNode(2); 
    root->right = newNode(3); 
    root->left->right = newNode(4); 
    root->left->right->right = newNode(5); 
    root->left->right->right->right = newNode(6); 

    cout << SumOfTopView(root); 

    return 0; 
} 

```

## Java

```java

// Java implementation of the approach 
import java.util.*; 
class Sol 
{ 

// Structure of binary tree 
static class Node  
{ 
    Node left; 
    Node right; 
    int hd; 
    int data; 
}; 

// Function to create a new node 
static Node newNode(int key) 
{ 
    Node node = new Node(); 
    node.left = node.right = null; 
    node.data = key; 
    return node; 
} 

// Function that returns the sum of 
// nodes in top view of binary tree 
static int SumOfTopView(Node root) 
{ 
    if (root == null) 
        return 0; 

    Queue<Node> q = new LinkedList<Node>(); 

    Map<Integer,Integer> m = new HashMap<Integer,Integer>(); 
    int hd = 0; 

    root.hd = hd; 

    int sum = 0; 

    // Push node and horizontal distance to queue 
    q.add(root); 

    while (q.size() > 0)  
    { 
        hd = root.hd; 

        // Count function returns 1 if the container 
        // contains an element whose key is equivalent 
        // to hd, or returns zero otherwise. 
        if (!m.containsKey(hd))  
        { 
            m.put(hd, root.data); 
            sum += m.get(hd); 
        } 
        if (root.left != null)  
        { 
            root.left.hd = hd - 1; 
            q.add(root.left); 
        } 
        if (root.right != null)  
        { 
            root.right.hd = hd + 1; 
            q.add(root.right); 
        } 
        q.remove(); 
        if(q.size() > 0) 
            root = q.peek(); 
    } 

    return sum; 
} 

// Driver code 
public static void main(String args[]) 
{ 
    Node root = newNode(1); 
    root.left = newNode(2); 
    root.right = newNode(3); 
    root.left.right = newNode(4); 
    root.left.right.right = newNode(5); 
    root.left.right.right.right = newNode(6); 

    System.out.print(SumOfTopView(root)); 
} 
} 

// This code is contributed by Arnab Kundu 

```

## Python3

```py

# Python3 implementation of the approach 
from collections import defaultdict 

class Node:  

    def __init__(self, key): 
        self.data = key 
        self.hd = None
        self.left = None
        self.right = None

# Function that returns the sum of 
# nodes in top view of binary tree 
def SumOfTopView(root): 

    if root == None: 
        return 0

    q = [] 

    m = defaultdict(lambda:0) 
    hd, Sum = 0, 0

    root.hd = hd 

    # Push node and horizontal 
    # distance to queue 
    q.append(root) 

    while len(q) > 0: 
        hd = root.hd 

        # Count function returns 1 if  
        # the container contains an  
        # element whose key is equivalent 
        # to hd, or returns zero otherwise. 
        if m[hd] == 0:  
            m[hd] = root.data 
            Sum += m[hd] 

        if root.left != None:  
            root.left.hd = hd - 1
            q.append(root.left) 

        if root.right != None:  
            root.right.hd = hd + 1
            q.append(root.right) 

        q.pop(0) 
        if len(q) > 0: 
            root = q[0] 

    return Sum

# Driver code 
if __name__ == "__main__": 

    root = Node(1) 
    root.left = Node(2) 
    root.right = Node(3) 
    root.left.right = Node(4) 
    root.left.right.right = Node(5) 
    root.left.right.right.right = Node(6) 

    print(SumOfTopView(root)) 

# This code is contributed by Rituraj Jain 

```

## C#

```cs

// C# implementation of the approach 
using System; 
using System.Collections.Generic; 

class GFG 
{ 

// Structure of binary tree 
public class Node  
{ 
    public Node left; 
    public Node right; 
    public int hd; 
    public int data; 
}; 

// Function to create a new node 
static Node newNode(int key) 
{ 
    Node node = new Node(); 
    node.left = node.right = null; 
    node.data = key; 
    return node; 
} 

// Function that returns the sum of 
// nodes in top view of binary tree 
static int SumOfTopView(Node root) 
{ 
    if (root == null) 
        return 0; 

    Queue<Node> q = new Queue<Node>(); 

    Dictionary<int, 
               int> m = new Dictionary<int, 
                                       int>(); 
    int hd = 0; 

    root.hd = hd; 

    int sum = 0; 

    // Push node and horizontal distance to queue 
    q.Enqueue(root); 

    while (q.Count > 0)  
    { 
        hd = root.hd; 

        // Count function returns 1 if the container 
        // contains an element whose key is equivalent 
        // to hd, or returns zero otherwise. 
        if (!m.ContainsKey(hd))  
        { 
            m.Add(hd, root.data); 
            sum += m[hd]; 
        } 

        if (root.left != null)  
        { 
            root.left.hd = hd - 1; 
            q.Enqueue(root.left); 
        } 

        if (root.right != null)  
        { 
            root.right.hd = hd + 1; 
            q.Enqueue(root.right); 
        } 
        q.Dequeue(); 
        if(q.Count > 0) 
            root = q.Peek(); 
    } 
    return sum; 
} 

// Driver code 
public static void Main(String []args) 
{ 
    Node root = newNode(1); 
    root.left = newNode(2); 
    root.right = newNode(3); 
    root.left.right = newNode(4); 
    root.left.right.right = newNode(5); 
    root.left.right.right.right = newNode(6); 

    Console.Write(SumOfTopView(root)); 
} 
} 

// This code is contributed by Princi Singh 

```

**输出**：

```
12

```



* * *

* * *



