# 二叉树中的前三个元素

> 原文:[https://www . geesforgeks . org/top-三元素-二叉树/](https://www.geeksforgeeks.org/top-three-elements-binary-tree/)

我们有一个简单的二叉树，我们必须打印二叉树中最大的 3 个元素。
**例:**

```
Input : 
          1
         /  \
        2    3
       / \   / \
      4  5   4  5
Output :Three largest elements are 5 4 3
```

**逼近**我们可以简单的取三个变量第一、第二、第三分别存储第一大、第二大、第三大，进行前序遍历，每次都会相应的更新元素。
这种方法只需要 0(n)时间。
算法-

```
1- Take 3 variables first, second, third
2- Perform a preorder traversal
    if (root==NULL)
         return
    if root's data is larger then first
         update third with second
         second with first
         first with root's data
    else if root's data is larger then 
         second and not equal to first
            update third with second
            second with root's data
    else if root's data is larger then 
         third and not equal to first & 
         second
            update third with root's data
3- call preorder for root->left
4- call preorder for root->right
```

## C++

```
// CPP program to find largest three elements in
// a binary tree.
#include <bits/stdc++.h>
using namespace std;

struct Node {
  int data;
  struct Node *left;
  struct Node *right;
};

/* Helper function that allocates a new Node with the
   given data and NULL left and right pointers. */
struct Node *newNode(int data) {
  struct Node *node = new Node;
  node->data = data;
  node->left = NULL;
  node->right = NULL;
  return (node);
}

// function to find three largest element
void threelargest(Node *root, int &first, int &second,
                                          int &third) {
  if (root == NULL)
    return;

  // if data is greater than first large number
  // update the top three list
  if (root->data > first) {
    third = second;
    second = first;
    first = root->data;
  }

  // if data is greater than second large number
  // and not equal to first update the bottom
  // two list
  else if (root->data > second && root->data != first) {
    third = second;
    second = root->data;
  }

  // if data is greater than third large number
  // and not equal to first & second update the
  // third highest list
  else if (root->data > third &&
           root->data != first &&
           root->data != second)
    third = root->data;

  threelargest(root->left, first, second, third);
  threelargest(root->right, first, second, third);
}

// driver function
int main() {
  struct Node *root = newNode(1);
  root->left = newNode(2);
  root->right = newNode(3);
  root->left->left = newNode(4);
  root->left->right = newNode(5);
  root->right->left = newNode(4);
  root->right->right = newNode(5);

  int first = 0, second = 0, third = 0;
  threelargest(root, first, second, third);
  cout << "three largest elements are "
       << first << " " << second << " "
       << third;
  return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find largest three elements
// in a binary tree.
import java.util.*;

class GFG
{
static class Node
{
    int data;
    Node left;
    Node right;
};

static int first, second, third;

/* Helper function that allocates
a new Node with the given data and
null left and right pointers. */
static Node newNode(int data)
{
    Node node = new Node();
    node.data = data;
    node.left = null;
    node.right = null;
    return (node);
}

// function to find three largest element
static void threelargest(Node root)
{
if (root == null)
    return;

// if data is greater than first large number
// update the top three list
if (root.data > first)
{
    third = second;
    second = first;
    first = root.data;
}

// if data is greater than second large number
// and not equal to first update the bottom
// two list
else if (root.data > second &&
         root.data != first)
{
    third = second;
    second = root.data;
}

// if data is greater than third large number
// and not equal to first & second update the
// third highest list
else if (root.data > third &&
         root.data != first &&
         root.data != second)
    third = root.data;

threelargest(root.left);
threelargest(root.right);
}

// driver function
public static void main(String[] args)
{
    Node root = newNode(1);
    root.left = newNode(2);
    root.right = newNode(3);
    root.left.left = newNode(4);
    root.left.right = newNode(5);
    root.right.left = newNode(4);
    root.right.right = newNode(5);

    first = 0; second = 0; third = 0;
    threelargest(root);
    System.out.print("three largest elements are " +
                      first + " " + second + " " + third);
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program to find largest three
# elements in a binary tree.

# Helper function that allocates a new
# Node with the given data and None
# left and right pointers.
class newNode:
  def __init__(self, data):
      self.data = data
      self.left = None
      self.right = None

# function to find three largest element
def threelargest(root, first, second, third):
  if (root == None):
    return

  # if data is greater than first large
  # number update the top three list
  if (root.data > first[0]):
    third[0] = second[0]
    second[0] = first[0]
    first[0] = root.data

  # if data is greater than second large
  # number and not equal to first update
  # the bottom two list
  elif (root.data > second[0] and
        root.data != first[0]):
    third[0] = second[0]
    second[0] = root.data

  # if data is greater than third large
  # number and not equal to first & second
  # update the third highest list
  elif (root.data > third[0] and
        root.data != first[0] and
        root.data != second[0]):
      third[0] = root.data

  threelargest(root.left, first,
                  second, third)
  threelargest(root.right, first,
                   second, third)

# Driver Code
if __name__ == '__main__':

    root = newNode(1)
    root.left = newNode(2)
    root.right = newNode(3)
    root.left.left = newNode(4)
    root.left.right = newNode(5)
    root.right.left = newNode(4)
    root.right.right = newNode(5)

    first = [0]
    second = [0]
    third = [0]
    threelargest(root, first, second, third)
    print("three largest elements are",
           first[0], second[0], third[0])

# This code is contributed by PranchalK
```

## C#

```
// C# program to find largest three elements
// in a binary tree.
using System;
class GFG
{
public class Node
{
    public int data;
    public Node left;
    public Node right;
};

static int first, second, third;

/* Helper function that allocates
a new Node with the given data and
null left and right pointers. */
static Node newNode(int data)
{
    Node node = new Node();
    node.data = data;
    node.left = null;
    node.right = null;
    return (node);
}

// function to find three largest element
static void threelargest(Node root)
{
    if (root == null)
        return;

    // if data is greater than first large number
    // update the top three list
    if (root.data > first)
    {
        third = second;
        second = first;
        first = root.data;
    }

    // if data is greater than second large number
    // and not equal to first update the bottom
    // two list
    else if (root.data > second &&
             root.data != first)
    {
        third = second;
        second = root.data;
    }

    // if data is greater than third large number
    // and not equal to first & second update the
    // third highest list
    else if (root.data > third &&
             root.data != first &&
             root.data != second)
        third = root.data;

    threelargest(root.left);
    threelargest(root.right);
}

// Driver Code
public static void Main(String[] args)
{
    Node root = newNode(1);
    root.left = newNode(2);
    root.right = newNode(3);
    root.left.left = newNode(4);
    root.left.right = newNode(5);
    root.right.left = newNode(4);
    root.right.right = newNode(5);

    first = 0; second = 0; third = 0;
    threelargest(root);
    Console.WriteLine("three largest elements are " +
                       first + " " + second + " " + third);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

    // Javascript program to find largest
    // three elements in a binary tree.

    class Node
    {
        constructor(data) {
           this.left = null;
           this.right = null;
           this.data = data;
        }
    }

    let first, second, third;

    /* Helper function that allocates
    a new Node with the given data and
    null left and right pointers. */
    function newNode(data)
    {
        let node = new Node(data);
        return (node);
    }

    // function to find three largest element
    function threelargest(root)
    {
        if (root == null)
            return;

        // if data is greater than first large number
        // update the top three list
        if (root.data > first)
        {
            third = second;
            second = first;
            first = root.data;
        }

        // if data is greater than second large number
        // and not equal to first update the bottom
        // two list
        else if (root.data > second &&
                 root.data != first)
        {
            third = second;
            second = root.data;
        }

        // if data is greater than third large number
        // and not equal to first & second update the
        // third highest list
        else if (root.data > third &&
                 root.data != first &&
                 root.data != second)
            third = root.data;

        threelargest(root.left);
        threelargest(root.right);
    }

    let root = newNode(1);
    root.left = newNode(2);
    root.right = newNode(3);
    root.left.left = newNode(4);
    root.left.right = newNode(5);
    root.right.left = newNode(4);
    root.right.right = newNode(5);

    first = 0; second = 0; third = 0;
    threelargest(root);
    document.write("three largest elements are " +
                      first + " " + second + " " + third);

</script>
```

**Output:** 

```
three largest elements are 5 4 3
```

**时间复杂度:** O(N)

**辅助空间:** O(1)