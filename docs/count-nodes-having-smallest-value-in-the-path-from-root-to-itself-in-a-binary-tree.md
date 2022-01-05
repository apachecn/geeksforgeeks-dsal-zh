# 计算二叉树中从根到自身的路径中具有最小值的节点

> 原文:[https://www . geeksforgeeks . org/count-nodes-在二叉树中从根到自身的路径中具有最小值/](https://www.geeksforgeeks.org/count-nodes-having-smallest-value-in-the-path-from-root-to-itself-in-a-binary-tree/)

给定一棵 [**二叉树**](https://www.geeksforgeeks.org/binary-tree-data-structure/) ，任务是计算给定二叉树中的节点数，使得从根到该节点的路径包含值大于或等于该节点的节点。

**示例:**

```
Input:
               6
             /   \
            7     4
           / \   / \
          3   7 1   2

Output: 5
Explanation:
Root node 6 is considered as its the only node 
in the path from root to itself.
Node 4 has the minimum value in it's path 6->4.
Node 1 has the minimum value in it's path 6->4->1.
Node 2 has the minimum value in it's path 6->4->2.
Node 3 has the minimum value in it's path 6->7->3.

Input:
               8
             /   \
            6     5
           / \   / \
          6   7 3   9

Output: 5
Explanation:
Root node 8 is considered as its the only node
in the path from root to itself.
Node 6 has the minimum value in it's path 8->6.
Node 6 has the minimum value in it's path 8->6->6.
Node 5 has the minimum value in it's path 8->5.
Node 3 has the minimum value in it's path 8->5->3.
```

**方法:**想法是在给定的二叉树上进行[前序遍历](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)。按照以下步骤解决问题:

1.  创建一个函数来计算满足给定条件的节点数。
2.  如果当前节点为空，则返回到上一个节点。
3.  使用变量 **minNodeVal** 存储从根到当前节点的路径上的最小节点值。
4.  如果当前节点的值小于或等于 **minNodeVal** ，则将最终计数增加 1，并更新 **minNodeVal** 的值。
5.  为当前节点的左右子节点调用函数，并对每个节点重复此过程，以获得所需节点的总数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Structure of a tree node
struct Node {
    int key;
    Node *left, *right;
};

// Function to create new tree node
Node* newNode(int key)
{
    Node* temp = new Node;
    temp->key = key;
    temp->left = temp->right = NULL;
    return temp;
}

// Function to find the total
// number of required nodes
void countReqNodes(Node* root,
                   int minNodeVal, int& ans)
{
    // If current node is null then
    // return to the parent node
    if (root == NULL)
        return;

    // Check if current node value is
    // less than or equal to minNodeVal
    if (root->key <= minNodeVal) {

        // Update the value of minNodeVal
        minNodeVal = root->key;

        // Update the count
        ans++;
    }

    // Go to the left subtree
    countReqNodes(root->left,
                  minNodeVal, ans);

    // Go to the right subtree
    countReqNodes(root->right,
                  minNodeVal, ans);
}

// Driver Code
int main()
{
    /* Binary Tree creation
               8
             /   \
            /     \
           6       5
          / \     /  \
         /   \   /    \
        6     7 3      9
    */

    Node* root = newNode(8);
    root->left = newNode(6);
    root->right = newNode(5);
    root->left->left = newNode(6);
    root->left->right = newNode(7);
    root->right->left = newNode(3);
    root->right->right = newNode(9);

    int ans = 0, minNodeVal = INT_MAX;

    // Function Call
    countReqNodes(root, minNodeVal, ans);

    // Print the result
    cout << ans;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Structure of a tree node
static class Node
{
    int key;
    Node left, right;
};

// Function to create new tree node
static Node newNode(int key)
{
    Node temp = new Node();
    temp.key = key;
    temp.left = temp.right = null;
    return temp;
}
static int ans;

// Function to find the total
// number of required nodes
static void countReqNodes(Node root,
                          int minNodeVal)
{

    // If current node is null then
    // return to the parent node
    if (root == null)
        return;

    // Check if current node value is
    // less than or equal to minNodeVal
    if (root.key <= minNodeVal)
    {

        // Update the value of minNodeVal
        minNodeVal = root.key;

        // Update the count
        ans++;
    }

    // Go to the left subtree
    countReqNodes(root.left,
                  minNodeVal);

    // Go to the right subtree
    countReqNodes(root.right,
                  minNodeVal);
}

// Driver Code
public static void main(String[] args)
{

    /* Binary Tree creation
               8
             /   \
            /     \
           6       5
          / \     /  \
         /   \   /    \
        6     7 3      9
    */

    Node root = newNode(8);
    root.left = newNode(6);
    root.right = newNode(5);
    root.left.left = newNode(6);
    root.left.right = newNode(7);
    root.right.left = newNode(3);
    root.right.right = newNode(9);

    int  minNodeVal = Integer.MAX_VALUE;
    ans = 0;

    // Function Call
    countReqNodes(root, minNodeVal);

    // Print the result
    System.out.print(ans);
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program for the above approach
import sys

ans = 0

# Class of a tree node
class Node:

    def __init__(self, key):

        self.key = key
        self.left = None
        self.right = None

# Function to find the total
# number of required nodes
def countReqNodes(root, minNodeVal):

    global ans

    # If current node is null then
    # return to the parent node
    if root == None:
        return

    # Check if current node value is
    # less than or equal to minNodeVal   
    if root.key <= minNodeVal:

        # Update the value of minNodeVal
        minNodeVal = root.key

        # Update the count
        ans += 1

    # Go to the left subtree   
    countReqNodes(root.left, minNodeVal)

    # Go to the right subtree
    countReqNodes(root.right, minNodeVal)

# Driver Code
if __name__ == '__main__':

     # Binary Tree creation
     #           8
     #         /   \
     #        /     \
     #       6       5
     #      / \     /  \
     #     /   \   /    \
     #    6     7 3      9
     #

    root = Node(8)

    root.left = Node(6)
    root.right = Node(5)
    root.left.left = Node(6)
    root.left.right = Node(7)
    root.right.left = Node(3)
    root.right.right = Node(9)

    minNodeVal = sys.maxsize

    # Function Call
    countReqNodes(root, minNodeVal)

    # Print the result
    print(ans)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Structure of a tree node
public class Node
{
    public int key;
    public Node left, right;
};

// Function to create new tree node
static Node newNode(int key)
{
    Node temp = new Node();
    temp.key = key;
    temp.left = temp.right = null;
    return temp;
}

static int ans;

// Function to find the total
// number of required nodes
static void countReqNodes(Node root,
                          int minNodeVal)
{

    // If current node is null then
    // return to the parent node
    if (root == null)
        return;

    // Check if current node value is
    // less than or equal to minNodeVal
    if (root.key <= minNodeVal)
    {

        // Update the value of minNodeVal
        minNodeVal = root.key;

        // Update the count
        ans++;
    }

    // Go to the left subtree
    countReqNodes(root.left,
                  minNodeVal);

    // Go to the right subtree
    countReqNodes(root.right,
                  minNodeVal);
}

// Driver Code
public static void Main(String[] args)
{

    /* Binary Tree creation
               8
             /   \
            /     \
           6       5
          / \     /  \
         /   \   /    \
        6     7 3      9
    */

    Node root = newNode(8);
    root.left = newNode(6);
    root.right = newNode(5);
    root.left.left = newNode(6);
    root.left.right = newNode(7);
    root.right.left = newNode(3);
    root.right.right = newNode(9);

    int  minNodeVal = int.MaxValue;
    ans = 0;

    // Function Call
    countReqNodes(root, minNodeVal);

    // Print the result
    Console.Write(ans);
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Structure of tree node
class Node
{
    constructor(key)
    {

        this.left = null;
        this.right = null;
        this.key = key;
    }
}

// Function to create new tree node
function newNode(key)
{
    let temp = new Node(key);
    return temp;
}

let ans;

// Function to find the total
// number of required nodes
function countReqNodes(root, minNodeVal)
{

    // If current node is null then
    // return to the parent node
    if (root == null)
        return;

    // Check if current node value is
    // less than or equal to minNodeVal
    if (root.key <= minNodeVal)
    {

        // Update the value of minNodeVal
        minNodeVal = root.key;

        // Update the count
        ans++;
    }

    // Go to the left subtree
    countReqNodes(root.left,
                  minNodeVal);

    // Go to the right subtree
    countReqNodes(root.right,
                  minNodeVal);
}

// Driver code

/* Binary Tree creation
           8
         /   \
        /     \
       6       5
      / \     /  \
     /   \   /    \
    6     7 3      9
*/
let root = newNode(8);
root.left = newNode(6);
root.right = newNode(5);
root.left.left = newNode(6);
root.left.right = newNode(7);
root.right.left = newNode(3);
root.right.right = newNode(9);

let  minNodeVal = Number.MAX_VALUE;
ans = 0;

// Function Call
countReqNodes(root, minNodeVal);

// Print the result
document.write(ans);

// This code is contributed by suresh07

</script>
```

**Output:** 

```
5
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)