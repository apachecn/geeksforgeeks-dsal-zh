# 检查二叉树中的两个节点是否是兄弟

> 原文:[https://www . geeksforgeeks . org/check-如果二叉树中的两个节点是兄弟节点/](https://www.geeksforgeeks.org/check-if-two-nodes-in-a-binary-tree-are-siblings/)

给定一棵二叉树和两个节点，任务是检查节点是否是彼此的兄弟。

如果两个节点处于同一级别，并且其父节点相同，则称其为**兄弟节点**。

**示例:**

```
Input : 
       1
      /  \
     2    3
    / \  / \
   4   5 6  7
First node is 4 and Second node is 6.
Output : No, they are not siblings.

Input :
         1
        /  \
       5    6
      /    /  \
     7     3   4
First node is 3 and Second node is 4
Output : Yes
```

**方法:**仔细观察可以得出，二叉树中的任意节点最多可以有两个子节点。因此，由于两个兄弟的父节点必须是相同的，所以我们的想法是简单地遍历树，对于每个节点，检查两个给定的节点是否是它的子节点。如果树中的任何节点为真，则打印是，否则打印否

下面是上述方法的实现:

## C++

```
// C++ program to check if two nodes are
// siblings

#include <bits/stdc++.h>
using namespace std;

// Binary Tree Node
struct Node {
    int data;
    Node *left, *right;
};

// Utility function to create a new node
struct Node* newNode(int data)
{
    struct Node* node = new Node;
    node->data = data;
    node->left = node->right = NULL;

    return (node);
}

// Function to find out if two nodes are siblings
bool CheckIfNodesAreSiblings(Node* root, int data_one,
                             int data_two)
{
    if (!root)
        return false;

    // Compare the two given nodes with
    // the childrens of current node
    if (root->left && root->right) {
        int left = root->left->data;
        int right = root->right->data;

        if (left == data_one && right == data_two)
            return true;
        else if (left == data_two && right == data_one)
            return true;
    }

    // Check for left subtree
    if (root->left)
        if(CheckIfNodesAreSiblings(root->left, data_one,
                                data_two))
          return true;

    // Check for right subtree
    if (root->right)
        if(CheckIfNodesAreSiblings(root->right, data_one,
                                data_two))
          return true;
}

// Driver code
int main()
{

    struct Node* root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->right->left = newNode(5);
    root->right->right = newNode(6);
    root->left->left->right = newNode(7);

    int data_one = 5;
    int data_two = 6;

    if (CheckIfNodesAreSiblings(root, data_one, data_two))
        cout << "YES";
    else
        cout << "NO";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if two nodes
// are siblings
import java.util.*;

class GFG{

// Binary Tree Node
static class Node
{
    int data;
    Node left, right;
};

// Utility function to create a
// new node
static Node newNode(int data)
{
    Node node = new Node();
    node.data = data;
    node.left = node.right = null;

    return (node);
}
static Node root = null;

// Function to find out if two nodes are siblings
static boolean CheckIfNodesAreSiblings(Node root,
                                       int data_one,
                                       int data_two)
{
    if (root == null)
        return false;

    // Compare the two given nodes with
    // the childrens of current node
    if (root.left != null && root.right != null)
    {
        int left = root.left.data;
        int right = root.right.data;

        if (left == data_one &&
           right == data_two)
            return true;
        else if (left == data_two &&
                right == data_one)
            return true;
    }

    // Check for left subtree
    if (root.left != null)
        CheckIfNodesAreSiblings(root.left,
                                data_one,
                                data_two);

    // Check for right subtree
    if (root.right != null)
        CheckIfNodesAreSiblings(root.right,
                                data_one,
                                data_two);
    return true;
}

// Driver code
public static void main(String[] args)
{
    root = newNode(1);
    root.left = newNode(2);
    root.right = newNode(3);
    root.left.left = newNode(4);
    root.right.left = newNode(5);
    root.right.right = newNode(6);
    root.left.left.right = newNode(7);

    int data_one = 5;
    int data_two = 6;

    if (CheckIfNodesAreSiblings(root,
                                data_one,
                                data_two))
        System.out.print("YES");
    else
        System.out.print("NO");
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to check if two
# nodes are siblings

# Binary Tree Node
class Node:

    def __init__(self, key):

        self.data = key
        self.left = None
        self.right = None

# Function to find out if two nodes are siblings
def CheckIfNodesAreSiblings(root, data_one,
                                  data_two):

    if (root == None):
        return False

    # Compare the two given nodes with
    # the childrens of current node
    ans = False

    if (root.left != None and root.right != None):
        left = root.left.data
        right = root.right.data

        if (left == data_one and right == data_two):
            return True
        elif (left == data_two and right == data_one):
            return True

    # Check for left subtree
    if (root.left != None):
        ans = ans or CheckIfNodesAreSiblings(root.left,
                                       data_one,
                                       data_two)

    # Check for right subtree
    if (root.right != None):
        ans = ans or CheckIfNodesAreSiblings(root.right,
                                       data_one,
                                       data_two)

    return ans   

# Driver code
if __name__ == '__main__':

    root = Node(1)
    root.left = Node(2)
    root.right = Node(3)
    root.left.left = Node(4)
    root.right.left = Node(5)
    root.right.right = Node(6)
    root.left.left.right = Node(7)

    data_one = 5
    data_two = 6

    if (CheckIfNodesAreSiblings(root,
                                data_one,
                                data_two)):
        print("YES")
    else:
        print("NO")

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to check if two nodes
// are siblings
using System;

// Binary Tree Node
public class Node
{
    public int data;
    public Node left, right;

    // Utility function to create a
    // new node
    public Node(int item)
    {
        data = item;
        left = right = null;
    }
}

class GFG{

static Node root = null;

// Function to find out if two
// nodes are siblings
static bool CheckIfNodesAreSiblings(Node root,
                                    int data_one,
                                    int data_two)
{
    if (root == null)
    {
        return false;
    }

    // Compare the two given nodes with
    // the childrens of current node
    if (root.left != null && root.right != null)
    {
        int left = root.left.data;
        int right = root.right.data;

        if (left == data_one && right == data_two)
        {
            return true;
        }
        else if (left == data_two && right == data_one)
        {
            return true;
        }
    }

    // Check for left subtree
    if (root.left != null)
    {
        CheckIfNodesAreSiblings(root.left, data_one,
                                data_two);
    }

    // Check for right subtree
    if (root.right != null)
    {
        CheckIfNodesAreSiblings(root.right, data_one,
                                data_two);
    }
    return true;
}

// Driver code
static public void Main()
{
    GFG.root = new Node(1);
    GFG.root.left = new Node(2);
    GFG.root.right = new Node(3);
    GFG.root.left.left = new Node(4);
    GFG.root.right.left = new Node(5);
    GFG.root.right.right = new Node(6);
    GFG.root.left.left.right = new Node(7);

    int data_one = 5;
    int data_two = 6;

    if (CheckIfNodesAreSiblings(root, data_one,
                                data_two))
    {
        Console.WriteLine("YES");
    }
    else
    {
        Console.WriteLine("NO");
    }
}
}

// This code is contributed by avanitrachhadiya2155
```

## java 描述语言

```
<script>

// Javascript program to check if two nodes
// are siblings

// Binary Tree Node
class Node
{
    constructor(data)
    {
        this.data = data;
        this.left = this.right = null;
    }
}

let root = null;

// Function to find out if two nodes are siblings
function CheckIfNodesAreSiblings(
    root, data_one, data_two)
{
    if (root == null)
        return false;

    // Compare the two given nodes with
    // the childrens of current node
    if (root.left != null && root.right != null)
    {
        let left = root.left.data;
        let right = root.right.data;

        if (left == data_one &&
           right == data_two)
            return true;

        else if (left == data_two &&
                right == data_one)
            return true;
    }

    // Check for left subtree
    if (root.left != null)
        CheckIfNodesAreSiblings(root.left,
                                data_one,
                                data_two);

    // Check for right subtree
    if (root.right != null)
        CheckIfNodesAreSiblings(root.right,
                                data_one,
                                data_two);
    return true;
}

// Driver code
root = new Node(1);
root.left = new Node(2);
root.right = new Node(3);
root.left.left = new Node(4);
root.right.left = new Node(5);
root.right.right = new Node(6);
root.left.left.right = new Node(7);

let data_one = 5;
let data_two = 6;

if (CheckIfNodesAreSiblings(root,
                            data_one,
                            data_two))
    document.write("YES");
else
    document.write("NO");

// This code is contributed by unknown2108

</script>
```

**Output:** 

```
YES
```