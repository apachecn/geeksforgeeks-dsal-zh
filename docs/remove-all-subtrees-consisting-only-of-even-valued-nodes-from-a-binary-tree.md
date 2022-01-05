# 从二叉树中移除仅由偶数值节点组成的所有子树

> 原文:[https://www . geesforgeks . org/remove-all-subtrees-仅由二进制树中的偶数值节点组成/](https://www.geeksforgeeks.org/remove-all-subtrees-consisting-only-of-even-valued-nodes-from-a-binary-tree/)

给定一个[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)，任务是移除所有不包含任何奇值节点的子树。删除这些子树后，打印树的[水平顺序遍历](https://www.geeksforgeeks.org/level-order-tree-traversal/)。
***注意:**删除的节点打印**空**。*

**示例:**

> **输入:**下面是给定的树:
> 1
> \
> 2
> /\
> 8 5
> T8】输出: 1 NULL 2 NULL 5
> **说明:**
> 修剪后的树:
> 1
> \
> 2
> \
> 5
> 
> **输入:**下面是给定的树:
> **1
> /\
> 2 7
> /\/\
> 8 10 12 5
> **输出:** 1 NULL 7 NULL 5
> **说明:**
> 修剪后的树:
> **1
> \
> 7
> \
> 5****

******方法:**为了解决给定的问题，想法是使用 [DFS 遍历](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/)遍历树，并且将使用[回溯](https://www.geeksforgeeks.org/backtracking-algorithms/)的概念。按照以下步骤解决问题:****

*   ****[使用](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/) [DFS 遍历](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/)遍历给定的树，并执行以下步骤:

    *   如果根节点为**空**，则返回。
    *   如果叶节点值为偶数，则通过返回**空**删除该节点。否则，从当前递归调用返回根节点。
    *   使用上述条件递归更新左右子树。**** 
*   ****完成上述步骤后，使用[级顺序遍历](https://www.geeksforgeeks.org/level-order-tree-traversal/)打印更新后的树，用空值代替删除的节点。****

****下面是上述方法的实现:****

## ****C++****

```
**// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Node of the tree
struct node {
    int data;
    struct node *left, *right;
};

// Function to create a new node
node* newNode(int key)
{
    node* temp = new node;
    temp->data = key;
    temp->left = temp->right = NULL;
    return (temp);
}

// Function to print tree level wise
void printLevelOrder(node* root)
{
    // Base Case
    if (!root)
        return;

    // Create an empty queue for
    // level order traversal
    queue<node*> q;

    // Enqueue Root
    q.push(root);

    while (!q.empty()) {

        // Print front of queue and
        // remove it from queue
        node* temp = q.front();
        cout << temp->data << " ";
        q.pop();

        // If left child is present
        if (temp->left != NULL) {

            q.push(temp->left);
        }

        // Otherwise
        else if (temp->right != NULL) {

            cout << "NULL ";
        }

        // If right child is present
        if (temp->right != NULL) {

            q.push(temp->right);
        }

        // Otherwise
        else if (temp->left != NULL) {

            cout << "NULL ";
        }
    }
}

// Function to remove subtrees
node* pruneTree(node* root)
{
    // Base Case
    if (!root) {
        return NULL;
    }

    // Search for required condition
    // in left and right half
    root->left = pruneTree(root->left);
    root->right = pruneTree(root->right);

    // If the node is even
    // and leaf node
    if (root->data % 2 == 0
        && !root->right
        && !root->left)
        return NULL;

    return root;
}

// Driver Code
int main()
{
    struct node* root = newNode(1);
    root->left = newNode(2);
    root->left->left = newNode(8);
    root->left->right = newNode(10);
    root->right = newNode(7);
    root->right->left = newNode(12);
    root->right->right = newNode(5);

    // Function Call
    node* newRoot = pruneTree(root);

    // Print answer
    printLevelOrder(newRoot);

    return 0;
}**
```

## ****Java 语言(一种计算机语言，尤用于创建网站)****

```
**// Java program for the above approach
import java.util.*;
class GFG
{

// Node of the tree
static class node
{
    int data;
    node left, right;
};

// Function to create a new node
static node newNode(int key)
{
    node temp = new node();
    temp.data = key;
    temp.left = temp.right = null;
    return (temp);
}

// Function to print tree level wise
static void printLevelOrder(node root)
{

    // Base Case
    if (root==null)
        return;

    // Create an empty queue for
    // level order traversal
    Queue<node> q = new LinkedList<>();

    // Enqueue Root
    q.add(root);
    while (!q.isEmpty())
    {

        // Print front of queue and
        // remove it from queue
        node temp = q.peek();
        System.out.print(temp.data+ " ");
        q.remove();

        // If left child is present
        if (temp.left != null)
        {
            q.add(temp.left);
        }

        // Otherwise
        else if (temp.right != null)
        {
            System.out.print("null ");
        }

        // If right child is present
        if (temp.right != null)
        {
            q.add(temp.right);
        }

        // Otherwise
        else if (temp.left != null)
        {
            System.out.print("null ");
        }
    }
}

// Function to remove subtrees
static node pruneTree(node root)
{
    // Base Case
    if (root == null)
    {
        return null;
    }

    // Search for required condition
    // in left and right half
    root.left = pruneTree(root.left);
    root.right = pruneTree(root.right);

    // If the node is even
    // and leaf node
    if (root.data % 2 == 0
        && root.right==null
        && root.left==null)
        return null;

    return root;
}

// Driver Code
public static void main(String[] args)
{
    node root = newNode(1);
    root.left = newNode(2);
    root.left.left = newNode(8);
    root.left.right = newNode(10);
    root.right = newNode(7);
    root.right.left = newNode(12);
    root.right.right = newNode(5);

    // Function Call
    node newRoot = pruneTree(root);

    // Print answer
    printLevelOrder(newRoot);
}
}

// This code is contributed by shikhasingrajput**
```

## ****蟒蛇 3****

```
**# Python 3 program for the above approach

# Node of the tree
class node:
    def __init__(self,data):
        self.data = data
        self.left = None
        self.right = None

# Function to print tree level wise
def printLevelOrder(root):

    # Base Case
    if (root==None):
        return

    # Create an empty queue for
    # level order traversal
    q = []

    # Enqueue Root
    q.append(root)

    while(len(q)>0):
        # Print front of queue and
        # remove it from queue
        temp = q[0]
        print(temp.data,end = " ")
        q = q[1:]

        # If left child is present
        if (temp.left != None):
            q.append(temp.left)

        # Otherwise
        elif (temp.right != None):
            print("NULL",end= " ")

        # If right child is present
        if (temp.right != None):
            q.append(temp.right)

        # Otherwise
        elif (temp.left != None):
            print("NULL",end = " ")

# Function to remove subtrees
def pruneTree(root):

    # Base Case
    if (root==None):
        return None

    # Search for required condition
    # in left and right half
    root.left = pruneTree(root.left)
    root.right = pruneTree(root.right)

    # If the node is even
    # and leaf node
    if (root.data % 2 == 0 and root.right == None and root.left==None):
        return None

    return root

# Driver Code
if __name__ == '__main__':
    root = node(1)
    root.left = node(2)
    root.left.left = node(8)
    root.left.right = node(10)
    root.right = node(7)
    root.right.left = node(12)
    root.right.right = node(5)

    # Function Call
    newRoot = pruneTree(root)

    # Print answer
    printLevelOrder(newRoot)

    # This code is contributed by SURENDRA_GANGWAR.**
```

## ****C#****

```
**// C# program for the above approach
using System;
using System.Collections.Generic;

public class GFG
{

// Node of the tree
class node
{
    public int data;
    public node left, right;
};

// Function to create a new node
static node newNode(int key)
{
    node temp = new node();
    temp.data = key;
    temp.left = temp.right = null;
    return (temp);
}

// Function to print tree level wise
static void printLevelOrder(node root)
{

    // Base Case
    if (root == null)
        return;

    // Create an empty queue for
    // level order traversal
    Queue<node> q = new Queue<node>();

    // Enqueue Root
    q.Enqueue(root);
    while (q.Count != 0)
    {

        // Print front of queue and
        // remove it from queue
        node temp = q.Peek();
        Console.Write(temp.data+ " ");
        q.Dequeue();

        // If left child is present
        if (temp.left != null)
        {
            q.Enqueue(temp.left);
        }

        // Otherwise
        else if (temp.right != null)
        {
            Console.Write("null ");
        }

        // If right child is present
        if (temp.right != null)
        {
            q.Enqueue(temp.right);
        }

        // Otherwise
        else if (temp.left != null)
        {
            Console.Write("null ");
        }
    }
}

// Function to remove subtrees
static node pruneTree(node root)
{

    // Base Case
    if (root == null)
    {
        return null;
    }

    // Search for required condition
    // in left and right half
    root.left = pruneTree(root.left);
    root.right = pruneTree(root.right);

    // If the node is even
    // and leaf node
    if (root.data % 2 == 0
        && root.right==null
        && root.left==null)
        return null;

    return root;
}

// Driver Code
public static void Main(String[] args)
{
    node root = newNode(1);
    root.left = newNode(2);
    root.left.left = newNode(8);
    root.left.right = newNode(10);
    root.right = newNode(7);
    root.right.left = newNode(12);
    root.right.right = newNode(5);

    // Function Call
    node newRoot = pruneTree(root);

    // Print answer
    printLevelOrder(newRoot);
}
}

// This code is contributed by shikhasingrajput**
```

## ****java 描述语言****

```
**<script>
    // Javascript program for the above approach

    // Node of the tree
    class node
    {
        constructor(key) {
           this.left = null;
           this.right = null;
           this.data = key;
        }
    }

    // Function to create a new node
    function newNode(key)
    {
        let temp = new node(key);
        return (temp);
    }

    // Function to print tree level wise
    function printLevelOrder(root)
    {

        // Base Case
        if (root == null)
            return;

        // Create an empty queue for
        // level order traversal
        let q = [];

        // Enqueue Root
        q.push(root);
        while (q.length != 0)
        {

            // Print front of queue and
            // remove it from queue
            let temp = q[0];
            document.write(temp.data+ " ");
            q.shift();

            // If left child is present
            if (temp.left != null)
            {
                q.push(temp.left);
            }

            // Otherwise
            else if (temp.right != null)
            {
                document.write("Null ");
            }

            // If right child is present
            if (temp.right != null)
            {
                q.push(temp.right);
            }

            // Otherwise
            else if (temp.left != null)
            {
                document.write("Null ");
            }
        }
    }

    // Function to remove subtrees
    function pruneTree(root)
    {

        // Base Case
        if (root == null)
        {
            return null;
        }

        // Search for required condition
        // in left and right half
        root.left = pruneTree(root.left);
        root.right = pruneTree(root.right);

        // If the node is even
        // and leaf node
        if (root.data % 2 == 0
            && root.right==null
            && root.left==null)
            return null;

        return root;
    }

    let root = newNode(1);
    root.left = newNode(2);
    root.left.left = newNode(8);
    root.left.right = newNode(10);
    root.right = newNode(7);
    root.right.left = newNode(12);
    root.right.right = newNode(5);

    // Function Call
    let newRoot = pruneTree(root);

    // Print answer
    printLevelOrder(newRoot);

   // This code is contributed by decode2207.
</script>**
```

******Output:** 

```
1 NULL 7 NULL 5
```**** 

*******时间复杂度:**O(N)*
T5**辅助空间:** O(1)****