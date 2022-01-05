# 检查二叉树是否为奇偶树

> 原文:[https://www . geesforgeks . org/check-if-a-a-binary-tree-is-an-偶数-奇数-tree-or-not/](https://www.geeksforgeeks.org/check-if-a-binary-tree-is-an-even-odd-tree-or-not/)

给定一棵[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)，任务是检查二叉树是否为奇偶二叉树。

> 当所有处于偶数层的节点都具有偶数值时(假设**根**处于第 **0** 层)，并且所有处于奇数层的节点都具有奇数值，则**二叉树**被称为奇偶树。

**示例:**

> **输入:**
> 
> ```
>              2
>             / \
>            3   9
>           / \   \
>          4   10  6
> ```
> 
> **输出:**是
> **说明:**
> 只有 0 级(偶数)的节点才是 2 级(偶数)。
> 1 级节点为 3 和 9(均为奇数)。
> 2 级节点为 4、10、6(均为偶数)。
> 因此，二叉树是奇偶二叉树。
> 
> **输入:**
> 
> ```
>              4
>             / \
>            3   7
>           / \   \
>          4   10  5
> ```
> 
> **输出:**否

**方法:**按照以下步骤解决问题:

1.  其思想是执行[级序遍历](https://www.geeksforgeeks.org/level-order-tree-traversal/)并检查出现在偶数级的节点是否为偶数值，出现在奇数级的节点是否为奇数值。
2.  如果发现奇数层的任何节点具有奇数值，反之亦然，则打印“**否**”。
3.  否则，完成树的遍历后，打印“ **YES** ”。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include<bits/stdc++.h>
using namespace std;

struct Node
{
    int val;
    Node *left, *right;
};

struct Node* newNode(int data)
{
    struct Node* temp = (struct Node*)malloc(sizeof(struct Node));
    temp->val = data;
    temp->left = NULL;
    temp->right = NULL;
    return temp;
}

// Function to check if the
// tree is even-odd tree
bool isEvenOddBinaryTree(Node *root)
{
    if (root == NULL)
        return true;

    // Stores nodes of each level
    queue<Node*> q;
    q.push(root);

    // Store the current level
    // of the binary tree
    int level = 0;

    // Traverse until the
    // queue is empty
    while (!q.empty())
    {

        // Stores the number of nodes
        // present in the current level
        int size = q.size();

        for(int i = 0; i < size; i++)
        {
            Node *node = q.front();

            // Check if the level
            // is even or odd
            if (level % 2 == 0)
            {
                if (node->val % 2 == 1)
                    return false;
            }
            else if (level % 2 == 1)
            {
                if (node->val % 2 == 0)
                    return true;
            }

            // Add the nodes of the next
            // level into the queue
            if (node->left != NULL)
            {
                q.push(node->left);
            }
            if (node->right != NULL)
            {
                q.push(node->right);
            }
        }

        // Increment the level count
        level++;
    }
    return true;
}

// Driver Code
int main()
{

    // Construct a Binary Tree
    Node *root = NULL;
    root = newNode(2);
    root->left = newNode(3);
    root->right = newNode(9);
    root->left->left = newNode(4);
    root->left->right = newNode(10);
    root->right->right = newNode(6);

    // Check if the binary tree
    // is even-odd tree or not
    if (isEvenOddBinaryTree(root))
        cout << "YES";
    else
        cout << "NO";
}

// This code is contributed by ipg2016107
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program for the above approach
import java.util.*;

class GfG {

    // Tree node
    static class Node {
        int val;
        Node left, right;
    }

    // Function to return new tree node
    static Node newNode(int data)
    {
        Node temp = new Node();
        temp.val = data;
        temp.left = null;
        temp.right = null;
        return temp;
    }

    // Function to check if the
    // tree is even-odd tree
    public static boolean
    isEvenOddBinaryTree(Node root)
    {
        if (root == null)
            return true;

        // Stores nodes of each level
        Queue<Node> q
            = new LinkedList<>();
        q.add(root);

        // Store the current level
        // of the binary tree
        int level = 0;

        // Traverse until the
        // queue is empty
        while (!q.isEmpty()) {

            // Stores the number of nodes
            // present in the current level
            int size = q.size();

            for (int i = 0; i < size; i++) {
                Node node = q.poll();

                // Check if the level
                // is even or odd
                if (level % 2 == 0) {

                    if (node.val % 2 == 1)
                        return false;
                }
                else if (level % 2 == 1) {

                    if (node.val % 2 == 0)
                        return false;
                }

                // Add the nodes of the next
                // level into the queue
                if (node.left != null) {

                    q.add(node.left);
                }
                if (node.right != null) {

                    q.add(node.right);
                }
            }

            // Increment the level count
            level++;
        }

        return true;
    }

    // Driver Code
    public static void main(String[] args)
    {

        // Construct a Binary Tree
        Node root = null;
        root = newNode(2);
        root.left = newNode(3);
        root.right = newNode(9);
        root.left.left = newNode(4);
        root.left.right = newNode(10);
        root.right.right = newNode(6);

        // Check if the binary tree
        // is even-odd tree or not
        if (isEvenOddBinaryTree(root)) {

            System.out.println("YES");
        }
        else {

            System.out.println("NO");
        }
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Tree node
class Node:

    def __init__(self, data):

        self.left = None
        self.right = None
        self.val = data

# Function to return new tree node
def newNode(data):

    temp = Node(data)

    return temp

# Function to check if the
# tree is even-odd tree
def isEvenOddBinaryTree(root):

    if (root == None):
        return True

    q = []

    # Stores nodes of each level
    q.append(root)

    # Store the current level
    # of the binary tree
    level = 0

    # Traverse until the
    # queue is empty
    while (len(q) != 0):

        # Stores the number of nodes
        # present in the current level
        size = len(q)

        for i in range(size):
            node = q[0]
            q.pop(0)

            # Check if the level
            # is even or odd
            if (level % 2 == 0):

                if (node.val % 2 == 1):
                    return False

                elif (level % 2 == 1):
                    if (node.val % 2 == 0):
                        return False

                # Add the nodes of the next
                # level into the queue
                if (node.left != None):
                    q.append(node.left)

                if (node.right != None):
                    q.append(node.right)

            # Increment the level count
            level += 1

        return True

# Driver code
if __name__=="__main__":

    # Construct a Binary Tree
    root = None
    root = newNode(2)
    root.left = newNode(3)
    root.right = newNode(9)
    root.left.left = newNode(4)
    root.left.right = newNode(10)
    root.right.right = newNode(6)

    # Check if the binary tree
    # is even-odd tree or not
    if (isEvenOddBinaryTree(root)):
        print("YES")
    else:
        print("NO")

# This code is contributed by rutvik_56
```

## C#

```
// C# Program for the
// above approach
using System;
using System.Collections.Generic;
class GfG{

// Tree node
class Node
{
  public int val;
  public Node left, right;
}

// Function to return new
// tree node
static Node newNode(int data)
{
  Node temp = new Node();
  temp.val = data;
  temp.left = null;
  temp.right = null;
  return temp;
}

// Function to check if the
// tree is even-odd tree
static bool isEvenOddBinaryTree(Node root)
{
  if (root == null)
    return true;

  // Stores nodes of each level
  Queue<Node> q = new Queue<Node>();
  q.Enqueue(root);

  // Store the current level
  // of the binary tree
  int level = 0;

  // Traverse until the
  // queue is empty
  while (q.Count != 0)
  {
    // Stores the number of nodes
    // present in the current level
    int size = q.Count;

    for (int i = 0; i < size; i++)
    {
      Node node = q.Dequeue();

      // Check if the level
      // is even or odd
      if (level % 2 == 0)
      {
        if (node.val % 2 == 1)
          return false;
      }
      else if (level % 2 == 1)
      {
        if (node.val % 2 == 0)
          return false;
      }

      // Add the nodes of the next
      // level into the queue
      if (node.left != null)
      {
        q.Enqueue(node.left);
      }
      if (node.right != null)
      {
        q.Enqueue(node.right);
      }
    }

    // Increment the level count
    level++;
  }

  return true;
}

// Driver Code
public static void Main(String[] args)
{
  // Construct a Binary Tree
  Node root = null;
  root = newNode(2);
  root.left = newNode(3);
  root.right = newNode(9);
  root.left.left = newNode(4);
  root.left.right = newNode(10);
  root.right.right = newNode(6);

  // Check if the binary tree
  // is even-odd tree or not
  if (isEvenOddBinaryTree(root))
  {
    Console.WriteLine("YES");
  }
  else
  {
    Console.WriteLine("NO");
  }
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Tree node
class Node
{
    constructor(data)
    {
        this.left = null;
        this.right = null;
        this.val = data;
    }
}

// Function to return new tree node
function newNode(data)
{
    let temp = new Node(data);
    return temp;
}

// Function to check if the
// tree is even-odd tree
function isEvenOddBinaryTree(root)
{
    if (root == null)
        return true;

    // Stores nodes of each level
    let q = [];
    q.push(root);

    // Store the current level
    // of the binary tree
    let level = 0;

    // Traverse until the
    // queue is empty
    while (q.length > 0)
    {

        // Stores the number of nodes
        // present in the current level
        let size = q.length;

        for(let i = 0; i < size; i++)
        {
            let node = q[0];
            q.shift();

            // Check if the level
            // is even or odd
            if (level % 2 == 0)
            {
                if (node.val % 2 == 1)
                    return false;
            }
            else if (level % 2 == 1)
            {
                if (node.val % 2 == 0)
                    return false;
            }

            // Add the nodes of the next
            // level into the queue
            if (node.left != null)
            {
                q.push(node.left);
            }
            if (node.right != null)
            {
                q.push(node.right);
            }
        }

        // Increment the level count
        level++;
    }
    return true;
}

// Driver code

// Construct a Binary Tree
let root = null;
root = newNode(2);
root.left = newNode(3);
root.right = newNode(9);
root.left.left = newNode(4);
root.left.right = newNode(10);
root.right.right = newNode(6);

// Check if the binary tree
// is even-odd tree or not
if (isEvenOddBinaryTree(root))
{
    document.write("YES");
}
else
{
    document.write("NO");
}

// This code is contributed by suresh07

</script>
```

**Output:** 

```
YES
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)

**方法 2(利用亲子差异)**

**方法:**
想法是检查子节点和父节点之间的绝对差异。

1.如果根节点是奇数，返回“**否**”。

2.如果根节点是偶数，那么子节点应该是奇数，所以差应该总是奇数。在真实情况下返回“**是**”，否则返回“**否**”。

下面是上述方法的实现:

## C++

```
#include <bits/stdc++.h>
using namespace std;

// tree node
struct Node
{
    int data;
    Node *left, *right;
};

// returns a new
// tree Node
Node* newNode(int data)
{
    Node* temp = new Node();
    temp->data = data;
    temp->left = temp->right = NULL;
    return temp;
}

// Utility function to recursively traverse tree and check the diff between child nodes
bool BSTUtil(Node * root){
    if(root==NULL)
        return true;

    //if left nodes exist and absolute difference between left child and parent is divisible by 2, then return false       
    if(root->left!=NULL && abs(root->data - root->left->data)%2==0)
        return false;
     //if right nodes exist and absolute difference between right child and parent is divisible by 2, then return false
    if(root->right!=NULL && abs(root->data - root->right->data)%2==0)
        return false;

    //recursively traverse left and right subtree
    return BSTUtil(root->left) && BSTUtil(root->right);
}

// Utility function to check if binary tree is even-odd binary tree
bool isEvenOddBinaryTree(Node * root){
    if(root==NULL)
        return true;

    // if root node is odd, return false
    if(root->data%2 != 0)
        return false;

    return BSTUtil(root);  
}

// driver program
int main()
{
    // construct a tree
    Node* root = newNode(5);
    root->left = newNode(2);
    root->right = newNode(6);
    root->left->left = newNode(1);
    root->left->right = newNode(5);
    root->right->right = newNode(7);
    root->left->right->left = newNode(12);

    root->right->right->right = newNode(14);
    root->right->right->left = newNode(16);

    if(BSTUtil(root))
      cout<<"YES";
    else
      cout<<"NO";
    return 0;
}
```

**Output**

```
YES
```

***时间复杂度:O(N)***

***辅助空间:O(1)***