# 使用 STL 集的二叉树到二叉查找树的转换

> 原文:[https://www . geesforgeks . org/binary-tree-binary-search-tree-conversion-use-STL-set/](https://www.geeksforgeeks.org/binary-tree-binary-search-tree-conversion-using-stl-set/)

给定一个二叉树，将其转换成一个[二叉查找树](https://www.geeksforgeeks.org/binary-search-tree-set-1-search-and-insertion/)。转换必须以保持二叉树原始结构的方式进行。
这个解决方案将使用[套 C++ STL](https://www.geeksforgeeks.org/set-in-cpp-stl/) 代替基于数组的解决方案。
**示例:**

```
Example 1
Input:
          10
         /  \
        2    7
       / \
      8   4
Output:
          8
         /  \
        4    10
       / \
      2   7

Example 2
Input:
          10
         /  \
        30   15
       /      \
      20       5
Output:
          15
         /  \
       10    20
       /      \
      5        30
```

**解决方案**

1.  在进行有序遍历时，将二叉树的项目复制到**集合**中。这需要 0(n 对 n)的时间。请注意，C++ STL 中的 set 是使用自平衡二叉查找树实现的，如[红黑树](https://www.geeksforgeeks.org/red-black-tree-set-1-introduction-2/)、 [AVL 树](https://www.geeksforgeeks.org/avl-tree-set-1-insertion/)等
2.  不需要对集合进行排序，因为 C++中的**集合**是使用自平衡二分搜索法树实现的，因此插入、搜索、删除等每个操作都需要 O(log n)个时间。
3.  现在简单地将**设置**的项目从开始一个接一个地复制到树上，同时遍历树。需要注意的是，当从开始处复制**集合**的每一项时，我们首先在进行有序遍历时将其复制到树中，然后将其从集合中移除。

现在上面的解决方案比这里解释的基于数组的二叉树到二叉查找树的转换更简单，更容易实现- [二叉树到二叉查找树(Set-1)](https://www.geeksforgeeks.org/binary-tree-to-binary-search-tree-conversion/) 的转换，这里我们要单独做一个函数，把项从树复制到数组后，对数组的项进行排序。
使用集合将二叉树转换成二叉查找树的程序。

## C++

```
/* CPP program to convert a Binary tree to BST
   using sets as containers. */
#include <bits/stdc++.h>
using namespace std;

struct Node {
    int data;
    struct Node *left, *right;
};

// function to store the nodes in set while
// doing inorder traversal.
void storeinorderInSet(Node* root, set<int>& s)
{
    if (!root)
        return;

    // visit the left subtree first
    storeinorderInSet(root->left, s);

    // insertion takes order of O(logn) for sets
    s.insert(root->data);

    // visit the right subtree
    storeinorderInSet(root->right, s);

} // Time complexity  = O(nlogn)

// function to copy items of set one by one
// to the tree while doing inorder traversal
void setToBST(set<int>& s, Node* root)
{
    // base condition
    if (!root)
        return;

    // first move to the left subtree and
    // update items
    setToBST(s, root->left);

    // iterator initially pointing to the
    // beginning of set
    auto it = s.begin();

    // copying the item at beginning of
    // set(sorted) to the tree.
    root->data = *it;

    // now erasing the beginning item from set.
    s.erase(it);

    // now move to right subtree and update items
    setToBST(s, root->right);

} // T(n) = O(nlogn) time

// Converts Binary tree to BST.
void binaryTreeToBST(Node* root)
{
    set<int> s;

    // populating the set with the tree's
    // inorder traversal data
    storeinorderInSet(root, s);

    // now sets are by default sorted as
    // they are implemented using self-
    // balancing BST

    // copying items from set to the tree
    // while inorder traversal which makes a BST
    setToBST(s, root);

} // Time complexity  =  O(nlogn),
  // Auxiliary Space = O(n) for set.

// helper function to create a node
Node* newNode(int data)
{
    // dynamically allocating memory
    Node* temp = new Node();
    temp->data = data;
    temp->left = temp->right = NULL;
    return temp;
}

// function to do inorder traversal
void inorder(Node* root)
{
    if (!root)
        return;
    inorder(root->left);
    cout << root->data << " ";
    inorder(root->right);
}

int main()
{
    Node* root = newNode(5);
    root->left = newNode(7);
    root->right = newNode(9);
    root->right->left = newNode(10);
    root->left->left = newNode(1);
    root->left->right = newNode(6);
    root->right->right = newNode(11);

    /* Constructing tree given in the above figure
           5
         /   \
        7     9
       /\    / \
      1  6   10 11   */

    // converting the above Binary tree to BST
    binaryTreeToBST(root);
    cout << "Inorder traversal of BST is: " << endl;
    inorder(root);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/* Java program to convert a Binary tree to BST
using sets as containers. */
import java.util.*;

class Solution
{
static class Node
{
    int data;
    Node left, right;
}

// set
static Set<Integer> s = new HashSet<Integer>();

// function to store the nodes in set while
// doing inorder traversal.
static void storeinorderInSet(Node root)
{
    if (root == null)
        return;

    // visit the left subtree first
    storeinorderInSet(root.left);

    // insertion takes order of O(logn) for sets
    s.add(root.data);

    // visit the right subtree
    storeinorderInSet(root.right);

} // Time complexity = O(nlogn)

// function to copy items of set one by one
// to the tree while doing inorder traversal
static void setToBST( Node root)
{
    // base condition
    if (root == null)
        return;

    // first move to the left subtree and
    // update items
    setToBST( root.left);

    // iterator initially pointing to the
    // beginning of set
    // copying the item at beginning of
    // set(sorted) to the tree.
    root.data = s.iterator().next();

    // now erasing the beginning item from set.
    s.remove(root.data);

    // now move to right subtree and update items
    setToBST( root.right);

} // T(n) = O(nlogn) time

// Converts Binary tree to BST.
static void binaryTreeToBST(Node root)
{
    s.clear();

    // populating the set with the tree's
    // inorder traversal data
    storeinorderInSet(root);

    // now sets are by default sorted as
    // they are implemented using self-
    // balancing BST

    // copying items from set to the tree
    // while inorder traversal which makes a BST
    setToBST( root);

} // Time complexity = O(nlogn),
// Auxiliary Space = O(n) for set.

// helper function to create a node
static Node newNode(int data)
{
    // dynamically allocating memory
    Node temp = new Node();
    temp.data = data;
    temp.left = temp.right = null;
    return temp;
}

// function to do inorder traversal
static void inorder(Node root)
{
    if (root == null)
        return;
    inorder(root.left);
    System.out.print(root.data + " ");
    inorder(root.right);
}

// Driver code
public static void main(String args[])
{
    Node root = newNode(5);
    root.left = newNode(7);
    root.right = newNode(9);
    root.right.left = newNode(10);
    root.left.left = newNode(1);
    root.left.right = newNode(6);
    root.right.right = newNode(11);

    /* Constructing tree given in the above figure
        5
        / \
        7     9
    /\ / \
    1 6 10 11 */

    // converting the above Binary tree to BST
    binaryTreeToBST(root);
    System.out.println( "Inorder traversal of BST is: " );
    inorder(root);
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 program to convert a Binary tree
# to BST using sets as containers.

# Binary Tree Node
""" A utility function to create a
new BST node """
class newNode:

    # Construct to create a newNode
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# function to store the nodes in set
# while doing inorder traversal.
def storeinorderInSet(root, s):

    if (not root) :
        return

    # visit the left subtree first
    storeinorderInSet(root.left, s)

    # insertion takes order of O(logn)
    # for sets
    s.add(root.data)

    # visit the right subtree
    storeinorderInSet(root.right, s)

# Time complexity = O(nlogn)

# function to copy items of set one by one
# to the tree while doing inorder traversal
def setToBST(s, root) :

    # base condition
    if (not root):
        return

    # first move to the left subtree and
    # update items
    setToBST(s, root.left)

    # iterator initially pointing to
    # the beginning of set
    it = next(iter(s))

    # copying the item at beginning of
    # set(sorted) to the tree.
    root.data = it

    # now erasing the beginning item from set.
    s.remove(it)

    # now move to right subtree
    # and update items
    setToBST(s, root.right)

# T(n) = O(nlogn) time

# Converts Binary tree to BST.
def binaryTreeToBST(root):

    s = set()

    # populating the set with the tree's
    # inorder traversal data
    storeinorderInSet(root, s)

    # now sets are by default sorted as
    # they are implemented using self-
    # balancing BST

    # copying items from set to the tree
    # while inorder traversal which makes a BST
    setToBST(s, root)

# Time complexity = O(nlogn),
# Auxiliary Space = O(n) for set.

# function to do inorder traversal
def inorder(root) :

    if (not root) :
        return
    inorder(root.left)
    print(root.data, end = " ")
    inorder(root.right)

# Driver Code
if __name__ == '__main__':

    root = newNode(5)
    root.left = newNode(7)
    root.right = newNode(9)
    root.right.left = newNode(10)
    root.left.left = newNode(1)
    root.left.right = newNode(6)
    root.right.right = newNode(11)

    """ Constructing tree given in
        the above figure
        5
        / \
        7     9
    /\ / \
    1 6 10 11 """

    # converting the above Binary tree to BST
    binaryTreeToBST(root)
    print("Inorder traversal of BST is: ")
    inorder(root)

# This code is contributed by
# Shubham Singh(SHUBHAMSINGH10)
```

## C#

```
// C# program to convert
// a Binary tree to BST
using System;
using System.Collections;
using System.Collections.Generic;
using System.Linq;
class Solution{

class Node
{
  public int data;
  public Node left,
              right;
}

// set
static SortedSet<int> s =
       new SortedSet<int>();

// function to store the nodes
// in set while doing inorder
// traversal.
static void storeinorderInSet(Node root)
{
  if (root == null)
    return;

  // visit the left subtree
  // first
  storeinorderInSet(root.left);

  // insertion takes order of
  // O(logn) for sets
  s.Add(root.data);

  // visit the right subtree
  storeinorderInSet(root.right);

}

// Time complexity = O(nlogn)

// function to copy items of
// set one by one to the tree
// while doing inorder traversal
static void setToBST(Node root)
{
  // base condition
  if (root == null)
    return;

  // first move to the left
  // subtree and update items
  setToBST(root.left);

  // iterator initially pointing
  // to the beginning of set copying
  // the item at beginning of set(sorted)
  // to the tree.
  root.data = s.First();

  // now erasing the beginning item
  // from set.
  s.Remove(s.First());

  // now move to right subtree and
  // update items
  setToBST( root.right);
}

// T(n) = O(nlogn) time
 // Converts Binary tree to BST.
static void binaryTreeToBST(Node root)
{
  s.Clear();

  // populating the set with
  // the tree's inorder traversal
  // data
  storeinorderInSet(root);

  // now sets are by default sorted
  // as they are implemented using
  // self-balancing BST

  // copying items from set to the
  // tree while inorder traversal
  // which makes a BST
  setToBST( root);

}

// Time complexity = O(nlogn),
// Auxiliary Space = O(n) for set.

// helper function to create a node
static Node newNode(int data)
{
  // dynamically allocating
  // memory
  Node temp = new Node();
  temp.data = data;
  temp.left = temp.right = null;
  return temp;
}

// function to do inorder traversal
static void inorder(Node root)
{
  if (root == null)
    return;
  inorder(root.left);
  Console.Write(root.data + " ");
  inorder(root.right);
}

// Driver code
public static void Main(string []args)
{
  Node root = newNode(5);
  root.left = newNode(7);
  root.right = newNode(9);
  root.right.left = newNode(10);
  root.left.left = newNode(1);
  root.left.right = newNode(6);
  root.right.right = newNode(11);

  /* Constructing tree given in
  // the above figure
        5
        / \
        7     9
    /\ / \
    1 6 10 11 */

  // converting the above Binary
  // tree to BST
  binaryTreeToBST(root);
  Console.Write("Inorder traversal of " +
                "BST is: \n" );
  inorder(root);
}
}

// This code is contributed by Rutvik_56
```

## java 描述语言

```
<script>

// JavaScript program to convert
// a Binary tree to BST

class Node
{
  constructor()
  {
    this.data = 0;
    this.right = null;
    this.left = null;
  }
}

// set
var s = new Set();

// function to store the nodes
// in set while doing inorder
// traversal.
function storeinorderInSet(root)
{
  if (root == null)
    return;

  // visit the left subtree
  // first
  storeinorderInSet(root.left);

  // insertion takes order of
  // O(logn) for sets
  s.add(root.data);

  // visit the right subtree
  storeinorderInSet(root.right);

}

// Time complexity = O(nlogn)

// function to copy items of
// set one by one to the tree
// while doing inorder traversal
function setToBST(root)
{
  // base condition
  if (root == null)
    return;

  // first move to the left
  // subtree and update items
  setToBST(root.left);

  var tmp = [...s].sort((a,b)=> a-b);
  // iterator initially pointing
  // to the beginning of set copying
  // the item at beginning of set(sorted)
  // to the tree.
  root.data = tmp[0];

  // now erasing the beginning item
  // from set.
  s.delete(tmp[0]);

  // now move to right subtree and
  // update items
  setToBST( root.right);
}

// T(n) = O(nlogn) time
 // Converts Binary tree to BST.
function binaryTreeToBST(root)
{
  s = new Set();

  // populating the set with
  // the tree's inorder traversal
  // data
  storeinorderInSet(root);

  // now sets are by default sorted
  // as they are implemented using
  // self-balancing BST

  // copying items from set to the
  // tree while inorder traversal
  // which makes a BST
  setToBST( root);

}

// Time complexity = O(nlogn),
// Auxiliary Space = O(n) for set.

// helper function to create a node
function newNode(data)
{
  // dynamically allocating
  // memory
  var temp = new Node();
  temp.data = data;
  temp.left = temp.right = null;
  return temp;
}

// function to do inorder traversal
function inorder(root)
{
  if (root == null)
    return;
  inorder(root.left);
  document.write(root.data + " ");
  inorder(root.right);
}

// Driver code
var root = newNode(5);
root.left = newNode(7);
root.right = newNode(9);
root.right.left = newNode(10);
root.left.left = newNode(1);
root.left.right = newNode(6);
root.right.right = newNode(11);
/* Constructing tree given in
// the above figure
      5
      / \
      7     9
  /\ / \
  1 6 10 11 */
// converting the above Binary
// tree to BST
binaryTreeToBST(root);
document.write("Inorder traversal of " +
              "BST is: <br>" );
inorder(root);

</script>
```

**Output:** 

```
Inorder traversal of BST is: 
1 5 6 7 9 10 11
```

**时间复杂度:**O(n Log n)
T3】辅助空间: (n)