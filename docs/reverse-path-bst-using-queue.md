# 使用队列

反转 BST 中的路径

> 原文:[https://www.geeksforgeeks.org/reverse-path-bst-using-queue/](https://www.geeksforgeeks.org/reverse-path-bst-using-queue/)

给定一个二叉查找树和一把钥匙，你的任务就是反转二叉树的路径。
**先决条件:** [二叉树的反向路径](https://www.geeksforgeeks.org/reverse-tree-path/)

**示例:**

```
Input :       50
           /     \
          30      70
         /  \    /  \
       20   40  60   80 
k = 70
Output :
Inorder before reversal :
20 30 40 50 60 70 80 
Inorder after reversal :
20 30 40 70 60 50 80 

Input :       8
           /     \
          3       10
         /  \       \
       1    6         14
           /  \      /
          4    7    13
k = 13
Output :
Inorder before reversal :
1 3 4 6 7 8 10 13 14
Inorder after reversal :
1 3 4 6 7 13 14 8 10
```

**方法:**
取一个队列，将所有元素推到最后，给定的键将节点键替换为队列前面的元素直到根，然后打印树的顺序。

**以下是上述方法的实施:**

## C++

```
// C++ code to demonstrate insert
// operation in binary search tree
#include <bits/stdc++.h>
using namespace std;

struct node {
    int key;
    struct node *left, *right;
};

// A utility function to
// create a new BST node
struct node* newNode(int item)
{
    struct node* temp = new node;
    temp->key = item;
    temp->left = temp->right = NULL;
    return temp;
}

// A utility function to
// do inorder traversal of BST
void inorder(struct node* root)
{
    if (root != NULL) {
        inorder(root->left);
        cout << root->key << " ";
        inorder(root->right);
    }
}

// reverse tree path using queue
void reversePath(struct node** node,
            int& key, queue<int>& q1)
{
    /* If the tree is empty,
    return a new node */
    if (node == NULL)
        return;

    // If the node key equal
    // to key then
    if ((*node)->key == key)
    {
        // push current node key
        q1.push((*node)->key);

        // replace first node
        // with last element
        (*node)->key = q1.front();

        // remove first element
        q1.pop();

        // return
        return;
    }

    // if key smaller than node key then
    else if (key < (*node)->key)
    {
        // push node key into queue
        q1.push((*node)->key);

        // recursive call itself
        reversePath(&(*node)->left, key, q1);

        // replace queue front to node key
        (*node)->key = q1.front();

        // performe pop in queue
        q1.pop();
    }

    // if key greater than node key then
    else if (key > (*node)->key)
    {
        // push node key into queue
        q1.push((*node)->key);

        // recursive call itself
        reversePath(&(*node)->right, key, q1);

        // replace queue front to node key
        (*node)->key = q1.front();

        // performe pop in queue
        q1.pop();
    }

    // return
    return;
}

/* A utility function to insert
a new node with given key in BST */
struct node* insert(struct node* node,
                              int key)
{
    /* If the tree is empty,
    return a new node */
    if (node == NULL)
        return newNode(key);

    /* Otherwise, recur down the tree */
    if (key < node->key)
        node->left = insert(node->left, key);
    else if (key > node->key)
        node->right = insert(node->right, key);

    /* return the (unchanged) node pointer */
    return node;
}

// Driver Program to test above functions
int main()
{
    /* Let us create following BST
              50
           /     \
          30      70
         /  \    /  \
       20   40  60   80 */
    struct node* root = NULL;
    queue<int> q1;

    // reverse path till k
    int k = 80;
    root = insert(root, 50);
    insert(root, 30);
    insert(root, 20);
    insert(root, 40);
    insert(root, 70);
    insert(root, 60);
    insert(root, 80);

    cout << "Before Reverse :" << endl;
    // print inorder traversal of the BST
    inorder(root);

    cout << "\n";

    // reverse path till k
    reversePath(&root, k, q1);

    cout << "After Reverse :" << endl;

    // print inorder of reverse path tree
    inorder(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to demonstrate insert
// operation in binary search tree
import java.util.*;
class GFG
{
  static class node
  {
    int key;
    node left, right;
  };
  static node root = null;
  static Queue<Integer> q1;
  static int k;

  // A utility function to
  // create a new BST node
  static node newNode(int item)
  {
    node temp = new node();
    temp.key = item;
    temp.left = temp.right = null;
    return temp;
  }

  // A utility function to
  // do inorder traversal of BST
  static void inorder(node root)
  {
    if (root != null)
    {
      inorder(root.left);
      System.out.print(root.key + " ");
      inorder(root.right);
    }
  }

  // reverse tree path using queue
  static void reversePath(node node)
  {

    /* If the tree is empty,
        return a new node */
    if (node == null)
      return;

    // If the node key equal
    // to key then
    if ((node).key == k)
    {

      // push current node key
      q1.add((node).key);

      // replace first node
      // with last element
      (node).key = q1.peek();

      // remove first element
      q1.remove();

      // return
      return;
    }

    // if key smaller than node key then
    else if (k < (node).key)
    {

      // push node key into queue
      q1.add((node).key);

      // recursive call itself
      reversePath((node).left);

      // replace queue front to node key
      (node).key = q1.peek();

      // performe pop in queue
      q1.remove();
    }

    // if key greater than node key then
    else if (k > (node).key)
    {

      // push node key into queue
      q1.add((node).key);

      // recursive call itself
      reversePath((node).right);

      // replace queue front to node key
      (node).key = q1.peek();

      // performe pop in queue
      q1.remove();
    }

    // return
    return;
  }

  /* A utility function to insert
    a new node with given key in BST */
  static node insert(node node, int key)
  {

    /* If the tree is empty,
        return a new node */
    if (node == null)
      return newNode(key);

    /* Otherwise, recur down the tree */
    if (key < node.key)
      node.left = insert(node.left, key);
    else if (key > node.key)
      node.right = insert(node.right, key);

    /* return the (unchanged) node pointer */
    return node;
  }

  // Driver code
  public static void main(String[] args)
  {

    /* Let us create following BST
                  50
               /     \
              30      70
             /  \    /  \
           20   40  60   80 */
    q1 = new LinkedList<>();

    // reverse path till k
    k = 80;
    root = insert(root, 50);
    root = insert(root, 30);
    root = insert(root, 20);
    root = insert(root, 40);
    root = insert(root, 70);
    root = insert(root, 60);
    root = insert(root, 80);
    System.out.print("Before Reverse :"
                     + "\n");
    // print inorder traversal of the BST
    inorder(root);
    System.out.print("\n");

    // reverse path till k
    reversePath(root);
    System.out.print("After Reverse :"
                     + "\n");

    // print inorder of reverse path tree
    inorder(root);
  }
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python3 code to demonstrate insert
# operation in binary search tree
class Node:

    # Constructor to create a new node
    def __init__(self, data):
        self.key = data
        self.left = None
        self.right = None

# A utility function to
# do inorder traversal of BST
def inorder(root):
    if root != None:
        inorder(root.left)
        print(root.key, end = " ")
        inorder(root.right)

# reverse tree path using queue
def reversePath(node, key, q1):

    # If the tree is empty,
    # return a new node */
    if node == None:
        return

    # If the node key equal
    # to key then
    if node.key == key:

        # push current node key
        q1.insert(0, node.key)

        # replace first node
        # with last element
        node.key = q1[-1]

        # remove first element
        q1.pop()

        # return
        return

    # if key smaller than node key then
    elif key < node.key:

        # push node key into queue
        q1.insert(0, node.key)

        # recursive call itself
        reversePath(node.left, key, q1)

        # replace queue front to node key
        node.key = q1[-1]

        # performe pop in queue
        q1.pop()

    # if key greater than node key then
    elif (key > node.key):

        # push node key into queue
        q1.insert(0, node.key)

        # recursive call itself
        reversePath(node.right, key, q1)

        # replace queue front to node key
        node.key = q1[-1]

        # performe pop in queue
        q1.pop()

    # return
    return

# A utility function to insert
#a new node with given key in BST */
def insert(node, key):

    # If the tree is empty,
    # return a new node */
    if node == None:
        return Node(key)

    # Otherwise, recur down the tree */
    if key < node.key:
        node.left = insert(node.left, key)
    elif key > node.key:
        node.right = insert(node.right, key)

    # return the (unchanged) node pointer */
    return node

# Driver Code
if __name__ == '__main__':

    # Let us create following BST
    #             50
    #         /     \
    #         30     70
    #         / \ / \
    #     20 40 60 80 */
    root = None
    q1 = []

    # reverse path till k
    k = 80;
    root = insert(root, 50)
    insert(root, 30)
    insert(root, 20)
    insert(root, 40)
    insert(root, 70)
    insert(root, 60)
    insert(root, 80)

    print("Before Reverse :")

    # print inorder traversal of the BST
    inorder(root)

    # reverse path till k
    reversePath(root, k, q1)
    print()
    print("After Reverse :")

    # print inorder of reverse path tree
    inorder(root)    

# This code is contributed by PranchalK
```

## C#

```
// C# code to demonstrate insert
// operation in binary search tree
using System;
using System.Collections.Generic;

class GFG{

public class node
{
    public int key;
    public node left, right;
};

static node root = null;
static Queue<int> q1;
static int k;

// A utility function to
// create a new BST node
static node newNode(int item)
{
    node temp = new node();
    temp.key = item;
    temp.left = temp.right = null;
    return temp;
}

// A utility function to
// do inorder traversal of BST
static void inorder(node root)
{
    if (root != null)
    {
        inorder(root.left);
        Console.Write(root.key + " ");
        inorder(root.right);
    }
}

// Reverse tree path using queue
static void reversePath(node node)
{

    // If the tree is empty,
    // return a new node
    if (node == null)
        return;

    // If the node key equal
    // to key then
    if ((node).key == k)
    {

        // push current node key
        q1.Enqueue((node).key);

        // replace first node
        // with last element
        (node).key = q1.Peek();

        // Remove first element
        q1.Dequeue();

        // Return
        return;
    }

    // If key smaller than node key then
    else if (k < (node).key)
    {

        // push node key into queue
        q1.Enqueue((node).key);

        // Recursive call itself
        reversePath((node).left);

        // Replace queue front to node key
        (node).key = q1.Peek();

        // Performe pop in queue
        q1.Dequeue();
    }

    // If key greater than node key then
    else if (k > (node).key)
    {

        // push node key into queue
        q1.Enqueue((node).key);

        // Recursive call itself
        reversePath((node).right);

        // Replace queue front to node key
        (node).key = q1.Peek();

        // Performe pop in queue
        q1.Dequeue();
    }

    // Return
    return;
}

// A utility function to insert
// a new node with given key in BST
static node insert(node node, int key)
{

    // If the tree is empty,
    // return a new node
    if (node == null)
        return newNode(key);

    // Otherwise, recur down the tree
    if (key < node.key)
        node.left = insert(node.left, key);
    else if (key > node.key)
        node.right = insert(node.right, key);

    // Return the (unchanged) node pointer
    return node;
}

// Driver code
public static void Main(String[] args)
{

    /* Let us create following BST
          50
       /     \
      30      70
     /  \    /  \
    20   40  60   80 */
    q1 = new Queue<int>();

    // Reverse path till k
    k = 80;
    root = insert(root, 50);
    root = insert(root, 30);
    root = insert(root, 20);
    root = insert(root, 40);
    root = insert(root, 70);
    root = insert(root, 60);
    root = insert(root, 80);
    Console.Write("Before Reverse :" + "\n");

    // Print inorder traversal of the BST
    inorder(root);
    Console.Write("\n");

    // Reverse path till k
    reversePath(root);
    Console.Write("After Reverse :" + "\n");

    // Print inorder of reverse path tree
    inorder(root);
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>

// javascript code to demonstrate insert
// operation in binary search tree

class node
{
    constructor()
    {
        this.key = 0;
        this.left = null;
        this.right = null;
    }
};

var root = null;
var q1 = [];
var k = 0;

// A utility function to
// create a new BST node
function newNode(item)
{
    var temp = new node();
    temp.key = item;
    temp.left = temp.right = null;
    return temp;
}

// A utility function to
// do inorder traversal of BST
function inorder(root)
{
    if (root != null)
    {
        inorder(root.left);
        document.write(root.key + " ");
        inorder(root.right);
    }
}

// Reverse tree path using queue
function reversePath(node)
{

    // If the tree is empty,
    // return a new node
    if (node == null)
        return;

    // If the node key equal
    // to key then
    if ((node).key == k)
    {

        // push current node key
        q1.push((node).key);

        // replace first node
        // with last element
        (node).key = q1[0];

        // Remove first element
        q1.shift();

        // Return
        return;
    }

    // If key smaller than node key then
    else if (k < (node).key)
    {

        // push node key into queue
        q1.push((node).key);

        // Recursive call itself
        reversePath((node).left);

        // Replace queue front to node key
        (node).key = q1[0];

        // Performe pop in queue
        q1.shift();
    }

    // If key greater than node key then
    else if (k > (node).key)
    {

        // push node key into queue
        q1.push((node).key);

        // Recursive call itself
        reversePath((node).right);

        // Replace queue front to node key
        (node).key = q1[0];

        // Performe pop in queue
        q1.shift();
    }

    // Return
    return;
}

// A utility function to insert
// a new node with given key in BST
function insert(node, key)
{

    // If the tree is empty,
    // return a new node
    if (node == null)
        return newNode(key);

    // Otherwise, recur down the tree
    if (key < node.key)
        node.left = insert(node.left, key);
    else if (key > node.key)
        node.right = insert(node.right, key);

    // Return the (unchanged) node pointer
    return node;
}

// Driver code

/* Let us create following BST
      50
   /     \
  30      70
 /  \    /  \
20   40  60   80 */
q1 = [];

// Reverse path till k
k = 80;
root = insert(root, 50);
root = insert(root, 30);
root = insert(root, 20);
root = insert(root, 40);
root = insert(root, 70);
root = insert(root, 60);
root = insert(root, 80);
document.write("Before Reverse :" + "<br>");

// Print inorder traversal of the BST
inorder(root);
document.write("<br>");

// Reverse path till k
reversePath(root);
document.write("After Reverse :" + "<br>");

// Print inorder of reverse path tree
inorder(root);

// This code is contributed by itsok.
</script>
```

**Output:** 

```
Before Reverse :
20 30 40 50 60 70 80 
After Reverse :
20 30 40 80 60 70 50
```