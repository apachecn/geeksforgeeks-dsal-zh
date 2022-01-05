# 检查给定的 n 元树是否是二叉树

> 原文:[https://www . geeksforgeeks . org/check-如果给定的 n 元树是二叉树/](https://www.geeksforgeeks.org/check-if-the-given-n-ary-tree-is-a-binary-tree/)

给定一个 n 元树，任务是检查给定的树是否是二进制的。

**示例:**

```
Input: 
    A 
   / \  
  B   C
 / \   \
D   E   F
Output: Yes

Input: 
     A 
   / | \  
  B  C  D
         \
          F
Output: No
```

**方法:**二叉树中的每个节点最多可以有 2 个子节点。因此，对于给定树的每个节点，计算子节点的数量，如果任何节点的数量超过 2，则打印**否**否则打印**是**。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Structure of a node
// of an n-ary tree
struct Node {
    char key;
    vector<Node*> child;
};

// Utility function to create
// a new tree node
Node* newNode(int key)
{
    Node* temp = new Node;
    temp->key = key;
    return temp;
}

// Function that returns true
// if the given tree is binary
bool isBinaryTree(struct Node* root)
{

    // Base case
    if (!root)
        return true;

    // Count will store the number of
    // children of the current node
    int count = 0;
    for (int i = 0; i < root->child.size(); i++) {

        // If any child of the current node doesn't
        // satisfy the condition of being
        // a binary tree node
        if (!isBinaryTree(root->child[i]))
            return false;

        // Increment the count of children
        count++;

        // If current node has more
        // than 2 children
        if (count > 2)
            return false;
    }
    return true;
}

// Driver code
int main()
{
    Node* root = newNode('A');
    (root->child).push_back(newNode('B'));
    (root->child).push_back(newNode('C'));
    (root->child[0]->child).push_back(newNode('D'));
    (root->child[0]->child).push_back(newNode('E'));
    (root->child[1]->child).push_back(newNode('F'));

    if (isBinaryTree(root))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;
class GFG
{

// Structure of a node
// of an n-ary tree
static class Node
{
    int key;
    Vector<Node> child = new Vector<Node>();
};

// Utility function to create
// a new tree node
static Node newNode(int key)
{
    Node temp = new Node();
    temp.key = key;
    return temp;
}

// Function that returns true
// if the given tree is binary
static boolean isBinaryTree(Node root)
{

    // Base case
    if (root == null)
        return true;

    // Count will store the number of
    // children of the current node
    int count = 0;
    for (int i = 0; i < root.child.size(); i++)
    {

        // If any child of the current node doesn't
        // satisfy the condition of being
        // a binary tree node
        if (!isBinaryTree(root.child.get(i)))
            return false;

        // Increment the count of children
        count++;

        // If current node has more
        // than 2 children
        if (count > 2)
            return false;
    }
    return true;
}

// Driver code
public static void main(String[] args)
{
    Node root = newNode('A');
    (root.child).add(newNode('B'));
    (root.child).add(newNode('C'));
    (root.child.get(0).child).add(newNode('D'));
    (root.child.get(0).child).add(newNode('E'));
    (root.child.get(1).child).add(newNode('F'));

    if (isBinaryTree(root))
        System.out.println("Yes");
    else
        System.out.println("No");
}
}

// This code is contributed by PrinciRaj1992
```

## C#

```
// C# implementation of the above approach
using System;
using System.Collections.Generic;

class GFG
{

// Structure of a node
// of an n-ary tree
public class Node
{
    public int key;
    public List<Node> child = new List<Node>();
};

// Utility function to create
// a new tree node
static Node newNode(int key)
{
    Node temp = new Node();
    temp.key = key;
    return temp;
}

// Function that returns true
// if the given tree is binary
static bool isBinaryTree(Node root)
{

    // Base case
    if (root == null)
        return true;

    // Count will store the number of
    // children of the current node
    int count = 0;
    for (int i = 0; i < root.child.Count; i++)
    {

        // If any child of the current node doesn't
        // satisfy the condition of being
        // a binary tree node
        if (!isBinaryTree(root.child[i]))
            return false;

        // Increment the count of children
        count++;

        // If current node has more
        // than 2 children
        if (count > 2)
            return false;
    }
    return true;
}

// Driver code
public static void Main(String[] args)
{
    Node root = newNode('A');
    (root.child).Add(newNode('B'));
    (root.child).Add(newNode('C'));
    (root.child[0].child).Add(newNode('D'));
    (root.child[0].child).Add(newNode('E'));
    (root.child[1].child).Add(newNode('F'));

    if (isBinaryTree(root))
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Structure of a node of an n-ary tree
class Node
{
    constructor(key)
    {
        this.key = key;
        this.child = [];
    }
}

// Utility function to create
// a new tree node
function newNode(key)
{
    let temp = new Node(key);
    return temp;
}

// Function that returns true
// if the given tree is binary
function isBinaryTree(root)
{

    // Base case
    if (root == null)
        return true;

    // Count will store the number of
    // children of the current node
    let count = 0;
    for(let i = 0; i < root.child.length; i++)
    {

        // If any child of the current node doesn't
        // satisfy the condition of being
        // a binary tree node
        if (!isBinaryTree(root.child[i]))
            return false;

        // Increment the count of children
        count++;

        // If current node has more
        // than 2 children
        if (count > 2)
            return false;
    }
    return true;
}

// Driver code
let root = newNode('A');
(root.child).push(newNode('B'));
(root.child).push(newNode('C'));
(root.child[0].child).push(newNode('D'));
(root.child[0].child).push(newNode('E'));
(root.child[1].child).push(newNode('F'));

if (isBinaryTree(root))
    document.write("Yes");
else
    document.write("No");

// This code is contributed by divyeshrabadiya07

</script>
```

**Output:** 

```
Yes
```