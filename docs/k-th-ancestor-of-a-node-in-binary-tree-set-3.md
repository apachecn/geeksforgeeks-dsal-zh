# 二叉树中节点的第 K 个祖先|集合 3

> 原文:[https://www . geesforgeks . org/k-th-二叉树中节点的祖先-set-3/](https://www.geeksforgeeks.org/k-th-ancestor-of-a-node-in-binary-tree-set-3/)

给定一个二叉树，其中节点从 **1** 到 **N** 编号。给定一个节点和一个正整数 **K** 。我们必须打印二叉树中给定节点的 **K <sup>th</sup>** 祖先。如果不存在这样的祖先，则打印 **-1** 。
**例如下面给定二叉树中的****2<sup>nd</sup>**节点的祖先**4****5**就是 **1** 。 **3 <sup>rd</sup>** 节点的祖先 **4** 将为 **-1** 。

![](img/0b5eaaad45e1f0a3fcf1d9265341611c.png)

**方法:**首先我们从根中找到给定关键数据的路径，并将它存储到一个[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)中，然后我们简单地返回最后一个向量的第 k 个<sup>索引。
以下是上述方法的实现:</sup> 

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Structure of Tree
struct node {
    node *left, *right;
    int data;
};

// To create a new node
node* newNode(int data)
{
    node* temp = new node;
    temp->left = temp->right = NULL;
    temp->data = data;
    return temp;
}

// Function to find the path from
// root to the target node
bool RootToNode(node* root, int key, vector<int>& v)
{
    if (root == NULL)
        return false;

    // Add current node to the path
    v.push_back(root->data);

    // If current node is the target node
    if (root->data == key)
        return true;

    // If the target node exists in
    // the left or the right sub-tree
    if (RootToNode(root->left, key, v)
        || RootToNode(root->right, key, v))
        return true;

    // Remove the last inserted node as
    // it is not a part of the path
    // from root to target
    v.pop_back();
    return false;
}

// Driver code
int main()
{
    struct node* root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->left->right = newNode(5);
    root->right->left = newNode(6);
    root->right->right = newNode(7);

    // Given node
    int target = 4;

    // Vector to store the path from
    // root to the given node
    vector<int> v;

    // Find the path from root to the target node
    RootToNode(root, target, v);

    int k = 2;

    // Print the Kth ancestor
    if (k > v.size() - 1 || k <= 0)
        cout << -1;
    else
        cout << v[v.size() - 1 - k];
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Structure of Tree
static class node
{
    node left, right;
    int data;
};

// To create a new node
static node newNode(int data)
{
    node temp = new node();
    temp.left = temp.right = null;
    temp.data = data;
    return temp;
}

// Function to find the path from
// root to the target node
static boolean RootToNode(node root, int key,
                            Vector<Integer> v)
{
    if (root == null)
        return false;

    // Add current node to the path
    v.add(root.data);

    // If current node is the target node
    if (root.data == key)
        return true;

    // If the target node exists in
    // the left or the right sub-tree
    if (RootToNode(root.left, key, v)
        || RootToNode(root.right, key, v))
        return true;

    // Remove the last inserted node as
    // it is not a part of the path
    // from root to target
    v.removeElementAt(v.size()-1);
    return false;
}

// Driver code
public static void main(String[] args)
{
    node root = newNode(1);
    root.left = newNode(2);
    root.right = newNode(3);
    root.left.left = newNode(4);
    root.left.right = newNode(5);
    root.right.left = newNode(6);
    root.right.right = newNode(7);

    // Given node
    int target = 4;

    // Vector to store the path from
    // root to the given node
    Vector<Integer> v = new Vector<>();

    // Find the path from root to the target node
    RootToNode(root, target, v);

    int k = 2;

    // Print the Kth ancestor
    if (k > v.size() - 1 || k <= 0)
        System.out.println(-1);
    else
        System.out.println(v.get(v.size() - 1 - k));
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# To create a  node
class Node:

    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# Function to find the path
# from root to the target node
def RootToNode(root, key, v):

    if root == None:
        return False

    # Add current node to the path
    v.append(root.data)

    # If current node is the target node
    if root.data == key:
        return True

    # If the target node exists in
    # the left or the right sub-tree
    if (RootToNode(root.left, key, v) or
       RootToNode(root.right, key, v)):
        return True

    # Remove the last inserted node
    # as it is not a part of the
    # path from root to target
    v.pop()
    return False

# Driver code
if __name__ == "__main__":

    root = Node(1)
    root.left = Node(2)
    root.right = Node(3)
    root.left.left = Node(4)
    root.left.right = Node(5)
    root.right.left = Node(6)
    root.right.right = Node(7)

    # Given node
    target, k = 4, 2

    # Vector to store the path
    # from root to the given node
    v = []

    # Find the path from root to the target node
    RootToNode(root, target, v)

    # Print the Kth ancestor
    if k > len(v) - 1 or k <= 0:
        print(-1)
    else:
        print(v[len(v) - 1 - k])

# This code is contributed by Rituraj Jain
```

## C#

```
// C# implementation of above approach
using System.Collections.Generic;
using System;

class GFG
{

// Structure of Tree
public class node
{
    public node left, right;
    public int data;
};

// To create a new node
static node newNode(int data)
{
    node temp = new node();
    temp.left = temp.right = null;
    temp.data = data;
    return temp;
}

// Function to find the path from
// root to the target node
static bool RootToNode(node root, int key,
                            List<int> v)
{
    if (root == null)
        return false;

    // Add current node to the path
    v.Add(root.data);

    // If current node is the target node
    if (root.data == key)
        return true;

    // If the target node exists in
    // the left or the right sub-tree
    if (RootToNode(root.left, key, v)
        || RootToNode(root.right, key, v))
        return true;

    // Remove the last inserted node as
    // it is not a part of the path
    // from root to target
    v.Remove(v.Count-1);
    return false;
}

// Driver code
public static void Main(String[] args)
{
    node root = newNode(1);
    root.left = newNode(2);
    root.right = newNode(3);
    root.left.left = newNode(4);
    root.left.right = newNode(5);
    root.right.left = newNode(6);
    root.right.right = newNode(7);

    // Given node
    int target = 4;

    // Vector to store the path from
    // root to the given node
    List<int> v = new List<int>();

    // Find the path from root to the target node
    RootToNode(root, target, v);

    int k = 2;

    // Print the Kth ancestor
    if (k > v.Count - 1 || k <= 0)
        Console.WriteLine(-1);
    else
        Console.WriteLine(v[v.Count - 1 - k]);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript implementation of above approach

// Structure of Tree
class node
{
    constructor()
    {
        this.left = null;
        this.right = null;
        this.data = 0;
    }
};

// To create a new node
function newNode(data)
{
    var temp = new node();
    temp.left = temp.right = null;
    temp.data = data;
    return temp;
}

// Function to find the path from
// root to the target node
function RootToNode(root, key, v)
{
    if (root == null)
        return false;

    // push current node to the path
    v.push(root.data);

    // If current node is the target node
    if (root.data == key)
        return true;

    // If the target node exists in
    // the left or the right sub-tree
    if (RootToNode(root.left, key, v)
        || RootToNode(root.right, key, v))
        return true;

    // Remove the last inserted node as
    // it is not a part of the path
    // from root to target
    v.pop();
    return false;
}

// Driver code
var root = newNode(1);
root.left = newNode(2);
root.right = newNode(3);
root.left.left = newNode(4);
root.left.right = newNode(5);
root.right.left = newNode(6);
root.right.right = newNode(7);
// Given node
var target = 4;
// Vector to store the path from
// root to the given node
var v = [];
// Find the path from root to the target node
RootToNode(root, target, v);
var k = 2;
// Print the Kth ancestor
if (k > v.length - 1 || k <= 0)
    document.write(-1);
else
    document.write(v[v.length - 1 - k]);

</script>
```

**Output:** 

```
1
```