# 检查二叉树中子和属性的迭代方法

> 原文:[https://www . geesforgeks . org/迭代方法检查孩子-二进制树中的属性总和/](https://www.geeksforgeeks.org/iterative-approach-to-check-for-children-sum-property-in-a-binary-tree/)

给定一个二叉树，编写一个函数，如果树满足以下属性，则返回 true:
对于每个节点，数据值必须等于左右子节点中数据值的总和。对于空子代，将数据值视为 0。
**例:**

```
Input : 
       10
      /  \
     8    2
    / \    \
   3   5    2
Output : Yes

Input :
         5
        /  \
      -2    7
      / \    \
     1   6    7
Output : No
```

我们已经讨论了[递归](https://www.geeksforgeeks.org/check-for-children-sum-property-in-a-binary-tree/)方法。在这篇文章中，讨论了一种迭代方法。
**方法:**想法是用一个队列对二叉树进行级别顺序遍历，同时检查每个节点:

1.  如果当前节点有两个子节点，并且当前节点等于其左右子节点之和。
2.  如果当前节点刚刚离开子节点，并且当前节点等于它的左子节点。
3.  如果当前节点正好有一个右子节点，并且当前节点等于它的右子节点。

以下是上述方法的实现:

## C++

```
// C++ program to check children sum property
#include <bits/stdc++.h>
using namespace std;

// A binary tree node
struct Node {
    int data;
    Node *left, *right;
};

// Utility function to allocate memory for a new node
Node* newNode(int data)
{
    Node* node = new (Node);
    node->data = data;
    node->left = node->right = NULL;
    return (node);
}

// Function to check if the tree holds
// children sum property
bool CheckChildrenSum(Node* root)
{
    queue<Node*> q;

    // Push the root node
    q.push(root);

    while (!q.empty()) {
        Node* temp = q.front();
        q.pop();

        // If the current node has both left and right children
        if (temp->left && temp->right) {
            // If the current node is not equal to
            // the sum of its left and right children
            // return false
            if (temp->data != temp->left->data + temp->right->data)
                return false;

            q.push(temp->left);
            q.push(temp->right);
        }

        // If the current node has right child
        else if (!temp->left && temp->right) {
            // If the current node is not equal to
            // its right child return false
            if (temp->data != temp->right->data)
                return false;

            q.push(temp->right);
        }

        // If the current node has left child
        else if (!temp->right && temp->left) {
            // If the current node is not equal to
            // its left child return false
            if (temp->data != temp->left->data)
                return false;

            q.push(temp->left);
        }
    }

    // If the given tree has children
    // sum property return true
    return true;
}

// Driver code
int main()
{
    Node* root = newNode(10);
    root->left = newNode(8);
    root->right = newNode(2);
    root->left->left = newNode(3);
    root->left->right = newNode(5);
    root->right->right = newNode(2);

    if (CheckChildrenSum(root))
        printf("Yes");
    else
        printf("No");

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check children sum property
import java.util.*;
class GFG
{

// A binary tree node
static class Node
{
    int data;
    Node left, right;
}

// Utility function to allocate memory for a new node
static Node newNode(int data)
{
    Node node = new Node();
    node.data = data;
    node.left = node.right = null;
    return (node);
}

// Function to check if the tree holds
// children sum property
static boolean CheckChildrenSum(Node root)
{
    Queue<Node> q = new LinkedList<Node>();

    // add the root node
    q.add(root);

    while (q.size() > 0)
    {
        Node temp = q.peek();
        q.remove();

        // If the current node has both left and right children
        if (temp.left != null && temp.right != null)
        {
            // If the current node is not equal to
            // the sum of its left and right children
            // return false
            if (temp.data != temp.left.data + temp.right.data)
                return false;

            q.add(temp.left);
            q.add(temp.right);
        }

        // If the current node has right child
        else if (temp.left == null && temp.right != null)
        {
            // If the current node is not equal to
            // its right child return false
            if (temp.data != temp.right.data)
                return false;

            q.add(temp.right);
        }

        // If the current node has left child
        else if (temp.right == null && temp.left != null)
        {
            // If the current node is not equal to
            // its left child return false
            if (temp.data != temp.left.data)
                return false;

            q.add(temp.left);
        }
    }

    // If the given tree has children
    // sum property return true
    return true;
}

// Driver code
public static void main(String args[])
{
    Node root = newNode(10);
    root.left = newNode(8);
    root.right = newNode(2);
    root.left.left = newNode(3);
    root.left.right = newNode(5);
    root.right.right = newNode(2);

    if (CheckChildrenSum(root))
        System.out.printf("Yes");
    else
        System.out.printf("No");
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 program to check
# children sum property

# A binary tree node
class Node:

    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# Function to check if the tree holds
# children sum property
def CheckChildrenSum(root):

    q = []

    # Push the root node
    q.append(root)

    while len(q) != 0:
        temp = q.pop()

        # If the current node has both
        # left and right children
        if temp.left and temp.right:

            # If the current node is not equal
            # to the sum of its left and right
            # children, return false
            if (temp.data != temp.left.data +
                             temp.right.data):
                return False

            q.append(temp.left)
            q.append(temp.right)

        # If the current node has right child
        elif not temp.left and temp.right:

            # If the current node is not equal
            # to its right child return false
            if temp.data != temp.right.data:
                return False

            q.append(temp.right)

        # If the current node has left child
        elif not temp.right and temp.left:

            # If the current node is not equal
            # to its left child return false
            if temp.data != temp.left.data:
                return False

            q.append(temp.left)

    # If the given tree has children
    # sum property return true
    return True

# Driver code
if __name__ == "__main__":

    root = Node(10)
    root.left = Node(8)
    root.right = Node(2)
    root.left.left = Node(3)
    root.left.right = Node(5)
    root.right.right = Node(2)

    if CheckChildrenSum(root):
        print("Yes")
    else:
        print("No")

# This code is contributed
# by Rituraj Jain
```

## C#

```
// C# program to check children sum property
using System;
using System.Collections.Generic;

class GFG
{

// A binary tree node
public class Node
{
    public int data;
    public Node left, right;
}

// Utility function to allocate
// memory for a new node
static Node newNode(int data)
{
    Node node = new Node();
    node.data = data;
    node.left = node.right = null;
    return (node);
}

// Function to check if the tree holds
// children sum property
static Boolean CheckChildrenSum(Node root)
{
    Queue<Node> q = new Queue<Node>();

    // add the root node
    q.Enqueue(root);

    while (q.Count > 0)
    {
        Node temp = q.Peek();
        q.Dequeue();

        // If the current node has both
        // left and right children
        if (temp.left != null &&
            temp.right != null)
        {
            // If the current node is not equal to
            // the sum of its left and right children
            // return false
            if (temp.data != temp.left.data +
                             temp.right.data)
                return false;

            q.Enqueue(temp.left);
            q.Enqueue(temp.right);
        }

        // If the current node has right child
        else if (temp.left == null &&
                 temp.right != null)
        {
            // If the current node is not equal to
            // its right child return false
            if (temp.data != temp.right.data)
                return false;

            q.Enqueue(temp.right);
        }

        // If the current node has left child
        else if (temp.right == null &&
                 temp.left != null)
        {
            // If the current node is not equal to
            // its left child return false
            if (temp.data != temp.left.data)
                return false;

            q.Enqueue(temp.left);
        }
    }

    // If the given tree has children
    // sum property return true
    return true;
}

// Driver code
public static void Main(String []args)
{
    Node root = newNode(10);
    root.left = newNode(8);
    root.right = newNode(2);
    root.left.left = newNode(3);
    root.left.right = newNode(5);
    root.right.right = newNode(2);

    if (CheckChildrenSum(root))
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

    // JavaScript program to check children sum property

    // A binary tree node
    class Node
    {
        constructor(data) {
           this.left = null;
           this.right = null;
           this.data = data;
        }
    }

    // Utility function to allocate memory for a new node
    function newNode(data)
    {
        let node = new Node(data);
        return (node);
    }

    // Function to check if the tree holds
    // children sum property
    function CheckChildrenSum(root)
    {
        let q = [];

        // add the root node
        q.push(root);

        while (q.length > 0)
        {
            let temp = q[0];
            q.shift();

            // If the current node has both left and right children
            if (temp.left != null && temp.right != null)
            {
                // If the current node is not equal to
                // the sum of its left and right children
                // return false
                if (temp.data != temp.left.data + temp.right.data)
                    return false;

                q.push(temp.left);
                q.push(temp.right);
            }

            // If the current node has right child
            else if (temp.left == null && temp.right != null)
            {
                // If the current node is not equal to
                // its right child return false
                if (temp.data != temp.right.data)
                    return false;

                q.push(temp.right);
            }

            // If the current node has left child
            else if (temp.right == null && temp.left != null)
            {
                // If the current node is not equal to
                // its left child return false
                if (temp.data != temp.left.data)
                    return false;

                q.push(temp.left);
            }
        }

        // If the given tree has children
        // sum property return true
        return true;
    }

    let root = newNode(10);
    root.left = newNode(8);
    root.right = newNode(2);
    root.left.left = newNode(3);
    root.left.right = newNode(5);
    root.right.right = newNode(2);

    if (CheckChildrenSum(root))
        document.write("Yes");
    else
        document.write("No");

</script>
```

**Output:** 

```
Yes    
```

**时间复杂度** : O(N)，其中 N 为二叉树中的节点总数。
**辅助空间:** O(N)