# 检查所有叶子是否在同一水平

> 原文:[https://www.geeksforgeeks.org/check-leaves-level/](https://www.geeksforgeeks.org/check-leaves-level/)

给定一棵二叉树，检查所有的叶子是否在同一水平。

```
          12
        /    \
      5       7       
    /          \ 
   3            1
  Leaves are at same level

          12
        /    \
      5       7       
    /          
   3          
   Leaves are Not at same level

          12
        /    
      5             
    /   \        
   3     9
  /      /
 1      2
 Leaves are at same level

```

**方法 1(递归)**

想法是首先找到最左边叶子的级别，并将其存储在变量 leafLevel 中。然后将所有其他叶子的级别与 leafLevel 进行比较，如果相同，则返回 true，否则返回 false。我们以预先排序的方式遍历给定的二叉树。leaflevel 参数传递给所有调用。leafLevel 的值被初始化为 0，表示还没有看到第一片叶子。当我们找到第一片叶子时，这个值就会更新。后续叶片的等级(按预定顺序)与叶片等级进行比较。

## C++

```
// C++ program to check if all leaves
// are at same level
#include <bits/stdc++.h>
using namespace std;

// A binary tree node
struct Node
{
    int data;
    struct Node *left, *right;
};

// A utility function to allocate
// a new tree node
struct Node* newNode(int data)
{
    struct Node* node = (struct Node*) malloc(sizeof(struct Node));
    node->data = data;
    node->left = node->right = NULL;
    return node;
}

/* Recursive function which checks whether
all leaves are at same level */
bool checkUtil(struct Node *root,
            int level, int *leafLevel)
{
    // Base case
    if (root == NULL) return true;

    // If a leaf node is encountered
    if (root->left == NULL &&
        root->right == NULL)
    {
        // When a leaf node is found
        // first time
        if (*leafLevel == 0)
        {
            *leafLevel = level; // Set first found leaf's level
            return true;
        }

        // If this is not first leaf node, compare
        // its level with first leaf's level
        return (level == *leafLevel);
    }

    // If this node is not leaf, recursively
    // check left and right subtrees
    return checkUtil(root->left, level + 1, leafLevel) &&
            checkUtil(root->right, level + 1, leafLevel);
}

/* The main function to check
if all leafs are at same level.
It mainly uses checkUtil() */
bool check(struct Node *root)
{
    int level = 0, leafLevel = 0;
    return checkUtil(root, level, &leafLevel);
}

// Driver Code
int main()
{
    // Let us create tree shown in third example
    struct Node *root = newNode(12);
    root->left = newNode(5);
    root->left->left = newNode(3);
    root->left->right = newNode(9);
    root->left->left->left = newNode(1);
    root->left->right->left = newNode(1);
    if (check(root))
        cout << "Leaves are at same level\n";
    else
        cout << "Leaves are not at same level\n";
    getchar();
    return 0;
}

// This code is contributed
// by Akanksha Rai
```

## C

```
// C program to check if all leaves are at same level
#include <stdio.h>
#include <stdlib.h>

// A binary tree node
struct Node
{
    int data;
    struct Node *left, *right;
};

// A utility function to allocate a new tree node
struct Node* newNode(int data)
{
    struct Node* node = (struct Node*) malloc(sizeof(struct Node));
    node->data = data;
    node->left = node->right = NULL;
    return node;
}

/* Recursive function which checks whether all leaves are at same level */
bool checkUtil(struct Node *root, int level, int *leafLevel)
{
    // Base case
    if (root == NULL)  return true;

    // If a leaf node is encountered
    if (root->left == NULL && root->right == NULL)
    {
        // When a leaf node is found first time
        if (*leafLevel == 0)
        {
            *leafLevel = level; // Set first found leaf's level
            return true;
        }

        // If this is not first leaf node, compare its level with
        // first leaf's level
        return (level == *leafLevel);
    }

    // If this node is not leaf, recursively check left and right subtrees
    return checkUtil(root->left, level+1, leafLevel) &&
           checkUtil(root->right, level+1, leafLevel);
}

/* The main function to check if all leafs are at same level.
   It mainly uses checkUtil() */
bool check(struct Node *root)
{
   int level = 0, leafLevel = 0;
   return checkUtil(root, level, &leafLevel);
}

// Driver program to test above function
int main()
{
    // Let us create tree shown in thirdt example
    struct Node *root = newNode(12);
    root->left = newNode(5);
    root->left->left = newNode(3);
    root->left->right = newNode(9);
    root->left->left->left = newNode(1);
    root->left->right->left = newNode(1);
    if (check(root))
        printf("Leaves are at same level\n");
    else
        printf("Leaves are not at same level\n");
    getchar();
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if all leaves are at same level

// A binary tree node
class Node
{
    int data;
    Node left, right;

    Node(int item)
    {
        data = item;
        left = right = null;
    }
}

class Leaf
{
    int leaflevel=0;
}

class BinaryTree
{
    Node root;
    Leaf mylevel = new Leaf();

    /* Recursive function which checks whether all leaves are at same
       level */
    boolean checkUtil(Node node, int level, Leaf leafLevel)
    {
        // Base case
        if (node == null)
            return true;

        // If a leaf node is encountered
        if (node.left == null && node.right == null)
        {
            // When a leaf node is found first time
            if (leafLevel.leaflevel == 0)
            {
                // Set first found leaf's level
                leafLevel.leaflevel = level;
                return true;
            }

            // If this is not first leaf node, compare its level with
            // first leaf's level
            return (level == leafLevel.leaflevel);
        }

        // If this node is not leaf, recursively check left and right
        // subtrees
        return checkUtil(node.left, level + 1, leafLevel)
                && checkUtil(node.right, level + 1, leafLevel);
    }

    /* The main function to check if all leafs are at same level.
       It mainly uses checkUtil() */
    boolean check(Node node)
    {
        int level = 0;
        return checkUtil(node, level, mylevel);
    }

    public static void main(String args[])
    {
        // Let us create the tree as shown in the example
        BinaryTree tree = new BinaryTree();
        tree.root = new Node(12);
        tree.root.left = new Node(5);
        tree.root.left.left = new Node(3);
        tree.root.left.right = new Node(9);
        tree.root.left.left.left = new Node(1);
        tree.root.left.right.left = new Node(1);
        if (tree.check(tree.root))
            System.out.println("Leaves are at same level");
        else
            System.out.println("Leaves are not at same level");
    }
}

// This code has been contributed by Mayank Jaiswal
```

## 计算机编程语言

```
# Python program to check if all leaves are at same level

# A binary tree node
class Node:

    # Constructor to create a new node
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# Recursive function which check whether all leaves are at
# same level
def checkUtil(root, level):

    # Base Case
    if root is None:
        return True

    # If a tree node is encountered
    if root.left is None and root.right is None:

        # When a leaf node is found first time
        if check.leafLevel == 0 :
            check.leafLevel = level # Set first leaf found
            return True

        # If this is not first leaf node, compare its level
        # with first leaf's level
        return level == check.leafLevel

    # If this is not first leaf node, compare its level
    # with first leaf's level
    return (checkUtil(root.left, level+1)and
            checkUtil(root.right, level+1))

def check(root):
    level = 0
    check.leafLevel = 0
    return (checkUtil(root, level))

# Driver program to test above function
root = Node(12)
root.left = Node(5)
root.left.left = Node(3)
root.left.right = Node(9)
root.left.left.left = Node(1)
root.left.right.left = Node(2)

if(check(root)):
    print "Leaves are at same level"
else:
    print "Leaves are not at same level"

# This code is contributed by Nikhil Kumar Singh(nickzuck_007)
```

## C#

```
// C# program to check if all leaves
// are at same level
using System;

// A binary tree node
public class Node
{
    public int data;
    public Node left, right;

    public Node(int item)
    {
        data = item;
        left = right = null;
    }
}

public class Leaf
{
    public int leaflevel = 0;
}

class GFG
{
public Node root;
public Leaf mylevel = new Leaf();

/* Recursive function which checks
whether all leaves are at same level */
public virtual bool checkUtil(Node node, int level,
                              Leaf leafLevel)
{
    // Base case
    if (node == null)
    {
        return true;
    }

    // If a leaf node is encountered
    if (node.left == null && node.right == null)
    {
        // When a leaf node is found first time
        if (leafLevel.leaflevel == 0)
        {
            // Set first found leaf's level
            leafLevel.leaflevel = level;
            return true;
        }

        // If this is not first leaf node,
        // compare its level with first leaf's level
        return (level == leafLevel.leaflevel);
    }

    // If this node is not leaf, recursively
    // check left and right subtrees
    return checkUtil(node.left, level + 1, leafLevel) &&
           checkUtil(node.right, level + 1, leafLevel);
}

/* The main function to check if all leafs
are at same level. It mainly uses checkUtil() */
public virtual bool check(Node node)
{
    int level = 0;
    return checkUtil(node, level, mylevel);
}

// Driver Code
public static void Main(string[] args)
{
    // Let us create the tree as shown in the example
    GFG tree = new GFG();
    tree.root = new Node(12);
    tree.root.left = new Node(5);
    tree.root.left.left = new Node(3);
    tree.root.left.right = new Node(9);
    tree.root.left.left.left = new Node(1);
    tree.root.left.right.left = new Node(1);
    if (tree.check(tree.root))
    {
        Console.WriteLine("Leaves are at same level");
    }
    else
    {
        Console.WriteLine("Leaves are not at same level");
    }
}
}

// This code is contributed by Shrikant13
```

## java 描述语言

```
<script>

// Javascript program to check if all
// leaves are at same level

// A binary tree node
class Node
{
    constructor(item)
    {
        this.data = item;
        this.left = this.right = null;
    }
}
class Leaf
{
    leaflevel = 0;
}

let root;
let mylevel = new Leaf();

// Recursive function which checks
// whether all leaves are at same level
function checkUtil(node, level, leafLevel)
{

    // Base case
    if (node == null)
        return true;

    // If a leaf node is encountered
    if (node.left == null && node.right == null)
    {

        // When a leaf node is found first time
        if (leafLevel.leaflevel == 0)
        {

            // Set first found leaf's level
            leafLevel.leaflevel = level;
            return true;
        }

        // If this is not first leaf node,
        // compare its level with first leaf's level
        return (level == leafLevel.leaflevel);
    }

    // If this node is not leaf, recursively
    // check left and right subtrees
    return checkUtil(node.left, level + 1, leafLevel) &&
           checkUtil(node.right, level + 1, leafLevel);
}

// The main function to check if all
// leafs are at same level. It mainly
// uses checkUtil()
function check(node)
{
    let level = 0;
    return checkUtil(node, level, mylevel);
}

// Driver code

// Let us create the tree as shown in the example
root = new Node(12);
root.left = new Node(5);
root.left.left = new Node(3);
root.left.right = new Node(9);
root.left.left.left = new Node(1);
root.left.right.left = new Node(1);

if (check(root))
    document.write("Leaves are at same level");
else
    document.write("Leaves are not at same level");

// This code is contributed by rag2127

</script>
```

**输出:**

```
Leaves are at same level
```

**时间复杂度:**函数对树做简单遍历，所以复杂度为 O(n)。
T3】

**方法 2(迭代)**

它也可以通过迭代的方法来解决。
思想是迭代遍历树，当遇到第一个叶节点时，将其级别存储在结果变量中，现在每当遇到任何一个叶节点时，将其级别与之前存储的结果进行比较，它们是相同的，然后对树的其余部分进行处理，否则返回 false。

## C++

```
// C++ program to check if all leaf nodes are at
// same level of binary tree
#include <bits/stdc++.h>
using namespace std;

// tree node
struct Node {
    int data;
    Node *left, *right;
};

// returns a new tree Node
Node* newNode(int data)
{
    Node* temp = new Node();
    temp->data = data;
    temp->left = temp->right = NULL;
    return temp;
}

// return true if all leaf nodes are
// at same level, else false
int checkLevelLeafNode(Node* root)
{
    if (!root)
        return 1;

    // create a queue for level order traversal
    queue<Node*> q;
    q.push(root);

    int result = INT_MAX;
     int level = 0;

    // traverse until the queue is empty
    while (!q.empty()) {
        int size = q.size();
        level += 1;

        // traverse for complete level
        while(size > 0){
            Node* temp = q.front();
            q.pop();

            // check for left child
            if (temp->left) {
                q.push(temp->left);

                // if its leaf node
                if(!temp->left->right && !temp->left->left){

                    // if it's first leaf node, then update result
                    if (result == INT_MAX)
                        result = level;

                    // if it's not first leaf node, then compare
                    // the level with level of previous leaf node
                    else if (result != level)
                        return 0;                   
                }
            }

             // check for right child
            if (temp->right){
                q.push(temp->right);

                // if it's leaf node
                if (!temp->right->left && !temp->right->right)

                    // if it's first leaf node till now,
                    // then update the result
                    if (result == INT_MAX)
                        result = level;

                    // if it is not the first leaf node,
                    // then compare the level with level
                    // of previous leaf node
                    else if(result != level)
                        return 0;

               }
               size -= 1;
        }   
    }

    return 1;
}

// driver program
int main()
{
    // construct a tree
    Node* root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->right = newNode(4);
    root->right->left = newNode(5);
    root->right->right = newNode(6);

    int result = checkLevelLeafNode(root);
    if (result)
        cout << "All leaf nodes are at same level\n";
    else
        cout << "Leaf nodes not at same level\n";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if all leaf nodes are at 
// same level of binary tree
import java.util.*;

// User defined node class
class Node {
      int data;
      Node left, right;

      // Constructor to create a new tree node
      Node(int key) {
           int data = key;
           left = right = null;
      }
}

class GFG {

      // return true if all leaf nodes are
      // at same level, else false
      static boolean checkLevelLeafNode(Node root)
      {
             if (root == null)
                 return true;

             // create a queue for level order traversal
             Queue<Node> q = new LinkedList<>();
             q.add(root);

             int result = Integer.MAX_VALUE;
             int level = 0;

             // traverse until the queue is empty
             while (q.size() != 0) {
                    int size = q.size();
                    level++;

                    // traverse for complete level
                    while (size > 0) {
                         Node temp = q.remove();

                         // check for left child
                         if (temp.left != null) {
                             q.add(temp.left);

                              // if its leaf node
                              if (temp.left.left == null && temp.left.right == null) {

                                  // if it's first leaf node, then update result
                                  if (result == Integer.MAX_VALUE)
                                      result = level;

                                  // if it's not first leaf node, then compare 
                                  // the level with level of previous leaf node.
                                  else if (result != level)
                                       return false;
                              }
                         }

                          // check for right child
                          if (temp.right != null) {
                             q.add(temp.right);

                              // if its leaf node
                             if (temp.right.left == null && temp.right.right == null) {

                                  // if it's first leaf node, then update result
                                  if (result == Integer.MAX_VALUE)
                                      result = level;

                                  // if it's not first leaf node, then compare 
                                  // the level with level of previous leaf node.
                                  else if (result != level)
                                       return false;
                              }
                         }
                         size--;
                    }

             }
             return true;
      }

      // Driver code
      public static void main(String args[])
      {
             // construct a tree
             Node root = new Node(1);
             root.left = new Node(2);
             root.right = new Node(3);
             root.left.right = new Node(4);
             root.right.left = new Node(5);
             root.right.right = new Node(6);

             boolean result = checkLevelLeafNode(root);
             if (result == true)
                 System.out.println("All leaf nodes are at same level");
             else
                 System.out.println("Leaf nodes not at same level"); 
      }
}
// This code is contributed by rachana soma
```

## 蟒蛇 3

```
# Python3 program to check if all leaf nodes
# are at same level of binary tree
INT_MAX = 2**31
INT_MIN = -2**31

# Tree Node
# returns a new tree Node
class newNode:
    def __init__(self, data):
        self.data = data
        self.left = self.right = None

# return true if all leaf nodes are
# at same level, else false
def checkLevelLeafNode(root) :

    if (not root) :
        return 1

    # create a queue for level
    # order traversal
    q = []
    q.append(root)

    result = INT_MAX
    level = 0

    # traverse until the queue is empty
    while (len(q)):
        size = len(q)
        level += 1

        # traverse for complete level
        while(size > 0 or len(q)):
            temp = q[0]
            q.pop(0)

            # check for left child
            if (temp.left) :
                q.append(temp.left)

                # if its leaf node
                if(not temp.left.right and
                   not temp.left.left):

                    # if it's first leaf node,
                    # then update result
                    if (result == INT_MAX):
                        result = level

                    # if it's not first leaf node,
                    # then compare the level with
                    # level of previous leaf node
                    elif (result != level):
                        return 0                   

            # check for right child
            if (temp.right) :
                q.append(temp.right)

                # if it's leaf node
                if (not temp.right.left and
                    not temp.right.right):

                    # if it's first leaf node till now,
                    # then update the result
                    if (result == INT_MAX):
                        result = level

                    # if it is not the first leaf node,
                    # then compare the level with level
                    # of previous leaf node
                    elif(result != level):
                        return 0
                size -= 1
    return 1

# Driver Code
if __name__ == '__main__':

    # construct a tree
    root = newNode(1)
    root.left = newNode(2)
    root.right = newNode(3)
    root.left.right = newNode(4)
    root.right.left = newNode(5)
    root.right.right = newNode(6)

    result = checkLevelLeafNode(root)
    if (result) :
        print("All leaf nodes are at same level")
    else:
        print("Leaf nodes not at same level")

# This code is contributed by SHUBHAMSINGH10
```

## C#

```
// C# program to check if all leaf nodes are at
// same level of binary tree
using System;
using System.Collections.Generic;

// User defined node class
public class Node
{
    public int data;
    public Node left, right;

    // Constructor to create a new tree node
    public Node(int key)
    {
        int data = key;
        left = right = null;
    }
}

public class GFG
{

    // return true if all leaf nodes are
    // at same level, else false
    static bool checkLevelLeafNode(Node root)
    {
            if (root == null)
                return true;

            // create a queue for level order traversal
            Queue<Node> q = new Queue<Node>();
            q.Enqueue(root);

            int result = int.MaxValue;
            int level = 0;

            // traverse until the queue is empty
            while (q.Count != 0)
            {
                    int size = q.Count;
                    level++;

                    // traverse for complete level
                    while (size > 0)
                    {
                        Node temp = q.Dequeue();

                        // check for left child
                        if (temp.left != null)
                        {
                            q.Enqueue(temp.left);

                            // if its leaf node
                            if (temp.left.left != null &&
                                temp.left.right != null)
                            {

                                // if it's first leaf node, then update result
                                if (result == int.MaxValue)
                                    result = level;

                                // if it's not first leaf node, then compare
                                // the level with level of previous leaf node.
                                else if (result != level)
                                    return false;
                            }
                        }

                        // check for right child
                        if (temp.right != null)
                        {
                            q.Enqueue(temp.right);

                            // if its leaf node
                            if (temp.right.left != null &&
                                temp.right.right != null)
                            {

                                // if it's first leaf node, then update result
                                if (result == int.MaxValue)
                                    result = level;

                                // if it's not first leaf node, then compare
                                // the level with level of previous leaf node.
                                else if (result != level)
                                    return false;
                            }
                        }
                        size--;
                    }
            }
            return true;
    }

    // Driver code
    public static void Main(String []args)
    {
        // construct a tree
        Node root = new Node(1);
        root.left = new Node(2);
        root.right = new Node(3);
        root.left.right = new Node(4);
        root.right.left = new Node(5);
        root.right.right = new Node(6);

        bool result = checkLevelLeafNode(root);
        if (result == true)
            Console.WriteLine("All leaf nodes are at same level");
        else
            Console.WriteLine("Leaf nodes not at same level");
    }
}

// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program to check if all
// leaf nodes are at same level of binary tree

// User defined node class
class Node
{

    // Constructor to create a new tree node
    constructor(key)
    {
        this.data = key;
        this.left = this.right = null;
    }
}

// Return true if all leaf nodes are
// at same level, else false
function checkLevelLeafNode(root)
{
    if (root == null)
     return true;

    // Create a queue for level
    // order traversal
    let q = [];
    q.push(root);

    let result = Number.MAX_VALUE;
    let level = 0;

    // Traverse until the queue is empty
    while (q.length != 0)
    {
        let size = q.length;
        level++;

        // traverse for complete level
        while (size > 0)
        {
            let temp = q.shift();

            // check for left child
            if (temp.left != null)
            {
                q.push(temp.left);

                // if its leaf node
                if (temp.left.left == null &&
                    temp.left.right == null)
                {

                    // If it's first leaf node,
                    // then update result
                    if (result == Number.MAX_VALUE)
                        result = level;

                    // If it's not first leaf node,
                    // then compare the level with
                    // level of previous leaf node.
                    else if (result != level)
                        return false;
                }
            }

            // Check for right child
            if (temp.right != null)
            {
                q.push(temp.right);

                // If its leaf node
                if (temp.right.left == null &&
                    temp.right.right == null)
                {

                    // If it's first leaf node, then
                    // update result
                    if (result == Number.MAX_VALUE)
                        result = level;

                    // If it's not first leaf node,
                    // then compare the level with
                    // level of previous leaf node.
                    else if (result != level)
                        return false;
                }
            }
            size--;
        }
    }
    return true;
}

// Driver code

// construct a tree
let root = new Node(1);
root.left = new Node(2);
root.right = new Node(3);
root.left.right = new Node(4);
root.right.left = new Node(5);
root.right.right = new Node(6);

let result = checkLevelLeafNode(root);
if (result == true)
    document.write("All leaf nodes are at same level");
else
    document.write("Leaf nodes not at same level");

// This code is contributed by avanitrachhadiya2155

</script>
```

**输出:**

```
All leaf nodes are at same level
```

**时间复杂度:** O(n)
本代码由**–**[**曼德普·辛格**](https://github.com/msdeep14)
贡献

本文由 [**钱德拉·普拉卡什**](https://www.facebook.com/chandra.prakash.52643?fref=ts) 供稿。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。