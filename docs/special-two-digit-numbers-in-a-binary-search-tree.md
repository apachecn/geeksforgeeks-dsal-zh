# 二叉查找树的特殊两位数

> 原文:[https://www . geesforgeks . org/special-二进制搜索树中的两位数/](https://www.geeksforgeeks.org/special-two-digit-numbers-in-a-binary-search-tree/)

给定一个二分搜索法树，任务是计算具有特殊两位数的节点数。
先决条件:[特殊两位数](https://www.geeksforgeeks.org/special-two-digit-number/) | [二叉查找树](https://www.geeksforgeeks.org/binary-search-tree-set-1-search-and-insertion/)

示例:

```
Input : 15 7 987 21
Output : 0

Input : 19 99 57 1 22
Output : 2
```

**算法:**用变量计数递归遍历树的每个节点，检查每个节点的数据是否有特殊的两位数。如果是，则递增变量计数。最后，返回计数。

## C++

```
// C++ program to count number of nodes in
// BST containing two digit special number
#include <bits/stdc++.h>
using namespace std;

// A Tree node
struct Node
{
    struct Node *left;
    int info;
    struct Node *right;
};

// Function to create a new node
void insert(struct Node **rt, int key)
{
    if(*rt == NULL)
    {
        (*rt) = new Node();
        (*rt) -> left = NULL;
        (*rt) -> right = NULL;
        (*rt) -> info = key;
    }
    else if(key < ((*rt) -> info))
        insert(&((*rt) -> left), key);
    else
        insert(&(*rt) -> right, key);
}

// Function to find if number
// is special or not
int check(int num)
{
    int sum = 0, i = num, sum_of_digits, prod_of_digits ;

    // Check if number is two digit or not
    if(num < 10 || num > 99)
        return 0;
    else
    {
        sum_of_digits = (i % 10) + (i / 10);
        prod_of_digits = (i % 10) * (i / 10);
        sum = sum_of_digits + prod_of_digits;
    }

    if(sum == num)
        return 1;
    else
        return 0;
}

// Function to count number of special two digit number
void countSpecialDigit(struct Node *rt, int *c)
{
    int x;
    if(rt == NULL)
        return;
    else
    {
        x = check(rt -> info);
        if(x == 1)
            *c = *c + 1;
        countSpecialDigit(rt -> left, c);
        countSpecialDigit(rt -> right, c);
    }
}

// Driver program to test
int main()
{
    struct Node *root = NULL;

    // Initialize result
    int count = 0;

    // Function call to insert() to insert nodes
    insert(&root, 50);
    insert(&root, 29);
    insert(&root, 59);
    insert(&root, 19);
    insert(&root, 53);
    insert(&root, 556);
    insert(&root, 56);
    insert(&root, 94);
    insert(&root, 13);

    // Function call, to check each node for
    // special two digit number
    countSpecialDigit(root, &count);
    cout<< count;

    return 0;
}

// This code is contributed by itsok.
```

## C

```
// C program to count number of nodes in
// BST containing two digit special number
#include <stdio.h>
#include <stdlib.h>

// A Tree node
struct Node
{
    struct Node *left;
    int info;
    struct Node *right;
};

// Function to create a new node
void insert(struct Node **rt, int key)
{
    if(*rt == NULL)
    {
        (*rt) = (struct Node *)malloc(sizeof(struct Node));
        (*rt) -> left = NULL;
        (*rt) -> right = NULL;
        (*rt) -> info = key;
    }
    else if(key < ((*rt) -> info))
        insert(&((*rt) -> left), key);
    else
        insert(&(*rt) -> right, key);
}

// Function to find if number
// is special or not
int check(int num)
{
    int sum = 0, i = num, sum_of_digits, prod_of_digits ;

    // Check if number is two digit or not
    if(num < 10 || num > 99)
        return 0;
    else
    {
        sum_of_digits = (i % 10) + (i / 10);
        prod_of_digits = (i % 10) * (i / 10);
        sum = sum_of_digits + prod_of_digits;
    }

    if(sum == num)
        return 1;
    else
        return 0;
}

// Function to count number of special two digit number
void countSpecialDigit(struct Node *rt, int *c)
{
    int x;
    if(rt == NULL)
        return;
    else
    {
        x = check(rt -> info);
        if(x == 1)
            *c = *c + 1;
        countSpecialDigit(rt -> left, c);
        countSpecialDigit(rt -> right, c);
    }
}

// Driver program to test
int main()
{
    struct Node *root = NULL;

    // Initialize result
    int count = 0;

    // Function call to insert() to insert nodes
    insert(&root, 50);
    insert(&root, 29);
    insert(&root, 59);
    insert(&root, 19);
    insert(&root, 53);
    insert(&root, 556);
    insert(&root, 56);
    insert(&root, 94);
    insert(&root, 13);

    // Function call, to check each node for
    // special two digit number
    countSpecialDigit(root, &count);
    printf("%d", count);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count number of nodes in
// BST containing two digit special number

// A binary tree node
class Node
{
    int info;
    Node left, right;

    Node(int d)
    {
        info = d;
        left = right = null;
    }
}

class BinaryTree{

static Node head;
static int count;

// Function to create a new node
Node insert(Node node, int info)
{

    // If the tree is empty, return a new,
    // single node
    if (node == null)
    {
        return (new Node(info));
    }
    else
    {

        // Otherwise, recur down the tree
        if (info <= node.info)
        {
            node.left = insert(node.left, info);
        }
        else
        {
            node.right = insert(node.right, info);
        }

        // return the (unchanged) node pointer
        return node;
    }
}

// Function to find if number
// is special or not
static int check(int num)
{
    int sum = 0, i = num,
        sum_of_digits,
        prod_of_digits;

    // Check if number is two digit or not
    if (num < 10 || num > 99)
        return 0;
    else
    {
        sum_of_digits = (i % 10) + (i / 10);
        prod_of_digits = (i % 10) * (i / 10);
        sum = sum_of_digits + prod_of_digits;
    }

    if (sum == num)
        return 1;
    else
        return 0;
}

// Function to count number of special
// two digit number
static void countSpecialDigit(Node rt)
{
    int x;
    if (rt == null)
        return;
    else
    {
        x = check(rt.info);
        if (x == 1)
            count = count + 1;

        countSpecialDigit(rt.left);
        countSpecialDigit(rt.right);
    }
}

// Driver code
public static void main(String[] args)
{
    BinaryTree tree = new BinaryTree();
    Node root = null;

    root = tree.insert(root, 50);
    tree.insert(root, 29);
    tree.insert(root, 59);
    tree.insert(root, 19);
    tree.insert(root, 53);
    tree.insert(root, 556);
    tree.insert(root, 56);
    tree.insert(root, 94);
    tree.insert(root, 13);

    // Function call
    countSpecialDigit(root);
    System.out.println(count);
}
}

// This code is contributed by tushar_bansal
```

## 蟒蛇 3

```
# Python3 program to count number of nodes in
# BST containing two digit special number

# A Tree node
class Node:

    def __init__(self, x):

        self.data = x
        self.left = None
        self.right = None

# Function to create a new node
def insert(node, data):

    global succ

    # If the tree is empty, return
    # a new node
    root = node

    if (node == None):
        return Node(data)

    # If key is smaller than root's key,
    # go to left subtree and set successor
    # as current node
    if (data < node.data):
        root.left = insert(node.left, data)

    # Go to right subtree
    elif (data > node.data):
        root.right = insert(node.right, data)

    return root

# Function to find if number
# is special or not
def check(num):

    sum = 0
    i = num
    #sum_of_digits, prod_of_digits

    # Check if number is two digit or not
    if (num < 10 or num > 99):
        return 0
    else:
        sum_of_digits = (i % 10) + (i // 10)
        prod_of_digits = (i % 10) * (i // 10)
        sum = sum_of_digits + prod_of_digits

    if (sum == num):
        return 1
    else:
        return 0

# Function to count number of special
# two digit number
def countSpecialDigit(rt):

    global c

    if (rt == None):
        return
    else:
        x = check(rt.data)
        if (x == 1):
            c += 1

        countSpecialDigit(rt.left)
        countSpecialDigit(rt.right)

# Driver code
if __name__ == '__main__':

    root = None

    # Initialize result
    c = 0

    # Function call to insert() to
    # insert nodes
    root = insert(root, 50)
    root = insert(root, 29)
    root = insert(root, 59)
    root = insert(root, 19)
    root = insert(root, 53)
    root = insert(root, 556)
    root = insert(root, 56)
    root = insert(root, 94)
    root = insert(root, 13)

    # Function call, to check each node
    # for special two digit number
    countSpecialDigit(root)

    print(c)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to count number of nodes in
// BST containing two digit special number

// A binary tree node
using System;
public class Node
{
  public int info;
  public Node left, right; 
  public Node(int d)
  {
    info = d;
    left = right = null;
  }
}
public class BinaryTree
{
  public static Node head;
  public static int count;

  // Function to create a new node
  public Node insert(Node node, int info)
  {

    // If the tree is empty, return a new,
    // single node
    if(node == null)
    {
      return (new Node(info));
    }
    else
    {

      // Otherwise, recur down the tree
      if(info <= node.info)
      {
        node.left = insert(node.left, info);
      }
      else
      {
        node.right = insert(node.right, info);
      }
    }

    // return the (unchanged) node pointer
    return node;
  }

  // Function to find if number
  // is special or not
  static int check(int num)
  {
    int sum = 0, i = num, sum_of_digits, prod_of_digits;

    // Check if number is two digit or not
    if(num < 10 || num > 99)
    {
      return 0;
    }
    else
    {
      sum_of_digits = (i % 10) + (i / 10);
      prod_of_digits = (i % 10) * (i / 10);
      sum = sum_of_digits + prod_of_digits;
    }
    if(sum == num)
    {
      return 1;
    }
    else
    {
      return 0;
    }
  }

  // Function to count number of special
  // two digit number
  static void countSpecialDigit(Node rt)
  {
    int x;
    if(rt == null)
    {
      return;
    }
    else
    {
      x = check(rt.info);
      if(x == 1)
      {
        count = count + 1;

      }
      countSpecialDigit(rt.left);
      countSpecialDigit(rt.right);
    }
  }

  // Driver code
  static public void Main ()
  {
    BinaryTree tree = new BinaryTree();
    Node root = null;
    root = tree.insert(root, 50);
    tree.insert(root, 29);
    tree.insert(root, 59);
    tree.insert(root, 19);
    tree.insert(root, 53);
    tree.insert(root, 556);
    tree.insert(root, 56);
    tree.insert(root, 94);
    tree.insert(root, 13);

    // Function call
    countSpecialDigit(root);
    Console.WriteLine(count);
  }
}

// This code is contributed by avanitrachhadiya2155
```

## java 描述语言

```
<script>
// Javascript program to count number of nodes in
// BST containing two digit special number

// A binary tree node
class Node
{
    constructor(d)
    {
        this.info = d;
        this.left = this.right = null;
    }
}

let head;
let count=0;

// Function to create a new node
function insert(node,info)
{
    // If the tree is empty, return a new,
    // single node
    if (node == null)
    {
        return (new Node(info));
    }
    else
    {

        // Otherwise, recur down the tree
        if (info <= node.info)
        {
            node.left = insert(node.left, info);
        }
        else
        {
            node.right = insert(node.right, info);
        }

        // return the (unchanged) node pointer
        return node;
    }
}

// Function to find if number
// is special or not
function check(num)
{
    let sum = 0, i = num,
        sum_of_digits,
        prod_of_digits;

    // Check if number is two digit or not
    if (num < 10 || num > 99)
        return 0;
    else
    {
        sum_of_digits = (i % 10) + Math.floor(i / 10);
        prod_of_digits = (i % 10) * Math.floor(i / 10);
        sum = sum_of_digits + prod_of_digits;
    }

    if (sum == num)
        return 1;
    else
        return 0;
}

// Function to count number of special
// two digit number
function countSpecialDigit(rt)
{
    let x;
    if (rt == null)
        return;
    else
    {
        x = check(rt.info);
        if (x == 1)
            count = count + 1;

        countSpecialDigit(rt.left);
        countSpecialDigit(rt.right);
    }
}

// Driver code
let root = null;

root = insert(root, 50);
root=insert(root, 29);
root=insert(root, 59);
root=insert(root, 19);
root=insert(root, 53);
root=insert(root, 556);
root=insert(root, 56);
root=insert(root, 94);
root=insert(root, 13);

// Function call
countSpecialDigit(root);
document.write(count);

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
3
```

**时间复杂度:** O(N)，其中 N 为树中节点数。