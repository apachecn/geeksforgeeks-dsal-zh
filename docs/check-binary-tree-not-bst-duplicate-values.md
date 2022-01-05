# 检查二叉树(不是 BST)是否有重复值

> 原文:[https://www . geesforgeks . org/check-binary-tree-not-BST-replicate-values/](https://www.geeksforgeeks.org/check-binary-tree-not-bst-duplicate-values/)

检查二叉树(不是 BST)是否有重复值
示例:

```
Input : Root of below tree
         1
       /   \
      2     3
             \
              2
Output : Yes
Explanation : The duplicate value is 2.

Input : Root of below tree
         1
       /   \
     20     3
             \
              4
Output : No
Explanation : There are no duplicates.
```

一个简单的解决方案是在数组中存储给定二叉树的有序遍历。然后检查数组是否有重复。我们可以避免使用数组，在 O(n)时间内解决问题。想法是使用散列法。我们遍历给定的树，对于每个节点，我们检查它是否已经存在于哈希表中。如果存在，我们返回真(发现重复)。如果不存在，我们插入哈希表。

## C++

```
// C++ Program to check duplicates
// in Binary Tree
#include <bits/stdc++.h>
using namespace std;

// A binary tree Node has data,
// pointer to left child
// and a pointer to right child
struct Node {
    int data;
    struct Node* left;
    struct Node* right;
};

// Helper function that allocates
// a new Node with the given data
// and NULL left and right pointers.
struct Node* newNode(int data)
{
    struct Node* node = new Node;
    node->data = data;
    node->left = node->right = NULL;
    return (node);
}

bool checkDupUtil(Node* root, unordered_set<int> &s)
{
    // If tree is empty, there are no
    // duplicates.
    if (root == NULL)
       return false;

    // If current node's data is already present.
    if (s.find(root->data) != s.end())
       return true;

    // Insert current node
    s.insert(root->data);

    // Recursively check in left and right
    // subtrees.
    return checkDupUtil(root->left, s) ||
           checkDupUtil(root->right, s);
}

// To check if tree has duplicates
bool checkDup(struct Node* root)
{
    unordered_set<int> s;
    return checkDupUtil(root, s);
}

// Driver program to test above functions
int main()
{
    struct Node* root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(2);
    root->left->left = newNode(3);
    if (checkDup(root))
        printf("Yes");
    else
        printf("No");

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to check duplicates
// in Binary Tree
import java.util.HashSet;
public class CheckDuplicateValues {

    //Function that used HashSet to find presence of duplicate nodes
    public static boolean checkDupUtil(Node root, HashSet<Integer> s)
    {
        // If tree is empty, there are no
        // duplicates. 
        if (root == null)
            return false;

        // If current node's data is already present.
        if (s.contains(root.data))
            return true;

        // Insert current node
        s.add(root.data);

        // Recursively check in left and right
        // subtrees.
        return checkDupUtil(root.left, s) || checkDupUtil(root.right, s);
    }

    // To check if tree has duplicates
    public static boolean checkDup(Node root)
    {
        HashSet<Integer> s=new HashSet<>();
        return checkDupUtil(root, s);
    }

    public static void main(String args[]) {
        Node root = new Node(1);
        root.left = new Node(2);
        root.right = new Node(2);
        root.left.left = new Node(3);
        if (checkDup(root))
            System.out.print("Yes");
        else
            System.out.print("No");
    }
}

// A binary tree Node has data,
// pointer to left child
// and a pointer to right child
class Node {
    int data;
    Node left,right;
    Node(int data)
    {
        this.data=data;
    }
};
//This code is contributed by Gaurav Tiwari
```

## 计算机编程语言

```
""" Program to check duplicates
# in Binary Tree """

# Helper function that allocates a new
# node with the given data and None
# left and right poers.                                
class newNode:

    # Construct to create a new node
    def __init__(self, key):
        self.data = key
        self.left = None
        self.right = None

def checkDupUtil( root, s) :

    # If tree is empty, there are no
    # duplicates.
    if (root == None) :
        return False

    # If current node's data is already present.
    if root.data in s:
        return True

    # Insert current node
    s.add(root.data)

    # Recursively check in left and right
    # subtrees.
    return checkDupUtil(root.left, s) or checkDupUtil(root.right, s)

# To check if tree has duplicates
def checkDup( root) :

    s=set()
    return checkDupUtil(root, s)

# Driver Code
if __name__ == '__main__':
    root = newNode(1)
    root.left = newNode(2)
    root.right = newNode(2)
    root.left.left = newNode(3)
    if (checkDup(root)):
        print("Yes")
    else:
        print("No")

# This code is contributed by
# Shubham Singh(SHUBHAMSINGH10)
```

## C#

```
// C# Program to check duplicates
// in Binary Tree
using System;
using System.Collections;
using System.Collections.Generic;

class CheckDuplicateValues
{

    //Function that used HashSet to
    // find presence of duplicate nodes
    public static Boolean checkDupUtil(Node root, HashSet<int> s)
    {
        // If tree is empty, there are no
        // duplicates.
        if (root == null)
            return false;

        // If current node's data is already present.
        if (s.Contains(root.data))
            return true;

        // Insert current node
        s.Add(root.data);

        // Recursively check in left and right
        // subtrees.
        return checkDupUtil(root.left, s) ||
                checkDupUtil(root.right, s);
    }

    // To check if tree has duplicates
    public static Boolean checkDup(Node root)
    {
        HashSet<int> s = new HashSet<int>();
        return checkDupUtil(root, s);
    }

    public static void Main(String []args)
    {
        Node root = new Node(1);
        root.left = new Node(2);
        root.right = new Node(2);
        root.left.left = new Node(3);
        if (checkDup(root))
            Console.Write("Yes");
        else
            Console.Write("No");
    }
}

// A binary tree Node has data,
// pointer to left child
// and a pointer to right child
public class Node
{
    public int data;
    public Node left, right;
    public Node(int data)
    {
        this.data = data;
    }
};

// This code is contributed by Arnab Kundu
```

## java 描述语言

```
<script>

    // JavaScript Program to check duplicates in Binary Tree

    class Node
    {
        constructor(data) {
           this.left = null;
           this.right = null;
           this.data = data;
        }
    }

    // Function that used HashSet to find
    // presence of duplicate nodes
    function checkDupUtil(root, s)
    {
        // If tree is empty, there are no
        // duplicates. 
        if (root == null)
            return false;

        // If current node's data is already present.
        if (s.has(root.data))
            return true;

        // Insert current node
        s.add(root.data);

        // Recursively check in left and right
        // subtrees.
        return checkDupUtil(root.left, s) ||
        checkDupUtil(root.right, s);
    }

    // To check if tree has duplicates
    function checkDup(root)
    {
        let s = new Set();
        return checkDupUtil(root, s);
    }

    let root = new Node(1);
    root.left = new Node(2);
    root.right = new Node(2);
    root.left.left = new Node(3);
    if (checkDup(root))
      document.write("Yes");
    else
      document.write("No");

</script>
```

**输出:**

```
Yes
```